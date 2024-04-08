---
title: Notes de mise à jour de CEE-Outils
description: Consultez la liste des dernières améliorations apportées au module d'outils de la CEE.
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: e21f21e34f89b62842bd22c99ff5705f984898e0
workflow-type: tm+mt
source-wordcount: '2905'
ht-degree: 0%

---

# Notes de mise à jour de CEE-Outils

La variable [ece-tools](https://github.com/magento/ece-tools) Le module est un ensemble de scripts et d’outils conçus pour gérer et déployer des projets Cloud. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui fait partie de la [Suite d’outils cloud pour Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Voir [Mise à niveau des outils CEE](../dev-tools/update-package.md) pour plus d’informations sur la mise à jour vers la dernière version du `ece-tools` module.

La variable `ece-tools` Le module utilise la séquence de contrôle de version suivante : `200<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->


## v2002.1.18 {#latest}

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** — Prise en charge de PHP 8.3.
- ![icône de correctif](../../assets/fix.svg) Validator : validateur de fin de vie mis à jour.

## v2002.1.17

Date de publication : 16 janvier 2024

- ![icône de correctif](../../assets/fix.svg) **Validator pour Elasticsearch et OpenSearch**: correction du programme de validation qui générait un message trompeur pour installer un service de recherche lorsque LiveSearch est activé.<!-- MCLOUD-10167 -->
- ![icône de correctif](../../assets/fix.svg) **Avertissement de déploiement**: correction d’un problème qui entraînait des avertissements de déploiement sur les dossiers non vides.<!-- MCLOUD-8958 -->

## v2002.1.16

Date de publication : 16 octobre 2023

- ![nouvelle icône](../../assets/new.svg) **Variable d’environnement globale ENABLE_WEBHOOKS**: ajout de la propriété [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) variable globale à utiliser avec les webhooks Commerce pour se connecter à un point de terminaison externe, tel que l’action d’exécution App Builder ou un système de gestion de l’inventaire tiers.

## v2002.1.15

Date de publication : 31 juillet 2023

- ![icône de correctif](../../assets/fix.svg) **Codes d’erreur**: mise à jour du schéma de code d’erreur et du générateur de document de code d’erreur.
- ![icône de correctif](../../assets/fix.svg) **Validation pour le modèle Redis personnalisé**- Mise à jour du programme de validation pour les modèles d’arrière-plan Redis personnalisés. [Voir l’exemple de configuration du cache](../environment/variables-deploy.md#cache_configuration).
- ![icône de correctif](../../assets/fix.svg) **Validator pour RabbitMQ** Ajout de la prise en charge de RabbitMQ 3.11
- ![icône de correctif](../../assets/fix.svg) **Correction d’un lien incorrect**- Correction d’un lien incorrect vers la documentation d’intégration dans le modèle d’email de bienvenue.

## v2002.1.14

Date de publication : 10 mars 2023

- ![nouvelle icône](../../assets/new.svg) **PHP**: ajout de la prise en charge de PHP 8.2.
- ![nouvelle icône](../../assets/new.svg) **Validateurs pour les services**—Mise à jour des validateurs pour les services requis de Commerce 2.4.6 : MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x et RabbitMQ 3.9.
- ![icône de correctif](../../assets/fix.svg) **ece-tools db-dump**: correction d’un problème en raison duquel la variable `db-dump` pour arrêter prématurément.

## v2002.1.13

Date de publication : 27 octobre 2022

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge des événements d’Adobe I/O pour Adobe Commerce**. Les développeurs d’extensions peuvent désormais utiliser la variable [Événements d’Adobe I/O](https://developer.adobe.com/events/docs/) framework pour envoyer des informations d’événement Commerce d’instances Cloud à leurs applications écrites pour [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Les événements d’Adobe I/O pour Adobe Commerce sont présentés dans la section Aperçu du partenaire.<!-- CEXT-932 -->
- ![nouvelle icône](../../assets/new.svg) **Validator pour la configuration de OPcache**: ajout d’un programme de validation pour vérifier la configuration OPcache pour les chemins exclus.<!-- MCLOUD-9485 -->
- ![icône de correctif](../../assets/fix.svg) **Correction d’un problème lié à la configuration du cache de GraphQL.**—Maintenant, les outils de la CEE conservent le GraphQL `id_salt` dans `cache` dans la `app/etc/env.php` fichier .<!-- MCLOUD-9486 -->

## v2002.1.12

Date de publication : 13 septembre 2022

- ![nouvelle icône](../../assets/new.svg) **Activer`synchronous_replication`**—Jeu d’outils CEE `synchronous_replication=>true` dans le `app/etc/env.php` lors de `MYSQL_USE_SLAVE_CONNECTION` est activée. Cette configuration affecte uniquement Commerce 2.4.6+. Voir `MYSQL_USE_SLAVE_CONNECTION` description de la variable dans la variable [Déploiement de variables](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![nouvelle icône](../../assets/new.svg) **OpenSearch**: ajout d’une fonctionnalité pour configurer et définir la variable `opensearch` pour la prochaine version d’Adobe Commerce 2.4.6. Voir [Configuration du service OpenSearch](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.1

Date de publication : 4 août 2022

- ![icône de correctif](../../assets/fix.svg) **ElasticSuite Validator et OpenSearch**: correction d’un problème de validation de l’intégrité d’ElasticSuite lors de l’installation d’OpenSearch.<!-- MCLOUD-8767 -->
- ![icône de correctif](../../assets/fix.svg) **Types de retour pour les commandes de déploiement**: correction des types de retour pour les commandes de déploiement.<!-- AC-3208 -->
- ![icône de correctif](../../assets/fix.svg) **[!DNL RabbitMQ]Problème avec la nouvelle installation de Commerce 2.4.5**—Fixe [!DNL RabbitMQ] problème de blocage sur la nouvelle installation de Commerce 2.4.5.<!-- MCLOUD-9059 -->

## v2002.1.10

Date de publication : 31 mars 2022

- ![icône de correctif](../../assets/fix.svg) **Elasticsearch 7.10**—Mise à jour des validateurs pour la prise en charge de la version 7.10 d’Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **OpenSearch**: ajout de la prise en charge d’OpenSearch pour Adobe Commerce versions 2.4.4, 2.4.3-p2 et 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![nouvelle icône](../../assets/new.svg) **PHP**: ajout de la prise en charge de PHP 8.1.
- ![icône de correctif](../../assets/fix.svg) **symfony/process**—Ajout de la compatibilité avec symfony/process ^5.3.<!-- MCLOUD-8283 -->

- ![nouvelle icône](../../assets/new.svg) **Processus multiples des consommateurs**: ajout d’un `multiple_processes` afin que vous puissiez spécifier le nombre de processus à générer pour chaque consommateur. Voir `CRON_CONSUMERS_RUNNER` description de la variable dans la variable [Déploiement de variables](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![nouvelle icône](../../assets/new.svg) **Schéma OpenSearch et chemin d’accès complet à l’hôte**: ajout de la possibilité de configurer un schéma Elasticsearch et un chemin d’accès hôte complet.
- ![icône de correctif](../../assets/fix.svg) **AWS S3**: modification de la méthode d’activation d’AWS S3.
- ![icône de correctif](../../assets/fix.svg) **Correctif driver_options reader**—Ajout de la configuration de lecture driver_options pour la connexion DB à partir du `env.php` par `ece-tools` pour les validateurs.<!-- MCLOUD-8420 -->

## v2002.1.8

Date de publication : 25 octobre 2021

- ![nouvelle icône](../../assets/new.svg) **Autre emplacement de vidage**: ajout de la propriété `--dump-directory` afin que vous puissiez choisir un répertoire cible pour un vidage DB. Maintenant `/app/var/dump-main` est le répertoire cible par défaut pour un vidage DB. Voir [Gestion des sauvegardes : videz votre base de données](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![icône de correctif](../../assets/fix.svg) **Mettre à jour Monolog**: mise à jour de la version minimale requise pour le `monolog` vers `^2.3`.<!-- ACMP-1263 -->
- ![icône de correctif](../../assets/fix.svg) **Mettre à jour Symfony**: mise à jour des dépendances Symfony pour garantir la compatibilité avec Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![icône de correctif](../../assets/fix.svg) **Chargement automatique des fonctionnalités/résolutions**: correction d’un problème lors du déploiement dans un environnement d’intégration et de l’affichage de la variable `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` erreur.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Date de publication : 29 juillet 2021

**Mises à jour de configuration**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge du compositeur 2.0.<!--MCLOUD-8003-->

- ![icône de correctif](../../assets/fix.svg) **Configuration requise mise à jour pour le compositeur`symphony/console`**—Mise à jour des outils de la CEE `composer.json` configuration requise pour la variable `symphony/console` pour résoudre un problème qui provoquait la `di:compile` des commandes à échouer avec l’erreur suivante : `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour des vérifications de logiciels de fin de vie (`eol.yaml`) pour inclure Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Date de publication : 20 avril 2021

- ![nouvelle icône](../../assets/new.svg) **Identifiants d’authentification Redis**: ajout de la possibilité de lire les informations d’autorisation Redis à partir du `relationships` pendant la phase de déploiement.<!--MCLOUD-7694-->

- ![nouvelle icône](../../assets/new.svg) **informations d’identification d’autorisation Elasticsearch**: ajout de la possibilité de lire les informations d’autorisation d’Elasticsearch à partir du `relationships` pendant la phase de déploiement.<!--MCLOUD-7695-->

- ![nouvelle icône](../../assets/new.svg) **Service de stockage de session dédié**—Ajouté `redis-session` comme deuxième option pour le stockage de session. Vous pouvez utiliser la variable `redis-session` pour stocker des informations de session et utiliser la variable `redis` service pour le cache afin de fournir de meilleures performances.<!--MCLOUD-7698-->

- ![nouvelle icône](../../assets/new.svg) **Messages SPLIT_DB obsolètes**: ajout d’un avertissement de validateur et de messages critiques pour les utilisateurs obsolètes. `SPLIT_DB` pour Adobe Commerce 2.4.2 et sa suppression dans Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![icône de correctif](../../assets/fix.svg) **Version Elasticsearch à partir des relations**: Correction du programme de validation des services pour récupérer la version correcte de l’Elasticsearch à partir du `relationships` dans les environnements Cloud Docker et d’intégration.<!--MCLOUD-7572-->

- ![icône de correctif](../../assets/fix.svg) **Validation flexible des ports Redis**: Redis peut désormais valider le port dans une connexion de cache personnalisée à partir du `server` URL. Par exemple, vous pouvez ajouter votre numéro de port à l’URL de votre serveur comme suit : `server: 'tcp://rfs-store-simple-page-cache:26379'`. Cela permet d’éviter les erreurs de validation lorsque la variable `port` est manquante ou incorrecte.<!--MCLOUD-7722-->

- ![icône de correctif](../../assets/fix.svg) **Mise à niveau vers Adobe Commerce 2.4.2**: correction d’un problème qui obligeait les utilisateurs à exécuter manuellement. `bin/magento setup:upgrade` pour rendre leurs sites opérationnels après la mise à niveau vers Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Date de publication : 1 février 2021

- ![nouvelle icône](../../assets/new.svg) **Stockage distant**: ajout de la propriété `REMOTE_STORAGE` pour activer Cloud Projects pour le stockage à distance des fichiers multimédias à l’aide d’un service de stockage, tel qu’AWS S3. Cette option de configuration fait partie du package CEE-Outils, mais n’est pas prise en charge sur Adobe Commerce sur l’infrastructure cloud.<!--MCLOUD-7153-->

- ![nouvelle icône](../../assets/new.svg) **Nouveau `cloud:config:validate` command**—Ajout, commande `php vendor/bin/ece-tools cloud:config:validate` pour valider la variable `.magento.env.yaml` avant d’envoyer les modifications à l’environnement cloud distant.<!--MCLOUD-7120-->

- ![nouvelle icône](../../assets/new.svg) **Purge de l’opcache**: ajout de la prise en charge du paramètre `opcache.enable_cli` option PHP pour vider le fichier OPcache avant d’exécuter le point d’extension deploy. Cette configuration réinitialise la configuration du cache pour s’assurer que les paramètres de configuration actuels sont appliqués à chaque déploiement.<!--MCLOUD-7015-->

- ![nouvelle icône](../../assets/new.svg) **Validation de la base de données Aurora**: mise à jour de la validation du service de base de données afin qu’il soit compatible avec la base de données Aurora.<!--MCLOUD-7269-->

- ![nouvelle icône](../../assets/new.svg) **Nouvelle variable d’environnement SCD_NO_PARENT**: ajout de la propriété `SCD_NO_PARENT` Variable d’environnement (pour Adobe Commerce >=2.4.2) pour gérer la génération de contenu statique pour les thèmes parents.<!--MCLOUD-7284-->

- ![icône de correctif](../../assets/fix.svg) **Limites et commandes de mémoire**: correction d’un problème en raison duquel `php vendor/bin/ece-tools` ne fonctionnerait pas si la taille de la variable `cloud.log` a dépassé la limite de mémoire PHP. Au lieu de lire l’intégralité de la `cloud.log` dans la mémoire, nous ne lisons plus qu’un sous-ensemble plus petit de données du fichier journal.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![icône de correctif](../../assets/fix.svg) **Connexions à une base de données personnalisée**: fixe un `.magento.env.yaml` problème de configuration où les connexions de base de données personnalisées définies pour `DATABASE_CONFIGURATION` n’ont pas été utilisées. Les paramètres de connexion n’étaient pas ajoutés à `app/etc/env.php`.<!--MCLOUD-7426-->

- ![icône de correctif](../../assets/fix.svg) **Journaux des erreurs vides**: correction d’un problème en raison duquel les déploiements échouaient si la variable `cloud.error.log` était vide.<!--MCLOUD-7296-->

- ![icône de correctif](../../assets/fix.svg) **Validation MariaDB 10.3**— Correction de la validation de MariaDB 10.3 pour Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![icône de correctif](../../assets/fix.svg) **Cache : journalisation de la purge**: entrées de journal améliorées pour indiquer le début et la fin de la variable `cache:flush` étape .<!--MCLOUD-7503-->

## v2002.1.4

Date de publication : 19 novembre 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel le déploiement échouait lorsque le moteur de recherche spécifié dans la variable `SEARCH_CONFIGURATION` La variable d’environnement est une valeur autre que `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Date de publication : 9 novembre 2020

**Mises à jour de l’infrastructure**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge des outils CEE pour le lecture seule `pub/static` lorsqu’un contenu statique est défini pour être déployé dans l’étape de création.<!--MC-37699-->

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge d’Elasticsearch 7.9 et de Redis 6 pour la compatibilité avec les prochaines versions d’Adobe Commerce.<!--MCLOUD-7191-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour des outils de la CEE `composer.json` pour ajouter une dépendance requise pour l’outil Correctifs de qualité. Ceci corrige une dépendance circulaire qui existait entre les packages de CEE-Outils et de magento-cloud-Correctifs.<!--MCLOUD-6910-->

**Améliorations de la validation et du journal**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la validation du moteur de recherche pour garantir que `elasticsearch` est défini pour Adobe Commerce sur l’infrastructure cloud 2.4 et versions ultérieures. Si la validation échoue, le déploiement est arrêté avec un message d’erreur critique suggérant des correctifs pour le problème. Voir [Erreurs critiques, déploiement de l’étape](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![nouvelle icône](../../assets/new.svg) Ajout d’une validation Elasticsearch pour vérifier la compatibilité entre la version du service Elasticsearch et la version Adobe Commerce.<!--MCLOUD-7193-->

- ![nouvelle icône](../../assets/new.svg) Mise à jour du message d’erreur de compatibilité des Elasticsearch afin d’afficher les versions d’Elasticsearch compatibles avec le module d’Elasticsearch Adobe Commerce. Le message d’erreur fournit désormais les versions spécifiques de l’Elasticsearch à installer dans votre infrastructure cloud afin qu’elle soit compatible avec le module Elasticsearch utilisé par votre version d’Adobe Commerce. Voir [Erreurs d’avertissement, déploiement de l’étape](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![nouvelle icône](../../assets/new.svg) Ajout d’erreurs d’avertissement `2026` et `2027` pour non valide `MAGE_MODE` paramètre de variable d’environnement . La seule valeur valide est `production`. Avant ce correctif, `MAGE_MODE` peut être défini sur `developer` sans erreurs de déploiement, afin de générer des erreurs ultérieurement lors de la tentative d’écriture dans des fichiers en lecture seule. Voir [Erreurs d’avertissement](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![icône de correctif](../../assets/fix.svg) Correction de la validation des services Redis, RabbitMQ et MySQL pour s’assurer que ces versions sont compatibles avec la version d’Adobe Commerce. Les versions valides de ces services sont désormais écrites dans la `cloud.log`.<!--MCLOUD-7098-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de la `cloud.log` pour inclure la limite des demandes simultanées pour l’envoi de requêtes lors de la chaleur du cache. Cette valeur est configurée dans la variable [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) post-déploiement.<!--MCLOUD-5563-->

**Mises à jour des commandes de l’interface de ligne de commande**—

- ![nouvelle icône](../../assets/new.svg) Ajout de commandes d’interface de ligne de commande (`cloud:config:create` et `cloud:config:update`) pour créer et mettre à jour le `.magento.env.yaml` avec une configuration pouvant inclure une ou plusieurs variables de création, de déploiement et de post-déploiement. Voir [Création d’un fichier de configuration à partir de l’interface de ligne de commande](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Mises à jour des variables d’environnement**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) build . Définir la variable sur `true` empêche l’application d’exécuter la fonction `composer dump-autoload` lors d’une installation de Cloud Docker pour Commerce. La variable ne s’applique qu’aux conteneurs Cloud Docker pour Commerce avec des systèmes de fichiers modifiables (créés à des fins de test et de développement à l’aide de `./vendor/bin/ece-docker build:compose --with-test`). Avec de telles installations, sautez la variable `composer dump-autoload` empêche les erreurs lors de l’exécution d’autres commandes qui tentent d’accéder à des fichiers à partir d’une commande supprimée. `generated` répertoire .<!--MCLOUD-6939-->

## v2002.1.2

Date de publication : 5 août 2020

**Améliorations de la validation et du journal**—

- ![nouvelle icône](../../assets/new.svg) Ajout de la `schema.error.yaml` qui comprend toutes les notifications d’erreur et d’avertissement qui peuvent se produire pendant le processus de création, de déploiement et de post-déploiement, ainsi que des suggestions pour résoudre les erreurs. Les informations contenues dans ce fichier sont également disponibles dans la variable _Guide Cloud pour Commerce_. Voir [Référence de message d’erreur pour les outils de texte](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![nouvelle icône](../../assets/new.svg) Modification du journal des erreurs du cloud (`/var/log/cloud.error.log`) au format JSON pour faciliter l’analyse du journal par programmation.<!--MCLOUD-5879-->

- ![nouvelle icône](../../assets/new.svg) Ajout de vérifications d’erreurs supplémentaires pour créer, déployer et post-déployer le traitement et amélioration des vérifications existantes :

   - Code d’erreur 2026 : échec de la restauration de certaines données générées pendant la phase de création dans les répertoires montés.

   - Code d’erreur 3004 : impossible de créer des fichiers de sauvegarde.

   - Code d’erreur 102 : ajout de vérifications supplémentaires pour les problèmes qui se produisent lorsque la variable `env.php` Le fichier n’est pas modifiable <!--MCLOUD-6221-->

- ![nouvelle icône](../../assets/new.svg) Ajout de la **QUALITY_PATCH** pour spécifier un ou plusieurs correctifs de qualité à appliquer au cours du processus de déploiement. Voir [Créer des variables](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de l’infrastructure**—

   - ![nouvelle icône](../../assets/new.svg) **Amélioration de la journalisation**: amélioration de la fonctionnalité de suivi des journaux en attribuant des codes de sortie aux erreurs de déploiement critiques et en exposant les codes de sortie dans les notifications de messages d’erreur et les événements de journal. Voir [Référence de message d’erreur pour les outils de texte](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![nouvelle icône](../../assets/new.svg) Amélioration du processus de vidages de base de données (`vendor/bin/ece-tools db-dump`) et mise à jour des messages du journal afin de clarifier le fait que l’opération de vidage de la base de données bascule l’application en mode de maintenance, arrête les processus de file d’attente des consommateurs et désactive les tâches cron avant le début de la vidage.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème pour s’assurer que l’URL du projet est correctement mise à jour lors du déploiement dans les environnements d’évaluation et de production. Maintenant, `ece-tools` utilise l’URL de l’itinéraire avec la variable `primary:true` défini dans la configuration de l’itinéraire du projet. Voir [Déploiement de variables](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![icône de correctif](../../assets/fix.svg) Mise à jour de la `generate.xml` workflow de scénario de création pour appliquer des correctifs. Les correctifs doivent être appliqués plus tôt pour mettre à jour Adobe Commerce afin de résoudre les problèmes susceptibles d’entraîner la `di:compile` et `module:refresh` les étapes à échouer.<!--MCLOUD-5941-->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème dans le processus d’installation qui renvoyait incorrectement la variable `Crypt key missing` erreur. La variable `crypt/key` est générée automatiquement lors de l’installation.<!--MCLOUD-6120-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge de PHP 7.4 et MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des variables d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **SCD_USE_BALER** pour activer le module Baler pour le bundling JavaScript pendant le processus de création d’Adobe Commerce sur l’infrastructure cloud. Voir la description de la variable dans la section [variables de création](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la **REDIS_BACKEND** pour configurer le modèle d’arrière-plan Redis pour le cache Redis d’Adobe Commerce 2.3.5 ou version ultérieure. Voir la description de la variable dans la section [variables de déploiement](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des commandes de l’interface de ligne de commande**—

   - ![nouvelle icône](../../assets/new.svg) Mise à jour des commandes d’interface de ligne de commande suivantes avec une option pour une journalisation plus détaillée :

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Le niveau de journalisation de chaque appel est déterminé par la configuration de la variable [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) dans la variable `.magento.env.yaml` fichier .<!--MCLOUD-3503-->

- ![nouvelle icône](../../assets/new.svg) **Amélioration de la validation**—

   - ![nouvelle icône](../../assets/new.svg) **Vérifications de compatibilité Elasticsearch 7.x**: mise à jour de la validation des Elasticsearch pour les contrôles de compatibilité des logiciels Elasticsearch 7.x.<!--MCLOUD-5542-->

   - ![nouvelle icône](../../assets/new.svg) **Mise à jour des contrôles de version de service et de validation EOL**: mise à jour de la validation afin de vérifier les versions de service installées par rapport aux exigences d’Adobe Commerce 2.4.<!--MCLOUD-6144-->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème de validation en raison duquel le message d’avertissement suivant de post-déploiement s’affichait uniquement si la variable `post-deploy` La configuration du point d’extension est absente de `.magento.app.yaml` fichier :

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![nouvelle icône](../../assets/new.svg) **Ajout de la validation des dépendances Zend Framework**: ajout de la validation de la dépendance de compositeur pour Zend Framework qui a migré vers le projet Laminas. Si les dépendances requises sont manquantes, le message d’erreur suivant s’affiche pendant le processus de création.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Voir [Vérification des dépendances du framework Zend](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![nouvelle icône](../../assets/new.svg) **Ajout de la validation pour `env.php` fichier et données**: ajout de vérifications pour le `env.php` fichier et données pendant le processus d’installation et de mise à niveau.<!--MCLOUD-5991-->

      - Si la variable `env.php` n’apparaît pas dans l’installation et la variable `crypt/key` n’est pas spécifiée dans la variable `.magento.app.yaml` , le déploiement échoue avec la notification suivante :

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Si l’installation n’inclut pas la variable `env.php` ou la configuration ne contient qu’un seul type de cache, le `cron:enable` s’exécute pendant le processus de mise à niveau pour restaurer le fichier avec tous les `cache_types`. La notification suivante est ajoutée au journal :

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Date de publication : 6 février 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de l’infrastructure**—

   - ![nouvelle icône](../../assets/new.svg) **Ajout d’un package distinct pour Cloud Docker pour Commerce.**: dissociation du module Docker du `ece-tools` pour maintenir la qualité du code et fournir des versions indépendantes. Mises à jour et correctifs liés à `ece-tools` sont gérées à partir de la fonction [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) Référentiel GitHub.<!--MAGECLOUD-2927-->

   - ![nouvelle icône](../../assets/new.svg) **Fonctionnalités de correction mises à jour**: Déplacement de la fonctionnalité de correctif du package CEE-Outils vers un package distinct. [magento-cloud-Correctifs](https://github.com/magento/magento-cloud-patches) module. Pendant le déploiement, `ece-tools` utilise le nouveau package pour appliquer des correctifs. Voir [Notes de mise à jour des correctifs de cloud](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![nouvelle icône](../../assets/new.svg) **Dépendances du compositeur mises à jour**: mise à jour de la variable `composer.json` pour Adobe Commerce sur l’infrastructure cloud avec une dépendance pour la variable `magento/magento-cloud-docker` module. Maintenant, `ece-tools` inclut des dépendances pour tous les modules dans la variable [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Ces modules sont installés et mis à jour automatiquement lors de l’installation ou de la mise à jour. `ece-tools`.

- ![nouvelle icône](../../assets/new.svg) **Prise en charge des déploiements basés sur des scénarios**—<!--MAGECLOUD-4101-->

   - ![nouvelle icône](../../assets/new.svg) Vous pouvez désormais personnaliser les processus de création, de déploiement et de post-déploiement à l’aide de fichiers de configuration XML pour remplacer ou personnaliser la configuration par défaut.

   - ![nouvelle icône](../../assets/new.svg) **Modification de la variable `hooks` configuration dans`.magento.app.yaml`**: nous avons mis à jour la variable `hooks` format de configuration pour la prise en charge des déploiements basés sur des scénarios. Le format hérité de la version antérieure de CEE-Outils 2002.0.x est toujours pris en charge. Cependant, vous devez effectuer une mise à jour vers le nouveau format pour utiliser la fonctionnalité de déploiement basée sur un scénario. Voir [Déploiements basés sur des scénarios](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Avant de procéder à la mise à jour vers la version 2002.1.0 des outils de la CEE, passez en revue les [modifications incompatibles en amont](backward-incompatible-changes.md) pour en savoir plus sur les modifications qui peuvent nécessiter la mise à jour d’Adobe Commerce sur la configuration ou les processus d’un projet d’infrastructure cloud.

- ![nouvelle icône](../../assets/new.svg) **Mises à jour du service**—

   - ![nouvelle icône](../../assets/new.svg) Prise en charge de PHP 7.3.<!--MAGECLOUD-4022-->

   - ![nouvelle icône](../../assets/new.svg) Prise en charge supplémentaire de RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   - ![nouvelle icône](../../assets/new.svg) Ajout d’une validation permettant de vérifier les versions de service installées par rapport à la date de fin de vie de chaque service. Désormais, les clients reçoivent une notification s’ils disposent d’une version de service dans les trois mois suivant la date de fin de service, ainsi qu’un avertissement s’ils disposent d’une date de fin de service antérieure.<!--MAGECLOUD-4076-->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème de configuration de l’Elasticsearch pour s’assurer que les paramètres Elasticsearch corrects sont configurés dans tous les environnements.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Voir [Versions de service](../services/services-yaml.md#service-versions) pour obtenir la liste des services utilisés dans Adobe Commerce sur l’infrastructure cloud et leur compatibilité des versions avec le modèle Cloud.

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des variables d’environnement**—

   - ![nouvelle icône](../../assets/new.svg) Étendez les fonctionnalités de la fonction `WARM_UP_PAGES` pour prendre en charge le préchargement du cache pour des pages de produits spécifiques. Voir la définition développée dans la section [variables post-déploiement](../environment/variables-post-deploy.md#warm_up_pages) rubrique.<!--MAGECLOUD-4444-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la `ERROR_REPORT_DIR_NESTING_LEVEL` afin de simplifier la gestion des données des rapports d’erreur dans la variable `<magento_root>/var/report/` répertoire . Voir la description de la variable dans la section [variables de création](../environment/variables-build.md#error_report_dir_nesting_level) rubrique.

   - ![icône de correctif](../../assets/fix.svg) Suppression de la fonction `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`, et `STATIC_CONTENT_SYMLINK` des variables d’environnement. Voir [Modifications incompatibles en amont](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![icône de correctif](../../assets/fix.svg) Correction d’un problème dans le processus de configuration d’Elastic Suite, de sorte que la configuration par défaut soit écrasée comme prévu lors de la configuration de l’ `ELASTICSUITE_CONFIGURATION` deploy sans la variable `_merge` .<!--MAGECLOUD-4388-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des commandes de l’interface de ligne de commande**—

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle commande cron**: vous pouvez désormais gérer manuellement le traitement cron dans votre environnement Adobe Commerce sur l’infrastructure cloud à l’aide de la variable `cron:disable` et `cron:enable` des commandes. Utilisez la commande disable pour arrêter tous les processus cron actifs et désactiver toutes les tâches cron. Utilisez la commande enable pour réactiver les tâches cron lorsque vous êtes prêt. Voir [Désactivation des tâches cron](../application/crons-property.md#disable-cron-jobs).

   - ![nouvelle icône](../../assets/new.svg) **Amélioration des rapports d’erreur**: ajout d’une meilleure journalisation pour les échecs de commande de l’interface de ligne de commande qui se produisent pendant le traitement des outils ECE.<!--MAGECLOUD-4849-->

   - ![nouvelle icône](../../assets/new.svg) **Suppression des commandes de génération obsolètes**— Suppression des commandes de génération suivantes : `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`et renommé `ece-tools docker` Commandes à `ece-docker`. Voir [Modifications incompatibles en amont](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![nouvelle icône](../../assets/new.svg) Suppression de la valeur obsolète `build_options.ini` et ajout de la validation afin d’échouer à la création si le fichier existe. Utilisez la variable [.magento.env.yaml](../environment/configure-env-yaml.md) pour configurer les options de version.

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel le processus de création échouait lorsque la variable `config.php` est vide.<!--MAGECLOUD-4127-->

## 2002.0.23

Date de publication : 27 février 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de compatibilité avec `ece-tools` Versions de la version 2002.0.x qui empêchaient la génération de contenu statique à la demande de s’exécuter correctement en mode de production.

## Anciennes versions

Voir [archive des notes de mise à jour](cloud-release-archive.md) pour les versions 2002.0.22 et antérieures.
