---
title: Archivage des notes de mise à jour pour les outils citoyen
description: Découvrez les améliorations archivées pour les outils.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 196efa316b9998c1980412ad96577d7ce42d4aec
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Archivage des notes de mise à jour pour les outils citoyen

>[!NOTE]
>
>Ces notes de mise à jour contiennent des informations et des mises à jour pour `ece-tools` v2002.0.22 et versions ultérieures. Voir les [ notes de mise à jour de la suite d’outils cloud ](cloud-tools-suite.md) pour obtenir les dernières mises à jour de `ece-tools` et d’autres modules cloud.

## v2002.0.22

La version `ece-tools` 2002.0.22 modifie la structure du package `ece-tools` pour découpler la version de `Adobe Commerce on cloud infrastructure` correctifs de la version CEE-Outils. À compter de cette version, les correctifs et correctifs critiques seront fournis à l’aide du package [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches), qui est une nouvelle dépendance pour le package `ece-tools`. Nous avons apporté ces modifications afin de réduire la complexité de la planification des mises à jour des versions et de l’utilisation des contributions de la communauté.

- ![nouvelle icône](../../assets/new.svg) **Modifications du package CEE-Outils**

   - ![new icon](../../assets/new.svg) Déplacement des correctifs Adobe Commerce du package `ece-tools` vers un nouveau package de compositeur [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches).

   - ![new icon](../../assets/new.svg) Mise à jour du fichier `composer.json` pour le package `ece-tools` afin d’ajouter une dépendance pour le package `magento/magento-cloud-patches` v1.0.0.

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel le processus de correctif `ece-tools` était interrompu lors de l’application de correctifs sur des versions de sécurité uniquement, à partir de la version 2.3.2-p2 et versions ultérieures. Ce problème a été introduit par le nouveau système de contrôle de version adopté pour les [correctifs de sécurité uniquement](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/security-patches/overview).<!--MAGECLOUD-4661-->

