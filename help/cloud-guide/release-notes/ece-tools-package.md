---
title: Notes de mise à jour de CEE-Outils
description: Consultez la liste des dernières améliorations apportées au module d'outils de la CEE.
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: 923e2114270df22e134e0676ac97f84d770bb226
workflow-type: tm+mt
source-wordcount: '2929'
ht-degree: 0%

---

# Notes de mise à jour de CEE-Outils

Le package [ece-tools](https://github.com/magento/ece-tools) est un ensemble de scripts et d’outils conçus pour gérer et déployer des projets Cloud. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui fait partie de la [suite d’outils cloud pour Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Voir [Mise à niveau de CEE-Outils](../dev-tools/update-package.md) pour plus d’informations sur la mise à jour vers la dernière version du package `ece-tools`.

Le package `ece-tools` utilise la séquence de contrôle de version suivante : `200<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![Icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->

## v2002.1.19 {#latest}

Date de publication : 21 mai 2024

- ![nouvelle icône](../../assets/new.svg) **Lua** : ajout de l’option useLua pour CACHE_CONFIGURATION.
- ![Icône de correctif](../../assets/fix.svg) **Validator**—Mise à jour des validateurs pour les nouvelles versions de Redis et RabbitMQ.

## v2002.1.18

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** — Prise en charge de PHP 8.3.
- ![icône de correctif](../../assets/fix.svg) Validator - Validator EOL mise à jour.

## v2002.1.17

Date de publication : 16 janvier 2024

- ![Icône de correctif](../../assets/fix.svg) **Validator for Elasticsearch &amp; OpenSearch**—Correction du programme de validation qui produisait un message trompeur pour installer un service de recherche lorsque LiveSearch est activé.<!-- MCLOUD-10167 -->
- ![Icône de correctif](../../assets/fix.svg) **Avertissement de déploiement**—Correction d’un problème qui entraînait des avertissements de déploiement sur les dossiers non vides.<!-- MCLOUD-8958 -->

## v2002.1.16

Date de publication : 16 octobre 2023

- ![nouvelle icône](../../assets/new.svg) **ENABLE_WEBHOOKS variable d’environnement global**—Ajout de la variable globale [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) à utiliser avec les webhooks Commerce pour se connecter à un point de terminaison externe, tel qu’une action d’exécution App Builder ou un système de gestion d’inventaire tiers.

## v2002.1.15

Date de publication : 31 juillet 2023

- ![Icône de correctif](../../assets/fix.svg) **Codes d’erreur** : schéma de code d’erreur mis à jour et générateur de document de code d’erreur.
- ![icône de correctif](../../assets/fix.svg) **Validator for custom Redis model** - Mise à jour du programme de validation pour les modèles d’arrière-plan Redis personnalisés. [Voir l’exemple pour la configuration du cache ](../environment/variables-deploy.md#cache_configuration).
- ![icône de correctif](../../assets/fix.svg) **Validator for RabbitMQ** - Ajout de la prise en charge de RabbitMQ 3.11
- ![ icône de correctif](../../assets/fix.svg) **Correction du lien incorrect** : correction du lien incorrect vers la documentation d’intégration dans le modèle d’email de bienvenue.

## v2002.1.14

Date de publication : 10 mars 2023

- ![nouvelle icône](../../assets/new.svg) **PHP** : prise en charge de PHP 8.2.
- ![nouvelle icône](../../assets/new.svg) **Validators for Services**—Mise à jour des validateurs pour Commerce 2.4.6 des services requis : MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x et RabbitMQ 3.9.
- ![icône de correctif](../../assets/fix.svg) **ece-tools db-dump** : correction d’un problème en raison duquel l’opération `db-dump` s’arrêtait prématurément.

## v2002.1.13

Date de publication : 27 octobre 2022

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge des événements d’Adobe I/O pour Adobe Commerce**. Les développeurs d’extensions peuvent désormais utiliser la structure [Adobe I/O Events](https://developer.adobe.com/events/docs/) pour envoyer des informations d’événement Commerce des instances cloud à leurs applications écrites pour [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Les événements d’Adobe I/O pour Adobe Commerce sont dans l’aperçu du partenaire.<!-- CEXT-932 -->
- ![nouvelle icône](../../assets/new.svg) **Validator for OPcache configuration**—Ajout d’un programme de validation pour vérifier la configuration OPcache pour les chemins exclus.<!-- MCLOUD-9485 -->
- ![icône de correction](../../assets/fix.svg) **Correction d’un problème lié à la configuration du cache GraphQL**. Désormais, les outils de la CEE conservent la valeur GraphQL `id_salt` dans la configuration `cache` du fichier `app/etc/env.php`.<!-- MCLOUD-9486 -->

## v2002.1.12

Date de publication : 13 septembre 2022

- ![nouvelle icône](../../assets/new.svg) **Activez`synchronous_replication`**—Jeu d’outils CEE `synchronous_replication=>true` dans le fichier `app/etc/env.php` lorsque `MYSQL_USE_SLAVE_CONNECTION` est activé. Cette configuration affecte uniquement Commerce 2.4.6+. Voir la description de la variable `MYSQL_USE_SLAVE_CONNECTION` dans [Déployer des variables](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![nouvelle icône](../../assets/new.svg) **OpenSearch** : ajout d’une fonctionnalité permettant de configurer et de définir le moteur `opensearch` pour la prochaine version d’Adobe Commerce 2.4.6. Voir [Configuration du service OpenSearch](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.1

Date de publication : 4 août 2022

- ![icône de correction](../../assets/fix.svg) **ElasticSuite Validator and OpenSearch**—Correction du problème de validation de l’intégrité d’ElasticSuite lors de l’installation d’OpenSearch.<!-- MCLOUD-8767 -->
- ![Icône de correctif](../../assets/fix.svg) **Types de retour pour les commandes de déploiement**—Types de retour fixes pour les commandes de déploiement.<!-- AC-3208 -->
- ![icône de correction](../../assets/fix.svg) **[!DNL RabbitMQ]problème avec la nouvelle installation de Commerce 2.4.5**—Correction d’un problème de blocage [!DNL RabbitMQ] sur la nouvelle installation de Commerce 2.4.5.<!-- MCLOUD-9059 -->

## v2002.1.10

Date de publication : 31 mars 2022

- ![icône de correctif](../../assets/fix.svg) **Elasticsearch 7.10**—Mise à jour des validateurs pour la prise en charge de la version 7.10 d’Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **OpenSearch**—Ajout de la prise en charge d’OpenSearch pour Adobe Commerce versions 2.4.4, 2.4.3-p2 et 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![nouvelle icône](../../assets/new.svg) **PHP** : prise en charge de PHP 8.1.
- ![Icône de correctif](../../assets/fix.svg) **symfony/process**—Ajout de la compatibilité avec symfony/process ^5.3.<!-- MCLOUD-8283 -->

- ![nouvelle icône](../../assets/new.svg) **Processus multiples de consommateur** : ajout d’une option `multiple_processes` afin que vous puissiez spécifier le nombre de processus à générer pour chaque consommateur. Voir la description de la variable `CRON_CONSUMERS_RUNNER` dans [Déployer des variables](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![nouvelle icône](../../assets/new.svg) **OpenSearch scheme et chemin d’accès d’hôte complet** : ajout de la possibilité de configurer un schéma d’Elasticsearch et un chemin d’accès d’hôte complet.
- ![icône de correctif](../../assets/fix.svg) **AWS S3** : modification de la méthode d’activation d’AWS S3.
- ![icône de correctif](../../assets/fix.svg) **Fix driver_options reader**—Ajout de la configuration de lecture driver_options pour la connexion DB du fichier `env.php` par `ece-tools` pour les validateurs.<!-- MCLOUD-8420 -->

## v2002.1.8

Date de publication : 25 octobre 2021

- ![nouvelle icône](../../assets/new.svg) **Emplacement de vidage alternatif** : ajout de l’option `--dump-directory` afin que vous puissiez choisir un répertoire cible pour un vidage DB. Désormais `/app/var/dump-main` est le répertoire cible par défaut pour un vidage DB. Voir [Gestion des sauvegardes : sauvegarder votre base de données](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![Icône de correctif](../../assets/fix.svg) **Mise à jour de monolog**—Mise à jour de la version minimale requise pour le package `monolog` vers `^2.3`.<!-- ACMP-1263 -->
- ![Icône de correctif](../../assets/fix.svg) **Mettre à jour Symfony** : mise à jour des dépendances Symfony pour qu’elles soient compatibles avec Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![icône de correctif](../../assets/fix.svg) **Fonctionnalité/résolution du chargement automatique** : correction d’un problème lors du déploiement dans un environnement d’intégration et de l’affichage de l’erreur `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.`.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Date de publication : 29 juillet 2021

**Mises à jour de configuration**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge du compositeur 2.0.<!--MCLOUD-8003-->

- ![icône de correction](../../assets/fix.svg) **Mise à jour des exigences du compositeur pour`symphony/console`**—Mise à jour des exigences de version `composer.json` de la version CEE-Outils pour le package `symphony/console` afin de résoudre un problème qui entraînait l’échec des commandes `di:compile` avec l’erreur suivante : `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![Icône de correctif](../../assets/fix.svg) Mise à jour des vérifications de logiciels de fin de vie (`eol.yaml`) pour inclure Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Date de publication : 20 avril 2021

- ![new icon](../../assets/new.svg) **Redis authentication credentials** : ajout de la possibilité de lire les informations d’identification d’autorisation Redis à partir de la propriété `relationships` pendant la phase de déploiement.<!--MCLOUD-7694-->

- ![nouvelle icône](../../assets/new.svg) **informations d’identification d’autorisation Elasticsearch** : ajout de la possibilité de lire les informations d’identification d’autorisation Elasticsearch à partir de la propriété `relationships` pendant la phase de déploiement.<!--MCLOUD-7695-->

- ![nouvelle icône](../../assets/new.svg) **Service de stockage de session dédié**—Ajout de `redis-session` comme deuxième option pour le stockage de session. Vous pouvez utiliser le service `redis-session` pour stocker des informations de session et utiliser le service `redis` pour le cache afin de fournir de meilleures performances.<!--MCLOUD-7698-->

- ![nouvelle icône](../../assets/new.svg) **Messages SPLIT_DB obsolètes**—Ajout d’un avertissement de validateur et de messages critiques pour l’option `SPLIT_DB` obsolète pour Adobe Commerce 2.4.2 et sa suppression dans Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![icône de correctif](../../assets/fix.svg) **version Elasticsearch à partir des relations**—Correction du programme de validation des services pour récupérer la version correcte de l’Elasticsearch à partir des propriétés `relationships` dans Cloud Docker et les environnements d’intégration.<!--MCLOUD-7572-->

- ![icône de correction](../../assets/fix.svg) **Validation flexible du port Redis** : Redis peut désormais valider le port dans une connexion de cache personnalisée à partir de l’URL `server`. Par exemple, vous pouvez ajouter votre numéro de port à l’URL de votre serveur comme suit : `server: 'tcp://rfs-store-simple-page-cache:26379'`. Cela permet d&#39;empêcher les erreurs de validation lorsque l&#39;option `port` est manquante ou incorrecte.<!--MCLOUD-7722-->

- ![icône de correctif](../../assets/fix.svg) **Mise à niveau vers Adobe Commerce 2.4.2**—Correction du problème qui obligeait les utilisateurs à exécuter manuellement `bin/magento setup:upgrade` pour que leurs sites soient opérationnels après la mise à niveau vers Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Date de publication : 1 février 2021

- ![nouvelle icône](../../assets/new.svg) **Stockage à distance** : ajout de la variable d’environnement `REMOTE_STORAGE` pour activer les projets cloud pour le stockage à distance des fichiers multimédias à l’aide d’un service de stockage, tel qu’AWS S3. Cette option de configuration fait partie du package CEE-Outils, mais n&#39;est pas prise en charge sur Adobe Commerce sur l&#39;infrastructure cloud.<!--MCLOUD-7153-->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle `cloud:config:validate` commande**—Ajout d’une commande `php vendor/bin/ece-tools cloud:config:validate` pour valider la configuration `.magento.env.yaml` avant de pousser les modifications vers l’environnement cloud distant.<!--MCLOUD-7120-->

- ![nouvelle icône](../../assets/new.svg) **Purge du cache de l’ouverture**—Ajout de la prise en charge de l’option `opcache.enable_cli` PHP pour vider le cache de l’opération avant d’exécuter le crochet de déploiement. Cette configuration réinitialise la configuration du cache pour s&#39;assurer que les paramètres de configuration actuels sont appliqués à chaque déploiement.<!--MCLOUD-7015-->

- ![nouvelle icône](../../assets/new.svg) **Validation d’Aurora DB**—Mise à jour de la validation du service de base de données afin qu’il soit compatible avec la base de données Aurora.<!--MCLOUD-7269-->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement SCD_NO_PARENT**—Ajout de la variable d’environnement `SCD_NO_PARENT` (pour Adobe Commerce >=2.4.2) pour gérer la génération de contenu statique pour les thèmes parents.<!--MCLOUD-7284-->

- ![icône de correctif](../../assets/fix.svg) **Limites et commandes de mémoire** : correction d’un problème en raison duquel les commandes `php vendor/bin/ece-tools` ne fonctionnaient pas si la taille du fichier `cloud.log` dépassait la limite de mémoire PHP. Au lieu de lire l&#39;intégralité du fichier `cloud.log` en mémoire, nous ne lisons plus qu&#39;un sous-ensemble plus petit de données du fichier journal.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![icône de correction](../../assets/fix.svg) **** : correction d’un problème de configuration `.magento.env.yaml` en raison duquel les connexions de base de données personnalisées définies pour `DATABASE_CONFIGURATION` n’étaient pas utilisées. Les paramètres de connexion n&#39;ont pas été ajoutés à `app/etc/env.php`.<!--MCLOUD-7426-->

- ![Icône de correctif](../../assets/fix.svg) **Journaux d’erreur vides** : correction d’un problème qui provoquait l’échec des déploiements si le `cloud.error.log` était vide.<!--MCLOUD-7296-->

- ![Icône de correctif](../../assets/fix.svg) **Validation MariaDB 10.3**—Correction de la validation de MariaDB 10.3 pour Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![Icône de correctif](../../assets/fix.svg) **Cache:flush logging**—Amélioration des entrées de journal pour indiquer le début et la fin de l’étape `cache:flush`.<!--MCLOUD-7503-->

## v2002.1.4

Date de publication : 19 novembre 2020

- ![icône de correction](../../assets/fix.svg) Correction d’un problème qui provoquait l’échec du déploiement lorsque le moteur de recherche spécifié dans la variable d’environnement `SEARCH_CONFIGURATION` était une valeur autre que `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Date de publication : 9 novembre 2020

**Mises à jour de l’infrastructure**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge des outils CEE pour le répertoire `pub/static` en lecture seule lorsque le contenu statique est défini pour être déployé à l’étape de création.<!--MC-37699-->

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge d’Elasticsearch 7.9 et de Redis 6 pour la compatibilité avec les prochaines versions d’Adobe Commerce.<!--MCLOUD-7191-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour des outils de la gestion des balises numériques `composer.json` pour ajouter une dépendance requise pour l’outil de correctifs de qualité. Ceci corrige une dépendance circulaire qui existait entre les packages EC-Tools et magento-cloud-patches.<!--MCLOUD-6910-->

**Améliorations de la validation et du journal**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la validation du moteur de recherche pour s’assurer que `elasticsearch` est défini pour Adobe Commerce sur l’infrastructure cloud 2.4 et versions ultérieures. Si la validation échoue, le déploiement est arrêté avec un message d’erreur critique suggérant des correctifs pour le problème. Voir [Erreurs critiques, déploiement de l’étape](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![nouvelle icône](../../assets/new.svg) Ajout de la validation de l’Elasticsearch pour vérifier la compatibilité entre la version du service Elasticsearch et la version d’Adobe Commerce.<!--MCLOUD-7193-->

- ![nouvelle icône](../../assets/new.svg) Mise à jour du message d’erreur de compatibilité des Elasticsearch pour afficher les versions d’Elasticsearch compatibles avec le module d’Elasticsearch Adobe Commerce. Le message d’erreur fournit désormais les versions spécifiques de l’Elasticsearch à installer dans votre infrastructure cloud afin qu’elle soit compatible avec le module Elasticsearch utilisé par votre version d’Adobe Commerce. Voir [Erreurs d’avertissement, déploiement de l’étape](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![nouvelle icône](../../assets/new.svg) Ajout d’erreurs d’avertissement `2026` et `2027` pour le paramètre de variable d’environnement `MAGE_MODE` non valide. La seule valeur valide est `production`. Avant ce correctif, `MAGE_MODE` pouvait être défini sur `developer` sans erreurs de déploiement, pour entraîner des erreurs ultérieurement lors de la tentative d’écriture dans des fichiers en lecture seule. Voir [Erreurs d’avertissement](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![icône de correction](../../assets/fix.svg) Correction de la validation des services Redis, RabbitMQ et MySQL pour s’assurer que ces versions sont compatibles avec la version d’Adobe Commerce. Les versions valides de ces services sont maintenant écrites dans le `cloud.log`.<!--MCLOUD-7098-->

- ![ icône de correction ](../../assets/fix.svg) Mise à jour de `cloud.log` afin d’inclure la limite des demandes simultanées pour envoyer des demandes pendant la chaleur du cache. Cette valeur est configurée dans la variable [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) post-déploiement.<!--MCLOUD-5563-->

**Mises à jour des commandes de l’interface de ligne de commande**—

- ![nouvelle icône](../../assets/new.svg) Ajout de commandes d’interface de ligne de commande (`cloud:config:create` et `cloud:config:update`) pour créer et mettre à jour le fichier `.magento.env.yaml` avec une configuration pouvant inclure une ou plusieurs variables de création, de déploiement et de post-déploiement. Voir [Création d’un fichier de configuration à partir de l’interface en ligne de commande](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Mises à jour des variables d’environnement**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la variable de build [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload). La définition de la variable sur `true` empêche l’application d’exécuter la commande `composer dump-autoload` lors d’une installation de Cloud Docker for Commerce. La variable ne concerne que les conteneurs Cloud Docker pour Commerce avec des systèmes de fichiers modifiables (créés pour le test et le développement à l’aide de `./vendor/bin/ece-docker build:compose --with-test`). Pour de telles installations, ignorer la commande `composer dump-autoload` empêche les erreurs lors de l&#39;exécution d&#39;autres commandes qui tentent d&#39;accéder aux fichiers à partir d&#39;un répertoire `generated` supprimé.<!--MCLOUD-6939-->

## v2002.1.2

Date de publication : 5 août 2020

**Améliorations de la validation et du journal**—

- ![new icon](../../assets/new.svg) Ajout du fichier `schema.error.yaml` qui comprend toutes les notifications d’erreur et d’avertissement pouvant survenir pendant le processus de création, de déploiement et de post-déploiement, ainsi que des suggestions pour résoudre les erreurs. Les informations de ce fichier sont également disponibles dans le _Guide Cloud pour Commerce_. Voir [Référence du message d’erreur pour les outils-citoyen](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![nouvelle icône](../../assets/new.svg) Modification des entrées du journal des erreurs cloud (`/var/log/cloud.error.log`) au format JSON pour faciliter l’analyse du journal par programmation.<!--MCLOUD-5879-->

- ![nouvelle icône](../../assets/new.svg) Ajout de vérifications d’erreurs supplémentaires pour créer, déployer et post-déployer le traitement et amélioration des vérifications existantes :

   - Code d’erreur 2026 : échec de la restauration de certaines données générées pendant la phase de création dans les répertoires montés.

   - Code d’erreur 3004 : impossible de créer des fichiers de sauvegarde.

   - Code d’erreur 102 : ajout de vérifications supplémentaires pour les problèmes qui se produisent lorsque le fichier `env.php` n’est pas modifiable <!--MCLOUD-6221-->.

- ![nouvelle icône](../../assets/new.svg) Ajout de la variable d’environnement **QUALITY_PATCH** pour spécifier un ou plusieurs correctifs de qualité à appliquer pendant le processus de déploiement. Voir [Créer des variables](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de l’infrastructure**—

   - ![nouvelle icône](../../assets/new.svg) **Améliorations de la journalisation** : amélioration de la fonctionnalité de suivi des journaux en attribuant des codes de sortie aux erreurs de déploiement critiques et en exposant les codes de sortie dans les notifications de messages d’erreur et les événements de journal. Voir [Référence du message d’erreur pour les outils-citoyen](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![new icon](../../assets/new.svg) Amélioration du processus pour les vidages de base de données (`vendor/bin/ece-tools db-dump`) et mise à jour des messages de journal pour clarifier que l’opération de vidage de base de données passe en mode de maintenance, arrête les processus de file d’attente des consommateurs et désactive les tâches cron avant le début de la vidage.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème pour s’assurer que l’URL du projet est correctement mise à jour lors du déploiement dans les environnements d’évaluation et de production. Désormais, `ece-tools` utilise l’URL de l’itinéraire avec l’attribut `primary:true` défini dans la configuration de l’itinéraire du projet. Voir [Déploiement de variables](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![icône de correctif](../../assets/fix.svg) Mise à jour du workflow de scénario de version `generate.xml` pour appliquer des correctifs. Des correctifs doivent être appliqués plus tôt pour mettre à jour Adobe Commerce afin de résoudre les problèmes susceptibles d&#39;entraîner l&#39;échec des étapes `di:compile` et `module:refresh`.<!--MCLOUD-5941-->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème dans le processus d’installation qui renvoie incorrectement l’erreur `Crypt key missing`. La valeur `crypt/key` est générée automatiquement lors de l&#39;installation.<!--MCLOUD-6120-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de PHP 7.4 et MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de variable d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable **SCD_USE_BALER** pour activer le module Baler pour le regroupement JavaScript pendant le processus de création d’Adobe Commerce sur l’infrastructure cloud. Voir la description de la variable dans les [variables de build](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable d’environnement **REDIS_BACKEND** pour configurer le modèle principal Redis pour le cache Redis pour Adobe Commerce 2.3.5 ou version ultérieure. Voir la description de la variable dans [deploy variables](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de la commande CLI**—

   - ![nouvelle icône](../../assets/new.svg) Mise à jour des commandes de l’interface de ligne de commande suivantes avec une option de journalisation plus détaillée :

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Le niveau de journalisation de chaque appel est déterminé par la configuration de la variable [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) dans le fichier `.magento.env.yaml`.<!--MCLOUD-3503-->

- ![nouvelle icône](../../assets/new.svg) **Améliorations de la validation**—

   - ![nouvelle icône](../../assets/new.svg) **Vérifications de compatibilité Elasticsearch 7.x**—Mise à jour de la validation Elasticsearch pour les vérifications de compatibilité des logiciels Elasticsearch 7.x.<!--MCLOUD-5542-->

   - ![nouvelle icône](../../assets/new.svg) **{Mise à jour des contrôles de version de service et de validation EOL**—Mise à jour de la validation afin de vérifier les versions de service installées par rapport aux exigences d’Adobe Commerce 2.4.<!--MCLOUD-6144-->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème de validation de sorte que le message d’avertissement suivant après le déploiement s’affiche uniquement si la configuration du crochet `post-deploy` est manquante dans le fichier `.magento.app.yaml` :

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![nouvelle icône](../../assets/new.svg) **Ajout de la validation des dépendances Zend Framework** : ajout de la validation de la dépendance de compositeur pour Zend Framework qui a migré vers le projet Laminas. Si les dépendances requises sont manquantes, le message d’erreur suivant s’affiche pendant le processus de création.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Voir [Vérification des dépendances du Zend Framework](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![nouvelle icône](../../assets/new.svg) **Ajout de la validation du fichier `env.php` et des données**—Ajout de vérifications pour le fichier `env.php` et les données pendant le processus d&#39;installation et de mise à niveau.<!--MCLOUD-5991-->

      - Si le fichier `env.php` est manquant dans l’installation et que la valeur `crypt/key` n’est pas spécifiée dans le fichier `.magento.app.yaml`, le déploiement échoue avec la notification suivante :

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Si l&#39;installation n&#39;inclut pas le fichier `env.php` ou si la configuration ne contient qu&#39;un seul type de cache, la commande `cron:enable` s&#39;exécute pendant le processus de mise à niveau pour restaurer le fichier avec tous les `cache_types`. La notification suivante est ajoutée au journal :

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Date de publication : 6 février 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de l’infrastructure**—

   - ![nouvelle icône](../../assets/new.svg) **Ajout d’un package distinct pour Cloud Docker pour Commerce** : découplé le package Docker du package `ece-tools` pour maintenir la qualité du code et fournir des versions indépendantes. Les mises à jour et les correctifs liés à `ece-tools` sont gérés à partir du référentiel [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub.<!--MAGECLOUD-2927-->

   - ![nouvelle icône](../../assets/new.svg) **{Fonctionnalités de correction mises à jour** : déplacement de la fonctionnalité de correction du package CEE-Outils vers un package [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) distinct. Pendant le déploiement, `ece-tools` utilise le nouveau package pour appliquer des correctifs. Voir [Notes de mise à jour des correctifs de cloud](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![nouvelle icône](../../assets/new.svg) **Dépendances du compositeur mises à jour** : mise à jour du fichier `composer.json` pour Adobe Commerce sur l’infrastructure cloud avec une dépendance pour le package `magento/magento-cloud-docker`. Désormais, `ece-tools` comprend des dépendances pour tous les packages de [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Ces packages sont installés et mis à jour automatiquement lorsque vous installez ou mettez à jour `ece-tools`.

- ![nouvelle icône](../../assets/new.svg) **Prise en charge des déploiements basés sur des scénarios**—<!--MAGECLOUD-4101-->

   - ![nouvelle icône](../../assets/new.svg) Vous pouvez désormais personnaliser les processus de création, de déploiement et de post-déploiement à l’aide de fichiers de configuration XML pour remplacer ou personnaliser la configuration par défaut.

   - ![new icon](../../assets/new.svg) **Modification de la configuration `hooks` dans`.magento.app.yaml`** - Nous avons mis à jour le format de configuration `hooks` pour prendre en charge les déploiements basés sur des scénarios. Le format hérité de la version antérieure de CEE-Outils 2002.0.x est toujours pris en charge. Cependant, vous devez effectuer une mise à jour vers le nouveau format pour utiliser la fonctionnalité de déploiement basée sur un scénario. Voir [Déploiements basés sur des scénarios](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Avant de procéder à la mise à jour vers la version 2002.1.0 des outils de la CEE, passez en revue le [   modifications incompatibles](backward-incompatible-changes.md) pour en savoir plus sur les modifications qui peuvent nécessiter votre   mettre à jour Adobe Commerce sur la configuration ou les processus d’un projet d’infrastructure cloud.

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de PHP 7.3.<!--MAGECLOUD-4022-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   - ![nouvelle icône](../../assets/new.svg) Ajout d’une validation permettant de vérifier les versions de service installées par rapport à la date de fin de vie de chaque service. Désormais, les clients reçoivent une notification si une version de service est dans les trois mois suivant la date de fin de service et un avertissement si la date de fin de service est antérieure.<!--MAGECLOUD-4076-->

   - ![Icône de correctif](../../assets/fix.svg) Correction d’un problème de configuration de l’Elasticsearch pour s’assurer que les paramètres Elasticsearch corrects sont configurés dans tous les environnements.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Voir [Versions de service](../services/services-yaml.md#service-versions) pour obtenir la liste des services utilisés dans Adobe Commerce sur l’infrastructure cloud et leur compatibilité avec le modèle Cloud.

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de variable d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Extension de la fonctionnalité de la variable d’environnement `WARM_UP_PAGES` pour la prise en charge du préchargement du cache pour des pages de produits spécifiques. Voir la définition étendue dans la rubrique [Variables de post-déploiement](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-4444-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la variable d’environnement `ERROR_REPORT_DIR_NESTING_LEVEL` pour simplifier la gestion des données de rapport d’erreur dans le répertoire `<magento_root>/var/report/`. Voir la description de la variable dans la rubrique [variables de build](../environment/variables-build.md#error_report_dir_nesting_level) .

   - ![icône de correctif](../../assets/fix.svg) Suppression des variables d’environnement `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT` et `STATIC_CONTENT_SYMLINK`. Voir [Modifications incompatibles avec l’arrière](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![icône de correction](../../assets/fix.svg) Correction d’un problème dans le processus de configuration de la suite adaptative de sorte que la configuration par défaut soit écrasée comme prévu lorsque vous configurez la variable de déploiement `ELASTICSUITE_CONFIGURATION` sans l’option `_merge`.<!--MAGECLOUD-4388-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de la commande CLI**—

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle commande cron** : vous pouvez désormais gérer manuellement le traitement cron dans votre environnement d’infrastructure cloud Adobe Commerce à l’aide des commandes `cron:disable` et `cron:enable`. Utilisez la commande disable pour arrêter tous les processus cron actifs et désactiver toutes les tâches cron. Utilisez la commande enable pour réactiver les tâches cron lorsque vous êtes prêt. Voir [Désactivation des tâches cron](../application/crons-property.md#disable-cron-jobs).

   - ![nouvelle icône](../../assets/new.svg) **Rapports d’erreurs améliorés**—Ajout d’une meilleure journalisation pour les échecs de commande de l’interface de ligne de commande qui se produisent pendant le traitement des outils de la CEE.<!--MAGECLOUD-4849-->

   - ![nouvelle icône](../../assets/new.svg) **Supprimer les commandes de build obsolètes**— Suppression des commandes de build suivantes : `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump` et `ece-tools docker` renommés `ece-docker`. Voir [ Modifications incompatibles rétrogrades](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![new icon](../../assets/new.svg) Suppression du fichier `build_options.ini` obsolète et ajout de la validation pour échouer à la création si le fichier existe. Utilisez le fichier [.magento.env.yaml](../environment/configure-env-yaml.md) pour configurer les options de version.

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel le processus de création échouait lorsque le fichier `config.php` était vide.<!--MAGECLOUD-4127-->

## 2002.0.23

Date de publication : 27 février 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de compatibilité avec les versions de `ece-tools` 2002.0.x qui empêchaient la génération de contenu statique à la demande de se terminer correctement en mode de production.

## Anciennes versions

Voir l’ [ archive des notes de mise à jour](cloud-release-archive.md) pour les versions 2002.0.22 et antérieures.
