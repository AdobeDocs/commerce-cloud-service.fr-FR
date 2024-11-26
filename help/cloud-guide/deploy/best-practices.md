---
title: Bonnes pratiques de déploiement
description: Découvrez les bonnes pratiques de déploiement d’Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: 269681efb9925d78ffb608ecbef657be740b5531
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Bonnes pratiques de déploiement

Les scripts de création et de déploiement sont activés lorsque vous fusionnez du code dans un environnement distant. Ces scripts utilisent les [fichiers de configuration](../environment/overview.md) de l’environnement et le code de l’application pour fournir l’infrastructure cloud avec les données et services appropriés. En outre, ces scripts sont utilisés pour installer ou mettre à jour l’application Adobe Commerce, les services tiers et les extensions personnalisées dans l’environnement cloud.

Le processus de création et de déploiement diffère légèrement pour chaque plan :

- **Formules de démarrage** : pour l’environnement d’intégration, chaque branche active crée et se déploie dans un environnement complet pour l’accès et le test. Testez entièrement votre code après la fusion dans la branche `staging`. Pour lancer votre site, envoyez `staging` vers `master` pour le déployer dans l’environnement de production. Vous disposez d’un accès complet à toutes les branches via les commandes [!DNL Cloud Console] et l’interface de ligne de commande.

- **Pro plans** : pour l’environnement d’intégration, chaque branche active crée et se déploie dans un environnement complet pour l’accès et le test. Fusionnez votre code dans la branche `integration` avant de le fusionner dans les environnements d’évaluation et de production. Vous pouvez fusionner dans les environnements d’évaluation et de production à l’aide des commandes [!DNL Cloud Console] ou SSH et `magento-cloud` de l’interface de ligne de commande.

## Suivi du processus

Vous pouvez effectuer le suivi des actions de création et de déploiement en temps réel à l’aide du terminal ou des messages d’état [!DNL Cloud Console], `in-progress`, `pending`, `success` ou `failed` qui s’affichent pendant le processus de déploiement. Vous pouvez afficher les détails dans les fichiers journaux. Voir [Afficher les journaux](../test/log-locations.md).

Si vous utilisez des référentiels GitHub externes, le journal des opérations ne s’affiche pas dans la session GitHub. Cependant, vous pouvez toujours suivre l’activité dans l’interface pour le référentiel externe et le [!DNL Cloud Console]. Voir [Intégrations](../integrations/overview.md).