- ![icône de correctif](../../assets/fix.svg) **Correctifs et correctifs critiques** - Mettez à jour vos environnements cloud avec la version `ece-tools` 2002.0.22 pour appliquer les correctifs et correctifs critiques suivants. Ces correctifs sont inclus dans le package `magento/magento-cloud-patches` v1.0.0.

   - ![icône de correctif](../../assets/fix.svg) **Correctifs de sécurité du générateur de pages pour les versions 2.3.1.x et 2.3.2.x** - Correction d’un problème dans l’aperçu du créateur de pages qui permet aux utilisateurs non authentifiés d’accéder à certaines méthodes de création de modèles pouvant être utilisées pour déclencher l’exécution arbitraire de code sur le réseau (RCE), ce qui entraîne des fuites d’informations globales. Ce problème peut se produire lors de l’utilisation de versions de Page Builder non prises en charge avec Adobe Commerce versions 2.3.1 et 2.3.2.<!--MAGECLOUD-4649-->

   - ![icône de correctif](../../assets/fix.svg) **Correctifs MSI** - Correctifs qui provoquaient des erreurs d’indexation et des problèmes de performances lors de l’utilisation des paramètres de stock par défaut pour la gestion du stock.<!--MAGECLOUD-4428-->

   - ![ icône de correction ](../../assets/fix.svg) **Compatibilité descendante des nouvelles interfaces de messagerie** - Correction d’un problème d’incompatibilité ascendante provoqué par l’interface PHP `Magento\Framework\Mail\EmailMessageInterface` introduite dans Adobe Commerce v2.3.3. Dans la portée de ce correctif, le nouvel `EmailMessageInterface` hérite de l’ancien `MessageInterface` et les modules principaux Adobe Commerce sont restaurés pour dépendre de `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![icône de correction](../../assets/fix.svg) **La pagination du catalogue ne fonctionne pas sur Elasticsearch 6.x** - Correction d’un problème critique lié à la pagination des résultats de recherche qui affecte les clients utilisant Elasticsearch 6.x comme moteur de recherche de catalogue.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) **Images Nouveau Docker**—Pris en charge par les versions 2.3.3 et ultérieures<!-- MAGECLOUD-3345 -->

      - PHP version 7.3.<!-- MAGECLOUD-4017 -->

      - Cache de vernis 6.2.0<!-- MAGECLOUD-4017 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de l’application d’une configuration de crochet personnalisée spécifiée dans `.magento.app.yaml` dans l’environnement Docker. Auparavant, l’environnement Docker ne prenait en charge que la configuration du crochet par défaut.<!-- MAGECLOUD-3505-->

   - ![new icon](../../assets/new.svg) Les fichiers ENV Docker ne sont plus générés pendant la génération Docker et la commande `docker:config:convert` est obsolète. Les données correspondantes sont désormais stockées dans le fichier `docker-compose.yml`.<!-- MAGECLOUD-3816-->

   - ![nouvelle icône](../../assets/new.svg) **Image PHP mise à jour**-Ajout de Node.js à l’image Docker PHP pour prendre en charge les fonctionnalités node, npm et grunt-cli.<!-- MAGECLOUD-3953 -->

- ![nouvelle icône](../../assets/new.svg) ****- 

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable de déploiement **LOCK_PROVIDER** pour configurer le fournisseur de verrouillage qui empêche le lancement de tâches cron en double et de groupes cron. Voir la description de la variable dans la rubrique [variables de déploiement](../environment/variables-deploy.md#lock_provider).<!-- MAGECLOUD-4052 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable d’environnement **CONSUMERS_WAIT_FOR_MAX_MESSAGES** pour configurer la manière dont les consommateurs traitent les messages de la file d’attente des messages lors de l’utilisation de la variable d’environnement `CRON_CONSUMERS_RUNNER` pour gérer les tâches cron. Voir la description de la variable dans la rubrique [variables de déploiement](../environment/variables-deploy.md#consumers_wait_for_max_messages).<!-- MAGECLOUD-4071 -->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème qui pouvait entraîner des erreurs de blocage de base de données lorsque la tâche cron `consumers_runner` démarre plusieurs instances d’un même consommateur sur différents noeuds. Maintenant, si vous avez activé la variable de déploiement [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) dans votre environnement, la tâche `consumers_runner` utilise l’option `single-thread` pour démarrer une instance de chaque consommateur sur un seul noeud.<!-- MAGECLOUD-3913 -->

   - ![Icône de correctif](../../assets/fix.svg) Correction d’un problème affectant la fonctionnalité [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) qui utilise une URL de magasin par défaut. Désormais, si la commande `config:show:default-url` ne parvient pas à récupérer une URL de base, l&#39;URL de la variable MAGENTO_CLOUD_ROUTES est utilisée.<!-- MAGECLOUD-3866 -->

- ![nouvelle icône](../../assets/new.svg) Mise à jour des informations de journalisation renvoyées par la commande `module:refresh`. Vous pouvez maintenant voir une liste détaillée des modules activés dans le fichier `cloud.log`.<!-- MAGECLOUD-2514 -->

- ![nouvelle icône](../../assets/new.svg) Amélioration de la compatibilité des versions, de la validation et des notifications d’avertissement pour les problèmes de compatibilité entre la version d’Adobe Commerce et les services installés, tels que Elasticsearch, [!DNL RabbitMQ], Redis et DB.<!-- MAGECLOUD-3535 -->

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de la version 3.8.<!-- MAGECLOUD-4674--> de RabitMQ

- ![nouvelle icône](../../assets/new.svg) Mise à jour des validations interactives pour la compatibilité des services afin de refléter les versions prises en charge pour les nouvelles versions Adobe Commerce 2.3.3 et 2.2.10. Voir la [configuration système requise](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements) dans le _guide d&#39;installation_ pour connaître les versions recommandées.<!-- MAGECLOUD-4018 -->

- ![icône de correction](../../assets/fix.svg) Amélioration du message de journal renvoyé lorsque le processus de gestion des tâches cron de la phase de déploiement tente d’arrêter une tâche cron déjà terminée pour clarifier que ce problème n’est pas une erreur. Modification du niveau de journal de `INFO` à `DEBUG`.<!-- MAGECLOUD-3653-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème lors de l’exécution de la commande `setup:upgrade` qui n’interrompait pas le processus de déploiement lorsqu’un échec se produisait pendant la tâche `app:config:import`.<!-- MAGECLOUD-3806 -->

- ![nouvelle icône](../../assets/new.svg) Modification du niveau de journalisation par défaut du gestionnaire de fichiers en `debug` afin de réduire le nombre de détails dans le journal affiché dans le [!DNL Cloud Console], tout en fournissant des informations détaillées pour le débogage.<!-- MAGECLOUD-3871 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur lors du déploiement de contenu statique pendant la génération. Après une installation et un vidage de configuration `ece-tools`, une erreur s’est produite si aucun paramètre régional n’était spécifié pour l’utilisateur administrateur dans le fichier `config.php`. Désormais, il existe un paramètre régional par défaut pour l’utilisateur administrateur dans le fichier `config.php`.<!-- MAGECLOUD-3957 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’un `Undefined index error` qui se produisait lorsqu’une commande d’interface de ligne de commande `magento-cloud` échouait dans un environnement qui n’était pas configuré avec une URL sécurisée (https). Désormais, le package CEE-Outils utilise l&#39;URL de base (http) si l&#39;URL sécurisée n&#39;est pas disponible.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) Vous pouvez désormais effectuer des tests fonctionnels à l’aide du package `ece-tools` dans l’environnement Docker. Voir [test de l’application](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/).<!-- MAGECLOUD-3129/3684 -->

   - ![new icon](../../assets/new.svg) Ajout de la prise en charge de la configuration des modules PHP à l’aide du fichier `.magento.app.yaml`. Toutes les [extensions PHP spécifiées dans le fichier `.magento.app.yaml`](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/php-settings#enable-extensions) sont disponibles dans les conteneurs PHP Docker.<!-- MAGECLOUD-3357 -->

   - ![nouvelle icône](../../assets/new.svg) De nouvelles commandes sont disponibles pour améliorer l’expérience de ligne de commande Docker. Voir la section [`bin/magento-docker` de la référence Docker](https://developer.adobe.com/commerce/cloud-tools/docker/quick-reference/#cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![nouvelle icône](../../assets/new.svg) Possibilité d’utiliser Mutagen.io pour synchroniser les fichiers lors du développement entre l’hôte local et Docker.<!-- MAGECLOUD-3559 -->

   - ![icône de correction](../../assets/fix.svg) Correction du chemin par défaut lors de l’utilisation de l’environnement Docker. Désormais, lorsque vous utilisez SSH pour vous connecter au conteneur Docker, vous vous trouvez à la racine du projet dans le répertoire `/app`, comme prévu.<!-- MAGECLOUD-3582 -->

   - ![icône de correctif](../../assets/fix.svg) Mise à jour de la bibliothèque Sodium de la version 1.0.11 à la version 1.0.18, et mise à jour de l’extension Sodium PHP.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Les clients d’Adobe Commerce sur l’infrastructure cloud doivent [ envoyer un ticket d’assistance Adobe Commerce ](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) pour mettre à niveau le package libsodium sur les environnements de production et d’évaluation avant la mise à niveau vers Adobe Commerce 2.3.2. Actuellement, vous ne pouvez pas mettre à niveau les environnements de démarrage vers Adobe Commerce 2.3.2.

   - ![ icône de correctif ](../../assets/fix.svg) Ajout des `analysis-icu` et des `analysis-phonetic` modules externes Elasticsearch à toutes les images Docker.<!-- MAGECLOUD-3446 -->

   - ![Icône de correctif](../../assets/fix.svg) Validations améliorées : lors de l’utilisation d’options pour la commande `docker:build`, vous devez fournir une valeur lors de l’utilisation d’une option. En outre, ajout de la validation de la version de noeud lors de l&#39;utilisation de la commande `docker:build run`.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de variable d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge des préfixes de table de base de données à l’aide de la [ variable d’environnement DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable de déploiement **FORCE_UPDATE_URLS** pour mettre à jour les URL de base lors du déploiement vers les environnements de production et d’évaluation Pro et Starter. Voir la définition dans le contenu [deploy variables](../environment/variables-deploy.md#force_update_urls).<!-- MAGECLOUD-3602 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable de post-déploiement **TTFB_TESTED_PAGES** pour configurer les tests de page _Temps jusqu’au premier octet_ afin de vérifier les performances de l’application sur les sites déployés sur l’infrastructure cloud. Voir la description de la variable dans [les variables post-déploiement](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème lié à SCD multithread, qui provoquait des échecs aléatoires dans le déploiement de contenu statique. La solution consistait à définir la variable **SCD_THREADS** sur `1`. Vous pouvez maintenant augmenter le nombre suivant vos besoins. Voir les définitions dans les [variables de déploiement](../environment/variables-deploy.md#scd_threads) et les [variables de build](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![icône de correction](../../assets/fix.svg) Vous pouvez configurer la variable d’environnement **WARM_UP_PAGES** pour mettre en cache des pages uniques, plusieurs domaines et plusieurs pages. Voir la définition étendue dans le contenu [des variables post-déploiement](../environment/variables-post-deploy.md#warm_up_pages).<!-- MAGECLOUD-3258 -->

- ![Icône de correctif](../../assets/fix.svg) Ajout du fichier `pub/static/.htaccess` à la liste des exclusions. [Correctif soumis par Björn Kraus de PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’une erreur lorsque tous les messages de validation s’affichaient comme `Critical` si au moins un validateur de niveau critique renvoyait une erreur.<!-- MAGECLOUD-3178 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui provoquait un échec de déploiement si l’URL de base n’existait pas dans la base de données.<!-- MAGECLOUD-3075 -->

- ![new icon](../../assets/new.svg) Ajout d’une nouvelle **`env:config:show`commande** au package `ece-tools` qui affiche des services d’environnement, des routes ou des variables. Voir [Services, itinéraires et variables](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/ece-tools/package-overview#services-routes-and-variables). [Fonctionnalité soumise par Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur critique lors de la tentative d’installation d’Adobe Commerce 2.2.6 ou version antérieure avec `ece-tools` développé après la refactorisation du shell.<!-- MAGECLOUD-3665 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel les installations Adobe Commerce 2.1.x et 2.2.x échouaient avec un avertissement d’utilisation d’une version obsolète de Carbon.<!-- MAGECLOUD-3704 -->

- ![icône de correction](../../assets/fix.svg) Diminution du niveau de journal `cloud.log` pour la sortie du shell de `info` à `debug`.<!-- MAGECLOUD-3277 -->

- ![Icône de correctif](../../assets/fix.svg) Ajout de l’option `--remove-definers (-d)` à la commande `ece-tools db-dump` pour supprimer les définitions du fichier de vidage.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui remplace le fichier `env.php` lors d’un déploiement, entraînant la perte de configurations personnalisées. Cette mise à jour garantit qu&#39;Adobe Commerce sur l&#39;infrastructure cloud met à jour le fichier `env.php` avec chaque déploiement, tout en préservant les configurations personnalisées.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - ![nouvelle icône](../../assets/new.svg) Désormais, l’environnement Docker prend en charge la configuration cron définie dans la propriété [ crons du fichier .magento.app.yaml](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property).<!-- MAGECLOUD-3150 -->

   - ![nouvelle icône](../../assets/new.svg) **Nouveau conteneur Docker** : ajout d’un [conteneur proxy de terminaison TLS](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#varnish-container) pour faciliter l’arrêt SSL vernis via HTTPS.<!-- MAGECLOUD-2890 -->

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle image Docker** : ajout d’une image Node.js pour prendre en charge Gulp et d’autres fonctionnalités, telles que le test unitaire JS Jasmin.<!-- MAGECLOUD-3345 -->

   - ![nouvelle icône](../../assets/new.svg) **Modes de génération Docker**—Vous pouvez désormais choisir de lancer l’environnement Docker en [mode de production ou mode développeur](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/#launch-mode). Le mode Développeur prend en charge le développement actif avec des autorisations complètes de système de fichiers modifiables.<!-- MAGECLOUD-3152/3511 -->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème en raison duquel le déploiement de Docker échouait avec une erreur `Name or service not known` si le cache est configuré pour un service qui n’est pas disponible. Vous pouvez désormais supprimer un service du fichier [`.magento/services.yaml` ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/services-yaml). Le générateur de configuration Docker met automatiquement à jour le service dans le fichier `docker/config.php.dist`.<!-- MAGECLOUD-3369 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de validations interactives pour la compatibilité des services. Désormais, si un service demandé est incompatible avec la version Adobe Commerce ou d’autres services, le _mode interactif_ invite l’utilisateur à recevoir un message et à choisir de continuer. Voir les [versions de service](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#service-containers) disponibles pour Docker. Utilisez l&#39;option `-n` pour ignorer l&#39;interactivité à des fins de CICD.<!-- MAGECLOUD-3251 -->

   - ![Icône de correctif](../../assets/fix.svg) Correction d’un problème lié à la commande de composition Docker `db-dump` qui effaçait les vidages existants.<!-- MAGECLOUD-3366 -->

   - ![Icône de correctif](../../assets/fix.svg) Correction d’un problème qui affectait le stockage du cache Redis `session`, `default` et `page_cache` au même ID de base de données.<!-- MAGECLOUD-3172 -->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de variable d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) La nouvelle variable d’environnement **ELASTICSUITE\_CONFIGURATION** conserve vos paramètres de service personnalisés entre les déploiements. Voir la définition dans le contenu [deploy variables](../environment/variables-deploy.md#elasticsuite_configuration).<!-- MAGECLOUD-3205 -->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable d&#39;environnement **SCD_MAX_EXECUTION_TIMEOUT** afin que vous puissiez augmenter le temps de déploiement du contenu statique à partir du fichier `.magento.env.yaml`. Voir la définition dans les [variables de déploiement](../environment/variables-deploy.md#scd_max_execution_time), les [variables de build](../environment/variables-build.md#scd_max_execution_time) et les [variables globales](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![nouvelle icône](../../assets/new.svg) Ajout de la variable d’environnement **MAGENTO_CLOUD_LOCKS_DIR** pour configurer le chemin d’accès au point de montage du fournisseur de verrouillage sur l’infrastructure cloud. Le fournisseur de verrouillage empêche le lancement de tâches cron en double et de groupes cron. Cette variable est prise en charge sur Adobe Commerce version 2.2.5 et ultérieure et automatiquement configurée. Voir la définition dans [Variables cloud](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![icône de correction](../../assets/fix.svg) Modification des valeurs par défaut de la variable d’environnement **SCD_THREADS** afin de déterminer automatiquement la valeur optimale en fonction du nombre de threads du processeur détecté. Voir les définitions mises à jour dans les [variables de déploiement](../environment/variables-deploy.md#scd_threads) et les [variables de build](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème lié à un correctif pour le mécanisme d’isolation de la base de données qui provoquait une erreur lors de la mise à niveau vers Adobe Commerce sur la version 2002.0.16.<!-- MAGECLOUD-3383 -->

- ![Icône de correctif](../../assets/fix.svg) Ajout d’un correctif qui remplace les _Graphiques d’images Google_ par _Graphiques d’images_. Voir l’ [ article DevBlog sur l’obsolescence et la mise à jour des graphiques d’images Google pour M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![Icône de correctif](../../assets/fix.svg) Ajout de la validation de la [variable SEARCH_CONFIGURATION](../environment/variables-deploy.md#search_configuration). Le déploiement échoue lorsque l&#39;option &#39;engine&#39; n&#39;est pas définie et `_merge` n&#39;est pas obligatoire.<!-- MAGECLOUD-3470 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui exposait des données sensibles après une exception. Désormais, les informations sensibles sont masquées de manière appropriée.<!-- MAGECLOUD-3525 -->

- ![icône de correction](../../assets/fix.svg) Amélioration des paramètres de tolérance aux pannes du module de Magento Open Source. Dans le cas où Adobe Commerce ne peut pas lire les données de l’instance Redis `slave`, une lecture est effectuée à partir de l’instance Redis `master`. Voir [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>La version `ece-tools` 2002.0.17 comprend un correctif de sécurité important. Voir [Ressources techniques : correctifs de Magento Open Source](https://magento.com/tech-resources/download#download2288).

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—Pris en charge par les versions Adobe Commerce suivantes : 2.2.8 et versions ultérieures 2.2.x, 2.3.1 et 2.3.x

   - Ajout de la prise en charge de la version Elasticsearch 6.x.<!-- MAGECLOUD-3196 -->

   - Ajout de la prise en charge de Redis version 5.0.

- ![new icon](../../assets/new.svg) **New Docker images**—Ajout des services suivants à la version Docker :

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement** : auparavant, il existait un délai d’expiration codé en dur pour la compression SCD. Vous pouvez maintenant configurer le délai d’attente de compression SCD à l’aide de la variable d’environnement **SCD_COMPRESSION_TIMEOUT** . Voir les définitions dans les [variables de build](../environment/variables-build.md#scd_compression_timeout) et le contenu [variables de déploiement](../environment/variables-deploy.md#scd_compression_timeout).<!-- MAGECLOUD-2870 -->

- ![icône de correction](../../assets/fix.svg) Ajout de l’option `--use-rewrites` à la commande d’installation afin qu’elle utilise les réécritures du serveur web pour les liens générés dans le storefront et l’accès administrateur pour améliorer la sécurité et l’expérience client.<!-- MAGECLOUD-3246 -->

- ![icône de correction](../../assets/fix.svg) Ajout d’horodatages au fichier `var/log/install_upgrade.log` afin qu’il affiche les dates des événements d’installation et de mise à niveau.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - Désormais, la configuration de service par défaut générée dans l’environnement Docker est identique à la configuration par défaut dans le modèle Cloud.<!-- MAGECLOUD-3025 -->

   - Vous pouvez envoyer des courriers de votre environnement Docker à l’aide du service `sendmail`.<!-- MAGECLOUD-2907 -->

   - Ajout de la possibilité de [configurer Xdebug](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/) pour le débogage dans l’environnement Cloud Docker.<!-- MAGECLOUD-2891 -->

   - Correction d’un problème lié aux autorisations de service Web lors de la génération du fichier `docker-compose.yml`.<!-- MAGECLOUD-2883 -->

- ![nouvelle icône](../../assets/new.svg) **Amélioration de la mise à niveau** : ajout d’une validation pour confirmer que la propriété `autoload` du fichier `composer.json` contient les modifications de configuration requises avant la mise à niveau vers Adobe Commerce v2.3. Voir [Mise à niveau de version](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/upgrade/commerce-version).<!-- MAGECLOUD-2392 -->

- ![nouvelle icône](../../assets/new.svg) Le processus de compression lors du déploiement de contenu statique inclut désormais toutes les ressources (générées ou personnalisées en mode natif) et se produit pendant la phase de création au début de la [`build:transfer` section](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property). Auparavant, le processus de compression se produisait avant d’appliquer une minification et un regroupement personnalisés de ressources statiques. [Correctif soumis par Rafael Garcia Lepper de Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![icône de correction](../../assets/fix.svg) Correction d’une erreur de connexion à la base de données qui se produisait lors du déploiement immédiatement après la configuration d’une base de données et d’une relation de service supplémentaires. Ce correctif résout également un problème qui s’est produit pendant le processus de configuration de la création de rapports Commerce pour le démarrage. Pour commencer, cette mise à niveau est un &quot;must have&quot; pour l’utilisation du reporting Commerce.<!-- MAGECLOUD-3035 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème de validation avec la configuration de la base de données qui provoquait l’échec du processus de déploiement.<!-- MAGECLOUD-3003 -->

- ![icône de correction](../../assets/fix.svg) Mise à jour de la contrainte avec la version appropriée du package `symfony/yaml` à utiliser avec les [constantes PHP](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml#php-constants). L’analyse constante ne fonctionne pas lors de l’utilisation d’une version de package `symfony/yaml` antérieure à 3.2. [Correctif soumis par Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![nouvelle icône](../../assets/new.svg) **Vérification de la configuration de l&#39;environnement** : ajout d&#39;une validation pour vérifier la version PHP et avertir les utilisateurs s&#39;ils n&#39;utilisent pas la dernière version recommandée.<!--MAGECLOUD-2903-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème lié au traitement de variables JSON incorrectes. Désormais, si une variable JSON provoque une erreur de syntaxe, un avertissement s’affiche dans le fichier `cloud.log` et le déploiement continue à utiliser la variable par défaut.<!-- MAGECLOUD-2851 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur de connexion qui se produisait pendant le déploiement immédiatement après la désactivation du service Redis.<!-- MAGECLOUD-2747 -->

- ![nouvelle icône](../../assets/new.svg) **Modifications de journalisation**—Mise à jour du [niveau de journal](../environment/log-handlers.md#log-levels) de `Info` à `Notice` pour les événements de processus de création et de déploiement suivants : <!--MAGECLOUD-2925-->

   - Lancer et terminer le processus de réconciliation des modules installés dans `composer.json` avec les paramètres de configuration partagés dans le fichier `app/etc/config.php`

   - Démarrage et fin du processus de validation de configuration

   - Démarrage et fin du processus `setup:di:compile` pour générer des classes

- ![nouvelle icône](../../assets/new.svg) **Nouvelles variables d’environnement**—

   - **[Variable de déploiement RESOURCE_CONFIGURATION](../environment/variables-deploy.md#resource_configuration)** : utilisez cette variable pour mapper un nom de ressource à une connexion à une base de données.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION variable globale](../environment/variables-global.md#x_frame_configuration)** : utilisez cette variable pour modifier la configuration d’en-tête `X-Frame-Options` pour le rendu d’une page Adobe Commerce dans une `<frame>`, `<iframe>` ou `<object>`.<!-- MAGECLOUD-3048 -->

- ![Icône de correctif](../../assets/fix.svg) **Mises à jour de variable d’environnement**—Modification des variables d’environnement suivantes :

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)** : ajout de la fonctionnalité de préchargement du cache pour les pages spécifiées sur tous les domaines définis pour un magasin Adobe Commerce. Auparavant, si votre site était configuré avec plusieurs domaines, le processus de post-déploiement ne parvenait pas à précharger le cache des pages spécifiées sur les domaines autres que les domaines par défaut et renvoyait l’erreur suivante dans le journal de post-déploiement : `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL** : mise à jour de la documentation et de l’exemple de fichier `.magento.env.yaml` avec les valeurs par défaut correctes pour le niveau de compression SCD. Voir les définitions dans les [variables de build](../environment/variables-build.md#scd_compression_level) et le contenu [variables de déploiement](../environment/variables-deploy.md#scd_compression_level).<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES** : cette variable d’environnement est obsolète. Utilisez [SCD_MATRIX](../environment/variables-build.md#scd_matrix) pour contrôler la configuration du thème.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX** : correction du processus de validation afin d’éviter un problème qui se produisait lorsque SCD_MATRIX ignorait une valeur de thème contenant différents cas de caractères. Voir les définitions dans les [variables de build](../environment/variables-build.md#scd_matrix) et le contenu [variables de déploiement](../environment/variables-deploy.md#scd_matrix).<!-- MAGECLOUD-2904 -->

   - **Variables ADMIN**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Amélioration de la sécurité lors de la gestion des informations d’identification de l’utilisateur administrateur à l’aide de variables d’environnement. Vous ne pouvez plus utiliser les variables d’environnement ADMIN_EMAIL, ADMIN_USERNAME et ADMIN_PASSWORD pour remplacer les informations d’identification d’administrateur lors des mises à niveau. Si vous ne pouvez pas accéder au panneau d’administration, utilisez la fonction _Mot de passe oublié_ ou la commande d’interface de ligne de commande `admin:user:create` pour créer un nouvel utilisateur administrateur. Voir [Accès à votre panneau d’administration](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding#admin).

      - ADMIN_EMAIL n’est plus nécessaire lors de la mise à niveau ou de l’application de correctifs.

## v2002.0.15

- ![nouvelle icône](../../assets/new.svg) **Mises à jour Docker**—

   - Désormais, le générateur Docker utilise les services spécifiés dans les fichiers de configuration `.magento.app.yaml` et `.magento/services.yaml` lors de la [création de votre environnement Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/). Vous pouvez choisir une autre version de service à l&#39;aide des paramètres de build.<!-- MAGECLOUD-2888 -->

   - Ajout d’une image PHP 7.2 : ajout de la prise en charge de PHP 7.2 dans Cloud Docker ; mise à jour de la [configuration Launch Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) afin d’inclure l’option `docker:build --php` permettant de spécifier la version de PHP compatible avec votre version d’Adobe Commerce.<!-- MAGECLOUD-2799 -->

   - Ajout d’un [conteneur Cron](https://developer.adobe.com/commerce/cloud-tools/docker/containers/cli/#cron-container) basé sur l’image PHP-CLI.<!-- MAGECLOUD-2565 -->

   - Ajout des services suivants à la version Docker :

      - [!DNL RabbitMQ] 3.5 et 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 et 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 et 4.0<!-- MAGECLOUD-2886 -->

- ![new icon](../../assets/new.svg) **Configure with PHP constants**—Ajout de la prise en charge des [constantes PHP](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml#php-constants) dans le fichier de configuration `.magento.env.yaml`.<!-- MAGECLOUD- 2575 -->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement** : par défaut, seuls les Google Analytics sont activés dans l’environnement de production. Vous pouvez activer les Google Analytics sur les environnements d’évaluation et d’intégration à l’aide de la [variable d’environnement ENABLE_GOOGLE_ANALYTICS](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui supprimait les configurations cron personnalisées du fichier `env.php` après un redéploiement. Désormais, les configurations cron personnalisées restent en toute sécurité dans le fichier `env.php`.<!-- MAGECLOUD-2923 -->

- ![icône de correction](../../assets/fix.svg) Correction des incohérences dans les messages et des [niveaux de journal](../environment/log-handlers.md#log-levels) pour les phases de création, de déploiement et de post-déploiement. Augmentation des niveaux de messages du journal de début et de fin de **info** à **notice** pour toutes les phases et sous-phases. Ajout des messages de début et de fin du journal, le cas échéant.<!-- MAGECLOUD-2919 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème impliquant des processus cron qui empêchait le début de la phase de post-déploiement, lorsqu’elle était configurée. Désormais, si le crochet post-déploiement est activé, les processus cron sont à nouveau activés au début de la phase post-déploiement.<!-- MAGECLOUD-2862 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui empêchait l’installation réussie d’Adobe Commerce lors de la spécification d’une configuration de base de données personnalisée. Auparavant, le processus d&#39;installation utilisait la configuration de la base de données de la [variable d&#39;environnement MAGENTO_CLOUD_RELATIONSHIP](../environment/variables-cloud.md) même si vous aviez désigné des informations de connexion personnalisées dans la [ variable d&#39;environnement DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![icône de correction](../../assets/fix.svg) Correction de la commande `config:dump` de sorte qu&#39;elle inclut chaque paramètre régional de site web dans la section `system` du fichier `config.php`.<!--MAGECLOUD-2740-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui entraînait des erreurs _de nettoyage_ pendant la phase de post-déploiement en corrigeant la référence d’URL de base source.<!--MAGECLOUD-2797-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui générait incorrectement des fichiers pendant le processus `setup:di:compile`, ce qui affectait le module de paiement Amazon.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![nouvelle icône](../../assets/new.svg) **Vérifier l’état idéal** : l’assistant `ideal-state` vérifie désormais la configuration actuelle lors de chaque déploiement et fournit des instructions claires pour la mise à jour de la configuration afin d’obtenir un déploiement plus rapide sans interruption.<!--MAGECLOUD-2372-->

- ![ icône de correction ](../../assets/fix.svg) **Conformité PCI** : mise à jour des protocoles de messagerie pour Adobe Commerce sur l’infrastructure cloud afin d’exiger le protocole TLS (Transport Layer Security) version 1.2 lors de la connexion aux services de messagerie tiers. Si vous utilisez un service de messagerie qui ne prend pas en charge TLS version 1.2, vous devez mettre à niveau votre service. Sinon, le message d’erreur suivant s’affiche lorsque votre application Adobe Commerce tente de se connecter au serveur de messagerie pour envoyer un courrier électronique : `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![nouvelle icône](../../assets/new.svg) **Amélioration du déploiement**—Ajout d’une validation pour avertir les clients si les options `dev`, `debug` ou `debug_logging` d’un environnement d’évaluation ou de production sont activées pour empêcher les problèmes de performances causés par une activité de journalisation excessive.<!--MAGECLOUD-2517-->

- ![Icône de correctif](../../assets/fix.svg) **Correctifs de déploiement**—

   - Désormais, le mode de maintenance est activé au début de la phase de déploiement et désactivé à la fin. Si le déploiement échoue, le site reste en mode de maintenance jusqu’à ce que les problèmes de déploiement soient résolus. Auparavant, le site revenait en mode de production même si le déploiement échouait.<!--MAGECLOUD-2603-->

      - Reprise des contrôles de validation de la phase de déploiement afin de rétrograder le niveau d’erreur pour les problèmes de déploiement suivants de `CRITICAL` à `WARNING` afin que le déploiement soit terminé. Auparavant, ces problèmes provoquaient l’échec du déploiement.

      - La configuration de l’environnement contient des valeurs incorrectes pour les variables de déploiement ou de cloud.

   - La version Elasticsearch de l’infrastructure cloud est incompatible avec la version du module de recherche flexible/élasticsearch pris en charge par Adobe Commerce sur l’infrastructure cloud. Consultez l’ [ article de dépannage des Elasticsearch](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) dans la base de connaissances du support Adobe Commerce.<!--MAGECLOUD-2600-->

   - Correction d&#39;un problème lié aux paramètres de configuration partagés dans le fichier `app/etc/config.php` qui provoquait des erreurs `recursion detected` lors du déploiement.<!--MAGECLOUD-2173-->

- ![Icône de correctif](../../assets/fix.svg) **Correctifs liés à Cron**—

   - Correction d’un problème de planification cron qui empêchait l’exécution des tâches si vous spécifiez une fréquence cron autre que la fréquence par défaut (1 minute).<!--MAGECLOUD-2602-->

   - Correction d’un problème au cours de la phase de déploiement en raison duquel les tâches cron continuaient à s’exécuter pendant le déploiement, ce qui pouvait entraîner des verrous de base de données et d’autres problèmes critiques. Désormais, toutes les tâches cron sont arrêtées avant le début de la phase de déploiement et redémarrées une fois le déploiement terminé.&lt;!—MAGECLOUD—2537—>

   - Correction du workflow de tâche cron dans les versions 2.2.x pour déverrouiller les tâches cron gelées afin qu’elles puissent être arrêtées avant de commencer le déploiement. Auparavant, une tâche cron gelée provoquait le blocage du déploiement.<!--MAGECLOUD-2501-->

- ![icône de correction](../../assets/fix.svg) Modification du format du fichier `config.php` généré par la commande `vendor/bin/ece-tools config:dump` afin d’utiliser la syntaxe de tableau court et la mise en retrait sur 4 espaces pour se conformer aux normes de codage Adobe Commerce.<!--MAGECLOUD-2527-->

- ![Icône de correctif](../../assets/fix.svg) Correction d’une erreur de déploiement qui se produisait lorsque les espaces réservés `.magento.env.yaml` contiennent `{{ base_url }}` et `{{ unsecure_base_url }}` pour les configurations web au lieu de la configuration d’URL par défaut pour un projet Adobe Commerce sur l’infrastructure cloud./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![nouvelle icône](../../assets/new.svg) **Activez le déploiement sans interruption**—Maintenant Adobe Commerce sur l’infrastructure cloud met en file d’attente les demandes avec les modifications de base de données requises pendant le déploiement et applique les modifications dès que le déploiement est terminé. Les demandes peuvent être conservées pendant 5 minutes au maximum pour garantir qu’aucune session n’est perdue. Voir [Options de déploiement de contenu statique pour réduire le temps d’arrêt du déploiement sur Cloud](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![nouvelle icône](../../assets/new.svg) **Docker Composition for Cloud**—Les améliorations suivantes ont été apportées au processus de [configuration et configuration Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) :

   - Ajout d’une commande—`docker:config:convert` pour convertir les fichiers de configuration PHP au format Docker ENV afin de simplifier la configuration de l’environnement. Vous copiez maintenant les fichiers de configuration PHP dans le répertoire Docker et les convertissez en fichiers Docker ENV. Voir [Launch Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/).<!--MAGECLOUD-2359-->

   - Le processus d’installation d’Adobe Commerce sur l’infrastructure cloud prend désormais en charge le déploiement sur les systèmes de fichiers en lecture seule et en lecture-écriture afin d’émuler plus étroitement le système de fichiers Cloud. Voir [Configuration de Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/).&lt;!—MAGECLOUD—2357—>

   - **Prise en charge du service Redis** : ajout d’une image Redis, déployée sur un conteneur Docker et configurée automatiquement pour fonctionner avec votre installation Docker.&lt;!—MAGECLOUD—2442—>

   - Vous disposez maintenant de la fonctionnalité de vidage de la base de données lorsque vous utilisez le conteneur de base de données [ de Cloud Docker. ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#database-container) Vous pouvez également [ partager des fichiers](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#sharing-data-between-host-machine-and-container) entre un ordinateur hôte et un conteneur à l&#39;aide du répertoire `docker/mnt`.<!-- MAGECLOUD-2577 -->

   - **Prise en charge du service de vernis** : ajout d’une image de vernis, qui est automatiquement déployée sur un conteneur Docker. Après le déploiement, vous pouvez configurer manuellement le vernis en suivant les bonnes pratiques d’Adobe Commerce. Voir [Configurer et utiliser le vernis](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cache/varnish/config-varnish).&lt;!—MAGECLOUD—2358—>

   - Accès sécurisé au site : ajout de la prise en charge SSL pour accéder à votre boutique Adobe Commerce et à votre panneau d’administration.&lt;!—MAGECLOUD—2360—>

- ![ icône de correctif ](../../assets/fix.svg) **Amélioration de la prise en charge de l’extension Adobe Commerce on cloud infrastructure** : mise à niveau de la version minimale requise pour le package guzzlehttp/guzzle dans Adobe Commerce on cloud infrastructure [fichier compositeur.json](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/overview) vers la version 6.2 afin que le package `ece-tools` soit compatible avec davantage d’extensions.<!--MAGECLOUD-2205-->

- ![nouvelle icône](../../assets/new.svg) **Appliquez des modifications personnalisées à votre application Adobe Commerce pendant la phase de création** : nous avons divisé la phase de création en deux processus distincts afin que vous puissiez utiliser des points d’extension pour appliquer des modifications personnalisées au contenu statique généré avant de compresser l’application pour le déploiement. Le processus _build:generate_ génère du code, applique des correctifs et génère du contenu statique. Le processus _build:transfer_ transfère le code généré et le contenu statique vers la destination finale. Voir [ hooks d’application ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property).<!--MAGECLOUD-2363-->

- ![ icône de correction ](../../assets/fix.svg) **Vérification de la configuration de l’environnement** : validation améliorée de la configuration de l’environnement pour avertir les clients des incompatibilités de version et des erreurs de configuration avant de créer et de déployer Adobe Commerce sur l’infrastructure cloud.

   - Ajout d’une validation spécifique à la version pour identifier les variables et valeurs d’environnement non prises en charge ou obsolètes.<!--MAGECLOUD-2183-->

   - Ajout d’une vérification de compatibilité des Elasticsearch pour avertir les utilisateurs des problèmes de configuration des Elasticsearch. Désormais, le déploiement échoue si la version du service Elasticsearch sur le serveur est incompatible avec Adobe Commerce. Auparavant, le déploiement réussissait même si la version de l’Elasticsearch était incompatible, ce qui provoquait des problèmes de catalogue de produits après le déploiement du site.<!--MAGECLOUD-2389-->

     Vous pouvez résoudre l&#39;incompatibilité en [envoyant un ticket de support](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/best-practices) pour mettre à niveau l&#39;Elasticsearch vers une version compatible, ou modifier la configuration Adobe Commerce pour spécifier une version compatible du client PHP Elasticsearch.

      - Pour Adobe Commerce version 2.1.x à 2.2.2, mettez à niveau Elasticsearch vers la version 2.4.

      - Pour Adobe Commerce version 2.2.3 et ultérieure, mettez à niveau l’Elasticsearch vers la version 5.2.

      - Si vous disposez d’Elasticsearch 1.x ou 2.x et que vous ne souhaitez pas effectuer la mise à niveau, mettez à jour la version du client PHP Elasticsearch Adobe Commerce dans le fichier compositeur.json vers `"elasticsearch/elasticsearch": "~2.0"`.

   - Amélioration de la validation des variables d’environnement afin d’identifier les paramètres de configuration pouvant entraîner des conflits lors des phases de création, de déploiement et de post-déploiement. Par exemple, un message d’avertissement s’affiche pendant le processus d’installation et de mise à niveau si le paramètre global pour le déploiement de contenu statique est en conflit avec les paramètres de la phase de création ou de déploiement.<!--MAGECLOUD-2156-->

- ![Icône de correctif](../../assets/fix.svg) **Mises à jour de variable d’environnement**—Modification des variables d’environnement suivantes :

   - **[SKIP_HTML_MINIFICATION variable globale](../environment/variables-global.md#skip_html_minification)** : modification de la valeur par défaut en `true` pour activer la minification de contenu d’HTML à la demande, ce qui réduit le temps d’arrêt lors du déploiement dans les environnements d’évaluation et de production. Cette configuration est requise pour les déploiements sans interruption.<!--MAGECLOUD-2435-->

   - **[Variable de déploiement CLEAN_STATIC_FILES](../environment/variables-deploy.md#clean_static_files)** : ajout de la capacité de gérer le traitement des fichiers statiques propres pour le contenu statique généré pendant la phase de génération en fonction du paramètre d’environnement CLEAN_STATIC_FILES . Auparavant, les fichiers de contenu statique générés pendant la phase de création étaient toujours nettoyés.<!--MAGECLOUD-1506-->

- ![icône de correctif](../../assets/fix.svg) **Journalisation** : les modifications suivantes ont été apportées pour améliorer les messages du journal et réduire la taille du journal :

   - Les entrées de journal des échecs de déploiement incluent désormais la sortie de commande des opérations qui provoquent les échecs même si votre configuration d’environnement ne spécifie pas la journalisation du niveau de débogage. Voir [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Ajout de la journalisation des échecs de déploiement qui se produisent lorsque des usines générées requises par certaines extensions ne peuvent pas être générées correctement, car le système de fichiers est en lecture seule.<!--MAGECLOUD-2209-->

   - Réduction de la taille du journal de déploiement et correction des problèmes de mise en forme causés par les commandes de configuration qui utilisent la barre de progression interactive.<!--MAGECLOUD-2402-->

   - Suppression de la verbalisation inutile et mise à jour des niveaux de priorité pour certaines instructions de journal.<!--MAGECLOUD-2227-->

- ![Icône de correctif](../../assets/fix.svg) **Correctifs spécifiques à Cron**—

   - Modification des paramètres de configuration de tâche cron par défaut pour la durée de vie de l’historique de la 3d (4320 min) à 1h (60 min) afin d’éviter les problèmes de performances et les échecs de déploiement qui peuvent se produire lorsque la file d’attente cron se remplit trop rapidement.<!--MAGECLOUD-2427-->

   - Amélioration du processus de gestion des tâches cron pendant la phase de déploiement afin d’empêcher les verrous de base de données et d’autres problèmes critiques. Désormais, toutes les tâches cron s’arrêtent pendant la phase de déploiement et redémarrent une fois le déploiement terminé.<!--MAGECLOUD-2445-->

   - Correction d’un problème lié au mécanisme de verrouillage pour la planification des consommateurs lancés par les tâches cron dans Adobe Commerce versions 2.2.0 et ultérieures afin d’empêcher les tâches cron de lancer des consommateurs en double.<!--MAGECLOUD-2464-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème lié au [processus de compression de contenu statique](../environment/variables-intro.md) (`gzip`) qui provoquait des erreurs `not overwritten` et `no such file or directory` lors du référencement du fichier compressé pendant le processus de déploiement.<!-- MAGECLOUD-2182-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui empêchait la commande `php ./vendor/bin/ece-tools config:dump` de supprimer des sections redondantes du fichier `config.php` pendant le processus de vidage si la langue de magasin n’était pas spécifiée. Vous pouvez désormais déplacer facilement vos fichiers de configuration entre les environnements. Après la mise à jour vers `ece-tools` v2002.0.13, régénérez les anciens fichiers `config.php` avec la commande `config:dump` améliorée. Voir [Gestion de la configuration des paramètres de magasin](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings).<!--MAGECLOUD-2444-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui provoquait une erreur lors de la phase de déploiement si la configuration d’itinéraire dans le fichier `.magento/routes.yaml` redirige d’un domaine [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) vers un domaine `www`.<!--MAGECLOUD-2556-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème lié à l’option `_merge` de la variable [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) qui provoquait des résultats de fusion incorrects si vous n’incluez pas le paramètre `engine` dans le fichier de configuration `.magento.env.yaml` mis à jour. Désormais, l’opération de fusion remplace correctement uniquement les valeurs que vous spécifiez dans le `.magento.env.yaml` mis à jour sans que vous ayez à définir le paramètre `engine`.<!--MAGECLOUD-2520-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème de configuration Redis qui activait incorrectement le verrouillage de session pour Adobe Commerce sur les versions 2.2.1 et ultérieures de l’infrastructure cloud, ce qui pouvait entraîner des performances et des délais d’attente lents. Désormais, le verrouillage de session est désactivé par défaut. Le problème était dû à un changement du comportement par défaut du paramètre `disable_locking` introduit dans la version 1.3.4 du package du gestionnaire de session Redis. Voir [colinmollenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![nouvelle icône](../../assets/new.svg) **Composer Docker pour Cloud**—Ajout d’une commande—`docker:build`—pour générer une configuration [Composer Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) à partir du référentiel `ece-tools` de Cloud.<!-- MAGECLOUD-2250 -->

- ![nouvelle icône](../../assets/new.svg) **Modifier les paramètres régionaux** : vous pouvez désormais modifier les paramètres régionaux du magasin sans le processus de configuration d’exportation et d’importation. Lorsque l&#39;application est en production et que SCD_ON_DEMAND est activé, les options de magasin et de paramètres régionaux d&#39;administration sont disponibles.<!-- MAGECLOUD-2019 -->

- ![nouvelle icône](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Plan du site et robots** : a créé un [workflow](../store/robots-sitemap.md) pour ajouter un fichier `robots.txt` et générer un fichier `sitemap.xml` pour une configuration de domaine unique sans avoir à modifier l’infrastructure.

- ![nouvelle icône](../../assets/new.svg) **Assistants**—Ajout de deux [assistants](../deploy/smart-wizards.md) pour vous aider dans la configuration du cloud :<!-- MAGECLOUD-1910 -->

   - `ideal-state` : configurez l’état idéal pour un temps d’arrêt minimal du déploiement.

   - `master-slave` : configuration de l’équilibrage de charge pour la base de données et Redis

- ![nouvelle icône](../../assets/new.svg) **Actualisation de module**—Ajout d’une commande cloud—`module:refresh`—pour activer les modules qui ont été désactivés ou n’ont pas été explicitement activés, comme cela est fait automatiquement lors d’une génération.<!-- MAGECLOUD-1521 -->

- ![nouvelle icône](../../assets/new.svg) Ajout de la possibilité de choisir la fusion ou le remplacement de la configuration pour les services à l’aide de l’option `_merge` dans les configurations [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSION](../environment/variables-deploy.md#session_configuration), [QUEUE](../environment/variables-deploy.md#queue_configuration) et [SEARCH](../environment/variables-deploy.md#search_configuration).<!-- MAGECLOUD-2105 -->

- ![nouvelle icône](../../assets/new.svg) **Fichier d’exemple de configuration d’environnement** : nous avons ajouté un fichier d’exemple `.magento.env.yaml` au package CEE-Outils qui inclut une description détaillée et des valeurs possibles pour chaque variable d’environnement.<!-- MAGECLOUD-1908 -->

   - Nous avons également ajouté une validation approfondie pour la configuration `.magento.env.yaml` qui empêche les échecs du processus de déploiement causés par des valeurs inattendues. Lorsqu’un échec se produit, vous recevez maintenant un message d’erreur détaillé commençant par : `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![new icon](../../assets/new.svg) Ajout des [**variables d’environnement**](../environment/variables-intro.md) suivantes :

   - Vous pouvez maintenant définir plusieurs paramètres régionaux pour chaque thème à l’aide de la nouvelle variable d’environnement [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix), ce qui réduit la quantité de fichiers de thème à déployer.<!-- MAGECLOUD-1501 -->

   - Ajout de la variable d&#39;environnement [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) pour personnaliser les connexions de base de données pour le déploiement.<!-- MAGECLOUD-2047 -->

   - La nouvelle variable [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) remplace le niveau de journalisation minimal pour tous les flux de sortie sans apporter de modifications au code.<!-- MAGECLOUD-2129 -->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème qui provoquait des temps d’arrêt entre la phase de déploiement et la phase de post-déploiement. Désormais, la phase de post-déploiement commence _immédiatement_ après la fin de la phase de déploiement.

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème qui ne nettoyait pas les tâches cron réussies, celles avec `status = success`, du planning.<!-- MAGECLOUD-2268 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème avec le crochet `post_deploy` qui effacait le cache lors de la phase de déploiement au lieu de la phase de post-déploiement du projet.<!-- MAGECLOUD-2113 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème lors de l’utilisation de SCD avec plusieurs paramètres régionaux, qui générait le même fichier `js-translation.json` pour chaque paramètre régional.<!-- MAGECLOUD-2034 -->

- ![icône de correction](../../assets/fix.svg) Optimisation de la commande `db:dump` dans le package `ece-tools` pour éviter de verrouiller les tables et augmenter la vitesse.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>La version 2002.0.11 des outils ECE est requise pour la compatibilité 2.2.4.

- ![nouvelle icône](../../assets/new.svg) **Configuration des connexions en lecture seule aux noeuds non maîtres** : cette version permet de configurer une connexion en lecture seule à un noeud non maître pour recevoir le trafic en lecture seule (pour [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) et pour <!--MAGECLOUD-143 -->

- ![nouvelle icône](../../assets/new.svg) **Assistant de configuration** : ajout d’un assistant pour vous aider à vérifier votre configuration pour le déploiement de contenu statique. Voir [Smart Wizards](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de la console Symfony**—Ajout de la prise en charge de la console Symfony 4 avec Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![icône de correctif](../../assets/fix.svg) **Optimisations de la planification Cron** : amélioration de la gestion des files d’attente et de la journalisation améliorée pour faciliter le débogage des problèmes liés à cron.<!-- MAGECLOUD-1607 -->

- ![icône de correction](../../assets/fix.svg) La validation du déploiement échoue si une valeur `ADMIN_EMAIL` ou `ADMIN_USERNAME` est identique à un compte administrateur existant.<!-- MAGECLOUD-1221 -->

- ![icône de correction](../../assets/fix.svg) Suppression de la prise en charge SOLR pour les versions 2.2.x. Les versions 2.1.x conservent la possibilité d’activer SOLR.<!-- MAGECLOUD-1282 -->

- ![icône de correction](../../assets/fix.svg) La première installation des environnements d’évaluation et de production d’un projet PRO inclut désormais différents préfixes d’index pour l’Elasticsearch afin d’éviter tout conflit potentiel tout en identifiant les enregistrements appartenant à chaque environnement.<!-- MAGECLOUD-1489 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui interrompait la phase de création de l’architecture héritée lors du déploiement de contenu statique.<!-- MAGECLOUD-2021 -->

- ![Icône de correctif](../../assets/fix.svg) **Améliorations spécifiques à Cron**—Réutilisation de l’implémentation de cron :<!-- MAGECLOUD-1607 -->

   - Correction d’un problème en raison duquel la file d’attente cron se remplissait rapidement. Maintenant, il efface les emplois obsolètes de cron d&#39;une manière plus fiable.

   - Réorganisation de la séquence des tâches cron afin que toutes les tâches dans des threads distincts soient lancées avant le groupe général.

   - Amélioration de la journalisation pour faciliter le débogage des problèmes cron.

   - **REMARQUE** : cette version résout de nombreux problèmes liés au cron. Si vous utilisez actuellement des correctifs liés à cron dans _m2-hotfixes_, supprimez-les.

- ![Icône de correctif](../../assets/fix.svg) **Améliorations spécifiques à SCD**—

   - Vous pouvez utiliser les variables d&#39;environnement `VERBOSE_COMMANDS` et `SCD_COMPRESSION_LEVEL` lors des phases _build_ et de_ploy.<!-- MAGECLOUD-1819 -->

   - Correction d’un problème en raison duquel le déploiement échouait avec une erreur aléatoire lors de la rencontre d’une valeur inattendue pour la variable d’environnement `SCD_COMPRESSION_LEVEL`. Amélioration de la validation de la configuration pour fournir des notifications significatives. Voir [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) pour connaître les valeurs acceptables.<!-- MAGECLOUD-2043 -->

   - Correction du comportement du flux de configuration de la variable d&#39;environnement `SCD_COMPRESSION_LEVEL` de sorte que les remplacements fonctionnent comme prévu.<!-- MAGECLOUD-2044 -->

   - Correction d’un problème qui empêchait la configuration de la variable d’environnement `SCD_THREADS` dans l’étape `.magento.env.yaml` file _deploy_.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![nouvelle icône](../../assets/new.svg) **Déploiement de contenu statique (SCD)** : il existe un nouveau processus de déploiement alternatif pour générer du contenu statique lorsque cela est demandé (sur demande). Cela réduit le temps d’arrêt et améliore la gestion du cache en générant les ressources les plus critiques.<!-- MAGECLOUD-1285 -->

   - **Nouvelle variable d&#39;environnement** : ajout de la variable d&#39;environnement global `SCD_ON_DEMAND` pour générer du contenu statique lorsque nécessaire.<!-- MAGECLOUD-1738 -->

   - **Hook de post-déploiement** : ajout d’un crochet `post_deploy` pour le fichier `.magento.app.yaml` qui efface le cache et pré-charge (warms) le cache _une fois_ que le conteneur commence à accepter les connexions. Il est disponible uniquement pour les projets Pro contenant des environnements d’évaluation et de production dans [!DNL Cloud Console] et pour les projets de démarrage. Bien que cela ne soit pas obligatoire, cela fonctionne en tandem avec la variable d&#39;environnement `SCD_ON_DEMAND`.<!-- MAGECLOUD-1788 -->

- ![nouvelle icône](../../assets/new.svg) **Optimisation**—Optimisation du déplacement ou de la copie de fichiers lors du déploiement pour améliorer la vitesse de déploiement et réduire les charges sur le système de fichiers.<!-- MAGECLOUD-1842 -->

- ![nouvelle icône](../../assets/new.svg) **Journalisation de déploiement** : ajout de la possibilité d’activer les gestionnaires Syslog et Graylog Extended Log Format (GELF) pour les journaux de sortie pendant le processus de déploiement. Voir [Gestionnaire de journalisation](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![new icon](../../assets/new.svg) Ajout des [**variables d’environnement**](../environment/variables-intro.md) suivantes :

   - `CRYPT_KEY` : spécifiez une clé cryptographique dans un autre environnement lors du déplacement d’une base de données.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Variable d’environnement globale_ qui ignore la copie des fichiers d’affichage statique dans le répertoire `var/view_preprocessed` et génère un HTML minimisé si nécessaire.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Variable d’environnement globale_ pour générer du contenu statique lorsque nécessaire.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES` : vous pouvez répertorier les pages à utiliser pour précharger le cache. Disponible dans les nouvelles [variables de post-déploiement](../environment/variables-post-deploy.md).

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui entraînait l’application locale d’un correctif interrompant le déploiement sur une instance. Maintenant, les outils de la CEE peuvent détecter qu&#39;un correctif a été appliqué.<!-- MAGECLOUD-982 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’un conflit entre la fonctionnalité de regroupement JavaScript et la fonctionnalité GZIP. Maintenant ces fonctionnalités fonctionnent correctement ensemble.<!-- MAGECLOUD-1735 -->

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème qui entraînait l’échec des commandes de l’interface de ligne de commande ECE-Tools lors de l’utilisation de versions antérieures de PHP 7.0.x.<!-- MAGECLOUD-1744 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui empêchait le déploiement de contenu statique avec la stratégie compacte dans plusieurs threads.<!-- MAGECLOUD-1822 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème de verrouillage de session Redis qui provoquait un délai de connexion administrateur. En outre, le correctif est disponible pour 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Vous devez [mettre à niveau Adobe Commerce sur le métapaquet d’infrastructure cloud](../dev-tools/install-package.md#update-the-metapackage) pour obtenir ceci et toutes les futures mises à jour.

- ![nouvelle icône](../../assets/new.svg) **ece-tools**—Le package `ece-tools` prend désormais en charge Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![nouvelle icône](../../assets/new.svg) **Configuration Redis** : vous pouvez désormais [ configurer la page Redis](../environment/variables-deploy.md#cache_configuration), le cache par défaut et le stockage de session Redis à l’aide d’une variable d’environnement.<!-- MAGECLOUD-1552 -->

- ![nouvelle icône](../../assets/new.svg) **Améliorations du service Search, AMQP et Redis** : nous avons unifié le flux de configuration du service afin qu’il se comporte désormais de la même manière pour tous les services. La modification manuelle du fichier `env.php` pour configurer les services n’est plus prise en charge. Vous devez utiliser des variables d&#39;environnement ou le fichier `.magento.env.yaml` à la place.<!-- MAGECLOUD-1437 -->

- ![Icône de correctif](../../assets/fix.svg) **Variables d’environnement**—

   - L’utilisation de `env:STATIC_CONTENT_THREADS` a été abandonnée et sera supprimée dans une prochaine version. Utilisez à la place [SCD_THREADS](../environment/variables-deploy.md#scd_threads).<!-- MAGECLOUD-1507 -->

   - La variable d’environnement `STATIC_CONTENT_EXCLUDE_THEMES` a été abandonnée. Vous devez utiliser la variable d&#39;environnement `SCD_EXCLUDE_THEMES` à la place.<!-- MAGECLOUD-1640 -->

- ![Icône de correctif](../../assets/fix.svg) **Journalisation** : nous avons simplifié la journalisation autour des opérations de correctif intégrées.<!-- MAGECLOUD-1674 -->

- ![icône de correction](../../assets/fix.svg) Nous avons supprimé la prise en charge du mode `developer` et la variable d&#39;environnement `APPLICATION_MODE`, car ils provoquaient un comportement inattendu.<!-- MAGECLOUD-1615 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui provoquait des échecs de déploiement de contenu statique liés à Redis. Désormais, le déploiement de contenu statique multithread s’exécute comme prévu.<!-- MAGECLOUD-1630 -->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui empêchait les utilisateurs d’enregistrer les modifications apportées aux champs de configuration dans l’administrateur, qui sont marqués comme sensibles après l’exécution de la commande `app:config:dump`.<!-- MAGECLOUD-1175 -->

- ![icône de correctif](../../assets/fix.svg) Nous avons ajouté la prise en charge d’une version antérieure de `symfony/yaml` pour résoudre les conflits avec certains packages, qui ne sont pas encore compatibles avec la dernière version.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>Nous avons fusionné `vendor/magento/ece-patches` avec `vendor/magento/ece-tools` dans cette version. Vous n’avez plus besoin de mettre à jour le package `vendor/magento/ece-patches` séparément.

**Nouvelles fonctionnalités :**

- **Journalisation améliorée**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Nous avons amélioré la messagerie des journaux afin de fournir de meilleures explications lorsque le processus de création ou de déploiement remplace une variable d’environnement.
   - Vous pouvez désormais visualiser la progression de l’installation et de la mise à niveau en temps réel. Suivez le fichier `install_update.log` pour afficher la progression. Par exemple,

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Nouvelle commande cron** : vous pouvez désormais déverrouiller des tâches cron bloquées spécifiques au lieu de les arrêter et de les relancer avec la commande [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451). Non disponible dans 2.1.<!-- MAGECLOUD-1367 -->

- **Fichier de configuration unifié** : vous pouvez désormais configurer les étapes de création et de déploiement à l’aide d’un fichier [`.magento.env.yaml`](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml).<!-- MAGECLOUD-1369 -->

- **Fichiers de configuration de sauvegarde** : le processus de déploiement crée désormais automatiquement une sauvegarde des fichiers de configuration `app/etc/env.php` et `app/etc/config.php` après le déploiement. Nous avons également ajouté une [nouvelle commande d’interface de ligne de commande](https://support.magento.com/hc/en-us/articles/360033182871) pour restaurer ces fichiers de configuration à partir d’une sauvegarde.<!-- MAGECLOUD-1372 -->

- **Résolution des problèmes d’erreurs de validation** : nous avons modifié la commande que vous devez utiliser pour résoudre les erreurs de validation lorsque `config.php` ne contient pas suffisamment de données pour le déploiement de contenu statique. Auparavant, le message d’erreur vous demandait d’exécuter `bin/magento app:config:dump`. Maintenant, vous devez exécuter `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Nouvelles variables d’environnement** : vous pouvez désormais utiliser des variables d’environnement pour connecter des services [search](../environment/variables-deploy.md#search_configuration) et [AMQP-based](../environment/variables-deploy.md#queue_configuration) personnalisés à votre site.<!-- MAGECLOUD-1410 -->

- Nous avons mis en oeuvre des correctifs intelligents. Désormais, le package applique des correctifs basés non pas sur Adobe Commerce sur la version de l’infrastructure cloud, mais sur la version du package corrigée.<!--MAGECLOUD-1090-->

**Problèmes résolus :**

- Correction d’un problème de journalisation qui provoquait des erreurs de build.<!-- MAGECLOUD-1162 -->

- Correction d’un problème qui provoquait des exceptions de délai d’expiration lors de l’exécution de déploiements en mode interactif.<!-- MAGECLOUD-1389 -->

- Correction d’un problème qui provoquait des erreurs lors de l’utilisation de la stratégie compacte pour la génération de contenu statique. Non disponible dans 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Correction d’un problème qui empêchait le script de déploiement d’identifier correctement les environnements d’évaluation et de production.<!-- MAGECLOUD-1493 -->

- Correction d’un problème en raison duquel des problèmes réseau perturbaient les connexions à la base de données et provoquaient des échecs pendant le processus d’installation et de mise à niveau.<!-- MAGECLOUD-1520 -->

- Correction d’un problème qui vous empêchait d’exporter plusieurs fois les fichiers de configuration à l’aide de `app:config:dump`. Non disponible dans 2.1.<!--  MAGECLOUD-1567  -->

- Nous avons corrigé un problème de _verrouillage_ de session Redis qui provoquait un délai de connexion _Admin_. Non disponible dans 2.1.<!--  MAGECLOUD-1582  -->

- Correction d’un problème de mise en oeuvre lié au contrôle de version qui provoquait un conflit avec d’autres modules de correctif basés sur le compositeur.<!-- MAGECLOUD-1450 -->

- Nous avons corrigé un problème qui provoquait des problèmes de mémoire PHP lors de l’importation.<!-- MAGECLOUD-1310 -->

- Suppression d’un correctif ; correction d’un bogue dans `colinmollenhour/credis` v1.6 pour activer la prise en charge d’Adobe Commerce sur l’infrastructure cloud 2.2.1. Non disponible dans 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Problèmes résolus :**

- Nous avons supprimé `var/view_preprocessed` symlinks pour résoudre un problème qui provoquait des conflits de minification JavaScript.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Problèmes résolus :**

- Correction d’un problème qui provoquait des erreurs `gzip` lorsqu’un nom de fichier ou de répertoire contenait des espaces.<!-- MAGECLOUD-1413 -->

- Correction d’un problème qui empêchait les scripts de déploiement de reconnaître et activer correctement les dépendances des modules.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Nouvelles fonctionnalités :**

- **Configurez un consommateur cron avec une variable d’environnement** : vous pouvez désormais configurer les consommateurs cron à l’aide de la nouvelle variable d’environnement `CRON_CONSUMERS_RUNNER`.

- **Analyse de la configuration** : nous analysons désormais les composants critiques pendant le processus de création/déploiement et arrêtons le processus en cas d’échec de l’analyse, ce qui empêche des temps d’arrêt inutiles en raison du fait que le site est en mode de maintenance.

- **Créer/déployer des notifications** : nous avons ajouté un fichier de configuration que vous pouvez utiliser pour [ configurer des notifications Slack et/ou par e-mail ](../environment/set-up-notifications.md) pour créer/déployer des actions dans tous vos environnements.

- **Compression de contenu statique** : nous compressons désormais le contenu statique à l’aide de [gzip](https://www.gnu.org/software/gzip/) pendant les phases de création et de déploiement. Cette compression, associée à une compression rapide, permet de réduire la taille de votre magasin et d’augmenter la vitesse de déploiement. Si nécessaire, vous pouvez désactiver la compression à l’aide d’une [option de build](../environment/variables-build.md) ou d’une [variable de déploiement](../environment/variables-deploy.md). Pour plus d’informations, consultez les rubriques suivantes :

   - [Variables d’environnement d’application](../application/variables-property.md)

   - [Performances du déploiement de contenu statique](../deploy/static-content.md)

   - [Processus de déploiement](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/best-practices)

- **Gestion de la configuration** : nous générons désormais automatiquement un fichier `app/etc/config.php` dans votre référentiel Git pendant la phase de création, s’il n’existe pas déjà. Le fichier généré automatiquement comprend uniquement une liste de modules et d’extensions. Si le fichier existe déjà, la phase de création se poursuit normalement. Si vous suivez la [gestion de configuration](../store/store-settings.md) ultérieurement, les commandes mettent à jour le fichier sans nécessiter d’autres étapes. Pour plus d’informations, voir [Processus de déploiement](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/best-practices) .

- **Décharges de base de données** : nous avons ajouté une commande d’interface de ligne de commande `magento/ece-tools` pour créer des vidages de base de données dans tous les environnements. Pour les environnements de production Pro-plan, cette commande est uniquement vidée à partir de l’un des trois noeuds haute disponibilité. Par conséquent, les données de production écrites sur un autre noeud pendant le vidage peuvent ne pas être copiées. Nous vous recommandons de mettre l’application en mode de maintenance avant d’effectuer un vidage de base de données dans les environnements de production. Voir [Gestion des sauvegardes](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/snapshots) pour plus d’informations.

- **Limites d’intervalle Cron levées** : l’intervalle cron par défaut pour tous les environnements configurés dans les régions us-3, eu-3 et ap-3 est d’1 minute. L’intervalle cron par défaut dans toutes les autres régions est de 5 minutes pour les environnements Pro Integration et de 1 minute pour les environnements Pro Staging et Production. Pour modifier vos tâches cron existantes, modifiez vos paramètres dans `.magento.app.yaml` ou créez un ticket de support pour les environnements de production/d’évaluation. Pour plus d’informations, voir [Configuration de tâches cron](../application/crons-property.md#set-up-cron-jobs) .

**Problèmes résolus :**

- Correction d’un problème qui provoquait de longs délais de déploiement en raison du processus de déploiement appelant l’opération `cache-clean` avant le déploiement de contenu statique.<!-- MAGECLOUD-1327 -->

- Correction d’un problème provoquant des erreurs lors de l’étape de génération statique du contenu du déploiement dans les environnements de production.<!-- MAGECLOUD-1322 -->

- Correction d’un problème qui empêchait certaines commandes `magento/ece-tools` de consigner la sortie sur `stderr`.<!-- MAGECLOUD-1264 -->

- Correction d’un problème qui empêchait la mise à jour des valeurs de l’URL de base dans `env.php` dans les branches dupliquées.<!-- MAGECLOUD-1242 -->

- Correction d’un problème en raison duquel la commande `magento setup:install` ajoutait un préfixe non sécurisé (`http://`) pour sécuriser les URL de base.<!-- MAGECLOUD-1171 -->

- Correction d’un problème empêchant les erreurs de correctif de provoquer des échecs de déploiement.<!-- MAGECLOUD-1170 -->

- Correction d&#39;un problème qui empêchait `ece-tools` d&#39;arrêter l&#39;exécution et de lancer une exception si aucun correctif ne pouvait être appliqué.<!-- MAGECLOUD-1152 -->

- Correction d’un problème qui provoquait des erreurs lors du chargement du storefront après l’activation de la minimisation des HTMLS dans l’administrateur.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Problèmes résolus :**

- Vous pouvez désormais [réinitialiser manuellement les tâches cron bloquées](https://support.magento.com/hc/en-us/articles/360033099451) à l’aide d’une commande d’interface de ligne de commande dans tous les environnements via un accès SSH. Le processus de déploiement réinitialise automatiquement les tâches cron.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Problèmes résolus :**

- Correction d’un problème en raison duquel les pages expiraient car Redis prenait trop de temps pour lire/écrire. Vous pouvez désormais utiliser le paramètre `disable_locking` dans les configurations Redis pour éviter ce problème.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Problèmes résolus :**

- Le processus de configuration [!DNL RabbitMQ] obtient désormais automatiquement tous les paramètres requis.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Nouvelles fonctionnalités :**

- Adobe Commerce sur l’infrastructure cloud prend désormais en charge les portées et les [stratégies de déploiement de contenu statique](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy). Nous avons ajouté le paramètre `–s` avec un paramètre par défaut `quick` pour la stratégie de déploiement de contenu statique. Vous pouvez utiliser la variable d’environnement [SCD_STRATEGY](../environment/variables-deploy.md) pour personnaliser et utiliser ces stratégies avec vos actions de création et de déploiement. Cette variable prend en charge les options `standard`, `quick` ou `compact`. Si vous sélectionnez `compact`, nous remplaçons la valeur `STATIC_CONTENT_THREADS` par `1`, ce qui peut ralentir le déploiement, en particulier dans les environnements de production. Non disponible dans 2.1.<!--- MAGECLOUD-1057 -->

- Nous avons créé un fichier journal sur les environnements pour capturer et compiler les actions de création et de déploiement. Le fichier `var/log/cloud.log` se trouve dans le répertoire racine de l&#39;application.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Problèmes résolus :**

- Refactorisation du package `ece-tools` pour le rendre compatible avec Adobe Commerce sur l&#39;infrastructure cloud 2.2.0 et versions ultérieures.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Correction d&#39;un problème qui empêchait `ece-tools` d&#39;interrompre l&#39;exécution et de lancer une exception si aucun correctif ne peut être appliqué.<!-- MAGECLOUD-1186 -->

- Correction d’un problème en raison duquel des exceptions étaient générées lorsque la compilation d’injection de dépendance (di) était ignorée pendant les builds.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Correction d’un problème en raison duquel le processus de déploiement écrasait les configurations Redis personnalisées dans le fichier `env.php`.<!-- MAGECLOUD-1019 -->

- Correction d’un problème en raison duquel les boucles de redirection étaient désactivées par l’administrateur sécurisé par défaut.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Ce package n’est plus compatible avec d’autres versions d’Adobe Commerce sur l’infrastructure cloud et **ne doit pas être utilisé.**

### Version initiale

Version initiale de `ece-tools` pour Adobe Commerce sur l’infrastructure cloud 2.2.0.
