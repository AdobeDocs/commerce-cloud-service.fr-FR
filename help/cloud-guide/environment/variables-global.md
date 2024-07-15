---
title: Variables globales
description: Consultez la liste des variables d’environnement qui contrôlent les actions dans Adobe Commerce lors du processus de déploiement de l’infrastructure cloud.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Variables globales

Les variables globales contrôlent les actions à chaque phase du processus de déploiement [!DNL Commerce] : création, déploiement et post-déploiement. Les variables globales ayant un impact sur chaque phase, vous devez les définir à l’étape `global` du fichier `.magento.env.yaml` :

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Pour plus d’informations sur la personnalisation du processus de création et de déploiement :

- [Configuration du déploiement](configure-env-yaml.md)
- [Processus de déploiement](../deploy/process.md)

## `ENABLE_EVENTING`

- **Par défaut**-_Non défini_
- **Version**—Adobe Commerce 2.4.5 et versions ultérieures

Lorsqu’il est défini sur `true`, il permet à cron d’exécuter les consommateurs de la file d’attente des messages. Les événements d’Adobe I/O pour Adobe Commerce utilisent les files d’attente de messages pour accélérer la diffusion des événements critiques.

Adobe recommande d’ajouter également la variable [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) à l’étape `deploy` du fichier `.magento.env.yaml` avec `cron_run` défini sur `true`.

L’exemple suivant illustre une variable `ENABLE_EVENTING` entièrement configurée.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Par défaut**-_Non défini_
- **Version**—Adobe Commerce 2.4.4 et versions ultérieures

Lorsqu’elle est définie sur `true`, active les webhooks Commerce. Le webhook s’exécute sur un point de terminaison externe, tel qu’une action d’exécution App Builder ou un système de gestion d’inventaire tiers. Le [_Guide des webhooks_](https://developer.adobe.com/commerce/extensibility/webhooks) décrit cette fonctionnalité en détail.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Permet de remplacer le niveau de journalisation minimum pour tous les flux de sortie sans modifier le code, ce qui permet de résoudre les problèmes liés au déploiement. Par exemple, si votre déploiement échoue, vous pouvez utiliser cette variable pour augmenter la granularité de journalisation globalement. Voir [Niveaux de journal](log-handlers.md#log-levels). La valeur `min_level` des gestionnaires de journalisation remplace ce paramètre.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>Le paramètre de la variable `MIN_LOGGING_LEVEL` ne modifie pas la configuration du niveau de journal pour le gestionnaire de fichiers, qui est défini par défaut sur `debug`.

## `SCD_ON_DEMAND`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Activez la génération de contenu statique lorsqu’un utilisateur le demande (SCD). Le contenu statique à la demande est idéal pour le workflow de développement et de test, car il réduit la durée de déploiement.

Le préchargement du cache à l’aide du point d’extension [`post_deploy`](../application/hooks-property.md) réduit le temps de disponibilité du site. Le réchauffement du cache est disponible uniquement pour les projets Pro contenant des environnements d’évaluation et de production dans [!DNL Cloud Console] et pour les projets de démarrage. Ajoutez la variable d&#39;environnement `SCD_ON_DEMAND` à l&#39;étape `global` dans le fichier `.magento.env.yaml` :

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

La variable `SCD_ON_DEMAND` ignore le SCD dans les deux phases (création et déploiement), efface les dossiers `pub/static` et `var/view_preprocessed` et écrit ce qui suit dans le fichier `app/etc/env.php` :

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Permet d’augmenter le temps d’exécution maximum prévu pour le déploiement de contenu statique.

Par défaut, Adobe Commerce définit l’exécution maximale prévue à 900 secondes, mais dans certains cas, il peut s’avérer nécessaire de consacrer plus de temps au déploiement de contenu statique pour un projet Cloud.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.4.2 et versions ultérieures

Définissez cette variable sur `true` pour empêcher la génération de contenu statique pour les thèmes parents pendant les phases de création et de déploiement. Lorsque cette option est définie sur `true`, moins de contenu statique est généré, ce qui améliore les délais de création et de déploiement globaux.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.3.0 et versions ultérieures

[Baler](https://github.com/magento/baler) est un module qui analyse le code JavaScript généré et crée un lot JavaScript optimisé. Le déploiement du lot optimisé sur votre site peut réduire le nombre de requêtes réseau lors du chargement de votre site et améliorer les temps de chargement des pages.

Définissez cette variable sur `true` pour exécuter Baler après l’exécution du déploiement de contenu statique.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installez et configurez le module Baler avant d’utiliser cette fonctionnalité. Etant donné que Baler est dans une version alpha, activez cette option uniquement dans les environnements d’évaluation.

## `SKIP_HTML_MINIFICATION`

- **Default** :
   - `true`—pour `ece-tools` 2002.0.13 et versions ultérieures
   - `false`—pour les versions antérieures de `ece-tools`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Active ou désactive la copie des fichiers d’affichage statique dans le répertoire `<magento_root>/init/` à la fin de l’étape de création. Si celle-ci est définie sur `true`, les fichiers ne sont pas copiés et la minification d’HTML est disponible sur demande. Définissez cette valeur sur `true` pour réduire le temps d’arrêt lors du déploiement dans les environnements d’évaluation et de production.

- **`false`** : copie le répertoire `view_preprocessed` dans le répertoire `<magento_root>/init/` à la fin de la phase de création et restaure le répertoire dans le répertoire `<magento_root>/var` au début de la phase de déploiement.
- **`true`** : active la minification d’HTML à la demande ; _not_ copie `<magento_root>var/view_preprocessed` dans le répertoire `<magento_root>/init/` à la fin de la phase de création.

Ajoutez la variable d&#39;environnement `SKIP_HTML_MINIFICATION` à l&#39;étape `global` dans le fichier `.magento.env.yaml` :

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Utilisez la variable `X_FRAME_CONFIGURATION` pour modifier la configuration de l’en-tête [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) de votre site Adobe Commerce. Cette configuration contrôle la manière dont le navigateur effectue le rendu d’une page dans `<frame>`, `<iframe>` ou `<object>`. Utilisez l’une des options suivantes :

- `DENY` : la page ne peut pas être affichée dans un cadre.
- `SAMEORIGIN`—(Paramètre Adobe Commerce par défaut.) La page ne peut être affichée que dans un cadre de la même origine que la page elle-même.

>[!WARNING]
>
>L’option `ALLOW-FROM <uri>` a été abandonnée car les navigateurs pris en charge par Adobe Commerce ne la prennent plus en charge. Voir [Compatibilité du navigateur](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Ajoutez la variable d&#39;environnement `X_FRAME_CONFIGURATION` à l&#39;étape `global` dans le fichier `.magento.env.yaml` :

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
