---
title: Gestion de la configuration du magasin
description: Découvrez comment gérer et synchroniser les paramètres de configuration du magasin dans tous les environnements Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, SCD
exl-id: f2dd876d-24ee-4d47-b9ac-44fcf77b61b5
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Gestion de la configuration du magasin

Les configurations par défaut de votre magasin sont stockées dans un `config.xml` pour le module approprié. Lorsque vous modifiez les paramètres dans l’administrateur Commerce ou la commande CLI `bin/magento config:set`, les modifications sont répercutées dans la base de données principale, en particulier dans la table `core_config_data`. Ces paramètres remplacent les configurations par défaut stockées dans le fichier `config.xml`.

Les paramètres de magasin, qui font référence aux configurations de la section Admin **Magasins** > **Paramètres** > **Configuration** , sont stockés dans les fichiers de configuration de déploiement en fonction du type de configuration :

- `app/etc/config.php` : paramètres de configuration pour les magasins, les sites web, les modules ou les extensions, l’optimisation des fichiers statiques et les valeurs système liées au déploiement de contenu statique. Voir la [référence config.php](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) dans le _Guide de configuration_.
- `app/etc/env.php` : valeurs des remplacements spécifiques au système et des paramètres sensibles qui doivent _NOT_ être stockés dans le contrôle source. Voir la [référence env.php](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) dans le _Guide de configuration_.

>[!NOTE]
>
>Comme Adobe Commerce sur l’infrastructure cloud prend uniquement en charge les modes de production et de maintenance, la section **Avancé** > **Développeur** n’est pas accessible dans l’administrateur. Vous devez disposer des [privilèges d’administrateur d’environnement](../project/user-access.md) pour terminer les tâches de gestion de la configuration. Vous pouvez configurer des paramètres supplémentaires à l’aide des [variables d’environnement](../environment/configure-env-yaml.md).

La gestion des configurations permet de déployer des paramètres de magasin cohérents dans vos environnements avec un temps d’arrêt minimal à l’aide du déploiement du pipeline. Adobe Commerce sur le projet d’infrastructure cloud inclut le serveur de génération, les scripts de génération et de déploiement, ainsi que les environnements de déploiement conçus en tenant compte de la [stratégie de déploiement de pipeline](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html).

## Schéma de remplacement de configuration

Toutes les configurations système sont définies lors des phases de création et de déploiement selon le schéma de remplacement suivant :

1. Si une variable d’environnement existe, utilisez la configuration personnalisée et ignorez la configuration par défaut.
1. Si aucune variable d’environnement n’existe, utilisez la configuration d’une paire nom-valeur `MAGENTO_CLOUD_RELATIONSHIPS` dans le fichier [`.magento.app.yaml`](../application/configure-app-yaml.md). Ignorez la configuration par défaut.
1. Si une variable d&#39;environnement n&#39;existe pas et que `MAGENTO_CLOUD_RELATIONSHIPS` ne contient pas de paire nom-valeur, supprimez toutes les configurations personnalisées et utilisez les valeurs de la configuration par défaut.

Pour résumer, les variables d’environnement remplacent toutes les autres valeurs.

>[!TIP]
>
>Voir [Gestion des configurations](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) dans le _Guide de configuration_ pour en savoir plus sur le schéma de remplacement pour le déploiement du pipeline.

Si le même paramètre est configuré à plusieurs endroits, l’application se base sur la hiérarchie de configuration suivante pour déterminer la valeur à appliquer à l’environnement :

| Priorité | Configuration<br>Méthode | Description |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br> variables d&#39;environnement | Valeurs ajoutées à partir de l’onglet _Variables_ de la configuration de l’environnement dans [!DNL Cloud Console]. Spécifiez ici des valeurs pour les configurations sensibles ou spécifiques à un environnement. Les paramètres spécifiés ici ne peuvent pas être modifiés à partir de l’administrateur. Voir [Variables de configuration d’environnement](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Valeurs ajoutées dans la section `variables` du fichier `.magento.app.yaml`. Spécifiez ici les valeurs afin d’assurer une configuration cohérente dans tous les environnements. **Ne spécifiez pas de valeurs sensibles dans le fichier `.magento.app.yaml`.** Voir [Paramètres de l’application](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | Les valeurs de configuration spécifiques à un environnement stockées ici sont ajoutées à l’aide de la commande `app:config:dump`. Définissez les valeurs sensibles et spécifiques au système à l’aide des variables d’environnement ou de l’interface de ligne de commande. Voir [Données sensibles](#sensitive-data). Le fichier `env.php` est **not** inclus dans le contrôle source. |
| 4 | `app/etc/config.php` | Les valeurs stockées ici sont ajoutées à l’aide de la commande `app:config:dump` . Les valeurs de configuration partagées sont ajoutées à `config.php`. Définissez la configuration partagée depuis l’administrateur ou à l’aide de l’interface de ligne de commande. Le fichier `config.php` est inclus dans le contrôle source. |
| 5 | Base | Les valeurs stockées ici sont ajoutées en définissant des configurations dans l’administrateur. Les configurations définies à l’aide des méthodes précédentes sont verrouillées (grisées) et ne peuvent pas être modifiées à partir de l’administrateur. |
| 6 | `config.xml` | De nombreuses configurations comportent des valeurs par défaut définies dans le fichier `config.xml` pour un module. Si Adobe Commerce ne trouve aucune valeur définie par l’une des méthodes précédentes, elle revient à la valeur par défaut, le cas échéant. |