>[!NOTE]
>
>Dans les environnements d’intégration, vous ne pouvez pas afficher les journaux de déploiement à partir de [!DNL Cloud Console]. Cette fonctionnalité est disponible uniquement pour les environnements de production et d’évaluation. Cependant, vous pouvez afficher les journaux pour chaque phase du déploiement dans n’importe quel environnement à l’aide des journaux [build and deploy](../test/log-locations.md#build-and-deploy-logs). Pour plus d’informations sur la résolution des problèmes, voir la [Référence d’erreur sur le déploiement](../dev-tools/error-reference.md).

Vous pouvez activer le [suivi des déploiements avec New Relic](../monitor/track-deployments.md) pour surveiller les événements de déploiement et analyser les performances entre les déploiements.

## Bonnes pratiques relatives aux versions et au déploiement

Consultez les bonnes pratiques et les considérations suivantes pour votre processus de déploiement :

- **Vérifiez que vous exécutez la version la plus récente du package `ece-tools`**.

  Voir les [notes de mise à jour pour les outils ECE](../release-notes/ece-tools-package.md).

- **Suivez le processus de création et de déploiement**

  Assurez-vous que chaque environnement contient le code correct pour éviter d’écraser les configurations lors de la fusion du code entre les environnements. Par exemple, pour appliquer les modifications de configuration à tous les environnements, modifiez et testez les modifications dans l’environnement local avant de les déployer dans l’environnement d’intégration distant. Ensuite, déployez et testez les modifications dans l’environnement d’évaluation avant de les déployer en production. Lorsque vous fusionnez d’un environnement à un autre, le déploiement remplace tout le code de l’environnement, à l’exception de la configuration et des paramètres spécifiques à l’environnement.

- **Utiliser les mêmes variables dans tous les environnements**

  Les valeurs de ces variables peuvent différer d’un environnement à l’autre ; toutefois, vous avez généralement besoin des mêmes variables dans chaque environnement. Voir [Gestion des configurations pour les paramètres de magasin](../store/store-settings.md).

- **Conserver les valeurs et données de configuration sensibles dans les variables spécifiques à l’environnement**

  Ces valeurs incluent des variables spécifiées à l’aide de l’interface de ligne de commande de Cloud, de [!DNL Cloud Console] ou ajoutées au fichier `env.php`. Voir [Niveaux de variable](../environment/variable-levels.md).

- **Assurez-vous que tout le code est disponible dans la branche d’environnement**

  Le référencement du code d’autres branches, telles qu’une branche privée, peut entraîner des problèmes pendant le processus de création et de déploiement. Par exemple, si vous référencez un thème d’une branche privée, il n’est pas accessible et ne peut pas être créé avec le code de l’application.

- **Ajouter des extensions, des intégrations et du code dans des branches itérées**

  Effectuez et testez les modifications localement, passez à `integration`, puis à `staging` et `production`. Testez et résolvez les problèmes dans chaque environnement avant de fusionner les mises à jour dans l’environnement suivant. Certaines extensions et intégrations doivent être activées et configurées dans un ordre spécifique en raison de dépendances. L’ajout et le test dans des groupes peuvent faciliter considérablement votre processus de création et de déploiement et vous aider à déterminer où des problèmes se produisent.

- **Vérifiez les versions et relations du service, ainsi que la possibilité de vous connecter**

  Vérifiez les services disponibles pour votre application et assurez-vous que vous utilisez la version la plus récente et la plus compatible. Voir [Relations de service](../services/services-yaml.md#service-relationships) et [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Guide d&#39;installation_ pour connaître les versions recommandées.

- **Testez localement et dans l’environnement d’intégration avant de procéder au déploiement vers l’évaluation et la production**

  Identifiez et corrigez les problèmes dans vos environnements locaux et d’intégration afin d’éviter les temps d’arrêt étendus lorsque vous déployez vers les environnements d’évaluation et de production.

  >[!TIP]
  >
  >Il existe des commandes [smart wizard](../deploy/smart-wizards.md) que vous pouvez utiliser pour vérifier que la configuration de votre projet cloud suit les bonnes pratiques de configuration de création et de déploiement, y compris la stratégie de déploiement de contenu statique (SCD).

- **Après avoir effectué les tests dans les environnements locaux et d’intégration, déployez et testez-les dans l’environnement d’évaluation**

  Voir [Test d’évaluation et de production](../test/staging-and-production.md).

- **Vérification de la configuration de l’environnement de production**

  Avant de procéder au déploiement en production, effectuez les tâches suivantes :

   - Assurez-vous que vous pouvez vous connecter aux trois noeuds de l’environnement de production à l’aide de [SSH](../development/secure-connections.md).

   - Vérifiez que les indexeurs sont définis sur _Mettre à jour lors de la planification_. Voir [Modes d’indexation](https://developer.adobe.com/commerce/php/development/components/indexing/) dans le _Guide du développeur d’extension_.

   - Préparez l’environnement en mettant à jour toutes les variables spécifiques à l’environnement dans le code de production, en vérifiant la disponibilité et la compatibilité du service et en apportant toute autre modification de configuration requise.

- **Surveillez le processus de déploiement**

  Passez en revue les messages d’état du déploiement et atténuez les problèmes si nécessaire. Consultez les [logs](../test/log-locations.md#) du cloud pour obtenir des messages de journal détaillés.

## Création et déploiement de l’intégration en cinq phases

Les phases suivantes se produisent dans votre environnement de développement local et dans l’environnement d’intégration. Pour les plans Pro, le code n’est pas déployé dans les environnements d’évaluation ou de production au cours de ces phases initiales.

### Phase 1 : code et validation de configuration

Lors de la configuration initiale d’un projet, [le modèle d’infrastructure cloud](https://github.com/magento/magento-cloud) fournit une base pour les fichiers de code. Ce référentiel de code est cloné à votre projet en tant que branche `master`.

- **Pour le démarrage**—`master` est votre environnement de production.
- **Pour Pro**—`master` commence comme branche d’origine pour l’environnement d’intégration.

Créez une branche à partir de `master` pour votre code personnalisé, vos extensions et modules, ainsi que vos intégrations tierces. Il existe un environnement d’intégration distante pour tester votre code dans le cloud.

Lorsque vous poussez votre code de votre espace de travail local vers le référentiel distant, une série de vérifications et validations de code se terminent avant que les scripts de création et de déploiement ne commencent. Le serveur Git intégré valide ce que vous poussez et apporte des modifications. Par exemple, si vous ajoutez un service OpenSearch, le serveur Git intégré vérifie que la topologie de votre grappe est modifiée en conséquence.

Si un fichier de configuration contient une erreur de syntaxe, le serveur Git rejette la notification push. Voir [Bloc de protection](../development/protective-block.md).

Cette phase exécute également `composer install` pour récupérer les dépendances.

### Phase 2 : création

>[!NOTE]
>
>Pendant la phase de génération, le site n’est pas en mode de maintenance et si des erreurs ou des problèmes se produisent n’est pas supprimé. Il crée uniquement le code qui a changé depuis le build précédent.

Cette phase crée le code base et exécute les points d’extension dans la section `build` de `.magento.app.yaml`. Le crochet de génération par défaut est la commande `php ./vendor/bin/ece-tools` et effectue les opérations suivantes :

- Applique des correctifs dans `vendor/magento/ece-patches` et des correctifs facultatifs spécifiques au projet dans `m2-hotfixes`.
- Régénère le code et la configuration [injection de dépendance](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary) (c’est-à-dire le répertoire `generated/`, qui comprend `generated/code` et `generated/metapackage`) en utilisant `bin/magento setup:di:compile`.
- Vérifie si le fichier [`app/etc/config.php`](../store/store-settings.md) existe dans le code base. Adobe Commerce génère automatiquement ce fichier s’il ne le détecte pas pendant la phase de création et comprend une liste de modules et d’extensions. Si elle existe, la phase de création se poursuit normalement, compresse les fichiers statiques à l’aide de GZIP et se déploie, ce qui réduit le temps d’arrêt pendant la phase de déploiement. Pour plus d&#39;informations sur la personnalisation ou la désactivation de la compression de fichier, voir [options de création](../environment/variables-build.md) .

>[!WARNING]
>
>À ce stade, la grappe n’a pas été créée. Par conséquent, ne tentez pas de vous connecter à une base de données ou ne supposez pas qu’il existe un processus de démon actif.

Une fois l’application créée, elle est montée sur un **système de fichiers en lecture seule**. Vous pouvez configurer des points de montage spécifiques qui seront lus/écrits. Vous ne pouvez pas effectuer de FTP sur le serveur et ajouter des modules. Au lieu de cela, vous devez ajouter du code à votre référentiel local et exécuter `git push`, qui crée et déploie l’environnement. Pour connaître la structure du projet, voir [Structure de répertoire de projet local](../project/file-structure.md).

### Phase 3 : préparation de la limace

Le résultat de la phase de génération est un système de fichiers en lecture seule appelé _limace_. Cette phase crée une archive et place la limace dans un stockage permanent. La prochaine fois que vous pousserez le code, si un service n’a pas changé, il utilisera la limace de l’archive.

- Rend l’intégration continue plus rapide en réutilisant le code inchangé
- Si le code change, met à jour la balise pour le prochain build pour la réutiliser
- Permet la restauration instantanée d’un déploiement, si nécessaire
- Inclut des fichiers statiques si le fichier `app/etc/config.php` existe dans le code base.

La balise de fermeture comprend tous les fichiers et dossiers **à l&#39;exception des** montages suivants configurés dans `magento.app.yaml` :

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Phase 4 : déploiement des diffusions et de la grappe

Vos applications et tous les services [backend](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary) fonctionnent comme suit :

- Monte chaque service dans un conteneur, tel que serveur web, OpenSearch, [!DNL RabbitMQ]
- Monte le système de fichiers en lecture-écriture (monté sur une grille de stockage distribué hautement disponible).
- Configure le réseau de sorte que les services puissent &quot;se voir&quot; (et uniquement les uns les autres).

>[!NOTE]
>
>Apportez vos modifications dans une branche Git une fois la création et le déploiement terminés et relancez la notification push. Tous les systèmes de fichiers d’environnement sont _en lecture seule_. Un système en lecture seule garantit les déploiements déterministes et améliore considérablement la sécurité de votre site, car aucun processus ne peut écrire dans le système de fichiers. Cela fonctionne également pour vous assurer que votre code est identique dans les environnements d’intégration, d’évaluation et de production.

### Phase 5 : hooks de déploiement

>[!NOTE]
>
>Cette phase met l’application [!DNL Commerce] en mode de maintenance jusqu’à ce que le déploiement soit terminé.

La dernière étape exécute un script de déploiement que vous pouvez utiliser pour anonymiser les données dans les environnements de développement, vider les caches et interroger les outils externes d’intégration continue. Lorsque ce script s’exécute, vous avez accès à tous les services de votre environnement, tels que Redis.

Si le fichier `app/etc/config.php` n’existe pas dans la base de code, les fichiers statiques sont compressés à l’aide de `gzip` et déployés pendant cette phase, ce qui augmente la durée de la phase de déploiement et de la maintenance du site.

>[!NOTE]
>
>Pour plus d&#39;informations sur la personnalisation ou la désactivation de la compression de fichiers, reportez-vous à la section [déploiement de variables](../environment/variables-deploy.md) .

Il existe deux hooks de déploiement. Le crochet `pre-deploy.php` effectue le nettoyage et la récupération nécessaires des ressources et du code générés dans le crochet de génération. Le crochet `php ./vendor/bin/ece-tools deploy` exécute une série de commandes et de scripts :

- Si Adobe Commerce n&#39;est **pas installé**, il s&#39;installe avec `bin/magento setup:install`, met à jour la configuration de déploiement, `app/etc/env.php` et la base de données de votre environnement spécifié, tels que les URL des réseaux et des sites web. **Important :** Lorsque vous avez terminé le [premier déploiement](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) au cours de la configuration, Adobe Commerce a été installé et déployé dans tous les environnements.

- Si Adobe Commerce **est installé**, effectuez les mises à niveau nécessaires. Le script de déploiement exécute `bin/magento setup:upgrade` pour mettre à jour le schéma et les données de la base de données (nécessaires après les mises à jour de l’extension ou du code principal), et met également à jour la configuration de déploiement, `app/etc/env.php`, et la base de données de votre environnement. Enfin, le script de déploiement efface le cache d’Adobe Commerce.

- Le script génère éventuellement du contenu web statique à l’aide de la commande `magento setup:static-content:deploy`.

- Utilise l’indicateur scopes (`-s` dans les scripts de génération) avec un paramètre par défaut `quick` pour la stratégie de déploiement de contenu statique. Vous pouvez personnaliser la stratégie à l’aide de la variable d’environnement [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Pour plus d’informations sur ces options et fonctionnalités, voir [Stratégies de déploiement de fichiers statiques](../deploy/static-content.md) et l’indicateur `-s` pour [ Déployer des fichiers d’affichage statique](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>Le script de déploiement utilise les valeurs définies par les fichiers de configuration dans le répertoire `.magento`, puis le script supprime le répertoire et son contenu. Votre environnement de développement local n’est pas affecté.

### Post-déploiement : configuration du routage

Pendant le déploiement en cours d’exécution, le processus interrompt le trafic entrant au point d’entrée pendant 60 secondes et reconfigure le routage afin que le trafic web arrive au niveau de la grappe nouvellement créée.

Le déploiement réussi supprime le mode de maintenance pour permettre un accès normal et crée des fichiers de sauvegarde (BAK) pour les fichiers de configuration `app/etc/env.php` et `app/etc/config.php`.

Activez la génération de contenu statique à l’aide de la variable `SCD_ON_DEMAND` et configurez le [`post_deploy` hook](../application/hooks-property.md) afin qu’il efface le cache et pré-charge (réchauffe) le cache _après_ que le conteneur commence à accepter les connexions et _pendant_ le trafic entrant normal.

Pour consulter les journaux de création et de déploiement, voir [Affichage des journaux](../test/log-locations.md#view-and-manage-logs).
