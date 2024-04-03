---
title: Bonnes pratiques de déploiement
description: Découvrez les bonnes pratiques de déploiement d’Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Bonnes pratiques de déploiement

Les scripts de création et de déploiement sont activés lorsque vous fusionnez du code dans un environnement distant. Ces scripts utilisent un environnement [fichiers de configuration](../environment/overview.md) et le code de l’application pour fournir une infrastructure cloud avec les données et les services appropriés. En outre, ces scripts sont utilisés pour installer ou mettre à jour l’application Adobe Commerce, les services tiers et les extensions personnalisées dans l’environnement cloud.

Le processus de création et de déploiement diffère légèrement pour chaque plan :

- **Formules de démarrage**: pour l’environnement d’intégration, chaque branche active crée et se déploie dans un environnement complet pour y accéder et y effectuer des tests. Testez entièrement votre code après la fusion dans le `staging` branche. Pour lancer votre site, appuyez sur `staging` to `master` pour effectuer un déploiement dans l’environnement de production. Vous disposez d’un accès complet à toutes les branches via la variable [!DNL Cloud Console] et les commandes de l’interface de ligne de commande.

- **Formules Pro**: pour l’environnement d’intégration, chaque branche active crée et se déploie dans un environnement complet pour y accéder et y effectuer des tests. Fusionnez votre code vers le `integration` avant de fusionner dans les environnements d’évaluation et de production. Vous pouvez fusionner dans les environnements d’évaluation et de production à l’aide de la variable [!DNL Cloud Console] ou en utilisant SSH et `magento-cloud` Commandes de l’interface de ligne de commande.

## Suivi du processus

Vous pouvez effectuer le suivi des actions de création et de déploiement en temps réel à l’aide du terminal ou de la variable [!DNL Cloud Console] Messages d’état —`in-progress`, `pending`, `success`, ou `failed`: s’affiche pendant le processus de déploiement. Vous pouvez afficher les détails dans les fichiers journaux. Voir [Afficher les journaux](../test/log-locations.md).

Si vous utilisez des référentiels GitHub externes, le journal des opérations ne s’affiche pas dans la session GitHub. Cependant, vous pouvez toujours suivre l’activité dans l’interface pour le référentiel externe et le [!DNL Cloud Console]. Voir [Intégrations](../integrations/overview.md).