{style="table-layout:auto"}

## Dépôt de configuration

Vous pouvez utiliser la commande `ece-tools` suivante pour générer un fichier `config.php` contenant toutes les configurations de magasin actuelles :

```bash
./vendor/bin/ece-tools config:dump
```

Les données &quot;vidées&quot; vers le fichier `app/etc/config.php` deviennent _verrouillées_, ce qui signifie que le champ correspondant dans l’administrateur Commerce devient **lecture seule**. Le fichier `config.php` comprend uniquement les paramètres que vous configurez. Les valeurs par défaut ne sont pas verrouillées. En verrouillant uniquement les valeurs que vous mettez à jour, vous avez également la garantie que toutes les extensions utilisées dans les environnements d’évaluation et de production ne sont pas rompues en raison de configurations en lecture seule, notamment Fastly.

>[!WARNING]
>
>La commande `ece-tools config:dump` ne récupère pas les configurations détaillées des modules, tels que B2B. Si vous avez besoin d’un vidage de configuration complet, utilisez la commande `app:config:dump`, mais cette commande verrouille les valeurs de configuration en lecture seule.

### Données sensibles

Toutes les configurations sensibles sont exportées vers le fichier `app/etc/env.php` lorsque vous utilisez la commande `bin/magento app:config:dump`. Vous pouvez définir des valeurs sensibles à l’aide de la commande d’interface en ligne de commande : `bin/magento config:sensitive:set`. Voir [Paramètres sensibles et spécifiques à l’environnement](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) dans le guide _Extensions PHP Commerce_ pour savoir comment désigner les paramètres de configuration comme étant sensibles ou spécifiques au système.

Consultez la liste des [ paramètres sensibles ou spécifiques au système ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) dans le _Guide de configuration_.

### Performances SCD

Selon la taille de votre magasin, vous pouvez déployer un grand nombre de fichiers de contenu statique. Normalement, le contenu statique est déployé pendant la phase de déploiement lorsque l’application est en mode de maintenance. La configuration la plus optimale consiste à générer du contenu statique pendant la phase de création. Voir [Choix d’une stratégie de déploiement](../deploy/static-content.md).

