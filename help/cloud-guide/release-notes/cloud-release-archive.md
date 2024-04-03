---
title: Archivage des notes de mise à jour pour les outils citoyen
description: Découvrez les améliorations archivées pour les outils.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Archivage des notes de mise à jour pour les outils citoyen

>[!NOTE]
>
>Ces notes de mise à jour contiennent des informations et des mises à jour sur les `ece-tools` v2002.0.22 et versions ultérieures. Voir [Notes de mise à jour de la suite Cloud Tools](cloud-tools-suite.md) pour obtenir les dernières mises à jour d’ `ece-tools` et d’autres modules Cloud.

## v2002.0.22

La variable `ece-tools` La version 2002.0.22 modifie la structure du `ece-tools` pour découpler la version de `Adobe Commerce on cloud infrastructure` correctifs de la version CEE-Outils. À partir de cette version, les correctifs et correctifs critiques seront fournis à l’aide de la [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) qui est une nouvelle dépendance pour la variable `ece-tools` module. Nous avons apporté ces modifications afin de réduire la complexité de la planification des mises à jour des versions et de l’utilisation des contributions de la communauté.

- ![nouvelle icône](../../assets/new.svg) **Modifications apportées au module CEE-Outils**

   - ![nouvelle icône](../../assets/new.svg) Déplacement des correctifs Adobe Commerce à partir du `ece-tools` vers un nouveau module [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) module compositeur.

   - ![nouvelle icône](../../assets/new.svg) Mise à jour de la `composer.json` pour le fichier `ece-tools` pour ajouter une dépendance pour la variable `magento/magento-cloud-patches` Package v1.0.0.

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel la variable `ece-tools` correction du processus à interrompre lors de l’application de jeux de correctifs sur les versions de sécurité uniquement, à partir de la version 2.3.2-p2 et versions ultérieures. Ce problème a été introduit par le nouveau système de contrôle de version adopté pour [correctifs de sécurité uniquement](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![icône de correctif](../../assets/fix.svg) **Correctifs et correctifs critiques**-Mettre à jour vos environnements cloud avec `ece-tools` version 2002.0.22 pour appliquer les correctifs et correctifs critiques suivants. Ces correctifs sont inclus dans la variable `magento/magento-cloud-patches` Package v1.0.0.

   - ![icône de correctif](../../assets/fix.svg) **Correctifs de sécurité de Page Builder pour les versions 2.3.1.x et 2.3.2.x**-Correction d’un problème dans l’aperçu du Créateur de pages qui permettait aux utilisateurs non authentifiés d’accéder à certaines méthodes de création de modèles pouvant être utilisées pour déclencher l’exécution arbitraire du code sur le réseau (RCE), ce qui entraînait des fuites d’informations globales. Ce problème peut se produire lors de l’utilisation de versions non prises en charge de Page Builder avec Adobe Commerce versions 2.3.1 et 2.3.2.<!--MAGECLOUD-4649-->

   - ![icône de correctif](../../assets/fix.svg) **Correctifs MSI**- Correction de problèmes qui provoquaient des erreurs d’indexation et des problèmes de performances lors de l’utilisation des paramètres de stock par défaut pour la gestion du stock.<!--MAGECLOUD-4428-->

   - ![icône de correctif](../../assets/fix.svg) **Compatibilité descendante des nouvelles interfaces de messagerie**-Correction d’un problème d’incompatibilité en amont provoqué par le paramètre `Magento\Framework\Mail\EmailMessageInterface` Interface PHP introduite dans Adobe Commerce v2.3.3. Dans la portée de ce correctif, la nouvelle `EmailMessageInterface` hérite de l’ancien `MessageInterface`, et les modules principaux Adobe Commerce dépendent désormais de `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![icône de correctif](../../assets/fix.svg) **La pagination du catalogue ne fonctionne pas sur Elasticsearch 6.x**-Correction d’un problème critique lié à la pagination des résultats de recherche qui affectait les clients utilisant Elasticsearch 6.x comme moteur de recherche de catalogue.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) **Nouvelles images Docker**—Pris en charge par les versions 2.3.3 et ultérieures<!-- MAGECLOUD-3345 -->

      - PHP version 7.3.<!-- MAGECLOUD-4017 -->

      - Cache Varnish 6.2.0<!-- MAGECLOUD-4017 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge d’appliquer une configuration de crochet personnalisée spécifiée dans `.magento.app.yaml` dans l’environnement Docker. Auparavant, l’environnement Docker ne prenait en charge que la configuration du crochet par défaut.<!-- MAGECLOUD-3505-->

   - ![nouvelle icône](../../assets/new.svg) Les fichiers ENV Docker ne sont plus générés pendant la génération Docker et la variable `docker:config:convert` est obsolète. Les données correspondantes sont désormais stockées dans la variable `docker-compose.yml` fichier .<!-- MAGECLOUD-3816-->

   - ![nouvelle icône](../../assets/new.svg) **Image PHP mise à jour**-Ajout de Node.js à l’image du Docker PHP pour prendre en charge les fonctionnalités node, npm et grunt-cli.<!-- MAGECLOUD-3953 -->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des variables d’environnement**-

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **LOCK_PROVIDER** deploy pour configurer le fournisseur de verrouillage qui empêche le lancement des tâches cron et des groupes cron en double. Voir la description de la variable dans la section [variables de déploiement](../environment/variables-deploy.md#lock_provider) rubrique.<!-- MAGECLOUD-4052 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **CONSUMERS_WAIT_FOR_MAX_MESSAGES** variable d’environnement pour configurer la manière dont les consommateurs traitent les messages de la file d’attente des messages lors de l’utilisation de la variable `CRON_CONSUMERS_RUNNER` pour gérer les tâches cron. Voir la description de la variable dans la section [variables de déploiement](../environment/variables-deploy.md#consumers_wait_for_max_messages) rubrique.<!-- MAGECLOUD-4071 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui pouvait entraîner des erreurs de blocage de base de données lors de l’événement `consumers_runner` la tâche cron démarre plusieurs instances d’un même consommateur sur différents noeuds. Maintenant, si vous avez activé la variable [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) déploie la variable dans votre environnement, la variable `consumers_runner` La tâche utilise la fonction `single-thread` pour démarrer une instance de chaque consommateur sur un seul noeud.<!-- MAGECLOUD-3913 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème affectant [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) qui utilise une URL de magasin par défaut. Maintenant, si la variable `config:show:default-url` ne peut pas récupérer une URL de base, alors l’URL de la variable MAGENTO_CLOUD_ROUTES est utilisée.<!-- MAGECLOUD-3866 -->

- ![nouvelle icône](../../assets/new.svg) Mise à jour des informations de journalisation renvoyées par le `module:refresh` . Vous pouvez désormais voir une liste détaillée des modules activés dans le `cloud.log` fichier .<!-- MAGECLOUD-2514 -->

- ![nouvelle icône](../../assets/new.svg) Amélioration de la validation de la compatibilité des versions et des notifications d’avertissement pour les problèmes de compatibilité entre la version d’Adobe Commerce et les services installés, tels que Elasticsearch, [!DNL RabbitMQ], Redis et DB.<!-- MAGECLOUD-3535 -->

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de la version 3.8 de RabitMQ.<!-- MAGECLOUD-4674-->

- ![nouvelle icône](../../assets/new.svg) Mise à jour des validations interactives pour la compatibilité des services afin de refléter les versions prises en charge pour les nouvelles versions Adobe Commerce 2.3.3 et 2.2.10. Voir [Configuration requise](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) dans le _Guide d’installation_ pour les versions recommandées.<!-- MAGECLOUD-4018 -->

- ![icône de correctif](../../assets/fix.svg) Amélioration du message de journal renvoyé lorsque le processus de gestion des tâches cron de la phase de déploiement tente d’arrêter une tâche cron déjà terminée pour clarifier que ce problème n’est pas une erreur. Modification du niveau de journal de `INFO` to `DEBUG`.<!-- MAGECLOUD-3653-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lors de l’exécution de la variable `setup:upgrade` qui n’a pas interrompu le processus de déploiement lorsqu’un échec s’est produit au cours de la `app:config:import` tâche.<!-- MAGECLOUD-3806 -->

- ![nouvelle icône](../../assets/new.svg) Modification du niveau de journalisation par défaut du gestionnaire de fichiers en `debug` pour réduire la quantité de détails dans le journal affiché dans la variable [!DNL Cloud Console], tout en fournissant des informations détaillées pour le débogage.<!-- MAGECLOUD-3871 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur lors du déploiement de contenu statique lors de la génération. Après une installation et `ece-tools` config dump, une erreur s’est produite si aucun paramètre régional n’était spécifié pour l’utilisateur administrateur dans la variable `config.php` fichier . Désormais, il existe un paramètre régional par défaut pour l’utilisateur admin dans le `config.php` fichier .<!-- MAGECLOUD-3957 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’une `Undefined index error` qui survient lorsqu’un événement `magento-cloud` La commande d’interface de ligne de commande échoue dans un environnement qui n’est pas configuré avec une URL sécurisée (https). Désormais, le package CEE-Outils utilise l’URL de base (http) si l’URL sécurisée n’est pas disponible.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) Vous pouvez désormais effectuer des tests fonctionnels à l’aide de la fonction `ece-tools` dans l’environnement Docker. Voir [test d’application](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de la configuration des modules PHP à l’aide du `.magento.app.yaml` fichier . Quelconque [Extensions PHP spécifiées dans `.magento.app.yaml` fichier](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) sont disponibles dans les conteneurs PHP Docker.<!-- MAGECLOUD-3357 -->

   - ![nouvelle icône](../../assets/new.svg) De nouvelles commandes sont disponibles pour améliorer l’expérience de ligne de commande Docker. Voir [`bin/magento-docker` section de référence Docker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la possibilité d’utiliser Mutagen.io pour synchroniser les fichiers pendant le développement entre l’hôte local et Docker.<!-- MAGECLOUD-3559 -->

   - ![icône de correctif](../../assets/fix.svg) Correction du chemin par défaut lors de l’utilisation de l’environnement Docker. Désormais, lorsque vous utilisez SSH pour vous connecter au conteneur Docker, vous vous trouvez à la racine du projet dans le `/app` , comme prévu.<!-- MAGECLOUD-3582 -->

   - ![icône de correctif](../../assets/fix.svg) Mise à jour de la bibliothèque Sodium de la version 1.0.11 vers la version 1.0.18, et mise à jour de l’extension Sodium PHP.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Les clients d’Adobe Commerce sur l’infrastructure cloud doivent [Envoi d’un ticket d’assistance Adobe Commerce](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) pour mettre à niveau le package libsodium sur les environnements de production et d’évaluation avant la mise à niveau vers Adobe Commerce 2.3.2. Actuellement, vous ne pouvez pas mettre à niveau les environnements de démarrage vers Adobe Commerce 2.3.2.

   - ![icône de correctif](../../assets/fix.svg) Ajout de la `analysis-icu` et la variable `analysis-phonetic` Modules externes Elasticsearch à toutes les images Docker.<!-- MAGECLOUD-3446 -->

   - ![icône de correctif](../../assets/fix.svg) Validations améliorées : lors de l’utilisation d’options pour la variable `docker:build` , vous devez fournir une valeur lors de l’utilisation d’une option. En outre, ajout de la validation de la version de noeud lors de l’utilisation de la propriété `docker:build run` .<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des variables d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge des préfixes de table de base de données à l’aide du [Variable d’environnement DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **FORCE_UPDATE_URLS** déploie la variable pour mettre à jour les URL de base lors du déploiement dans les environnements de production et d’évaluation Pro et Starter. Voir la définition dans la section [variables de déploiement](../environment/variables-deploy.md#force_update_urls) contenu.<!-- MAGECLOUD-3602 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **TTF_TESTED_PAGES** variable post-déploiement à configurer _Time to First Byte_ tests de page pour vérifier les performances de l’application sur les sites déployés sur l’infrastructure cloud. Voir la description de la variable dans [variables post-déploiement](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié aux SCD multithreads, qui provoquait des échecs aléatoires dans le déploiement de contenu statique. La solution impliquait de définir la variable **SCD_THREADS** vers `1`. Vous pouvez maintenant augmenter le nombre suivant vos besoins. Reportez-vous aux définitions de la section [variables de déploiement](../environment/variables-deploy.md#scd_threads) et la variable [variables de création](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![icône de correctif](../../assets/fix.svg) Vous pouvez configurer la variable **WARM_UP_PAGES** pour mettre en cache des pages uniques, plusieurs domaines et plusieurs pages. Voir la définition développée dans la section [variables post-déploiement](../environment/variables-post-deploy.md#warm_up_pages) contenu.<!-- MAGECLOUD-3258 -->

- ![icône de correctif](../../assets/fix.svg) Ajout de la `pub/static/.htaccess` vers la liste d’exclusion. [Correctif soumis par Björn Kraus de PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur lors de l’affichage de tous les messages de validation comme `Critical` si au moins un validateur de niveau critique a renvoyé une erreur.<!-- MAGECLOUD-3178 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait un échec de déploiement si l’URL de base n’existait pas dans la base de données.<!-- MAGECLOUD-3075 -->

- ![nouvelle icône](../../assets/new.svg) Ajout d’une nouvelle **`env:config:show`command** à la fonction `ece-tools` module qui affiche des services d’environnement, des itinéraires ou des variables. Voir [Services, itinéraires et variables](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Fonctionnalité présentée par Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur critique lors de la tentative d’installation d’Adobe Commerce 2.2.6 ou version antérieure avec `ece-tools` développer après la refactorisation du shell.<!-- MAGECLOUD-3665 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel les installations d’Adobe Commerce 2.1.x et 2.2.x échouaient avec un avertissement d’utilisation d’une version obsolète de Carbon.<!-- MAGECLOUD-3704 -->

- ![icône de correctif](../../assets/fix.svg) Diminuer les `cloud.log` niveau de journal de la sortie shell à partir de `info` to `debug`.<!-- MAGECLOUD-3277 -->

- ![icône de correctif](../../assets/fix.svg) Ajout de la `--remove-definers (-d)` à l’option `ece-tools db-dump` pour supprimer les définitions du fichier de vidage.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui remplaçait le paramètre `env.php` lors d’un déploiement, ce qui entraîne la perte des configurations personnalisées. Cette mise à jour permet de s’assurer qu’Adobe Commerce sur l’infrastructure cloud met à jour la variable `env.php` avec chaque déploiement, tout en conservant les configurations personnalisées.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) Désormais, l’environnement Docker prend en charge la configuration cron définie dans la variable [propriété crons du fichier .magento.app.yaml](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![nouvelle icône](../../assets/new.svg) **Nouveau conteneur Docker**: ajout d’un [Conteneur proxy de terminaison TLS](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) pour faciliter l’arrêt Varnish SSL par HTTPS.<!-- MAGECLOUD-2890 -->

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle image Docker**: ajout d’une image Node.js pour la prise en charge de Gulp et d’autres fonctionnalités, telles que le test d’unité JS Jasmin.<!-- MAGECLOUD-3345 -->

   - ![nouvelle icône](../../assets/new.svg) **Modes de création Docker**: vous pouvez désormais choisir de lancer l’environnement Docker dans [Mode Production ou mode Développeur](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). Le mode Développeur prend en charge le développement actif avec des autorisations complètes de système de fichiers modifiables.<!-- MAGECLOUD-3152/3511 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel le déploiement de Docker échouait avec une `Name or service not known` si le cache est configuré pour un service qui n’est pas disponible. Désormais, vous pouvez supprimer un service du [`.magento/services.yaml` fichier](https://devdocs.magento.com/cloud/project/services.html). Le générateur de configuration Docker met à jour le service dans `docker/config.php.dist` fichier automatiquement.<!-- MAGECLOUD-3369 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de validations interactives pour la compatibilité des services. Désormais, si un service demandé est incompatible avec la version Adobe Commerce ou d’autres services, la variable _mode interactif_ invite l’utilisateur à recevoir un message et à choisir de continuer. Voir [Versions de service](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) disponible pour Docker. Utilisez la variable `-n` pour ignorer l’interactivité à des fins de CICD.<!-- MAGECLOUD-3251 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié à la composition Docker. `db-dump` qui effaçait les vidages existants.<!-- MAGECLOUD-3366 -->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui affectait des Redis `session`, `default`, et `page_cache` stockage dans le cache vers le même ID de base de données.<!-- MAGECLOUD-3172 -->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des variables d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) La nouvelle **ELASTICSUITE\_CONFIGURATION** La variable d’environnement conserve vos paramètres de service personnalisés entre les déploiements. Voir la définition dans la section [variables de déploiement](../environment/variables-deploy.md#elasticsuite_configuration) contenu.<!-- MAGECLOUD-3205 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **SCD_MAX_EXECUTION_TIMEOUT** afin que vous puissiez augmenter le temps nécessaire pour effectuer le déploiement de contenu statique à partir de la variable `.magento.env.yaml` fichier . Voir la définition dans la section [variables de déploiement](../environment/variables-deploy.md#scd_max_execution_time), la variable [variables de création](../environment/variables-build.md#scd_max_execution_time), et la variable [variables globales](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![nouvelle icône](../../assets/new.svg) Ajout de la **MAGENTO_CLOUD_LOCKS_DIR** pour configurer le chemin d’accès au point de montage du fournisseur de verrouillage sur l’infrastructure cloud. Le fournisseur de verrouillage empêche le lancement de tâches cron en double et de groupes cron. Cette variable est prise en charge sur Adobe Commerce version 2.2.5 et ultérieure et automatiquement configurée. Voir la définition dans [Variables cloud](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![icône de correctif](../../assets/fix.svg) Modification de la variable **SCD_THREADS** valeurs par défaut de la variable d’environnement pour déterminer automatiquement la valeur optimale en fonction du nombre de threads du processeur détecté. Voir les définitions mises à jour dans la section [variables de déploiement](../environment/variables-deploy.md#scd_threads) et la variable [variables de création](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié à un correctif pour le mécanisme d’isolation de la base de données qui provoquait une erreur lors de la mise à niveau vers Adobe Commerce sur la version 2002.0.16 de l’infrastructure cloud.<!-- MAGECLOUD-3383 -->

- ![icône de correctif](../../assets/fix.svg) Ajout d’un correctif qui remplace _Graphiques d’images Google_ avec _Graphiques d’images_. Consultez l’article DevBlog . [Obsolescence et mise à jour des graphiques Google pour M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![icône de correctif](../../assets/fix.svg) Ajout de la validation de la variable [Variable SEARCH_CONFIGURATION](../environment/variables-deploy.md#search_configuration). Le déploiement échoue lorsque l’option &quot;moteur&quot; n’est pas définie et `_merge` n’est pas obligatoire.<!-- MAGECLOUD-3470 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui exposait des données sensibles après une exception. Désormais, les informations sensibles sont masquées de manière appropriée.<!-- MAGECLOUD-3525 -->

- ![icône de correctif](../../assets/fix.svg) Amélioration des paramètres de tolérance aux pannes du module de Magento Open Source. Dans le cas où Adobe Commerce ne peut pas lire les données des Redis `slave` instance, une lecture est faite à partir du Redis `master` instance. Voir [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>La variable `ece-tools` La version 2002.0.17 comprend un correctif de sécurité important. Voir [Ressources techniques : correctifs pour les Magento Open Sources](https://magento.com/tech-resources/download#download2288).

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—Pris en charge par les versions Adobe Commerce suivantes : 2.2.8 et versions ultérieures 2.2.x, 2.3.1 et versions ultérieures 2.3.x

   - Ajout de la prise en charge de la version 6.x d’Elasticsearch.<!-- MAGECLOUD-3196 -->

   - Ajout de la prise en charge de Redis version 5.0.

- ![nouvelle icône](../../assets/new.svg) **Nouvelles images Docker**—Ajout des services suivants à la version Docker :

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement**: auparavant, il existait un délai d’expiration codé en dur pour la compression SCD. Vous pouvez maintenant configurer le délai d’expiration de la compression SCD à l’aide de la fonction **SCD_COMPRESSION_TIMEOUT** Variable d’environnement. Reportez-vous aux définitions de la section [variables de création](../environment/variables-build.md#scd_compression_timeout) et la variable [variables de déploiement](../environment/variables-deploy.md#scd_compression_timeout) contenu.<!-- MAGECLOUD-2870 -->

- ![icône de correctif](../../assets/fix.svg) Ajout de la `--use-rewrites` à la commande install afin d’utiliser les réécritures du serveur web pour les liens générés dans le storefront et l’accès administrateur pour améliorer la sécurité et l’expérience client.<!-- MAGECLOUD-3246 -->

- ![icône de correctif](../../assets/fix.svg) Ajout d’horodatages à la variable `var/log/install_upgrade.log` afin qu’il affiche les dates des événements d’installation et de mise à niveau.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - Désormais, la configuration de service par défaut générée dans l’environnement Docker est identique à la configuration par défaut dans le modèle Cloud.<!-- MAGECLOUD-3025 -->

   - Vous pouvez envoyer du courrier à partir de votre environnement Docker à l’aide de la fonction `sendmail` service.<!-- MAGECLOUD-2907 -->

   - Ajout de la capacité à [configurer Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) pour déboguer dans l’environnement Cloud Docker.<!-- MAGECLOUD-2891 -->

   - Correction d’un problème lié aux autorisations de service Web lors de la génération de la variable `docker-compose.yml` fichier .<!-- MAGECLOUD-2883 -->

- ![nouvelle icône](../../assets/new.svg) **Amélioration de la mise à niveau**: ajout d’une validation pour confirmer que la variable `autoload` dans la propriété `composer.json` contient les modifications de configuration requises avant la mise à niveau vers Adobe Commerce v2.3. Voir [Version de mise à niveau](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![nouvelle icône](../../assets/new.svg) Le processus de compression dans le déploiement de contenu statique inclut désormais toutes les ressources (générées en mode natif ou personnalisées) et se produit pendant la phase de création au début de la [`build:transfer` section](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Auparavant, le processus de compression se produisait avant d’appliquer une minification et un regroupement personnalisés de ressources statiques. [Correctif soumis par Rafael Garcia Lepper de Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur de connexion à la base de données qui se produisait lors du déploiement immédiatement après la configuration d’une base de données et d’une relation de service supplémentaires. Ce correctif résout également un problème qui s’est produit pendant le processus de configuration de la création de rapports Commerce pour le démarrage. Pour commencer, cette mise à niveau est un &quot;must have&quot; pour l’utilisation des rapports de commerce.<!-- MAGECLOUD-3035 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de validation de la configuration de la base de données en raison duquel le processus de déploiement échouait.<!-- MAGECLOUD-3003 -->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de la contrainte avec la version appropriée de la variable `symfony/yaml` module à utiliser avec [constantes PHP](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). L’analyse constante ne fonctionne pas lors de l’utilisation d’une `symfony/yaml` version de package antérieure à 3.2. [Correctif soumis par Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![nouvelle icône](../../assets/new.svg) **Vérification de la configuration de l’environnement**: ajout d’une validation permettant de vérifier la version PHP et d’avertir les utilisateurs s’ils n’utilisent pas la dernière version recommandée.<!--MAGECLOUD-2903-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié au traitement des variables JSON incorrectes. Désormais, si une variable JSON entraîne une erreur de syntaxe, un avertissement s’affiche dans la variable `cloud.log` Le déploiement et le fichier continuent à utiliser la variable par défaut.<!-- MAGECLOUD-2851 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur de connexion qui se produisait lors du déploiement immédiatement après la désactivation du service Redis.<!-- MAGECLOUD-2747 -->

- ![nouvelle icône](../../assets/new.svg) **Modifications de journalisation**: mise à jour de la variable [niveau de journal](../environment/log-handlers.md#log-levels) de `Info` to `Notice` pour les événements de processus de création et de déploiement suivants :<!--MAGECLOUD-2925-->

   - Démarrage et fin du processus de réconciliation des modules installés dans `composer.json` avec les paramètres de configuration partagés dans la `app/etc/config.php` fichier

   - Démarrage et fin du processus de validation de configuration

   - Début et fin de la `setup:di:compile` processus de génération de classes

- ![nouvelle icône](../../assets/new.svg) **Nouvelles variables d’environnement**—

   - **[Variable de déploiement RESOURCE_CONFIGURATION](../environment/variables-deploy.md#resource_configuration)**: utilisez cette variable pour mapper un nom de ressource à une connexion de base de données.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION variable globale](../environment/variables-global.md#x_frame_configuration)**: utilisez cette variable pour modifier la variable `X-Frame-Options` configuration d’en-tête pour le rendu d’une page Adobe Commerce dans une `<frame>`, `<iframe>`, ou `<object>`.<!-- MAGECLOUD-3048 -->

- ![icône de correctif](../../assets/fix.svg) **Mises à jour des variables d’environnement**—Modification des variables d’environnement suivantes :

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**: ajout de la fonctionnalité de préchargement du cache pour les pages spécifiées sur tous les domaines définis pour un magasin Adobe Commerce. Auparavant, si votre site était configuré avec plusieurs domaines, le processus de post-déploiement ne parvenait pas à précharger le cache pour les pages spécifiées sur les domaines autres que les domaines par défaut et renvoyait l’erreur suivante dans le journal de post-déploiement : `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**—Mise à jour de la documentation et de l’exemple `.magento.env.yaml` avec les valeurs par défaut correctes pour le niveau de compression SCD. Reportez-vous aux définitions de la section [variables de création](../environment/variables-build.md#scd_compression_level) et la variable [variables de déploiement](../environment/variables-deploy.md#scd_compression_level) contenu.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES**: cette variable d’environnement est obsolète. Utilisez la variable [SCD_MATRIX](../environment/variables-build.md#scd_matrix) pour contrôler la configuration du thème.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX**: correction du processus de validation afin d’éviter un problème qui se produisait lorsque SCD_MATRIX ignorait une valeur de thème contenant différents cas de caractères. Reportez-vous aux définitions de la section [variables de création](../environment/variables-build.md#scd_matrix) et la variable [variables de déploiement](../environment/variables-deploy.md#scd_matrix) contenu.<!-- MAGECLOUD-2904 -->

   - **Variables ADMIN**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Amélioration de la sécurité lors de la gestion des informations d’identification de l’utilisateur administrateur à l’aide de variables d’environnement. Vous ne pouvez plus utiliser les variables d’environnement ADMIN_EMAIL, ADMIN_USERNAME et ADMIN_PASSWORD pour remplacer les informations d’identification d’administrateur lors des mises à niveau. Si vous ne pouvez pas accéder au panneau d’administration, utilisez le _Mot de passe oublié_ ou la fonction `admin:user:create` Commande d’interface de ligne de commande pour créer un utilisateur administrateur. Voir [Accès à votre panneau d’administration](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL n’est plus nécessaire lors de la mise à niveau ou de l’application de correctifs.

## v2002.0.15

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - Désormais, Docker Generator utilise les services spécifiés dans la variable `.magento.app.yaml` et `.magento/services.yaml` fichiers de configuration lors de [création de votre environnement Docker](https://devdocs.magento.com/cloud/docker/docker-config.html). Vous pouvez choisir une autre version de service à l’aide des paramètres de version.<!-- MAGECLOUD-2888 -->

   - Ajout d’une image PHP 7.2 : ajout de la prise en charge de PHP 7.2 dans Cloud Docker ; mise à jour de la fonction [Configuration de Launch Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) pour inclure la variable `docker:build --php` pour spécifier la version de PHP compatible avec votre version d’Adobe Commerce.<!-- MAGECLOUD-2799 -->

   - Ajout d’une [Conteneur Cron](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) en fonction de l’image PHP-CLI.<!-- MAGECLOUD-2565 -->

   - Ajout des services suivants à la version Docker :

      - [!DNL RabbitMQ] 3.5 et 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 et 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 et 4.0<!-- MAGECLOUD-2886 -->

- ![nouvelle icône](../../assets/new.svg) **Configuration avec des constantes PHP**: ajout de la prise en charge de [constantes PHP](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) dans le `.magento.env.yaml` fichier de configuration.<!-- MAGECLOUD- 2575 -->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement**: par défaut, seuls les Google Analytics sont activés dans l’environnement de production. Vous pouvez activer les Google Analytics dans les environnements d’évaluation et d’intégration à l’aide de la variable  [Variable d’environnement ENABLE_GOOGLE_ANALYTICS](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui supprimait les configurations cron personnalisées de la `env.php` après un redéploiement. Désormais, les configurations cron personnalisées restent dans la variable `env.php` fichier .<!-- MAGECLOUD-2923 -->

- ![icône de correctif](../../assets/fix.svg) Correction des incohérences dans les messages et [niveaux de journal](../environment/log-handlers.md#log-levels) pour les phases de création, de déploiement et de post-déploiement. Augmentation des niveaux de messages de début et de fin du journal à partir de **info** to **notice** pour toutes les phases et sous-phases. Ajout des messages de début et de fin du journal, le cas échéant.<!-- MAGECLOUD-2919 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème concernant les processus cron qui empêchait le début de la phase de post-déploiement, lorsqu’ils étaient configurés. Désormais, si le crochet post-déploiement est activé, les processus cron sont à nouveau activés au début de la phase post-déploiement.<!-- MAGECLOUD-2862 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui empêchait l’installation réussie d’Adobe Commerce lors de la spécification d’une configuration de base de données personnalisée. Auparavant, le processus d’installation utilisait la configuration de la base de données du [Variable Magento_CLOUD_RELATIONSHIP](../environment/variables-cloud.md) même si vous avez désigné des informations de connexion personnalisées dans la variable [Variable d’environnement DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![icône de correctif](../../assets/fix.svg) Correction de la variable `config:dump` afin d’inclure chaque paramètre régional du site web dans la variable `system` de la `config.php` fichier .<!--MAGECLOUD-2740-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui entraînait _chauffage_ lors de la phase de post-déploiement en corrigeant la référence de l’URL de base source.<!--MAGECLOUD-2797-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui générait incorrectement des fichiers pendant la `setup:di:compile` qui a affecté le module paiement d’Amazon.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![nouvelle icône](../../assets/new.svg) **Vérification de l’état idéal**—The `ideal-state` L’assistant vérifie désormais la configuration actuelle au cours de chaque déploiement et fournit des instructions claires pour la mise à jour de la configuration afin d’accélérer le déploiement sans interruption.<!--MAGECLOUD-2372-->

- ![icône de correctif](../../assets/fix.svg) **Conformité PCI**: mise à jour des protocoles de messagerie d’Adobe Commerce sur l’infrastructure cloud afin qu’ils requièrent la version 1.2 de Transport Layer Security (TLS) lors de la connexion à des services de messagerie tiers. Si vous utilisez un service de messagerie qui ne prend pas en charge TLS version 1.2, vous devez mettre à niveau votre service. Dans le cas contraire, le message d’erreur suivant s’affiche lorsque votre application Adobe Commerce tente de se connecter au serveur de messagerie pour envoyer un courrier électronique : `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![nouvelle icône](../../assets/new.svg) **Amélioration du déploiement**: ajout d’une validation pour avertir les clients si un environnement d’évaluation ou de production possède `dev`, `debug`, ou `debug_logging` options activées pour empêcher les problèmes de performances causés par une activité de journalisation excessive.<!--MAGECLOUD-2517-->

- ![icône de correctif](../../assets/fix.svg) **Correctifs de déploiement**—

   - Désormais, le mode de maintenance est activé au début de la phase de déploiement et désactivé à la fin. Si le déploiement échoue, le site reste en mode de maintenance jusqu’à ce que les problèmes de déploiement soient résolus. Auparavant, le site revenait en mode de production même si le déploiement échouait.<!--MAGECLOUD-2603-->

      - Reprise des contrôles de validation de la phase de déploiement afin de rétrograder le niveau d’erreur pour les problèmes de déploiement suivants de `CRITICAL` to `WARNING` pour que le déploiement soit terminé. Auparavant, ces problèmes provoquaient l’échec du déploiement.

      - La configuration de l’environnement contient des valeurs incorrectes pour les variables de déploiement ou de cloud.

   - La version Elasticsearch de l’infrastructure cloud est incompatible avec la version du module de recherche flexible/élasticsearch pris en charge par Adobe Commerce sur l’infrastructure cloud. Voir [Article de dépannage pour les Elasticsearch](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) dans la base de connaissances du support Adobe Commerce.<!--MAGECLOUD-2600-->

   - Correction d’un problème lié aux paramètres de configuration partagés dans la variable `app/etc/config.php` fichier provoqué `recursion detected` erreurs lors du déploiement.<!--MAGECLOUD-2173-->

- ![icône de correctif](../../assets/fix.svg) **Correctifs liés à Cron**—

   - Correction d’un problème de planification cron qui empêchait l’exécution des tâches si vous spécifiez une fréquence cron autre que la fréquence par défaut (1 minute).<!--MAGECLOUD-2602-->

   - Correction d’un problème au cours de la phase de déploiement en raison duquel les tâches cron continuaient à s’exécuter pendant le déploiement, ce qui pouvait entraîner des verrous de base de données et d’autres problèmes critiques. Désormais, toutes les tâches cron sont arrêtées avant le début de la phase de déploiement et redémarrées une fois le déploiement terminé.&lt;!—MAGECLOUD—2537—>

   - Correction du workflow de tâche cron dans les versions 2.2.x pour déverrouiller les tâches cron gelées afin qu’elles puissent être arrêtées avant de commencer le déploiement. Auparavant, une tâche cron figée provoquait le blocage du déploiement.<!--MAGECLOUD-2501-->

- ![icône de correctif](../../assets/fix.svg) Modification du format de la variable `config.php` généré par le `vendor/bin/ece-tools config:dump` pour utiliser la syntaxe de tableau court et la mise en retrait 4 espaces afin de respecter les normes de codage Adobe Commerce.<!--MAGECLOUD-2527-->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur de déploiement qui se produisait lors de la `.magento.env.yaml` contains `{{ base_url }}` et `{{ unsecure_base_url }}` des espaces réservés aux configurations web au lieu de la configuration d’URL par défaut pour un projet d’infrastructure cloud Adobe Commerce./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![nouvelle icône](../../assets/new.svg) **Activation du déploiement sans interruption**: Adobe Commerce sur l’infrastructure cloud met désormais en file d’attente les demandes avec les modifications de base de données requises pendant le déploiement et applique les modifications dès que le déploiement est terminé. Les demandes peuvent être conservées pendant 5 minutes au maximum pour garantir qu’aucune session n’est perdue. Voir [Options de déploiement de contenu statique pour réduire le temps d’arrêt du déploiement sur le cloud](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![nouvelle icône](../../assets/new.svg) **Composition Docker pour Cloud**: les améliorations suivantes ont été apportées au [Configuration et configuration du Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) process:

   - Ajout d’une commande —`docker:config:convert` pour convertir des fichiers de configuration PHP au format Docker ENV afin de simplifier la configuration de l’environnement. Vous copiez maintenant les fichiers de configuration PHP dans le répertoire Docker et les convertissez en fichiers Docker ENV. Voir [Launch Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Le processus d’installation d’Adobe Commerce sur l’infrastructure cloud prend désormais en charge le déploiement sur les systèmes de fichiers en lecture seule et en lecture-écriture afin d’émuler plus étroitement le système de fichiers Cloud. Voir [Configuration de Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Prise en charge du service Redis**: ajout d’une image Redis, qui est déployée dans un conteneur Docker et configurée automatiquement pour fonctionner avec votre installation Docker.&lt;!—MAGECLOUD—2442—>

   - Désormais, vous disposez de la fonctionnalité de vidage DB lors de l’utilisation de Cloud Docker. [conteneur de base de données](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Vous pouvez également [partage de fichiers](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) entre un ordinateur hôte et un conteneur à l’aide de la variable `docker/mnt` répertoire .<!-- MAGECLOUD-2577 -->

   - **Prise en charge du service en pointillé**— Ajout d’une image vernis, qui est déployée automatiquement sur un conteneur Docker. Après le déploiement, vous pouvez configurer manuellement le vernis en suivant les bonnes pratiques d’Adobe Commerce. Voir [Configurer et utiliser le vernis](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Accès sécurisé au site : ajout de la prise en charge SSL pour accéder à votre boutique Adobe Commerce et à votre panneau d’administration.&lt;!—MAGECLOUD—2360—>

- ![icône de correctif](../../assets/fix.svg) **Amélioration de la prise en charge des extensions d’infrastructure cloud par Adobe Commerce**: mise à niveau de la version minimale requise pour le package guzzlehttp/guzzle dans Adobe Commerce sur l’infrastructure cloud. [fichier compositeur.json](https://devdocs.magento.com/cloud/reference/cloud-composer.html) vers la version 6.2 de sorte que la variable `ece-tools` est compatible avec d’autres extensions.<!--MAGECLOUD-2205-->

- ![nouvelle icône](../../assets/new.svg) **Application de modifications personnalisées à votre application Adobe Commerce pendant la phase de création**: la phase de création a été scindée en deux processus distincts, de sorte que vous puissiez utiliser des crochets pour appliquer des modifications personnalisées au contenu statique généré avant de compresser l’application en vue du déploiement. La variable _build:generate_ Le processus génère du code, applique des correctifs et génère du contenu statique. La variable _build:transfer_ Le processus transfère le code généré et le contenu statique vers la destination finale. Voir [Hooks d’application](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![icône de correctif](../../assets/fix.svg) **Vérification de la configuration des environnements**: validation améliorée de la configuration de l’environnement afin d’avertir les clients des incompatibilités de version et des erreurs de configuration avant de créer et de déployer Adobe Commerce sur l’infrastructure cloud.

   - Ajout d’une validation spécifique à la version afin d’identifier les variables et valeurs d’environnement non prises en charge ou obsolètes.<!--MAGECLOUD-2183-->

   - Ajout d’une vérification de compatibilité des Elasticsearch pour avertir les utilisateurs des problèmes de configuration des Elasticsearch. Désormais, le déploiement échoue si la version du service Elasticsearch sur le serveur est incompatible avec Adobe Commerce. Auparavant, le déploiement réussissait même si la version de l’Elasticsearch était incompatible, ce qui provoquait des problèmes de catalogue de produits après le déploiement du site.<!--MAGECLOUD-2389-->

     Vous pouvez résoudre l’incompatibilité en [envoi d’un ticket d’assistance](https://devdocs.magento.com/cloud/trouble/trouble.html) pour mettre à niveau l’Elasticsearch vers une version compatible, ou modifiez la configuration Adobe Commerce afin de spécifier une version compatible du client PHP Elasticsearch.

      - Pour Adobe Commerce version 2.1.x à 2.2.2, mettez à niveau Elasticsearch vers la version 2.4.

      - Pour Adobe Commerce version 2.2.3 et ultérieure, mettez à niveau l’Elasticsearch vers la version 5.2.

      - Si vous disposez de la version 1.x ou 2.x d’Elasticsearch et que vous ne souhaitez pas effectuer la mise à niveau, mettez à jour la version du client PHP d’Adobe Commerce Elasticsearch en indiquant `"elasticsearch/elasticsearch": "~2.0"`.

   - Amélioration de la validation des variables d’environnement afin d’identifier les paramètres de configuration pouvant entraîner des conflits lors des phases de création, de déploiement et de post-déploiement. Par exemple, un message d’avertissement s’affiche pendant le processus d’installation et de mise à niveau si le paramètre global pour le déploiement de contenu statique est en conflit avec les paramètres de la phase de création ou de déploiement.<!--MAGECLOUD-2156-->

- ![icône de correctif](../../assets/fix.svg) **Mises à jour des variables d’environnement**—Modification des variables d’environnement suivantes :

   - **[SKIP_HTML_MINIFICATION variable globale](../environment/variables-global.md#skip_html_minification)**: modification de la valeur par défaut en `true` pour activer la minimisation du contenu HTML à la demande, ce qui réduit le temps d’arrêt lors du déploiement dans les environnements d’évaluation et de production. Cette configuration est requise pour les déploiements sans interruption.<!--MAGECLOUD-2435-->

   - **[Variable de déploiement CLEAN_STATIC_FILES](../environment/variables-deploy.md#clean_static_files)**: ajout de la capacité de gérer le traitement des fichiers statiques propres pour le contenu statique généré lors de la phase de création en fonction du paramètre d’environnement CLEAN_STATIC_FILES . Auparavant, les fichiers de contenu statique générés pendant la phase de création étaient toujours nettoyés.<!--MAGECLOUD-1506-->

- ![icône de correctif](../../assets/fix.svg) **Journalisation**—Les modifications suivantes ont été apportées pour améliorer les messages du journal et réduire la taille du journal :

   - Les entrées de journal des échecs de déploiement incluent désormais la sortie de commande des opérations qui provoquent les échecs même si votre configuration d’environnement ne spécifie pas la journalisation du niveau de débogage. Voir [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Ajout de la journalisation des échecs de déploiement qui se produisent lorsque des usines générées requises par certaines extensions ne peuvent pas être générées correctement, car le système de fichiers est en lecture seule.<!--MAGECLOUD-2209-->

   - Réduction de la taille du journal de déploiement et correction des problèmes de mise en forme causés par les commandes de configuration qui utilisent la barre de progression interactive.<!--MAGECLOUD-2402-->

   - Suppression de la verbalisation inutile et mise à jour des niveaux de priorité pour certaines instructions de journal.<!--MAGECLOUD-2227-->

- ![icône de correctif](../../assets/fix.svg) **Correctifs spécifiques à Cron**—

   - Modification des paramètres de configuration de tâche cron par défaut pour la durée de vie de l’historique, passés de 3 j (4320 min) à 1 h (60 min) afin d’éviter les problèmes de performances et les échecs de déploiement qui peuvent se produire lorsque la file d’attente cron se remplit trop rapidement.<!--MAGECLOUD-2427-->

   - Amélioration du processus de gestion des tâches cron pendant la phase de déploiement afin d’empêcher les verrous de base de données et d’autres problèmes critiques. Désormais, toutes les tâches cron s’arrêtent pendant la phase de déploiement et redémarrent une fois le déploiement terminé.<!--MAGECLOUD-2445-->

   - Correction d’un problème lié au mécanisme de verrouillage pour la planification des consommateurs lancés par les tâches cron dans Adobe Commerce versions 2.2.0 et ultérieures afin d’empêcher les tâches cron de lancer des consommateurs en double.<!--MAGECLOUD-2464-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié à la fonction [processus de compression de contenu statique](../environment/variables-intro.md) (`gzip`) qui a provoqué `not overwritten` et `no such file or directory` lors du référencement du fichier compressé pendant le processus de déploiement.<!-- MAGECLOUD-2182-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui empêchait la variable `php ./vendor/bin/ece-tools config:dump` de supprimer les sections redondantes de la commande `config.php` lors du processus de vidage, si le paramètre régional de magasin n’est pas spécifié. Vous pouvez désormais déplacer facilement vos fichiers de configuration entre les environnements. Après la mise à jour vers `ece-tools` v2002.0.13, régénérer les fichiers plus anciens `config.php` fichiers avec l’amélioration `config:dump` . Voir [Gestion des configurations pour les paramètres du magasin](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur lors de la phase de déploiement si la configuration d’itinéraire dans la variable `.magento/routes.yaml` redirections de fichiers depuis un [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) vers un domaine `www` domaine.<!--MAGECLOUD-2556-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié à la fonction `_merge` pour l’ [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) qui générait des résultats de fusion incorrects si vous n’incluez pas la variable `engine` dans le paramètre mis à jour `.magento.env.yaml` fichier de configuration. Désormais, l’opération de fusion remplace correctement uniquement les valeurs que vous spécifiez dans la mise à jour `.magento.env.yaml` sans que vous ayez à définir la variable `engine` .<!--MAGECLOUD-2520-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de configuration de Redis qui entraînait un verrouillage de session incorrect pour Adobe Commerce sur les versions 2.2.1 et ultérieures de l’infrastructure cloud, ce qui pouvait entraîner des performances et des délais d’attente lents. Désormais, le verrouillage de session est désactivé par défaut. Le problème était dû à un changement du comportement par défaut de la variable `disable_locking` introduit dans la version 1.3.4 du package du gestionnaire de session Redis. Voir [module colinmollenhour/php-redis-session-abstract](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![nouvelle icône](../../assets/new.svg) **Composition Docker pour Cloud**—Ajout d’une commande—`docker:build`: pour générer une [Composition Docker](https://devdocs.magento.com/cloud/docker/docker-config.html) configuration à partir du cloud `ece-tools` référentiel.<!-- MAGECLOUD-2250 -->

- ![nouvelle icône](../../assets/new.svg) **Modifier les paramètres régionaux**— Vous pouvez désormais modifier les paramètres régionaux du magasin sans passer par le processus de configuration de l’exportation et de l’importation. Lorsque l’application est en production et que SCD_ON_DEMAND est activé, les options de magasin et de paramètres régionaux d’administration sont disponibles.<!-- MAGECLOUD-2019 -->

- ![nouvelle icône](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Carte du site et robots**: création d’un [workflow](../store/robots-sitemap.md) pour ajouter une `robots.txt` et générer un `sitemap.xml` pour une configuration de domaine unique sans avoir à modifier l’infrastructure.

- ![nouvelle icône](../../assets/new.svg) **Assistants**—Ajout de deux [assistant](../deploy/smart-wizards.md) pour vous aider à configurer Cloud :<!-- MAGECLOUD-1910 -->

   - `ideal-state`: configurez l’état idéal pour un temps d’arrêt minimal du déploiement.

   - `master-slave`—configuration de l’équilibrage de charge pour la base de données et Redis

- ![nouvelle icône](../../assets/new.svg) **Actualisation des modules**—Ajout d’une commande Cloud—`module:refresh`: pour activer les modules qui ont été désactivés ou n’ont pas été activés explicitement, comme cela est fait automatiquement lors d’une génération.<!-- MAGECLOUD-1521 -->

- ![nouvelle icône](../../assets/new.svg) Ajout de la possibilité de choisir de fusionner ou de remplacer la configuration pour les services à l’aide de la variable `_merge` dans [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSION](../environment/variables-deploy.md#session_configuration), [QUEUE](../environment/variables-deploy.md#queue_configuration), et [RECHERCHE](../environment/variables-deploy.md#search_configuration) configurations.<!-- MAGECLOUD-2105 -->

- ![nouvelle icône](../../assets/new.svg) **Exemple de fichier de configuration d’environnement**—Nous avons ajouté une `.magento.env.yaml` fichier d’exemple dans le package CEE-Outils qui comprend une description détaillée et les valeurs possibles pour chaque variable d’environnement.<!-- MAGECLOUD-1908 -->

   - Nous avons également ajouté une validation approfondie pour la variable `.magento.env.yaml` qui empêche les échecs du processus de déploiement dus à des valeurs inattendues. Lorsqu’un échec se produit, vous recevez maintenant un message d’erreur détaillé qui commence par : `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![nouvelle icône](../../assets/new.svg) Ajout des éléments suivants : [**Variables d’environnement**](../environment/variables-intro.md):

   - Vous pouvez maintenant définir plusieurs paramètres régionaux pour chaque thème à l’aide du nouveau [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) qui réduit la quantité de fichiers de thème à déployer.<!-- MAGECLOUD-1501 -->

   - Ajout de la [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) pour personnaliser les connexions à la base de données en vue du déploiement.<!-- MAGECLOUD-2047 -->

   - La nouvelle [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) remplace le niveau de journalisation minimal pour tous les flux de sortie sans apporter de modifications au code.<!-- MAGECLOUD-2129 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui entraînait des temps d’arrêt entre la phase de déploiement et la phase de post-déploiement. La phase de post-déploiement commence maintenant. _immédiatement_ une fois la phase de déploiement terminée.

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel les tâches cron réussies n’étaient pas nettoyées, les tâches avec `status = success`, dans le planning.<!-- MAGECLOUD-2268 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lié à la fonction `post_deploy` point d’extension qui a effacé le cache lors de la phase de déploiement au lieu de la phase de post-déploiement du projet.<!-- MAGECLOUD-2113 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème lors de l’utilisation de SCD avec plusieurs paramètres régionaux, qui généraient le même `js-translation.json` pour chaque paramètre régional.<!-- MAGECLOUD-2034 -->

- ![icône de correctif](../../assets/fix.svg) Optimisation de la `db:dump` dans la fonction `ece-tools` afin d’éviter de verrouiller les tables et d’augmenter la vitesse.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>La version 2002.0.11 des outils ECE est requise pour la compatibilité 2.2.4.

- ![nouvelle icône](../../assets/new.svg) **Configuration des connexions en lecture seule aux noeuds non maîtres**: cette version permet de configurer une connexion en lecture seule à un noeud non maître pour recevoir du trafic en lecture seule (pour  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) et pour <!--MAGECLOUD-143 -->

- ![nouvelle icône](../../assets/new.svg) **Assistant de configuration**: ajout d’un assistant pour vous aider à vérifier votre configuration pour le déploiement de contenu statique. Voir [Assistant dynamique](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de Symfony Console**: ajout de la prise en charge de Symfony Console 4 avec Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![icône de correctif](../../assets/fix.svg) **Optimisations de la planification Cron**: gestion améliorée des files d’attente et journalisation améliorée pour faciliter le débogage des problèmes liés à cron.<!-- MAGECLOUD-1607 -->

- ![icône de correctif](../../assets/fix.svg) La validation du déploiement échoue si une `ADMIN_EMAIL` ou `ADMIN_USERNAME` est identique à un compte administrateur existant.<!-- MAGECLOUD-1221 -->

- ![icône de correctif](../../assets/fix.svg) Suppression de la prise en charge de SOLR pour les versions 2.2.x. Les versions 2.1.x conservent la possibilité d’activer SOLR.<!-- MAGECLOUD-1282 -->

- ![icône de correctif](../../assets/fix.svg) La première installation des environnements d’évaluation et de production d’un projet PRO inclut désormais différents préfixes d’index pour Elasticsearch afin d’éviter tout conflit potentiel tout en identifiant les enregistrements appartenant à chaque environnement.<!-- MAGECLOUD-1489 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui interrompait la phase de création pour l’architecture héritée lors du déploiement de contenu statique.<!-- MAGECLOUD-2021 -->

- ![icône de correctif](../../assets/fix.svg) **Améliorations spécifiques à Cron**—Reprise de l’implémentation de cron :<!-- MAGECLOUD-1607 -->

   - Correction d’un problème en raison duquel la file d’attente cron se remplissait rapidement. Maintenant, il efface les emplois obsolètes de cron d&#39;une manière plus fiable.

   - Réorganisation de la séquence des tâches cron afin que toutes les tâches dans des threads distincts soient lancées avant le groupe général.

   - Amélioration de la journalisation pour faciliter le débogage des problèmes cron.

   - **REMARQUE**: cette version résout de nombreux problèmes liés à cron. Si vous utilisez actuellement des correctifs liés à cron dans _m2-hotfixes_, supprimez-les.

- ![icône de correctif](../../assets/fix.svg) **Améliorations spécifiques aux SCD**—

   - Vous pouvez utiliser la variable `VERBOSE_COMMANDS` et la variable `SCD_COMPRESSION_LEVEL` variables d’environnement pendant les deux _build_ et des phases de déploiement.<!-- MAGECLOUD-1819 -->

   - Correction d’un problème en raison duquel le déploiement échouait avec une erreur aléatoire en cas de rencontre d’une valeur inattendue pour la variable `SCD_COMPRESSION_LEVEL` Variable d’environnement. Amélioration de la validation de la configuration pour fournir des notifications significatives. Voir [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) pour des valeurs acceptables.<!-- MAGECLOUD-2043 -->

   - Correction du comportement de la fonction `SCD_COMPRESSION_LEVEL` flux de configuration des variables d’environnement afin que les remplacements fonctionnent comme prévu.<!-- MAGECLOUD-2044 -->

   - Correction d’un problème qui empêchait la configuration de la variable `SCD_THREADS` de la variable d’environnement `.magento.env.yaml` fichier _deploy_ scène.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![nouvelle icône](../../assets/new.svg) **Déploiement de contenu statique (SCD)**: il existe un nouveau processus de déploiement alternatif pour générer du contenu statique lorsque cela est demandé (sur demande). Cela réduit le temps d’arrêt et améliore la gestion du cache en générant les ressources les plus critiques.<!-- MAGECLOUD-1285 -->

   - **Nouvelle variable d’environnement**: ajout de la propriété `SCD_ON_DEMAND` variable d’environnement globale pour générer du contenu statique, si nécessaire.<!-- MAGECLOUD-1738 -->

   - **crochet après déploiement**: ajout d’un `post_deploy` hook pour `.magento.app.yaml` fichier qui efface le cache et pré-charge (réchauffements) le cache _after_ le conteneur commence à accepter les connexions. Il est disponible uniquement pour les projets Pro qui contiennent des environnements d’évaluation et de production dans [!DNL Cloud Console] et pour les projets de démarrage. Bien que cela ne soit pas obligatoire, cela fonctionne en tandem avec la fonction `SCD_ON_DEMAND` Variable d’environnement.<!-- MAGECLOUD-1788 -->

- ![nouvelle icône](../../assets/new.svg) **Optimisation**: optimisation du déplacement ou de la copie des fichiers lors du déploiement pour améliorer la vitesse de déploiement et réduire les charges sur le système de fichiers.<!-- MAGECLOUD-1842 -->

- ![nouvelle icône](../../assets/new.svg) **Journalisation de déploiement**: ajout de la possibilité d’activer les gestionnaires Syslog et Graylog Extended Log Format (GELF) pour les journaux de sortie pendant le processus de déploiement. Voir [Gestionnaire de journalisation](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![nouvelle icône](../../assets/new.svg) Ajout des éléments suivants : [**Variables d’environnement**](../environment/variables-intro.md):

   - `CRYPT_KEY`: fournissez une clé cryptographique à un autre environnement lors du déplacement d’une base de données.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Global_ Variable d’environnement qui ignore la copie des fichiers d’affichage statique dans la variable `var/view_preprocessed` et génère un HTML minimisé si nécessaire.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Global_ Variable d’environnement pour générer du contenu statique, si nécessaire.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES`: vous pouvez répertorier les pages à utiliser pour précharger le cache. Disponible dans la nouvelle [Variables de post-déploiement](../environment/variables-post-deploy.md).

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel un correctif appliqué localement interrompait le déploiement sur une instance. Maintenant, les outils de la CEE peuvent détecter qu’un correctif a été appliqué.<!-- MAGECLOUD-982 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un conflit entre la fonctionnalité de bundling JavaScript et la fonctionnalité GZIP. Ces fonctions fonctionnent correctement ensemble.<!-- MAGECLOUD-1735 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui entraînait l’échec des commandes de l’interface de ligne de commande CEE-Outils lors de l’utilisation de versions antérieures de PHP 7.0.x.<!-- MAGECLOUD-1744 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui empêchait le déploiement de contenu statique avec la stratégie compacte dans plusieurs threads.<!-- MAGECLOUD-1822 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de verrouillage de session Redis qui provoquait un délai de connexion de l’administrateur. En outre, le correctif est disponible pour la version 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Vous devez [mise à niveau du métaphorage Adobe Commerce sur l’infrastructure cloud](../dev-tools/install-package.md#update-the-metapackage) pour obtenir ceci et toutes les futures mises à jour.

- ![nouvelle icône](../../assets/new.svg) **ece-tools**—The `ece-tools` prend désormais en charge Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![nouvelle icône](../../assets/new.svg) **Configuration des redis**—Vous pouvez maintenant [configurer Redis](../environment/variables-deploy.md#cache_configuration) mise en cache des pages et par défaut et stockage de session Redis à l’aide d’une variable d’environnement.<!-- MAGECLOUD-1552 -->

- ![nouvelle icône](../../assets/new.svg) **Améliorations du service Search, AMQP et Redis**: nous avons unifié le flux de configuration du service afin qu’il se comporte désormais de la même manière pour tous les services. Modification manuelle de la `env.php` n’est plus pris en charge pour configurer les services. Vous devez utiliser des variables d’environnement ou la variable `.magento.env.yaml` à la place.<!-- MAGECLOUD-1437 -->

- ![icône de correctif](../../assets/fix.svg) **Variables d’environnement**—

   - L’utilisation de `env:STATIC_CONTENT_THREADS` a été abandonné et sera supprimé dans une version ultérieure. Utilisez la variable [SCD_THREADS](../environment/variables-deploy.md#scd_threads) au lieu de .<!-- MAGECLOUD-1507 -->

   - La variable `STATIC_CONTENT_EXCLUDE_THEMES` La variable d’environnement était obsolète. Vous devez utiliser la variable `SCD_EXCLUDE_THEMES` Variable d’environnement à la place.<!-- MAGECLOUD-1640 -->

- ![icône de correctif](../../assets/fix.svg) **Journalisation**: nous avons simplifié la journalisation des opérations de correction intégrées.<!-- MAGECLOUD-1674 -->

- ![icône de correctif](../../assets/fix.svg) Nous avons supprimé `developer` la prise en charge du mode et `APPLICATION_MODE` car elles provoquaient un comportement inattendu.<!-- MAGECLOUD-1615 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait des échecs de déploiement de contenu statique liés à Redis. Désormais, le déploiement de contenu statique multithread s’exécute comme prévu.<!-- MAGECLOUD-1630 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui empêchait les utilisateurs d’enregistrer les modifications apportées aux champs de configuration dans l’administrateur, qui sont marqués comme sensibles après l’exécution de la fonction `app:config:dump` .<!-- MAGECLOUD-1175 -->

- ![icône de correctif](../../assets/fix.svg) Nous avons ajouté la prise en charge d’une version antérieure de `symfony/yaml` pour résoudre les conflits avec certains packages, qui ne sont pas encore compatibles avec la dernière version.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>Nous avons fusionné `vendor/magento/ece-patches` avec `vendor/magento/ece-tools` dans cette version. Vous n’avez plus besoin de mettre à jour la variable `vendor/magento/ece-patches` module séparément.

**Nouvelles fonctionnalités :**

- **Journalisation améliorée**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Nous avons amélioré la messagerie des journaux afin de fournir de meilleures explications lorsque le processus de création ou de déploiement remplace une variable d’environnement.
   - Vous pouvez désormais visualiser la progression de l’installation et de la mise à niveau en temps réel. Parcourez les `install_update.log` pour afficher la progression. Par exemple,

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Nouvelle commande cron**: vous pouvez désormais déverrouiller des tâches cron bloquées spécifiques au lieu de les arrêter et de les relancer avec l’événement [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) . Non disponible dans 2.1.<!-- MAGECLOUD-1367 -->

- **Fichier de configuration unifié**: vous pouvez désormais configurer les étapes de création et de déploiement à l’aide d’une [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) fichier .<!-- MAGECLOUD-1369 -->

- **Fichiers de configuration de sauvegarde**: le processus de déploiement crée désormais automatiquement une sauvegarde de la variable `app/etc/env.php` et `app/etc/config.php` fichiers de configuration après le déploiement. Nous avons également ajouté une [nouvelle commande CLI](https://support.magento.com/hc/en-us/articles/360033182871) pour restaurer ces fichiers de configuration à partir d’une sauvegarde.<!-- MAGECLOUD-1372 -->

- **Résolution des erreurs de validation**: nous avons modifié la commande que vous devez utiliser pour résoudre les erreurs de validation lors de la `config.php` ne contient pas suffisamment de données pour le déploiement de contenu statique. Auparavant, le message d’erreur vous demandait de l’exécuter. `bin/magento app:config:dump`. Maintenant, vous devez exécuter `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Nouvelles variables d’environnement**: vous pouvez désormais utiliser des variables d’environnement pour vous connecter à des [search](../environment/variables-deploy.md#search_configuration) et [Basé sur AMQP](../environment/variables-deploy.md#queue_configuration) des services à votre site ;<!-- MAGECLOUD-1410 -->

- Nous avons mis en oeuvre des correctifs intelligents. Désormais, le package applique des correctifs basés non pas sur Adobe Commerce sur la version de l’infrastructure cloud, mais sur la version du package corrigée.<!--MAGECLOUD-1090-->

**Problèmes résolus :**

- Correction d’un problème de journalisation qui provoquait des erreurs de création.<!-- MAGECLOUD-1162 -->

- Correction d’un problème qui provoquait des exceptions de délai d’expiration lors de l’exécution de déploiements en mode interactif.<!-- MAGECLOUD-1389 -->

- Correction d’un problème qui provoquait des erreurs lors de l’utilisation de la stratégie compacte pour la génération de contenu statique. Non disponible dans 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Correction d’un problème qui empêchait le script de déploiement d’identifier correctement les environnements d’évaluation et de production.<!-- MAGECLOUD-1493 -->

- Correction d’un problème qui entraînait des problèmes de réseau qui perturbaient les connexions de la base de données et causait des échecs pendant le processus d’installation et de mise à niveau.<!-- MAGECLOUD-1520 -->

- Correction d’un problème empêchant l’exportation des fichiers de configuration à l’aide de `app:config:dump` plus d&#39;une fois. Non disponible dans 2.1.<!--  MAGECLOUD-1567  -->

- Nous avons corrigé une session Redis. _verrouillage_ qui a provoqué un problème _Administration_ délai de connexion. Non disponible dans 2.1.<!--  MAGECLOUD-1582  -->

- Correction d’un problème de mise en oeuvre lié au contrôle de version qui provoquait un conflit avec d’autres modules de correctif basés sur le compositeur.<!-- MAGECLOUD-1450 -->

- Nous avons corrigé un problème qui provoquait des problèmes de mémoire PHP lors de l’importation.<!-- MAGECLOUD-1310 -->

- Suppression du correctif ; correction d’un bogue dans `colinmollenhour/credis` v1.6 pour activer la prise en charge d’Adobe Commerce sur l’infrastructure cloud 2.2.1. Non disponible dans 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Problèmes résolus :**

- Nous avons supprimé `var/view_preprocessed` symlinks pour résoudre un problème qui provoquait des conflits de minification JavaScript.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Problèmes résolus :**

- Nous avons corrigé un problème qui provoquait `gzip` lorsqu’un nom de fichier ou de répertoire contient des espaces.<!-- MAGECLOUD-1413 -->

- Correction d’un problème qui empêchait les scripts de déploiement de reconnaître et d’activer correctement les dépendances des modules.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Nouvelles fonctionnalités :**

- **Configuration d’un consommateur cron avec une variable d’environnement**: vous pouvez désormais configurer les consommateurs cron à l’aide de la nouvelle `CRON_CONSUMERS_RUNNER` Variable d’environnement.

- **Analyse de configuration**: nous analysons désormais les composants critiques pendant le processus de création/déploiement et arrêtons le processus en cas d’échec de l’analyse, ce qui empêche des temps d’arrêt inutiles en raison du fait que le site est en mode de maintenance.

- **Créer/déployer des notifications**: nous avons ajouté un fichier de configuration à utiliser. [configurer des notifications Slack et/ou par e-mail ;](../environment/set-up-notifications.md) pour les actions de création/déploiement dans tous vos environnements.

- **Compression de contenu statique**: le contenu statique est désormais compressé à l’aide de la commande [gzip](https://www.gnu.org/software/gzip/) pendant les phases de création et de déploiement. Cette compression, associée à une compression rapide, permet de réduire la taille de votre magasin et d’augmenter la vitesse de déploiement. Si nécessaire, vous pouvez désactiver la compression à l’aide d’un [option de création](../environment/variables-build.md) ou [variable de déploiement](../environment/variables-deploy.md). Pour plus d’informations, consultez les rubriques suivantes :

   - [Variables d’environnement d’application](../application/variables-property.md)

   - [Performances du déploiement de contenu statique](../deploy/static-content.md)

   - [Processus de déploiement](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Gestion des configurations**: la génération automatique d’un `app/etc/config.php` dans votre référentiel Git pendant la phase de création, s’il n’existe pas déjà. Le fichier généré automatiquement comprend uniquement une liste de modules et d’extensions. Si le fichier existe déjà, la phase de création se poursuit normalement. Si vous suivez [Gestion des configurations](../store/store-settings.md) ultérieurement, les commandes mettent à jour le fichier sans nécessiter d’étapes supplémentaires. Voir [Processus de déploiement](https://devdocs.magento.com/cloud/reference/discover-deploy.html) pour plus d’informations.

- **Blocages de base de données**—Nous avons ajouté une `magento/ece-tools` Commande d’interface de ligne de commande pour créer des vidages de base de données dans tous les environnements. Pour les environnements de production Pro-plan, cette commande est uniquement vidée à partir de l’un des trois noeuds haute disponibilité. Par conséquent, les données de production écrites sur un autre noeud pendant le vidage peuvent ne pas être copiées. Nous vous recommandons de mettre l’application en mode de maintenance avant d’effectuer un vidage de base de données dans les environnements de production. Voir [Gestion des sauvegardes](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) pour plus d’informations.

- **Suppression des limites d’intervalle Cron**: l’intervalle cron par défaut pour tous les environnements configurés dans les régions us-3, eu-3 et ap-3 est de 1 minute. L’intervalle cron par défaut dans toutes les autres régions est de 5 minutes pour les environnements Pro Integration et de 1 minute pour les environnements Pro Staging et Production. Pour modifier vos tâches cron existantes, modifiez vos paramètres dans `.magento.app.yaml` ou créez un ticket d’assistance pour les environnements de production/d’évaluation. Voir [Configuration de tâches cron](../application/crons-property.md#set-up-cron-jobs) pour plus d’informations.

**Problèmes résolus :**

- Correction d’un problème qui provoquait de longs délais de déploiement en raison du processus de déploiement appelant la variable `cache-clean` avant le déploiement du contenu statique.<!-- MAGECLOUD-1327 -->

- Correction d’un problème provoquant des erreurs lors de l’étape de génération de contenu statique du déploiement dans les environnements de production.<!-- MAGECLOUD-1322 -->

- Correction d’un problème empêchant certains `magento/ece-tools` des commandes de la sortie de connexion à `stderr`.<!-- MAGECLOUD-1264 -->

- Correction d’un problème empêchant les valeurs d’URL de base dans `env.php` de la mise à jour dans les branches dupliquées.<!-- MAGECLOUD-1242 -->

- Correction d’un problème en raison duquel la variable `magento setup:install` pour ajouter un préfixe non sécurisé (`http://`) pour sécuriser les URL de base.<!-- MAGECLOUD-1171 -->

- Correction d’un problème qui empêchait les erreurs de correctif de provoquer des échecs de déploiement.<!-- MAGECLOUD-1170 -->

- Correction d’un problème empêchant `ece-tools` d’arrêter l’exécution et de lancer une exception si aucun correctif ne peut être appliqué.<!-- MAGECLOUD-1152 -->

- Correction d’un problème qui provoquait des erreurs lors du chargement du storefront après l’activation de la minification de HTML dans l’administrateur.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Problèmes résolus :**

- Vous pouvez désormais [réinitialisation manuelle des tâches cron bloquées](https://support.magento.com/hc/en-us/articles/360033099451) à l’aide d’une commande d’interface de ligne de commande dans tous les environnements via un accès SSH. Le processus de déploiement réinitialise automatiquement les tâches cron.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Problèmes résolus :**

- Correction d’un problème en raison duquel les pages expiraient car Redis prenait trop de temps pour lire/écrire. Vous pouvez désormais utiliser la variable `disable_locking` dans les configurations Redis pour éviter ce problème.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Problèmes résolus :**

- La variable [!DNL RabbitMQ] le processus de configuration récupère désormais automatiquement tous les paramètres requis.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Nouvelles fonctionnalités :**

- Adobe Commerce sur l’infrastructure cloud prend désormais en charge les portées et les [stratégies de déploiement de contenu statique](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). Nous avons ajouté la variable `–s` avec le paramètre par défaut `quick` pour la stratégie de déploiement de contenu statique. Vous pouvez utiliser la variable d’environnement. [SCD_STRATEGY](../environment/variables-deploy.md) pour personnaliser et utiliser ces stratégies avec vos actions de création et de déploiement. Cette variable prend en charge les options. `standard`, `quick`, ou `compact`. Si vous sélectionnez `compact`, nous remplaçons la variable `STATIC_CONTENT_THREADS` avec la valeur `1`, qui peut ralentir le déploiement, en particulier dans les environnements de production. Non disponible dans 2.1.<!--- MAGECLOUD-1057 -->

- Nous avons créé un fichier journal sur les environnements pour capturer et compiler les actions de création et de déploiement. La variable `var/log/cloud.log` se trouve dans le répertoire de l’application racine.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Problèmes résolus :**

- Refactorisation de la variable `ece-tools` pour le rendre compatible avec Adobe Commerce sur l’infrastructure cloud 2.2.0 et versions ultérieures.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Nous avons corrigé un problème qui empêchait `ece-tools` d’arrêter l’exécution et de lancer une exception si aucun correctif ne peut être appliqué.<!-- MAGECLOUD-1186 -->

- Correction d’un problème en raison duquel des exceptions étaient générées lorsque la compilation d’injection de dépendance (di) était ignorée pendant les versions.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Correction d’un problème en raison duquel le processus de déploiement remplaçait les configurations Redis personnalisées dans la variable `env.php` fichier .<!-- MAGECLOUD-1019 -->

- Correction d’un problème en raison duquel les boucles de redirection étaient désactivées par l’administrateur sécurisé par défaut.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Ce package n’est plus compatible avec les autres versions d’Adobe Commerce sur l’infrastructure cloud et **should not** à utiliser.

### Version initiale

Version initiale de `ece-tools` pour Adobe Commerce sur l’infrastructure cloud 2.2.0.
