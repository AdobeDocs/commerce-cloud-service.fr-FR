---
title: Package Cloud Docker
description: Consultez la liste des dernières améliorations apportées au module Cloud Docker.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: bc76cba0219f16fd055c20289811b51c35c9b026
workflow-type: tm+mt
source-wordcount: '3662'
ht-degree: 0%

---

# Package Cloud Docker

La variable [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) Le module fournit des fonctionnalités et des images Docker pour déployer Adobe Commerce dans un environnement cloud local. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui est un composant de [Suite d’outils cloud pour Commerce](cloud-tools-suite.md).

La variable `magento/magento-cloud-docker` Le package utilise la séquence de versions suivante : `<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->

## v1.3.7 {#latest}

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** — Ajout de la prise en charge des images PHP 8.3 et PHP 8.3.
- ![nouvelle icône](../../assets/new.svg) **Nginx** — Ajout de l’image nginx v. 1.24.
- ![nouvelle icône](../../assets/new.svg) **OpenSearch** - Ajout de l’image OpenSearch v. 2.12, 1.3.
- ![nouvelle icône](../../assets/new.svg) **Compositeur** - Mise à jour de la version du compositeur vers la version 2.2.23.

## v1.3.6

Date de publication : 31 juillet 2023

- ![nouvelle icône](../../assets/new.svg) **Ajout d’une nouvelle version de service**—OpenSearch 2.5.
- ![nouvelle icône](../../assets/new.svg) **Activation du cache du compositeur**: vous pouvez désormais étendre la configuration Docker pour activer l’effacement du cache du compositeur lors du démarrage du conteneur Docker. Voir [Étendre la configuration Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) dans le _Cloud Docker pour Commerce_ guide.

## v1.3.5

Date de publication : 10 mars 2023

- ![nouvelle icône](../../assets/new.svg) **ionCube**—Ajout de l’extension ionCube pour l’image PHP 8.1.
- ![nouvelle icône](../../assets/new.svg) **Ajout de nouvelles versions de service**—OpenSearch 2.3 et 2.4, PHP 8.2, Varnish 7.1.1.
- ![nouvelle icône](../../assets/new.svg) **Prise en charge améliorée de PHP 8.2**—Correction de problèmes de compatibilité avec certaines versions de PHP 8.2.x pour prendre en charge Commerce 2.4.6.
- ![icône de correctif](../../assets/fix.svg) **Problème de compositeur**: correction de problèmes survenant après la mise à jour de la version du compositeur dans les conteneurs Docker.

## v1.3.4

Date de publication : 27 octobre 2022

- ![nouvelle icône](../../assets/new.svg) **Ajout de nouvelles images en vernis**: ajout d’images pour Varnish 6.5, 7.0 et 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Date de publication : 13 septembre 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge d’Apple M1 (ARM64)**: ajout de modifications aux images Docker pour activer la prise en charge de l’architecture Apple M1 (ARM64).<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![icône de correctif](../../assets/fix.svg) **Mailhog**: correction d’un problème en raison duquel le service de messagerie n’interceptait pas les emails en mode développeur.<!-- MCLOUD-8643 -->
- ![icône de correctif](../../assets/fix.svg) **init-docker.sh**: correction du programme de validation des versions de service dans la variable `init-docker.sh` script.<!-- MCLOUD-8765 -->

## v1.3.2

Date de publication : 31 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Ajout d’une image Elasticsearch 7.10**<!-- MCLOUD-8548 -->

## v1.3.1

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de PHP 8.1**: ajout de la prise en charge de PHP 8.1.
- ![nouvelle icône](../../assets/new.svg) **OpenSearch**—Ajout d’images des versions 1.1 et 1.2 d’OpenSearch.
- ![nouvelle icône](../../assets/new.svg) **Compositeur 2.1**—Définissez le compositeur 2.1.x par défaut dans les images PHP 8.x.
- ![nouvelle icône](../../assets/new.svg) **Améliorations des images PHP**—

   - Ajout d’images PHP 8.1.
   - Mise à niveau de xDebug version 3.1.2
   - Mise à niveau de xmlrpc 1.0.0RC3

- ![icône de correctif](../../assets/fix.svg) **Améliorations apportées à Elasticsearch et OpenSearch**: améliorations apportées aux fichiers Dockerfile Elasticsearch et OpenSearch ; suppression de l’image Elasticsearch 5.2.
- ![icône de correctif](../../assets/fix.svg) **Extension Sodium**: activé le `sodium` par défaut dans toutes les images PHP.
- ![icône de correctif](../../assets/fix.svg) **Volume du cache du compositeur**: chemin d’accès fixe pour que le volume de cache du compositeur ait des modules compositeur en mémoire cache.
- ![icône de correctif](../../assets/fix.svg) **Limite de mémoire dans nginx**: correction d’une limitation de mémoire dans l’image NGINX.

## v1.3.0

Date de publication : 25 octobre 2021

- ![icône de correctif](../../assets/fix.svg) **Amélioration du processus du mode Développeur**—Auparavant, vous deviez spécifier le mode dans les étapes de création et de déploiement. Maintenant, le `--mode` dans le `build` détermine le mode dans la version ultérieure. `deploy` étape . La définition du mode après le déploiement n’est plus nécessaire. Voir [Mode Développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![icône de correctif](../../assets/fix.svg) **Améliorations du système de fichiers en lecture seule**—<!-- ACMP-1106 -->
   - Correction d’un problème qui entraînait le démarrage d’un conteneur PHP pour la configuration des emails.
   - Peut utiliser des variables d’environnement dans des fichiers INI.
   - Assurez-vous que les points d’entrée PHP n’ont pas besoin d’autorisation d’écriture.
- ![icône de correctif](../../assets/fix.svg) **Noeud de mise à jour**—Mettez à jour la version de noeud groupé ; lors de l’installation de Node dans les images PHP-CLI, il utilise désormais la version actuelle de LTS.<!-- ACMP-1539 -->
- ![icône de correctif](../../assets/fix.svg) **Mettre à jour Symfony**: mise à jour des dépendances de configuration Symfony pour qu’elles soient compatibles avec Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Date de publication : 29 juillet 2021

- ![nouvelle icône](../../assets/new.svg) **Nouveau `Zookeeper` container**: ajout d’un [Conteneur Zookeeper](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) pour gérer la configuration du fournisseur de verrouillage pour les projets qui ne sont pas déployés sur l’infrastructure Adobe Commerce on Cloud.<!--MCLOUD-8000-->

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge du compositeur 2.0.**—Ajout de la version 2.0 du compositeur au fichier de configuration du compositeur pour prendre en charge les mises à niveau du compositeur 1.0 qui approche la fin de vie.<!--MCLOUD-8003-->

## v1.2.3

Date de publication : 14 juin 2021

- ![nouvelle icône](../../assets/new.svg) **Ajout de PHP 8.0.**: mise à jour de PHP vers la version 8.0, ce qui vous permet de profiter de toutes les nouvelles fonctionnalités et optimisations incluses dans PHP 8.0.<!--MCLOUD-7941-->
- ![nouvelle icône](../../assets/new.svg) **Mise à jour vers Varnish 6.6 et Elasticsearch 7.11.2**: les liens suivants fournissent des informations sur la version [Cache Varnish 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) et Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![nouvelle icône](../../assets/new.svg) **Ajout `ioncube` extension pour une image PHP 7.4**—The `ioncube` l’extension a été ajoutée à l’image PHP 7.4 après avoir été initialement exclue de la mise à niveau de PHP 7.3 vers PHP 7.4. *[Envoyé par mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![nouvelle icône](../../assets/new.svg) **Ajout d’une option de synchronisation de fichier :`manual-native`**—The `manual-native` l’option de synchronisation des fichiers permet un contrôle manuel de la synchronisation, ce qui garantit de meilleures performances pour les environnements macOS et Windows. En savoir plus sur l’utilisation de la variable `manual-native` dans [Mode Développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) et [Synchronisation des données dans un environnement de développement Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![nouvelle icône](../../assets/new.svg) **Suppression des suppressions de volume de `up` et `down` Commandes**—The `--volume` a été supprimée de la fonction `bin/magento-docker up` et `bin/magento-docker down` , remplacée par la nouvelle commande `bin/magento-docker init` avec un avertissement de perte de données. Cette modification permet d’éviter la perte accidentelle de données. *[Envoyé par joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![icône de correctif](../../assets/fix.svg) **Mis à jour `CN` pour le certificat généré**: suppression du codage en dur `CN` à partir du fichier Dockerfile. Cette valeur a créé une erreur de certificat (`NET::ERR_CERT_INVALID`) qui a provoqué la variable `--host` pour l’ `ece-docker build:compose` à ignorer.<!--MCLOUD-7934-->

## v1.2.2

Date de publication : 20 avril 2021

- ![nouvelle icône](../../assets/new.svg) **Mis à jour `host.docker.internal` être indépendant des plateformes**: vous pouvez désormais créer les mêmes scripts Docker Composer pour Ubuntu, Windows et macOS. L’utilisation de Xdebug sur Ubuntu ne nécessite plus de variable d’environnement distincte. [Correctif proposé par Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![nouvelle icône](../../assets/new.svg) **Mise à jour de init-docker.sh**: ajout de la propriété `mounts` vers l’objet `MAGENTO_CLOUD_APPLICATION` Variable d’environnement. [Correctif proposé par Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![nouvelle icône](../../assets/new.svg) **Mise à jour de init-docker.sh**: mise à jour de la variable `init-docker.sh` script avec PHP 7.4 et les versions 1.2.1 de Cloud Docker. [Correctif proposé par Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![nouvelle icône](../../assets/new.svg) **Sodium activé par défaut**: activé le `sodium` extension PHP par défaut dans les images PHP Docker.<!--MCLOUD-7548-->
- ![nouvelle icône](../../assets/new.svg) **`custom-registry`option**: ajout d’un `--custom-registry` option à `php ./vendor/bin/ece-docker build:compose` pour utiliser votre propre registre des images.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![nouvelle icône](../../assets/new.svg) **Suppression des anciennes versions d’Elasticsearch**: suppression des versions 1.7 et 2.4 des Elasticsearch des images Elasticsearch.<!--MCLOUD-7504-->
- ![nouvelle icône](../../assets/new.svg) **Génération automatique de certificats NGINX**: suppression des certificats existants de l’image NGINX. Les certificats NGINX sont désormais générés automatiquement avec chaque nouveau déploiement pour une sécurité améliorée.<!--MCLOUD-7396-->
- ![icône de correctif](../../assets/fix.svg) **Activé`opcache.validate_timestamps`**: activé le `opcache.validate_timestamps` paramètre PHP par défaut en mode développeur. L’activation de ce paramètre corrige le problème en raison duquel les modifications apportées au système de fichiers n’étaient pas reconnues dans Docker.<!--MCLOUD-7466-->
- ![icône de correctif](../../assets/fix.svg) **Fixe`build:custom:compose`**: correction de la variable `build:custom:compose` pour générer une erreur lorsque les fichiers ne peuvent pas être remplacés pendant le processus de génération. Le lancement d’une erreur permet d’éviter les situations où `docker-compose up` peut utiliser les fichiers incorrects.<!--MCLOUD-7457-->
- ![icône de correctif](../../assets/fix.svg) **Fixe `--sync_engine="native"` option**: correction du problème en mode de production (`--mode="production"`), la variable `--sync_engine="native"` ne créerait aucune entrée pour les dossiers locaux dans `docker.composer.yml` fichier .<!--MCLOUD-7254-->
- ![icône de correctif](../../assets/fix.svg) **Correction des erreurs de validation de version de service.**—Ajout de versions de service pour [!DNL RabbitMQ], Elasticsearch et autres services liés à `type` dans la propriété `MAGENTO_CLOUD_RELATIONSHIP` Variable . Ajout de ces versions au `relationships` correction des erreurs de validation survenues pendant la phase de déploiement.<!--MCLOUD-7572-->

## v1.2.1

Date de publication : 21 décembre 2020

- ![nouvelle icône](../../assets/new.svg) **Options de commande NGINX**—Ajout des options de commande de génération pour modifier le nombre de NGINX `worker_processes` et NGINX `worker_connections` pour TLS et les services Web. La variable `worker_process` permet de définir la valeur sur `auto`. Exemples : <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![nouvelle icône](../../assets/new.svg) **Option de commande TLS**—Ajout de l’option de commande de création pour créer une configuration sans le service TLS. Exemple : <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![nouvelle icône](../../assets/new.svg) **consommation de mémoire NGINX**: réduction de la mémoire consommée par le processus NGINX pour TLS et les services Web.<!--MCLOUD-7259-->

- ![nouvelle icône](../../assets/new.svg) **Blackfire**: désactivation de l’extension PHP Blackfire par défaut dans l’image Cloud Docker.

- ![icône de correctif](../../assets/fix.svg) **Conteneur PHP-FPM**: correction de la vérification de l’intégrité du conteneur PHP-FPM en modifiant la variable `WEB_PORT` de `80` to `8080`.<!--MCLOUD-7232-->

- ![icône de correctif](../../assets/fix.svg) **Dénomination de volume non valide**: correction d’une erreur de nommage de volume non valide en mode développeur.<!--MCLOUD-7442-->

- ![icône de correctif](../../assets/fix.svg) **Port en amont NGINX**: mise à jour de l’image Docker NGINX 1.19 afin d’utiliser le port 8080 pour éviter une boucle infinie. [Correctif proposé par Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Date de publication : 9 novembre 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur—**

   - ![nouvelle icône](../../assets/new.svg) **Conteneur PHP-FPM**: ajout de la prise en charge de l’extension gnupg PHP. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![icône de correctif](../../assets/fix.svg) **Conteneur de base de données**: correction du contrôle de l’intégrité du conteneur de la base de données en ajoutant le mot de passe de la base de données requis à la commande de contrôle de l’intégrité.<!--MCLOUD-7122-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur Elasticsearch**

      - Ajout de la prise en charge d’Elasticsearch 7.9 pour la compatibilité avec les prochaines versions d’Adobe Commerce.<!--MCLOUD-7190-->

      - **Configuration du module externe Elasticsearch**: ajout de la prise en charge de l’utilisation des informations de configuration du module externe Elasticsearch à partir du `services.yaml` pour générer le fichier `docker-compose.yaml` pour un environnement Cloud Docker pour Commerce. Voir [Plug-ins Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Prise en charge des modules externes Elasticsearch**: ajout de la prise en charge des modules externes Elasticsearch suivants : `analysis-icu`, `analysis-phonetic`, `analysis-stempel`, et `analysis-nori`. La variable `analysis-icu` et `analysis-phonetic` les modules externes sont installés par défaut. Vous pouvez ajouter ou supprimer le `analysis-stempel` et `analysis-nori` modules externes selon les besoins.<!--MCLOUD-2789-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur CLI**

      - **Exécution de commandes dans des conteneurs PHP Docker**: vous pouvez désormais utiliser l’interface de ligne de commande de Cloud Docker pour exécuter des commandes dans des conteneurs PHP de votre environnement Docker sans avoir à installer PHP sur l’hôte. Par exemple, la commande suivante crée la configuration :  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Voir [Interface de ligne de commande de Cloud Docker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - Ajout du client OpenSSH-client aux conteneurs CLI PHP. Vous pouvez désormais utiliser le transfert ssh-agent pour le compositeur si la fonction `composer.json` Le fichier contient des référentiels git privés qui nécessitent un client ssh pour utiliser les commandes du compositeur.<!--MCLOUD-6008-->

   - ![icône de correctif](../../assets/fix.svg) **Conteneur TLS**—Maintenant, la variable [Conteneur TLS](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) est basé sur la variable `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Image Docker au lieu de l’image CentOS. Cette modification corrige les problèmes qui provoquaient des erreurs lors de l’envoi de requêtes HTTPS entre des conteneurs dans l’environnement Cloud Docker.<!--MCLOUD-6469-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur de tests**: ajout d’un conteneur de test pour le test de l’application, puis ajout de la variable `--with-test` au Docker `build:compose` pour créer le conteneur uniquement lors du test dans l’environnement Docker. Voir [test d’application](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur FPM-XDEBUG**

      - ![nouvelle icône](../../assets/new.svg) **Configuration de Xdebug sous Linux**: ajout de la propriété `--set-docker-host` à l’option `ece-docker build:compose` pour configurer la fonction `host.docker.internal` dans le conteneur Xdebug. Cette option est requise pour utiliser Xdebug sur les systèmes Linux. Voir [Configuration de Xdebug pour Docker](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![icône de correctif](../../assets/fix.svg) Correction de la configuration de la variable Xdebug pour que Docker ENTRYPOINT soit résolu. `uninitialized "with_xdebug" variable` erreurs dans les journaux. [Correctif proposé par Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**

   - **Configuration de MailHog**—Vous pouvez désormais utiliser les éléments suivants : `ece-docker build:compose` options de commande pour désactiver MailHog et spécifier des ports : `--no-mailhog`, `--mailhog-http-port`, et `--mailhog-smtp-port`. Voir [Configuration du courrier électronique](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Pour Cloud Docker pour Commerce version 1.2.0 et ultérieure, Adobe fournit désormais des images Docker pour chaque version de correctif, et le générateur de configuration Docker crée la configuration Docker avec une version de correctif spécifiée au lieu d’utiliser la dernière version. Auparavant, le générateur de configuration Docker créait la configuration à l’aide de la dernière version de correctif qui pouvait interrompre les environnements Cloud Docker pour Commerce créés à l’aide d’une version antérieure.<!--MCLOUD-7093-->

   - **Spécification d’images et de versions personnalisées dans une configuration Cloud Docker personnalisée**: mise à jour de la variable `build:custom:compose` avec des options pour spécifier des images et des versions personnalisées lors de la génération d’un fichier de configuration de composition Docker personnalisé (`docker-compose.yaml`). Voir [Création d’une configuration Composer Docker personnalisée](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Mise à jour de la configuration de l’hôte Docker afin d’exposer le port 443 pour activer l’accès à Adobe Commerce (`https://magento2.docker`) de tous les conteneurs de l’interface en ligne de commande. Vous pouvez modifier le port par défaut en ajoutant la variable `--tls-port` lorsque vous générez le fichier de configuration Docker.<!--MCLOUD-6806-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel la version de Cloud Docker pour Commerce échouait si la variable `app/etc/env.php` existe.<!--MCLOUD-6732-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de la configuration de création pour remplacer les volumes nommés par des volumes réguliers afin d’éviter des problèmes lors du déploiement de Cloud Docker pour Commerce sous Linux ou sous-système Windows pour Linux (WSL2).<!--MCLOUD-6732-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de Cloud Docker pour les tests fonctionnels Commerce afin de prendre en charge le compositeur 2.0.<!--MCLOUD-7183-->

## v1.1.2

Date de publication : 9 septembre 2020

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge d’Elasticsearch 7.7<!--MCLOUD-6219-->

## v1.1.1

Date de publication : 5 août 2020

- ![icône de correctif](../../assets/fix.svg) **Mise à jour de la configuration des emails**: mise à jour de la configuration par défaut de Cloud Docker pour Commerce afin de prendre en charge le service MailHog au lieu d’utiliser SendMail. Voir [Configuration du courrier électronique](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![icône de correctif](../../assets/fix.svg) Restauration de la bibliothèque PS dans la configuration de l’environnement Cloud Docker pour corriger la situation. `ps:  command not found` erreurs.<!--MCLOUD-6621-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de la configuration par défaut de Cloud Docker pour Commerce afin de supprimer le montage automatique du point d’entrée de la base de données et des volumes MariaDB pour corriger le problème. `Cannot create container for service db` erreurs qui peuvent se produire lors du démarrage de votre environnement Cloud Docker.

  Vous pouvez maintenant configurer l’environnement Cloud Docker pour monter les répertoires de la base de données en ajoutant les options suivantes au `ece-docker build:compose` command : `--with-entry-point` et `with-mariadb-conf`. Voir [Options de configuration du service](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour des commandes de l’interface de ligne de commande**

| Action | Commande |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Ajouter un point d’entrée au conteneur de la base de données pour restaurer la base de données à partir de la sauvegarde | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Ajouter un volume de configuration MariaDB | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de la solution de performances de la base de données partagée**: vous pouvez maintenant configurer et déployer un magasin à l’aide de la solution de performances de la base de données de partage dans l’environnement Cloud Docker.<!--MCLOUD-3740-->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge du déploiement d’Adobe Commerce et de Magento Open Source**: vous pouvez désormais utiliser Cloud Docker pour Commerce pour déployer un environnement de développement local pour les projets qui ne sont pas hébergés sur Adobe Commerce sur l’infrastructure cloud.<!--MCLOUD-5667-->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de Blackfire.io**: ajout de la prise en charge de l’utilisation de la variable [Extension Blackfire.io](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) pour les tests de performances automatisés. [Correctif proposé par Adarsh Manickam de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur**

   - **Varnish**: désormais, le vernis est le cache par défaut lorsque vous déployez Adobe Commerce dans un environnement Cloud Docker à l’aide d’une version prise en charge du modèle d’application Cloud. Voir [Conteneur en vernis](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Ajout de la `--no-varnish` pour ignorer l’installation du service Varnish lorsque vous générez le fichier de configuration de Cloud Docker.<!--MCLOUD-2634-->

   - ![nouvelle icône](../../assets/new.svg) **Base**

      - Ajout de la prise en charge de la base de données MySQL. Vous pouvez maintenant configurer l’environnement Cloud Docker avec MariaDB ou MySQL. Voir [Options de configuration du service](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Ajout de la possibilité de définir les paramètres d’incrément et de décalage pour la réplication de la base de données lors de la génération du fichier de composition Docker. Voir [Conteneurs de services](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![nouvelle icône](../../assets/new.svg) **PHP-FPM**

      - Prise en charge de PHP 7.4. [Correctif proposé par Mohanela Murugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Ajout de la possibilité de copier une `php.ini` dans le répertoire du projet racine de l’environnement Cloud Docker et appliquez des paramètres PHP personnalisés aux conteneurs PHP-FPM et CLI. Voir [Personnalisation des paramètres PHP](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Ajout d’un contrôle d’intégrité du conteneur. [Correctif soumis par Visanth Sampath de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![icône de correctif](../../assets/fix.svg) **Node.js**: mise à jour de la version par défaut de Node.js de la version 8 à la version 10 afin d’améliorer la sécurité. Node.js version 8 est obsolète et n’est plus mis à jour avec des correctifs de bogues ou de sécurité. [Correctif proposé par Mohan Elamurugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![nouvelle icône](../../assets/new.svg) **Elasticsearch**

      - Ajout de la prise en charge d’Elasticsearch 6.8, 7.2, 7.5 et 7.6.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Ajout de la possibilité de personnaliser la variable [Configuration du conteneur Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) lorsque vous générez le fichier de configuration de composition Docker.<!--MCLOUD-3059-->

      - Ajout de la `--no-es` aux options de configuration du service pour générer le fichier de configuration Docker Composer . Utilisez cette option pour ignorer l’installation du conteneur Elasticsearch et utilisez plutôt la recherche MySQL . Cette option est prise en charge uniquement pour Adobe Commerce versions 2.3.5 et antérieures.<!--MCLOUD-3766-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur FPM-XDEBUG**: ajout d’une option de configuration de service pour installer et configurer Xdebug pour le débogage de PHP dans votre environnement Cloud Docker. Voir [Configuration de Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**

   - Ajout de contrôles de l’intégrité pour les conteneurs de service PHP-FPM, Redis, Elasticsearch et MySQL Docker.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Le mode de synchronisation des fichiers par défaut a été remplacé par `native` en mode Développeur.<!--MCLOUD-3890 -->

   - Ajout d’informations de version à l’image de conteneur de service Docker générique lors de la génération de la variable `docker-compose.yml` fichier .<!--MCLOUD-3878-->

   - Amélioration de la capacité à gérer les réponses volumineuses à partir du conteneur PHP-FPM en amont en augmentant la variable `fastcgi_buffers` pour le serveur Nginx.<!--MCLOUD-5980-->

   - Amélioration des performances de synchronisation des fichiers de multi-agène en ajoutant une seconde session de synchronisation pour synchroniser les fichiers dans `vendor` répertoire . Cette modification empêche le mutagène de se bloquer pendant le processus de synchronisation des fichiers. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![nouvelle icône](../../assets/new.svg) **Mises à jour des commandes de l’interface de ligne de commande**

| Action | Commande |
| -------- | --------------- |
| Effacer le cache des Redis | `bin/magento-docker flush-redis` |
| Effacer le cache de marque | `bin/magento-docker flush-varnish` |
| Ignorer l’installation de marque par défaut | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Personnalisation des options des Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [Suppression de la configuration Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| Configuration du conteneur DB avec MySQL version 5.6 ou 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Définition d’une URL de base personnalisée | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Ajout d’un conteneur pour la configuration Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![icône de correctif](../../assets/fix.svg) Correction de la configuration de la synchronisation des fichiers de mutagène pour empêcher mutagène de créer des sessions obsolètes. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de configuration qui provoquait des erreurs de syntaxe dans le journal de composition Docker lors du démarrage du conteneur PHP-FPM. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![icône de correctif](../../assets/fix.svg) Correction des erreurs de conflit de volume qui se produisaient parfois lors de l’utilisation de plusieurs environnements Docker. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/168).

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel la variable `ece-docker build:compose` échoue si la configuration incluait Blackfire.io. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de la configuration d’image de ligne de commande PHP afin d’éviter les erreurs de mémoire insuffisante qui se produisaient lors de l’installation de plusieurs modules à l’aide de Cloud Docker for Commerce. [Correctif proposé par Mohan Elamurugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![icône de correctif](../../assets/fix.svg) Ajout de la prise en charge de plusieurs utilisateurs MySQL dans l’environnement Cloud Docker. Dans les versions antérieures, la variable `build:compose` l’opération a échoué si la variable `magento.app.yaml` spécifie plusieurs utilisateurs de la base de données. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![icône de correctif](../../assets/fix.svg) Supprimé `rsyslog` des conteneurs PHP de Cloud Docker pour Commerce afin de résoudre les problèmes de compatibilité qui généraient des notifications d’avertissement lors du déploiement. Cloud Docker n’utilise pas l’utilitaire rsyslog.<!--MCLOUD-6173-->

## v1.0.0

Date de publication : 5 février 2020

- ![nouvelle icône](../../assets/new.svg) **Création d’un package distinct à diffuser`Cloud Docker for Commerce`**: Déplacement du code source pour diffuser Cloud Docker for Commerce à partir du `ece-tools` du référentiel [new `magento-cloud-docker` référentiel](https://github.com/magento/magento-cloud-docker) pour maintenir la qualité du code et fournir des versions indépendantes. Le nouveau module est une dépendance pour les outils CEE v2002.1.0 et versions ultérieures.

  Lorsque vous mettez à jour des outils de texte, vous mettez également à jour la variable `magento/magento-cloud-docker` vers la version 1.0.0. Si vous avez utilisé Cloud Docker pour Commerce avec une version antérieure `ece-tools` (2002.0.x), passez en revue la [incompatibilités rétroactives](backward-incompatible-changes.md) et mettez à jour votre projet en tant que scripts, commandes et processus selon les besoins.

- ![nouvelle icône](../../assets/new.svg) **Ajout du contrôle de version aux images Docker**: vous devez maintenant mettre à jour la variable `magento/magento-cloud-docker` pour obtenir les images mises à jour.<!--MAGECLOUD-4737-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur**—

   - ![nouvelle icône](../../assets/new.svg) **Conteneur PHP-FPM**—

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de Node.js**: mise à jour de l’image PHP-FPM pour prendre en charge les fonctionnalités node, npm et grunt-cli dans le conteneur PHP.<!--MAGECLOUD-3953-->

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de [ionCube](https://www.ioncube.com/)**: mise à jour de la configuration Docker par défaut pour prendre en charge ionCube dans l’environnement de développement Docker local.<!--MAGECLOUD-4354-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur web**—

      - ![nouvelle icône](../../assets/new.svg) **Personnalisation de la configuration NGINX**: ajout de la fonctionnalité de montage d’une `nginx.conf` dans l’environnement Cloud Docker pour Commerce. Voir [Conteneur web](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![nouvelle icône](../../assets/new.svg) **Certificats NGINX générés automatiquement**: le fichier de configuration Docker inclut désormais la configuration permettant de générer automatiquement des certificats NGINX pour le conteneur Web.<!--MAGECLOUD-4258-->

   - ![nouvelle icône](../../assets/new.svg) **Nouveau conteneur Selenium**: ajout d’un [Conteneur Selenium](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) pour prendre en charge les tests d’application Adobe Commerce à l’aide de la structure de test fonctionnel du Magento (MFTF).<!--MAGECLOUD-4040-->

   - ![nouvelle icône](../../assets/new.svg) **[!DNL RabbitMQ]prise en charge des versions**: mise à jour de la variable [!DNL RabbitMQ] configuration de conteneur pour la prise en charge [!DNL RabbitMQ] version 3.8.<!--MAGECLOUD-4674-->

   - ![icône de correctif](../../assets/fix.svg) **Conteneur de base de données persistant**—The `magento-db: /var/lib/mysql` le volume de la base de données persiste maintenant après l’arrêt et la suppression de la configuration Docker, et il est restauré lorsque vous redémarrez la configuration Docker. Vous devez maintenant supprimer manuellement le volume de la base de données. Voir [Conteneurs de base].<!--MAGECLOUD-3978-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur TLS**—

      - ![nouvelle icône](../../assets/new.svg) **Mise à jour de l’image de base du conteneur pour utiliser l’image officielle**—The [Conteneur TLS cloud](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) L&#39;image est maintenant basée sur la version officielle `debian:jessie` Image Docker.—<!--MAGECLOUD-4163-->

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de la fonction [Proxy D’Arrêt TLS En Livre]**—The [Fichier de configuration Pound](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) ajoute les variables ENV suivantes pour personnaliser la configuration Docker pour le conteneur TLS :

         - **`TimeOut`**—Définit la valeur de délai d’expiration Time to First Byte (TTF). La valeur par défaut est de 300 secondes.

         - **`RewriteLocation`**: détermine si le proxy Pound réécrit l’emplacement par défaut vers l’URL de demande. La valeur par défaut est `0` pour empêcher la réécriture de rompre les redirections vers des sites web externes tels qu’un site d’authentification unique externe. [Correctif soumis par Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![nouvelle icône](../../assets/new.svg) Augmentation de la valeur du délai d’expiration dans la configuration du conteneur TLS de 15 à 300 secondes. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur en vernis**—

      - ![nouvelle icône](../../assets/new.svg) **Mise à jour de l’image de base du conteneur pour utiliser l’image officielle**—The [Conteneur de vernis de cloud](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) est désormais basé sur le `centos` Image Docker.<!--MAGECLOUD-4163-->

      - ![nouvelle icône](../../assets/new.svg) **Amélioration de la configuration du délai d’expiration par défaut**-Added `.first_byte_timeout` et `.between_bytes_timeout` configuration du conteneur de vernis. Les deux valeurs de délai d’expiration sont par défaut définies sur `300s` (5 minutes). [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![icône de correctif](../../assets/fix.svg) **Ignorer la marque pendant les sessions Xdebug**: mise à jour de la configuration du conteneur de vernis pour renvoyer la valeur `pass` sur les requêtes reçues lorsque Xdebug est activé. Dans les versions précédentes, vous ne pouviez pas utiliser Xdebug si l’environnement Docker incluait le vernis. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**—

   - ![nouvelle icône](../../assets/new.svg) **Gestion des montages et des volumes pour votre projet**: ajout de la capacité de gérer les montages et les volumes lors du lancement d’un environnement Docker pour le développement local. Voir [Partage des données du projet].<!--MAGECLOUD-3248-->

   - ![nouvelle icône](../../assets/new.svg) **Prise en charge du mode pont réseau**: ajout de la prise en charge du mode de pont réseau pour activer les connexions entre les conteneurs Docker sur le réseau local.<!--MAGECLOUD-4165-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur cron désactivé par défaut**: pour améliorer les performances, le conteneur Cron n’est plus configuré par défaut lors de la création de l’environnement Docker. Vous pouvez utiliser la variable `--with-cron` sur la commande Docker build pour ajouter un conteneur Cron à votre environnement. Voir [Gestion des tâches cron](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![nouvelle icône](../../assets/new.svg) **Arrêt de la synchronisation des fichiers de sauvegarde volumineux**—Ajout de fichiers d’archive et de vidages DB (ZIP, SQL, GZ et BZ2) à la liste d’exclusion dans la variable `dist/docker-sync.yml` et `dist/mutagen.sh` fichiers . La synchronisation de fichiers volumineux (> 1 Go) peut entraîner une période d’inactivité et les fichiers de sauvegarde ne nécessitent normalement pas de synchronisation, car vous pouvez les régénérer.<!--MAGECLOUD-3979-->

- ![nouvelle icône](../../assets/new.svg) **Modifications des commandes**—

   - ![icône de correctif](../../assets/fix.svg) Renommé `./bin/docker` vers `./bin/magento-docker` pour résoudre un problème en raison duquel certains environnements Docker étaient rompus, car la variable `./bin/docker` remplace les fichiers binaires Docker existants. Ceci est une [modification incompatible rétroactive](backward-incompatible-changes.md) qui nécessite des mises à jour de vos scripts et commandes.<!-- MAGECLOUD-4038 -->

   - ![nouvelle icône](../../assets/new.svg) **Ajout d’une option de configuration de service pour exposer le port de la base de données à l’hôte.**: utilisez la variable `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` pour exposer le port de la base de données à l’hôte lors de la création de la variable `docker-compose.yml` fichier : `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle commande de post-déploiement**: auparavant, les hooks de post-déploiement définis dans la variable `.magento.app.yaml` s’exécutait automatiquement après le déploiement d’Adobe Commerce sur un conteneur Cloud Docker à l’aide de la variable `cloud-deploy` . Maintenant, vous devez émettre une `cloud-post-deploy` pour exécuter les hooks post-deploy après le déploiement. Consultez les instructions de lancement mises à jour pour [développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) et [production](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) mode .<!--MAGECLOUD-3996-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de la `--rm` option à `./bin/magento-docker` pour les conteneurs de création et de déploiement. Cette opération supprime le conteneur une fois la tâche terminée.<!--MAGECLOUD-4205-->

   - ![nouvelle icône](../../assets/new.svg) **Mises à jour de `build:compose` command**—

      - ![nouvelle icône](../../assets/new.svg) Ajout de la `--sync-engine="native"` à l’option `docker-build` pour désactiver la synchronisation des fichiers lorsque vous générez le fichier de configuration Docker Composer en mode développeur. Utilisez cette option lors du développement sur des systèmes Linux, qui ne nécessitent pas de synchronisation de fichiers pour le développement Docker local. Voir [Synchronisation des données dans l’environnement Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![nouvelle icône](../../assets/new.svg) Modification du paramètre de synchronisation des fichiers par défaut de `docker-sync` to `native`. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![nouvelle icône](../../assets/new.svg) **Amélioration de la validation**—

   - ![nouvelle icône](../../assets/new.svg) Ajout d’une validation au processus de déploiement pour les environnements de développement Docker locaux afin de vérifier que la configuration de l’environnement Cloud inclut la clé de chiffrement requise pour déchiffrer la base de données. Désormais, un message d’erreur s’affiche dans le journal si la configuration de l’environnement ne spécifie aucune valeur pour la clé de chiffrement.<!--MAGECLOUD-4423-->

   - ![nouvelle icône](../../assets/new.svg) Ajout d’un contrôle d’intégrité du conteneur au service Elasticsearch afin de s’assurer que le service est prêt avant de poursuivre le traitement de création et de déploiement. Si le contrôle de l’intégrité renvoie une erreur, le conteneur redémarre automatiquement.<!--MAGECLOUD-4456-->