Si vous avez activé Configuration Management après avoir vidé les configurations, vous devez déplacer les variables SCD_* de l’étape de déploiement vers l’étape de création pour activer correctement la génération de contenu statique pendant la phase de création. Voir [Variables d’environnement](../environment/configure-env-yaml.md#environment-variables).

**Avant la gestion de la configuration** :

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

**Après avoir activé Configuration Management** :

Déplacez les variables SCD_* vers l’étape de création :

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```

>[!NOTE]
>
>Avant de déployer des fichiers statiques, les phases de création et de déploiement compressent le contenu statique à l’aide de GZIP. La compression de fichiers statiques réduit la charge du serveur et améliore les performances du site. Voir [options de création](../environment/variables-build.md) pour en savoir plus sur la personnalisation ou la désactivation de la compression de fichier.

## Procédure de gestion des paramètres

Voici un aperçu général de ce processus :

![Présentation de la gestion de la configuration de démarrage](../../assets/starter/configuration-management-flow.png)

**Pour configurer votre magasin et générer un fichier de configuration** :

1. Effectuez toutes les configurations pour vos magasins dans l’Admin pour l’un des environnements :

   - Démarrage : une branche de développement active
   - Pro : branche active dans l’environnement d’intégration

   Ces configurations n’incluent pas les produits réels, sauf si vous envisagez de vider la base de données de cet environnement vers les environnements d’évaluation et de production. En règle générale, les bases de données de développement n’incluent pas vos données de magasin complètes.

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Créez un vidage local de la base distante.

   ```bash
   magento-cloud db:dump
   ```

1. Ajoutez, validez et poussez les modifications de code pour mettre à jour un environnement distant.

   ```bash
   git add app/etc/config.php
   ```

   ```bash
   git commit -m "Add system-specific configuration"
   ```

   ```bash
   git push origin <branch-name>
   ```

Une fois le déploiement terminé, connectez-vous à l’administrateur de l’environnement mis à jour pour vérifier les paramètres. Continuez à fusionner toutes les configurations supplémentaires aux environnements d’évaluation et de production, si nécessaire.

### Mise à jour des configurations

Lorsque vous modifiez votre environnement par l’intermédiaire de l’administrateur et exécutez à nouveau la commande, de nouvelles configurations sont ajoutées au code dans le fichier `config.php`.

>[!WARNING]
>
>Bien que vous puissiez modifier manuellement le fichier `config.php` dans les environnements d’évaluation et de production, il est **non** recommandé. Le fichier permet de préserver la cohérence de toutes les configurations dans tous les environnements. Ne supprimez jamais le fichier `config.php` pour le recréer. La suppression du fichier peut supprimer les configurations et paramètres spécifiques requis pour créer et déployer des processus.

### Restauration des fichiers de configuration

Des copies des fichiers `app/etc/env.php` et `app/etc/config.php` d’origine ont été créées pendant le processus de déploiement et stockées dans le même dossier. L’exemple suivant montre les fichiers BAK (sauvegarde) et PHP (fichiers originaux) dans le même dossier `app/etc` :

```
...
config.php.bak
di.xml
env.php.bak
vendor_path.php
config.php
db_schema.xml
env.php
...
```

Les anciennes configurations utilisaient le fichier `app/etc/config.local.php`. Voir [Migration des anciennes configurations](#migrate-older-configurations).

**Pour restaurer les fichiers de configuration** :

1. Sur votre poste de travail local, utilisez SSH pour vous connecter au projet et à l’environnement distants.

   ```bash
   magento-cloud ssh
   ```

1. Vérifiez l’emplacement et la disponibilité des fichiers de sauvegarde.

   ```bash
   ./vendor/bin/ece-tools backup:list
   ```

   Exemple de réponse :

   ```
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Restaurer les fichiers de sauvegarde.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Migration des anciennes configurations

Si vous effectuez une mise à niveau vers Adobe Commerce sur l’infrastructure cloud 2.2 ou une version ultérieure, vous souhaiterez peut-être migrer les paramètres du fichier `config.local.php` vers votre nouveau fichier `config.php`. Si les paramètres de configuration de votre administrateur correspondent au contenu du fichier, suivez les instructions pour générer et ajouter le fichier `config.php`.

S’ils diffèrent, vous pouvez ajouter du contenu du fichier `config.local.php` à votre nouveau fichier `config.php` :

1. Suivez les instructions pour générer le fichier `config.php`.

1. Ouvrez le fichier `config.php` et supprimez la dernière ligne.

1. Ouvrez le fichier `config.local.php` et copiez le contenu.

1. Collez le contenu dans le fichier `config.php`, enregistrez-le, puis complétez son ajout à Git.

1. Déployez dans vos environnements.

Cette migration n’est effectuée qu’une seule fois. Après la migration, utilisez le fichier `config.php`.

### Modifier les paramètres régionaux

Vous pouvez modifier les paramètres régionaux de votre magasin sans suivre un processus complexe d&#39;import et d&#39;export de configuration, _si_ vous avez activé [SCD_ON_DEMAND](../environment/variables-global.md#scd_on_demand). Vous pouvez mettre à jour les paramètres régionaux à l’aide de l’Admin.

Vous pouvez ajouter un autre paramètre régional à l’environnement d’évaluation ou de production en activant `SCD_ON_DEMAND` dans une branche d’intégration, en générant un fichier `config.php` mis à jour avec les nouvelles informations de paramètres régionaux et en copiant le fichier de configuration dans l’environnement cible.

>[!WARNING]
>
>Ce processus **remplace** la configuration du magasin ; procédez comme suit uniquement si les environnements contiennent les mêmes magasins.

1. Dans l’environnement d’intégration, activez la variable `SCD_ON_DEMAND` à l’aide du fichier [`.magento.env.yaml`](../environment/configure-env-yaml.md).

1. Ajoutez les paramètres régionaux nécessaires à l’aide de votre administrateur.

1. Utilisez SSH pour vous connecter à l’environnement distant et générer le fichier `/app/etc/config.php` contenant tous les paramètres régionaux.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Copiez le nouveau fichier de configuration de l’environnement d’intégration distante dans votre répertoire d’environnement local.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Ajoutez, validez et poussez les modifications de code pour mettre à jour un environnement distant.
