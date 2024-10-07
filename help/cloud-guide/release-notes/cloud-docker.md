---
title: Package Cloud Docker
description: Consultez la liste des dernières améliorations apportées au module Cloud Docker.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-10-07T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: fdb596430fbc532bed4a6b251872f44c5321d375
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 0%

---

# Package Cloud Docker

Le package [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) fournit des fonctionnalités et des images Docker pour déployer Adobe Commerce dans un environnement cloud local. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui est un composant de la [suite d’outils cloud pour Commerce](cloud-tools-suite.md).

Le package `magento/magento-cloud-docker` utilise la séquence de version suivante : `<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![Icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->

## v1.4.0 {#latest}

Date de publication : 7 octobre 2024

- ![Icône de correctif](../../assets/fix.svg) **Code restructuré** : suppression de la prise en charge des anciennes versions PHP (7.4, 7.3, 7.2) et des bibliothèques et images associées.

## v1.3.7

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** — Prise en charge des images PHP 8.3 et PHP 8.3.
- ![nouvelle icône](../../assets/new.svg) **Nginx** — Ajout d’une image nginx v. 1.24.
- ![nouvelle icône](../../assets/new.svg) **OpenSearch** - Image ajoutée OpenSearch v. 2.12, 1.3.
- ![nouvelle icône](../../assets/new.svg) **Compositeur** - Mise à jour de la version du compositeur vers la version 2.2.23.

## v1.3.6

Date de publication : 31 juillet 2023

- ![nouvelle icône](../../assets/new.svg) **Ajout d’une nouvelle version de service**—OpenSearch 2.5.
- ![nouvelle icône](../../assets/new.svg) **Activer le cache du compositeur**—Vous pouvez désormais étendre la configuration du Docker pour activer le compositeur d’effacement du cache lors du démarrage du conteneur Docker. Voir [Étendre la configuration Docker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) dans le guide _Cloud Docker for Commerce_.

## v1.3.5

Date de publication : 10 mars 2023

- ![new icon](../../assets/new.svg) **ionCube** : ajout de l’extension ionCube pour l’image PHP 8.1.
- ![nouvelle icône](../../assets/new.svg) **Ajout de nouvelles versions de service**—OpenSearch 2.3 et 2.4, PHP 8.2, Varnish 7.1.1.
- ![nouvelle icône](../../assets/new.svg) **Prise en charge améliorée de PHP 8.2** : correction de problèmes de compatibilité avec certaines versions de PHP 8.2.x pour prendre en charge Commerce 2.4.6.
- ![ icône de correctif ](../../assets/fix.svg) **Problème du compositeur** : correction de problèmes survenant après la mise à jour de la version du compositeur dans les conteneurs Docker.

## v1.3.4

Date de publication : 27 octobre 2022

- ![nouvelle icône](../../assets/new.svg) **Ajout d’images vernissées**—Ajout d’images pour Varnish 6.5, 7.0 et 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Date de publication : 13 septembre 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge d’Apple M1 (ARM64)**—Ajout de modifications aux images Docker pour activer la prise en charge de l’architecture Apple M1 (ARM64).<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![Icône de correctif](../../assets/fix.svg) **Mailhog** : correction d’un problème en raison duquel le service de messagerie n’interceptait pas les emails en mode développeur.<!-- MCLOUD-8643 -->
- ![icône de correctif](../../assets/fix.svg) **init-docker.sh**—Correction du programme de validation des versions de service dans le script `init-docker.sh`.<!-- MCLOUD-8765 -->

## v1.3.2

Date de publication : 31 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Image Elasticsearch 7.10 ajoutée**<!-- MCLOUD-8548 -->

## v1.3.1

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de PHP 8.1** : prise en charge de PHP 8.1.
- ![nouvelle icône](../../assets/new.svg) **OpenSearch**—Ajout d’images des versions 1.1 et 1.2 d’OpenSearch.
- ![nouvelle icône](../../assets/new.svg) **Compositeur 2.1**—Définir le compositeur 2.1.x par défaut dans les images PHP 8.x.
- ![nouvelle icône](../../assets/new.svg) **améliorations des images PHP**—

   - Ajout d’images PHP 8.1.
   - Mise à niveau de xDebug version 3.1.2
   - Mise à niveau de xmlrpc 1.0.0RC3

- ![ icône de correctif ](../../assets/fix.svg) **Améliorations Elasticsearch &amp; OpenSearch**—Améliorations apportées aux fichiers Dockerfiles Elasticsearch et OpenSearch ; suppression de l’image Elasticsearch 5.2.
- ![icône de correctif](../../assets/fix.svg) **Extension Sodium**—Activation de l’extension `sodium` par défaut dans toutes les images PHP.
- ![icône de correction](../../assets/fix.svg) **{volume du cache du compositeur** : chemin d’accès fixe pour que le volume du cache du compositeur ait des modules du compositeur en mémoire cache.
- ![icône de correctif](../../assets/fix.svg) **Limite de mémoire dans nginx** : correction d’une limitation de mémoire dans l’image NGINX.

## v1.3.0

Date de publication : 25 octobre 2021

- ![ icône de correctif ](../../assets/fix.svg) **** : auparavant, vous deviez spécifier le mode dans les étapes de création et de déploiement. Désormais, l’option `--mode` de l’étape `build` détermine le mode à l’étape `deploy` ultérieure. La définition du mode après le déploiement n’est plus nécessaire. Voir [Mode développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![icône de correctif](../../assets/fix.svg) **Améliorations du système de fichiers en lecture seule**—<!-- ACMP-1106 -->
   - Correction d’un problème qui entraînait le démarrage d’un conteneur PHP pour la configuration des emails.
   - Peut utiliser des variables d’environnement dans des fichiers INI.
   - Assurez-vous que les points d’entrée PHP n’ont pas besoin d’autorisation d’écriture.
- ![icône de correctif](../../assets/fix.svg) **Mettre à jour le noeud**—Mettre à jour la version du noeud groupé ; lors de l’installation du noeud dans des images de ligne de commande PHP, il utilise désormais la version actuelle de LTS.<!-- ACMP-1539 -->
- ![icône de correctif](../../assets/fix.svg) **Mettre à jour Symfony**—Mise à jour des dépendances de configuration Symfony pour qu’elles soient compatibles avec Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Date de publication : 29 juillet 2021

- ![nouvelle icône](../../assets/new.svg) **Nouveau `Zookeeper` conteneur** : ajout d’un [conteneur Zookeeper](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) pour gérer la configuration du fournisseur de verrouillages pour les projets qui ne sont pas déployés sur l’infrastructure Adobe Commerce on Cloud.<!--MCLOUD-8000-->

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge du compositeur 2.0.** : ajout de la version 2.0 du compositeur au fichier de configuration du compositeur pour la prise en charge des mises à niveau du compositeur 1.0 qui approche la fin de vie.<!--MCLOUD-8003-->

## v1.2.3

Date de publication : 14 juin 2021

- ![nouvelle icône](../../assets/new.svg) **Ajout de PHP 8.0**—Mise à jour de PHP vers la version 8.0, ce qui vous permet de tirer parti de toutes les nouvelles fonctionnalités et optimisations de PHP 8.0.<!--MCLOUD-7941-->
- ![nouvelle icône](../../assets/new.svg) **Mise à jour vers Varnish 6.6 et Elasticsearch 7.11.2** - Les liens suivants fournissent des informations de mise à jour sur [Varnish Cache 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) et Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![new icon](../../assets/new.svg) **Ajout de l’extension `ioncube` pour PHP 7.4 image** : l’extension `ioncube` a été ajoutée à l’image PHP 7.4 après avoir été initialement exclue de la mise à niveau de PHP 7.3 vers PHP 7.4. *[Envoyé par mattskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![nouvelle icône](../../assets/new.svg) **Ajout d’une option de synchronisation de fichier :`manual-native`** - L’option de synchronisation de fichiers `manual-native` offre un contrôle manuel sur la synchronisation, ce qui offre les meilleures performances pour les environnements macOS et Windows. Découvrez comment utiliser l’option `manual-native` en [mode Développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) et [Synchronisation des données dans un environnement de développement Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![nouvelle icône](../../assets/new.svg) **Suppression de volumes de `up` et de `down` commandes** : l’option `--volume` a été supprimée des commandes `bin/magento-docker up` et `bin/magento-docker down`, remplacée par la nouvelle commande `bin/magento-docker init` avec un avertissement de perte de données. Cette modification permet d’éviter la perte accidentelle de données. *[Envoyé par joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![ icône de correction ](../../assets/fix.svg) **Valeur `CN` mise à jour pour le certificat généré** : suppression de la valeur `CN` codée en dur du fichier Dockerfile. Cette valeur a créé une erreur de certificat (`NET::ERR_CERT_INVALID`) qui entraînait l&#39;exclusion de l&#39;option `--host` de la commande `ece-docker build:compose`.<!--MCLOUD-7934-->

## v1.2.2

Date de publication : 20 avril 2021

- ![nouvelle icône](../../assets/new.svg) **`host.docker.internal` mis à jour pour être indépendant de la plateforme** : vous pouvez désormais créer les mêmes scripts Docker Composer pour Ubuntu, Windows et macOS. L’utilisation de Xdebug sur Ubuntu ne nécessite plus de variable d’environnement distincte. [Correctif soumis par Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![new icon](../../assets/new.svg) **Mise à jour de init-docker.sh** : ajout de l’objet `mounts` à la variable d’environnement `MAGENTO_CLOUD_APPLICATION`. [Correctif soumis par Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![nouvelle icône](../../assets/new.svg) **Mise à jour de init-docker.sh** : mise à jour du script `init-docker.sh` avec les versions PHP 7.4 et Cloud Docker 1.2.1. [Correctif soumis par Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![new icon](../../assets/new.svg) **Sodium activé par défaut**—Activation de l’extension `sodium` PHP par défaut dans les images PHP Docker.<!--MCLOUD-7548-->
- ![nouvelle icône](../../assets/new.svg) **`custom-registry`option**—Ajout d’une option `--custom-registry` à la commande `php ./vendor/bin/ece-docker build:compose` pour l’utilisation de votre propre registre d’images.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![nouvelle icône](../../assets/new.svg) **Suppression des anciennes versions Elasticsearch**—Suppression des versions Elasticsearch 1.7 et 2.4 des images Elasticsearch.<!--MCLOUD-7504-->
- ![nouvelle icône](../../assets/new.svg) **Génération automatique de certificats NGINX** : suppression des certificats existants de l’image NGINX. Les certificats NGINX sont maintenant générés automatiquement avec chaque nouveau déploiement pour une sécurité améliorée.<!--MCLOUD-7396-->
- ![icône de correctif](../../assets/fix.svg) **`opcache.validate_timestamps`**—Activé le paramètre `opcache.validate_timestamps` PHP par défaut en mode développeur. L’activation de ce paramètre corrige le problème en raison duquel les modifications apportées au système de fichiers n’étaient pas reconnues dans Docker.<!--MCLOUD-7466-->
- ![icône de correctif](../../assets/fix.svg) **Correction de`build:custom:compose`** : correction de la commande `build:custom:compose` pour générer une erreur lorsque les fichiers ne peuvent pas être remplacés pendant le processus de création. Le lancement d’une erreur empêche les situations où `docker-compose up` pourrait utiliser les mauvais fichiers.<!--MCLOUD-7457-->
- ![Icône de correctif](../../assets/fix.svg) **Correction de l’option `--sync_engine="native"`**—Correction du problème en raison duquel, en mode de production (`--mode="production"`), l’option `--sync_engine="native"` ne créait aucune entrée pour les dossiers locaux dans le fichier `docker.composer.yml`.<!--MCLOUD-7254-->
- ![ icône de correction ](../../assets/fix.svg) **Correction des erreurs de validation de version de service** : ajout de versions de service pour [!DNL RabbitMQ], Elasticsearch et autres services à la propriété `type` de la variable `MAGENTO_CLOUD_RELATIONSHIP`. L&#39;ajout de ces versions à la variable `relationships` a corrigé les erreurs de validation qui se sont produites pendant la phase de déploiement.<!--MCLOUD-7572-->

## v1.2.1

Date de publication : 21 décembre 2020

- ![nouvelle icône](../../assets/new.svg) **options de commande NGINX**—Ajout d’options de commande de build pour modifier le nombre de NGINX `worker_processes` et NGINX `worker_connections` pour TLS et les services Web. Le paramètre `worker_process` conserve la possibilité de définir la valeur sur `auto`. Exemples : <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![nouvelle icône](../../assets/new.svg) **Option de commande TLS**—Ajout de l’option de commande de build pour créer une configuration sans le service TLS. Exemple : <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![nouvelle icône](../../assets/new.svg) **consommation de mémoire NGINX**—Réduction de la mémoire consommée par le processus NGINX pour TLS et services Web.<!--MCLOUD-7259-->

- ![nouvelle icône](../../assets/new.svg) **Blackfire** : désactivation de l’extension PHP du Blackfire par défaut dans l’image Cloud Docker.

- ![Icône de correctif](../../assets/fix.svg) **Conteneur PHP-FPM**—Correction de la vérification de l’intégrité du conteneur PHP-FPM en passant de `80` à `8080`.<!--MCLOUD-7232-->`WEB_PORT`

- ![Icône de correctif](../../assets/fix.svg) **Nommage de volume non valide**—Correction d&#39;une erreur avec nommage de volume non valide en mode développeur.<!--MCLOUD-7442-->

- ![icône de correctif](../../assets/fix.svg) **port en amont NGINX**—Mise à jour de l’image Docker NGINX 1.19 pour utiliser le port 8080 afin d’éviter une boucle infinie. [Correctif soumis par Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Date de publication : 9 novembre 2020

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur—**

   - ![nouvelle icône](../../assets/new.svg) **Conteneur PHP-FPM**—Ajout de la prise en charge de l’extension gnupg PHP. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![icône de correction](../../assets/fix.svg) **Conteneur de base de données** : correction de la vérification de l’intégrité du conteneur de base de données en ajoutant le mot de passe de base de données requis à la commande de contrôle de l’intégrité.<!--MCLOUD-7122-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur Elasticsearch**

      - Ajout de la prise en charge d’Elasticsearch 7.9 pour la compatibilité avec les prochaines versions d’Adobe Commerce.<!--MCLOUD-7190-->

      - **Configuration du module externe Elasticsearch** : ajout de la prise en charge de l’utilisation des informations de configuration du module externe Elasticsearch du fichier `services.yaml` pour générer le fichier `docker-compose.yaml` pour un environnement Cloud Docker pour Commerce. Voir [Plug-ins Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Prise en charge des modules externes Elasticsearch** : ajout de la prise en charge des modules externes Elasticsearch suivants : `analysis-icu`, `analysis-phonetic`, `analysis-stempel` et `analysis-nori`. Les modules externes `analysis-icu` et `analysis-phonetic` sont installés par défaut. Vous pouvez ajouter ou supprimer des modules externes `analysis-stempel` et `analysis-nori` si nécessaire.<!--MCLOUD-2789-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur CLI**

      - **Exécutez des commandes dans des conteneurs PHP Docker** : vous pouvez désormais utiliser l’interface de ligne de commande Cloud Docker pour exécuter des commandes dans des conteneurs PHP dans votre environnement Docker sans avoir à installer PHP sur l’hôte. Par exemple, la commande suivante crée la configuration : `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Voir [Interface de ligne de commande de Cloud Docker](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - Ajout du client OpenSSH-client aux conteneurs CLI PHP. Désormais, vous pouvez utiliser le transfert ssh-agent pour le compositeur si le fichier `composer.json` contient des référentiels git privés qui nécessitent un client ssh pour utiliser les commandes du compositeur.<!--MCLOUD-6008-->

   - ![Icône de correctif](../../assets/fix.svg) **Conteneur TLS**—Désormais, le [Conteneur TLS](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) est basé sur l’image `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Docker au lieu de l’image CentOS. Cette modification corrige les problèmes qui provoquaient des erreurs lors de l’envoi de requêtes HTTPS entre des conteneurs dans l’environnement Cloud Docker.<!--MCLOUD-6469-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur de test** : ajout d’un conteneur de test pour le test de l’application et ajout de l’option `--with-test` à la commande Docker `build:compose` pour créer le conteneur uniquement lors du test dans l’environnement Docker. Voir [test de l’application](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur FPM-XDEBUG**

      - ![nouvelle icône](../../assets/new.svg) **Configurer Xdebug sous Linux**—Ajout de l’option `--set-docker-host` à la commande `ece-docker build:compose` pour configurer la valeur `host.docker.internal` dans le conteneur Xdebug. Cette option est requise pour utiliser Xdebug sur les systèmes Linux. Voir [Configuration de Xdebug pour Docker](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![icône de correctif](../../assets/fix.svg) Correction de la configuration de variable Xdebug pour que le point d’entrée Docker résolve les erreurs `uninitialized "with_xdebug" variable` dans les journaux. [Correctif soumis par Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**

   - **Configuration de MailHog** : vous pouvez désormais utiliser les options de commande `ece-docker build:compose` suivantes pour désactiver MailHog et spécifier les ports : `--no-mailhog`, `--mailhog-http-port` et `--mailhog-smtp-port`. Voir [Configuration de l’email](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Pour Cloud Docker pour Commerce 1.2.0 et versions ultérieures, Adobe fournit désormais des images Docker pour chaque version de correctif, et le générateur de configuration Docker crée la configuration Docker avec une version de correctif spécifiée au lieu d’utiliser la dernière version. Auparavant, le générateur de configuration Docker créait la configuration à l’aide de la dernière version de correctif qui pouvait interrompre les environnements Cloud Docker pour Commerce créés à l’aide d’une version antérieure.<!--MCLOUD-7093-->

   - **Spécifiez des images et des versions personnalisées dans la configuration personnalisée de Cloud Docker** : mise à jour de la commande `build:custom:compose` avec des options permettant de spécifier des images et des versions personnalisées lors de la génération d’un fichier de configuration de composition Docker personnalisé (`docker-compose.yaml`). Voir [Création d’une configuration Docker Composer personnalisée](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Mise à jour de la configuration de l’hôte Docker afin d’exposer le port 443 pour permettre l’accès à Adobe Commerce (`https://magento2.docker`) à partir de tous les conteneurs de l’interface de ligne de commande. Vous pouvez modifier le port par défaut en ajoutant l&#39;option `--tls-port` lors de la génération du fichier de configuration Docker.<!--MCLOUD-6806-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème en raison duquel la version de Cloud Docker pour Commerce échouait si le fichier `app/etc/env.php` existait.<!--MCLOUD-6732-->

- ![icône de correction](../../assets/fix.svg) Mise à jour de la configuration de version pour remplacer les volumes nommés par des volumes réguliers afin d’éviter des problèmes lors du déploiement de Cloud Docker pour Commerce sous Linux ou sous-système Windows pour Linux (WSL2).<!--MCLOUD-6732-->

- ![icône de correctif](../../assets/fix.svg) Mise à jour de Cloud Docker pour les tests fonctionnels Commerce pour la prise en charge du compositeur 2.0.<!--MCLOUD-7183-->

## v1.1.2

Date de publication : 9 septembre 2020

- ![nouvelle icône](../../assets/new.svg) Ajout de la prise en charge d’Elasticsearch 7.7<!--MCLOUD-6219-->

## v1.1.1

Date de publication : 5 août 2020

- ![Icône de correctif](../../assets/fix.svg) **Configuration de courrier électronique mise à jour** : mise à jour de la configuration par défaut de Cloud Docker pour Commerce afin de prendre en charge le service MailHog au lieu d’utiliser SendMail. Voir [Configuration de l’email](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![icône de correction](../../assets/fix.svg) Restauration de la bibliothèque PS dans la configuration de l’environnement Cloud Docker pour corriger les `ps:  command not found` erreurs.<!--MCLOUD-6621-->

- ![icône de correction](../../assets/fix.svg) Mise à jour de la configuration par défaut de Cloud Docker pour Commerce afin de supprimer le montage automatique du point d’entrée de la base de données et des volumes MariaDB pour corriger les erreurs `Cannot create container for service db` qui peuvent se produire lors du démarrage de votre environnement Cloud Docker.

  Vous pouvez maintenant configurer l’environnement Cloud Docker pour monter les répertoires de la base de données en ajoutant les options suivantes à la commande `ece-docker build:compose` : `--with-entry-point` et `with-mariadb-conf`. Voir [Options de configuration de service](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de la commande CLI**

| Action | Commande |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Ajouter un point d’entrée au conteneur de la base de données pour restaurer la base de données à partir de la sauvegarde | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Ajouter un volume de configuration MariaDB | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de la solution de performances de la base de données partagée** : vous pouvez désormais configurer et déployer un magasin à l’aide de la solution de performances de la base de données partagée dans l’environnement Cloud Docker.<!--MCLOUD-3740-->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge du déploiement Adobe Commerce et Magento Open Source**—Vous pouvez désormais utiliser Cloud Docker pour Commerce pour déployer un environnement de développement local pour les projets qui ne sont pas hébergés sur Adobe Commerce sur l’infrastructure cloud<!--MCLOUD-5667-->

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de Blackfire.io** : ajout de la prise en charge de l’ [extension Blackfire.io](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) pour les tests de performances automatisés. [Correctif soumis par Adarsh Manickam de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur**

   - **Varnish** : désormais le vernis est le cache par défaut lorsque vous déployez Adobe Commerce dans un environnement Cloud Docker à l’aide d’une version prise en charge du modèle d’application Cloud. Voir [Conteneur de vernis](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Ajout de l’option `--no-varnish` pour ignorer l’installation du service Varnish lorsque vous générez le fichier de configuration Cloud Docker.<!--MCLOUD-2634-->

   - ![nouvelle icône](../../assets/new.svg) **Base de données**

      - Ajout de la prise en charge de la base de données MySQL. Vous pouvez maintenant configurer l’environnement Cloud Docker avec MariaDB ou MySQL. Voir [Options de configuration de service](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Ajout de la possibilité de définir les paramètres d’incrément et de décalage pour la réplication de la base de données lors de la génération du fichier de composition Docker. Voir [Conteneurs de services](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![nouvelle icône](../../assets/new.svg) **PHP-FPM**

      - Ajout de la prise en charge de PHP 7.4. [Correctif soumis par Mohanela Murugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Possibilité de copier un fichier `php.ini` dans le répertoire du projet racine dans l’environnement Cloud Docker et d’appliquer des paramètres PHP personnalisés aux conteneurs PHP-FPM et CLI. Voir [Personnaliser les paramètres PHP](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - Ajout d’un contrôle d’intégrité du conteneur. [Correctif soumis par Visanth Sampath de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![icône de correctif](../../assets/fix.svg) **Node.js** : mise à jour de la version par défaut de Node.js de la version 8 à la version 10 pour améliorer la sécurité. Node.js version 8 est obsolète et n’est plus mis à jour avec des correctifs de bogues ou de sécurité. [Correctif soumis par Mohan Elamurugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![nouvelle icône](../../assets/new.svg) **Elasticsearch**

      - Ajout de la prise en charge d’Elasticsearch 6.8, 7.2, 7.5 et 7.6.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Ajout de la possibilité de personnaliser la [configuration de conteneur Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) lors de la génération du fichier de configuration de composition Docker.<!--MCLOUD-3059-->

      - Ajout de l’option `--no-es` aux options de configuration du service pour la génération du fichier de configuration Docker Composer. Utilisez cette option pour ignorer l’installation du conteneur Elasticsearch et utilisez plutôt la recherche MySQL . Cette option est prise en charge uniquement pour Adobe Commerce versions 2.3.5 et antérieures.<!--MCLOUD-3766-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur FPM-XDEBUG** : ajout d’une option de configuration de service pour installer et configurer Xdebug pour le débogage de code PHP dans votre environnement Cloud Docker. Voir [Configuration de Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**

   - Ajout de contrôles de l’intégrité pour les conteneurs de service PHP-FPM, Redis, Elasticsearch et MySQL Docker.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Le mode de synchronisation des fichiers par défaut a été remplacé par `native` en mode Développeur.<!--MCLOUD-3890 -->

   - Ajout d’informations de version à l’image de conteneur de service Docker générique lors de la génération du fichier `docker-compose.yml`.<!--MCLOUD-3878-->

   - Amélioration de la capacité à gérer les réponses volumineuses du conteneur PHP-FPM en amont en augmentant la valeur `fastcgi_buffers` pour le serveur Nginx.<!--MCLOUD-5980-->

   - Amélioration des performances de synchronisation des fichiers de multi-agène en ajoutant une seconde session de synchronisation pour synchroniser les fichiers dans le répertoire `vendor`. Cette modification empêche le mutagène de se bloquer pendant le processus de synchronisation des fichiers. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![nouvelle icône](../../assets/new.svg) **Mises à jour de la commande CLI**

| Action | Commande |
| -------- | --------------- |
| Effacer le cache des Redis | `bin/magento-docker flush-redis` |
| Effacer le cache de marque | `bin/magento-docker flush-varnish` |
| Ignorer l’installation de marque par défaut | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Personnaliser les options d’Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [ Supprimer la configuration de l’Elasticsearch ](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| Configuration du conteneur DB avec MySQL version 5.6 ou 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Définition d’une URL de base personnalisée | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Ajout d’un conteneur pour la configuration Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![icône de correctif](../../assets/fix.svg) Correction de la configuration de la synchronisation de fichiers de mutagène pour empêcher les mutagènes de créer des sessions obsolètes. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème de configuration qui provoquait des erreurs de syntaxe dans le journal de composition Docker lors du démarrage du conteneur PHP-FPM. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![icône de correction](../../assets/fix.svg) Correction des erreurs de conflit de volume qui se produisaient parfois lors de l’utilisation de plusieurs environnements Docker. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/168).

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel la commande `ece-docker build:compose` échouait si la configuration incluait Blackfire.io. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![icône de correction](../../assets/fix.svg) Mise à jour de la configuration de l’image de ligne de commande PHP afin d’éviter les erreurs de mémoire insuffisante survenant lors de l’installation de plusieurs modules à l’aide de Cloud Docker pour Commerce. [Correctif soumis par Mohan Elamurugan de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![icône de correction](../../assets/fix.svg) Ajout de la prise en charge de plusieurs utilisateurs MySQL dans l’environnement Cloud Docker. Dans les versions antérieures, l’opération `build:compose` a échoué si le fichier `magento.app.yaml` spécifiait plusieurs utilisateurs de base de données. [Correctif soumis par G Arvind de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![ icône de correction ](../../assets/fix.svg) Suppression de `rsyslog` des conteneurs Cloud Docker pour Commerce PHP afin de résoudre les problèmes de compatibilité qui généraient des notifications d’avertissement lors du déploiement. Cloud Docker n&#39;utilise pas l&#39;utilitaire rsyslog.<!--MCLOUD-6173-->

## v1.0.0

Date de publication : 5 février 2020

- ![nouvelle icône](../../assets/new.svg) **Création d’un package distinct pour fournir`Cloud Docker for Commerce`** : déplacement du code source pour fournir Cloud Docker pour Commerce du référentiel `ece-tools` vers le [ nouveau `magento-cloud-docker` référentiel](https://github.com/magento/magento-cloud-docker) afin de maintenir la qualité du code et de fournir des versions indépendantes. Le nouveau module est une dépendance pour les outils CEE v2002.1.0 et versions ultérieures.

  Lorsque vous mettez à jour les outils de l&#39;éditeur de texte, vous mettez également à jour le package `magento/magento-cloud-docker` vers la version 1.0.0. Si vous avez utilisé Cloud Docker pour Commerce avec une version antérieure de `ece-tools` (2002.0.x), passez en revue les [incompatibilités ascendantes](backward-incompatible-changes.md) et mettez à jour votre projet en tant que scripts, commandes et processus, si nécessaire.

- ![nouvelle icône](../../assets/new.svg) **Ajout d’un contrôle de version aux images Docker** : vous devez maintenant mettre à jour le package `magento/magento-cloud-docker` pour obtenir les images mises à jour.<!--MAGECLOUD-4737-->

- ![nouvelle icône](../../assets/new.svg) **Mises à jour de conteneur**—

   - ![nouvelle icône](../../assets/new.svg) **Conteneur PHP-FPM**—

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de Node.js**—Mise à jour de l’image PHP-FPM pour prendre en charge le noeud, le npm et les fonctionnalités grunt-cli dans le conteneur PHP.<!--MAGECLOUD-3953-->

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge de [ionCube](https://www.ioncube.com/)** : mise à jour de la configuration Docker par défaut pour prendre en charge ionCube dans l’environnement de développement Docker local.<!--MAGECLOUD-4354-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur web**—

      - ![nouvelle icône](../../assets/new.svg) **Personnaliser la configuration NGINX** : ajout de la capacité de monter un fichier `nginx.conf` personnalisé dans l’environnement Cloud Docker pour Commerce. Voir [Conteneur Web](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![nouvelle icône](../../assets/new.svg) **Certificats NGINX générés automatiquement** : le fichier de configuration Docker inclut désormais la configuration permettant de générer automatiquement des certificats NGINX pour le conteneur Web.<!--MAGECLOUD-4258-->

   - ![nouvelle icône](../../assets/new.svg) **Nouveau conteneur Selenium**—Ajout d’un [conteneur Selenium](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) pour la prise en charge des tests d’application Adobe Commerce à l’aide de la structure de test fonctionnel de Magento (MFTF).<!--MAGECLOUD-4040-->

   - ![new icon](../../assets/new.svg) **[!DNL RabbitMQ]version support**—Mise à jour de la configuration de conteneur [!DNL RabbitMQ] pour la prise en charge de [!DNL RabbitMQ] version 3.8.<!--MAGECLOUD-4674-->

   - ![ icône de correction ](../../assets/fix.svg) **Conteneur de base de données persistant** : le volume de base de données `magento-db: /var/lib/mysql` persiste après l’arrêt et la suppression de la configuration Docker et la restauration lorsque vous redémarrez la configuration Docker. Vous devez maintenant supprimer manuellement le volume de la base de données. Voir [Conteneurs de base de données].<!--MAGECLOUD-3978-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur TLS**—

      - ![nouvelle icône](../../assets/new.svg) **Mise à jour de l’image de base du conteneur pour utiliser l’image officielle** - L’image [Conteneur TLS Cloud](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) est désormais basée sur l’image officielle `debian:jessie` Docker.—<!--MAGECLOUD-4163-->

      - ![nouvelle icône](../../assets/new.svg) **Ajout de la prise en charge du [proxy d’arrêt TLS Pound]**—Le [fichier de configuration Pound](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) ajoute les variables ENV suivantes pour personnaliser la configuration Docker pour le conteneur TLS :

         - **`TimeOut`** : définit la valeur de délai d’expiration Time to First Byte (TTF). La valeur par défaut est de 300 secondes.

         - **`RewriteLocation`** : détermine si le proxy Pound réécrit l’emplacement par défaut vers l’URL de demande. La valeur par défaut est `0` pour empêcher la réécriture de rompre les redirections vers des sites web externes tels qu’un site d’authentification unique externe. [Correctif soumis par Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![nouvelle icône](../../assets/new.svg) Augmentation de la valeur du délai d’expiration dans la configuration du conteneur TLS de 15 à 300 secondes. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur de vernis**—

      - ![nouvelle icône](../../assets/new.svg) **Mise à jour de l’image de base du conteneur pour utiliser l’image officielle** : le [conteneur de vernis de cloud](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) est désormais basé sur l’image officielle `centos` Docker.<!--MAGECLOUD-4163-->

      - ![nouvelle icône](../../assets/new.svg) **Amélioration de la configuration du délai d’expiration par défaut** - Ajout de la configuration `.first_byte_timeout` et `.between_bytes_timeout` au conteneur de vernis. Les deux valeurs de délai d’expiration sont par défaut de `300s` (5 minutes). [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![Icône de correctif](../../assets/fix.svg) **Ignorer le vernis pendant les sessions Xdebug**—Mise à jour de la configuration de conteneur de vernis pour renvoyer `pass` sur les demandes reçues lorsque Xdebug est activé. Dans les versions précédentes, vous ne pouviez pas utiliser Xdebug si l’environnement Docker incluait le vernis. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![nouvelle icône](../../assets/new.svg) **Modifications de la configuration Docker**—

   - ![nouvelle icône](../../assets/new.svg) **Gérer les montages et les volumes pour votre projet** : ajout de la capacité de gérer les montages et les volumes lors du lancement d’un environnement Docker pour le développement local. Voir [Partage des données de projet].<!--MAGECLOUD-3248-->

   - ![nouvelle icône](../../assets/new.svg) **Prise en charge du mode de pont réseau**—Ajout de la prise en charge du mode de pont réseau pour activer les connexions entre des conteneurs Docker sur le réseau local.<!--MAGECLOUD-4165-->

   - ![nouvelle icône](../../assets/new.svg) **Conteneur Cron désactivé par défaut**—Pour améliorer les performances, le conteneur Cron n’est plus configuré par défaut lors de la création de l’environnement Docker. Vous pouvez utiliser l’option `--with-cron` de la commande Docker build pour ajouter un conteneur Cron à votre environnement. Voir [Gestion des tâches cron](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![nouvelle icône](../../assets/new.svg) **Arrêtez de synchroniser les fichiers de sauvegarde volumineux** : ajout de fichiers de sauvegarde et d’archives DB (ZIP, SQL, GZ et BZ2) à la liste d’exclusion dans les fichiers `dist/docker-sync.yml` et `dist/mutagen.sh`. La synchronisation de fichiers volumineux (>1 Go) peut entraîner une période d’inactivité et les fichiers de sauvegarde ne nécessitent normalement pas de synchronisation puisque vous pouvez les régénérer.<!--MAGECLOUD-3979-->

- ![nouvelle icône](../../assets/new.svg) **Changements de commande**—

   - ![icône de correction](../../assets/fix.svg) Renommé le fichier `./bin/docker` en `./bin/magento-docker` pour résoudre un problème qui entraînait l’arrêt de certains environnements Docker, car le fichier `./bin/docker` remplaçait les fichiers binaires Docker existants. Il s’agit d’une [ modification incompatible en amont ](backward-incompatible-changes.md) qui nécessite des mises à jour de vos scripts et commandes.<!-- MAGECLOUD-4038 -->

   - ![nouvelle icône](../../assets/new.svg) **Ajout d’une option de configuration de service pour exposer le port de base de données à l’hôte**. Utilisez l’option `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` pour exposer le port de base de données à l’hôte lors de la création du fichier `docker-compose.yml` : `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![nouvelle icône](../../assets/new.svg) **Nouvelle commande de post-déploiement** : auparavant, les hooks de post-déploiement définis dans le fichier `.magento.app.yaml` s’exécutaient automatiquement après le déploiement d’Adobe Commerce sur un conteneur Cloud Docker à l’aide de la commande `cloud-deploy`. Maintenant, vous devez émettre une commande `cloud-post-deploy` distincte pour exécuter les hooks de post-déploiement après le déploiement. Voir les instructions de lancement mises à jour pour le mode [développeur](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) et le mode [production](https://devdocs.magento.com/cloud/docker/docker-mode-production.html).<!--MAGECLOUD-3996-->

   - ![nouvelle icône](../../assets/new.svg) Ajout de l’option `--rm` aux commandes `./bin/magento-docker` pour les conteneurs de création et de déploiement. Cette opération supprime le conteneur une fois la tâche terminée.<!--MAGECLOUD-4205-->

   - ![nouvelle icône](../../assets/new.svg) **Commande `build:compose` mise à jour**—

      - ![nouvelle icône](../../assets/new.svg) Ajout de l’option `--sync-engine="native"` à la commande `docker-build` pour désactiver la synchronisation des fichiers lorsque vous générez le fichier de configuration Docker Composer en mode développeur. Utilisez cette option lors du développement sur des systèmes Linux, qui ne nécessitent pas de synchronisation de fichiers pour le développement Docker local. Voir [Synchronisation des données dans l’environnement Docker](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![new icon](../../assets/new.svg) Modification du paramètre de synchronisation des fichiers par défaut de `docker-sync` à `native`. [Correctif soumis par Mathew Beane de Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![nouvelle icône](../../assets/new.svg) **Améliorations de la validation**—

   - ![nouvelle icône](../../assets/new.svg) Ajout d’une validation au processus de déploiement pour les environnements de développement Docker locaux afin de vérifier que la configuration de l’environnement Cloud inclut la clé de chiffrement requise pour déchiffrer la base de données. Désormais, vous recevez un message d’erreur dans le journal si la configuration de l’environnement ne spécifie aucune valeur pour la clé de chiffrement.<!--MAGECLOUD-4423-->

   - ![nouvelle icône](../../assets/new.svg) Ajout d’un contrôle d’intégrité du conteneur au service Elasticsearch pour s’assurer que le service est prêt avant de poursuivre le traitement de création et de déploiement. Si le contrôle de l&#39;intégrité renvoie une erreur, le conteneur redémarre automatiquement.<!--MAGECLOUD-4456-->