>[!NOTE]
>
>Dans les environnements d’intégration, vous ne pouvez pas afficher les journaux de déploiement à partir du [!DNL Cloud Console]. Cette fonctionnalité est disponible uniquement pour les environnements de production et d’évaluation. Cependant, vous pouvez afficher les journaux de chaque phase du déploiement dans n’importe quel environnement à l’aide de la variable [création et déploiement](../test/log-locations.md#build-and-deploy-logs) journaux. Pour plus d’informations sur le dépannage, voir [Référence des erreurs de déploiement](../dev-tools/error-reference.md).

Vous pouvez activer [Suivi des déploiements avec New Relic](../monitor/track-deployments.md) pour surveiller les événements de déploiement et analyser les performances entre les déploiements.

## Bonnes pratiques relatives aux versions et au déploiement

Consultez les bonnes pratiques et les considérations suivantes pour votre processus de déploiement :

- **Assurez-vous que vous exécutez la version la plus récente du `ece-tools` package**

  Voir [Notes de mise à jour pour les outils ECE](../release-notes/ece-tools-package.md).

- **Suivez le processus de création et de déploiement .**

  Assurez-vous que chaque environnement contient le code correct pour éviter d’écraser les configurations lors de la fusion du code entre les environnements. Par exemple, pour appliquer les modifications de configuration à tous les environnements, modifiez et testez les modifications dans l’environnement local avant de les déployer dans l’environnement d’intégration distant. Ensuite, déployez et testez les modifications dans l’environnement d’évaluation avant de les déployer en production. Lorsque vous fusionnez d’un environnement à un autre, le déploiement remplace tout le code de l’environnement, à l’exception de la configuration et des paramètres spécifiques à l’environnement.

- **Utiliser les mêmes variables dans tous les environnements**

  Les valeurs de ces variables peuvent différer d’un environnement à l’autre ; toutefois, vous avez généralement besoin des mêmes variables dans chaque environnement. Voir [Gestion des configurations pour les paramètres du magasin](../store/store-settings.md).

- **Conserver les données et les valeurs de configuration sensibles dans les variables spécifiques à l’environnement**

  Ces valeurs comprennent les variables spécifiées à l’aide de l’interface de ligne de commande de Cloud, la variable [!DNL Cloud Console]ou ajouté au `env.php` fichier . Voir [Niveaux de variable](../environment/variable-levels.md).

- **Assurez-vous que tout le code est disponible dans la branche d’environnement**

  Le référencement du code d’autres branches, telles qu’une branche privée, peut entraîner des problèmes pendant le processus de création et de déploiement. Par exemple, si vous référencez un thème d’une branche privée, il n’est pas accessible et ne peut pas être créé avec le code de l’application.

- **Ajout d’extensions, d’intégrations et de code dans des branches itérées**

  Apporter et tester les modifications localement, envoyer sur `integration`, puis à `staging` et `production`. Testez et résolvez les problèmes dans chaque environnement avant de fusionner les mises à jour dans l’environnement suivant. Certaines extensions et intégrations doivent être activées et configurées dans un ordre spécifique en raison de dépendances. L’ajout et le test dans des groupes peuvent faciliter considérablement votre processus de création et de déploiement et vous aider à déterminer où des problèmes se produisent.

- **Vérifier les versions et les relations du service et la possibilité de se connecter**

  Vérifiez les services disponibles pour votre application et assurez-vous que vous utilisez la version la plus récente et la plus compatible. Voir [Relations avec les services](../services/services-yaml.md#service-relationships) et [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Guide d’installation_ pour les versions recommandées.

- **Testez localement et dans l’environnement d’intégration avant de procéder au déploiement vers l’évaluation et la production**

  Identifiez et corrigez les problèmes dans vos environnements locaux et d’intégration afin d’éviter les temps d’arrêt étendus lorsque vous déployez vers les environnements d’évaluation et de production.

  >[!TIP]
  >
  >Il y a [assistant dynamique](../deploy/smart-wizards.md) commandes que vous pouvez utiliser pour vérifier que la configuration de votre projet cloud suit les bonnes pratiques en matière de configuration de création et de déploiement, y compris la stratégie de déploiement de contenu statique (SCD).

- **Après avoir effectué les tests dans les environnements locaux et d’intégration, déployez et testez-les dans l’environnement d’évaluation.**

  Voir [Test d’évaluation et de production](../test/staging-and-production.md).

- **Vérification de la configuration de l’environnement de production**

  Avant de procéder au déploiement en production, effectuez les tâches suivantes :

   - Assurez-vous que vous pouvez vous connecter aux trois noeuds de l’environnement de production à l’aide de [SSH](../development/secure-connections.md).

   - Vérifiez que les indexeurs sont définis sur _Mise à jour de la planification_. Voir [Modes d&#39;indexation](https://developer.adobe.com/commerce/php/development/components/indexing/) dans le _Guide du développeur de l’extension_.

   - Préparez l’environnement en mettant à jour toutes les variables spécifiques à l’environnement dans le code de production, en vérifiant la disponibilité et la compatibilité du service et en apportant toute autre modification de configuration requise.

- **Surveiller le processus de déploiement**

  Passez en revue les messages d’état du déploiement et atténuez les problèmes si nécessaire. Vérification du cloud [logs](../test/log-locations.md#) pour des messages de journal détaillés.

## Création et déploiement de l’intégration en cinq phases

Les phases suivantes se produisent dans votre environnement de développement local et dans l’environnement d’intégration. Pour les plans Pro, le code n’est pas déployé dans les environnements d’évaluation ou de production au cours de ces phases initiales.

### Phase 1 : code et validation de configuration

Lors de la configuration initiale d’un projet, [le modèle d’infrastructure cloud](https://github.com/magento/magento-cloud) fournit une base pour les fichiers de code. Ce référentiel de code est cloné dans votre projet en tant que `master` branche.

- **Pour commencer**—`master` branche est votre environnement de production.
- **Pour Pro**—`master` commence comme branche d’origine pour l’environnement d’intégration.

Création d’une branche à partir de `master` pour votre code personnalisé, les extensions et modules, ainsi que les intégrations tierces. Il existe un environnement d’intégration distante pour tester votre code dans le cloud.

Lorsque vous poussez votre code de votre espace de travail local vers le référentiel distant, une série de vérifications et validations de code se terminent avant que les scripts de création et de déploiement ne commencent. Le serveur Git intégré valide ce que vous poussez et apporte des modifications. Par exemple, si vous ajoutez un service OpenSearch, le serveur Git intégré vérifie que la topologie de votre grappe est modifiée en conséquence.

Si un fichier de configuration contient une erreur de syntaxe, le serveur Git rejette la notification push. Voir [Bloc de protection](../development/protective-block.md).

Cette phase s’exécute également. `composer install` pour récupérer les dépendances.

### Phase 2 : création

>[!NOTE]
>
>Pendant la phase de génération, le site n’est pas en mode de maintenance et si des erreurs ou des problèmes se produisent n’est pas supprimé. Il crée uniquement le code qui a changé depuis le build précédent.

Cette phase crée le code base et exécute les points d’extension dans la variable `build` section de `.magento.app.yaml`. Le point d’extension par défaut est le suivant : `php ./vendor/bin/ece-tools` et effectue les opérations suivantes :

- Applique des correctifs dans `vendor/magento/ece-patches`et les correctifs facultatifs spécifiques au projet dans `m2-hotfixes`
- Génère le code et la variable [injection de dépendance](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) configuration (c’est-à-dire : `generated/` , qui inclut `generated/code` et `generated/metapackage`) en utilisant `bin/magento setup:di:compile`.
- Vérifie si la variable [`app/etc/config.php`](../store/store-settings.md) existe dans le code base. Adobe Commerce génère automatiquement ce fichier s’il ne le détecte pas pendant la phase de création et comprend une liste de modules et d’extensions. Si elle existe, la phase de création se poursuit normalement, compresse les fichiers statiques à l’aide de GZIP et se déploie, ce qui réduit le temps d’arrêt pendant la phase de déploiement. Voir [options de création](../environment/variables-build.md) pour en savoir plus sur la personnalisation ou la désactivation de la compression de fichier.

>[!WARNING]
>
>À ce stade, la grappe n’a pas été créée. Par conséquent, ne tentez pas de vous connecter à une base de données ou ne supposez pas qu’il existe un processus de démon actif.

Une fois l’application créée, elle est montée sur un **système de fichiers en lecture seule**. Vous pouvez configurer des points de montage spécifiques qui seront lus/écrits. Vous ne pouvez pas effectuer de FTP sur le serveur et ajouter des modules. Au lieu de cela, vous devez ajouter du code à votre référentiel local et exécuter `git push`, qui crée et déploie l’environnement. Pour connaître la structure du projet, voir [Structure d’un répertoire de projet local](../project/file-structure.md).

### Phase 3 : préparation de la limace

Le résultat de la phase de création est un système de fichiers en lecture seule appelé _limace_. Cette phase crée une archive et place la limace dans un stockage permanent. La prochaine fois que vous pousserez le code, si un service n’a pas changé, il utilisera la limace de l’archive.

- Rend l’intégration continue plus rapide en réutilisant le code inchangé
- Si le code change, met à jour la balise pour le prochain build pour la réutiliser
- Permet la restauration instantanée d’un déploiement, si nécessaire
- Inclut des fichiers statiques si la variable `app/etc/config.php` existe dans le code base

La balise de fermeture comprend tous les fichiers et dossiers. **, à l’exception des éléments suivants** Monts configurés dans `magento.app.yaml`:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Phase 4 : déploiement des diffusions et de la grappe

Vos applications et tous les [backend](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) la prestation de services comme suit :

- monte chaque service dans un conteneur, tel que le serveur web, OpenSearch, [!DNL RabbitMQ]
- Monte le système de fichiers en lecture-écriture (monté sur une grille de stockage distribué hautement disponible).
- Configure le réseau de sorte que les services puissent &quot;se voir&quot; (et uniquement les uns les autres).

>[!NOTE]
>
>Apportez vos modifications dans une branche Git une fois la création et le déploiement terminés et relancez la notification push. Tous les systèmes de fichiers d’environnement _lecture seule_. Un système en lecture seule garantit les déploiements déterministes et améliore considérablement la sécurité de votre site, car aucun processus ne peut écrire dans le système de fichiers. Cela fonctionne également pour vous assurer que votre code est identique dans les environnements d’intégration, d’évaluation et de production.

### Phase 5 : hooks de déploiement

>[!NOTE]
>
>Cette phase place la variable [!DNL Commerce] en mode de maintenance jusqu’à la fin du déploiement.

La dernière étape exécute un script de déploiement que vous pouvez utiliser pour anonymiser les données dans les environnements de développement, vider les caches et interroger les outils externes d’intégration continue. Lorsque ce script s’exécute, vous avez accès à tous les services de votre environnement, tels que Redis.

Si la variable `app/etc/config.php` n’existe pas dans la base de code, les fichiers statiques sont compressés à l’aide de la commande `gzip` et déployés pendant cette phase, ce qui augmente la durée de la phase de déploiement et de la maintenance du site.

>[!NOTE]
>
>Voir [variables de déploiement](../environment/variables-deploy.md) pour en savoir plus sur la personnalisation ou la désactivation de la compression de fichier.

Il existe deux hooks de déploiement. La variable `pre-deploy.php` hook effectue le nettoyage et la récupération nécessaires des ressources et du code générés dans le crochet de génération. La variable `php ./vendor/bin/ece-tools deploy` hook exécute une série de commandes et de scripts :

- Si Adobe Commerce est **non installé**, il installe avec `bin/magento setup:install`, met à jour la configuration du déploiement, `app/etc/env.php`et la base de données de votre environnement spécifié, comme les URL des médias et des sites web. **Important :** Lorsque vous avez terminé la [Premier déploiement](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) lors de la configuration, Adobe Commerce a été installé et déployé dans tous les environnements.

- Si Adobe Commerce **est installé**, effectuez les mises à niveau nécessaires. Le script de déploiement s’exécute. `bin/magento setup:upgrade` mettre à jour le schéma et les données de la base de données (nécessaires après les mises à jour de l&#39;extension ou du code principal), et mettre à jour la configuration du déploiement, `app/etc/env.php`et la base de données de votre environnement. Enfin, le script de déploiement efface le cache d’Adobe Commerce.

- Le script génère éventuellement du contenu web statique à l’aide de la commande . `magento setup:static-content:deploy`.

- Utilise les portées (`-s` Indicateur dans les scripts de génération) avec le paramètre par défaut `quick` pour la stratégie de déploiement de contenu statique. Vous pouvez personnaliser la stratégie à l’aide de la variable d’environnement. [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Pour plus d’informations sur ces options et fonctionnalités, voir [Stratégies de déploiement des fichiers statiques](../deploy/static-content.md) et la variable `-s` indicateur pour [Déploiement de fichiers d’affichage statique](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>Le script de déploiement utilise les valeurs définies par les fichiers de configuration dans la variable `.magento` , puis le script supprime le répertoire et son contenu. Votre environnement de développement local n’est pas affecté.

### Post-déploiement : configuration du routage

Pendant le déploiement en cours d’exécution, le processus interrompt le trafic entrant au point d’entrée pendant 60 secondes et reconfigure le routage afin que le trafic web arrive au niveau de la grappe nouvellement créée.

Le déploiement réussi supprime le mode de maintenance pour permettre un accès normal et crée des fichiers de sauvegarde (BAK) pour le `app/etc/env.php` et la variable `app/etc/config.php` fichiers de configuration.

Activez la génération de contenu statique à l’aide de la fonction `SCD_ON_DEMAND` et configurez la variable [`post_deploy` hook](../application/hooks-property.md) afin qu’il efface le cache et pré-charge (réchauffe) le cache. _after_ le conteneur commence à accepter les connexions et _during_ trafic normal entrant.

Pour consulter les journaux de création et de déploiement, voir [Afficher les journaux](../test/log-locations.md#view-and-manage-logs).
