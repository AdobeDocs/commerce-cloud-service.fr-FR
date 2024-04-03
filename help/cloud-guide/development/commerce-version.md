---
title: Mise à niveau de la version Commerce
description: Découvrez comment mettre à niveau la version d’Adobe Commerce dans le projet d’infrastructure cloud.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 745a9f08353bd5dfbb871ca88947157c145c7c70
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Mise à niveau de la version Commerce

Vous pouvez mettre à niveau la base de code Adobe Commerce vers une version plus récente. Avant de mettre à niveau votre projet, passez en revue les [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Installation_ guide pour connaître les dernières exigences en matière de version logicielle.

Selon la configuration de votre projet, les tâches de mise à niveau peuvent inclure les éléments suivants :

- Les services de mise à jour, tels que MariaDB (MySQL), OpenSearch, RabbitMQ et Redis, sont compatibles avec les nouvelles versions d’Adobe Commerce.
- Convertissez un ancien fichier de gestion de configuration.
- Mettez à jour le `.magento.app.yaml` avec de nouveaux paramètres pour les hooks et les variables d’environnement.
- Mettez à niveau les extensions tierces vers la dernière version prise en charge.
- Mettez à jour le `.gitignore` fichier .

{{upgrade-tip}}

{{pro-update-service}}

## Mise à niveau à partir d’anciennes versions

Si vous commencez une mise à niveau à partir d’une version de Commerce antérieure à 2.1, certaines restrictions de la base de code Adobe Commerce peuvent affecter votre capacité à _update_ vers une version spécifique d’outils CEE ou vers _upgrade_ vers la version de commerce prise en charge suivante. Utilisez le tableau suivant pour déterminer le meilleur chemin d’accès :

| Version actuelle | Chemin de mise à niveau |
| ----------------- | ------------ |
| 2.1.3 et versions antérieures | Effectuez la mise à niveau d’Adobe Commerce vers la version 2.1.4 ou ultérieure avant de continuer. Ensuite, effectuez une [mise à niveau ponctuelle pour installer les outils CEE](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [Mettre à jour les outils ECE](../dev-tools/update-package.md) module.<br>Voir les notes de mise à jour pour [2002.0.9](../release-notes/cloud-release-archive.md#v200209) et versions ultérieures de 2002.0.x. |
| 2.1.15 - 2.1.16 | [Mettre à jour les outils ECE](../dev-tools/update-package.md) module.<br>Voir les notes de mise à jour pour[2002.0.9](../release-notes/cloud-release-archive.md#v200209) et plus tard. |
| 2.2.x et versions ultérieures | [Mettre à jour les outils ECE](../dev-tools/update-package.md) module.<br>Voir les notes de mise à jour pour[2002.0.8](../release-notes/cloud-release-archive.md#v200208) et plus tard. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Gestion des configurations

Les anciennes versions d’Adobe Commerce, telles que la version 2.1.4 ou ultérieure à la version 2.2.x ou ultérieure, utilisaient une `config.local.php` pour Configuration Management. Adobe Commerce version 2.2.0 et ultérieure utilise la variable `config.php` qui fonctionne exactement comme le fichier `config.local.php` , mais il comporte différents paramètres de configuration qui incluent une liste de vos modules activés et d’autres options de configuration.

Lorsque vous effectuez une mise à niveau à partir d’une ancienne version, vous devez migrer la variable `config.local.php` pour utiliser le fichier le plus récent `config.php` fichier . Procédez comme suit pour sauvegarder votre fichier de configuration et en créer un.

**Pour créer un `config.php` fichier**:

1. Création d’une copie de `config.local.php` fichier et nommez-le. `config.php`.

1. Ajoutez ce fichier au `app/etc` du projet.

1. Ajoutez et validez le fichier dans votre branche.

1. Envoyez le fichier à votre branche d’intégration.

1. Passez à la procédure de mise à niveau.

>[!WARNING]
>
>Après la mise à niveau, vous pouvez supprimer la variable `config.php` et générez un nouveau fichier complet. Vous ne pouvez supprimer ce fichier que pour le remplacer cette fois-ci. Après avoir généré une nouvelle `config.php` , vous ne pouvez pas supprimer le fichier pour en générer un nouveau. Voir [Gestion des configurations et déploiement du pipeline](../store/store-settings.md).

### Vérification des dépendances du compositeur Zend Framework

Lors de la mise à niveau vers **2.3.x ou version ultérieure de 2.2.x**, vérifiez que les dépendances Zend Framework ont été ajoutées à la variable `autoload` de la propriété `composer.json` pour prendre en charge Laminas. Ce module externe prend en charge de nouvelles exigences pour Zend Framework, qui a migré vers le projet Laminas. Voir [Migration de Zend Framework vers le projet Laminas](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) sur le _Magento DevBlog_.

**Pour vérifier la variable `auto-load:psr-4` configuration**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Extrayez votre branche d’intégration.

1. Ouvrez le `composer.json` dans un éditeur de texte.

1. Vérifiez les `autoload:psr-4` pour l’implémentation du gestionnaire de modules externes Zend pour la dépendance des contrôleurs.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Si la dépendance Zend est manquante, mettez à jour la variable `composer.json` fichier :

   - Ajoutez la ligne suivante au `autoload:psr-4` .

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Mettez à jour les dépendances du projet.

     ```bash
     composer update
     ```

   - Ajout, validation et modification du code push.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Fusionnez les modifications dans l’environnement d’évaluation, puis dans l’environnement de production.

## Fichiers de configuration

Avant de mettre à niveau l’application, vous devez mettre à jour les fichiers de configuration de votre projet afin de tenir compte des modifications apportées aux paramètres de configuration par défaut d’Adobe Commerce sur l’infrastructure cloud ou l’application. Les derniers paramètres par défaut sont disponibles dans la section [référentiel GitHub magento-cloud](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Vérifiez toujours les valeurs contenues dans la variable [.magento.app.yaml](../application/configure-app-yaml.md) pour la version installée, car il contrôle la manière dont votre application est créée et déployée vers l’infrastructure cloud. L’exemple suivant concerne la version 2.4.6 et utilise Composer 2.2.21. La variable `build: flavor:` n’est pas utilisée pour le compositeur 2.x ; voir [Installation et utilisation du compositeur 2](../application/properties.md#installing-and-using-composer-2).

**Pour mettre à jour la variable `.magento.app.yaml` fichier**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Ouvrez et modifiez les `magento.app.yaml` fichier .

1. Mettez à jour les options PHP.

   ```yaml
   type: php:8.2
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.2.21'
   ```

1. Modifiez la variable `hooks` property `build` et `deploy` des commandes.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Ajoutez les variables d’environnement suivantes à la fin du fichier.

   Pour Adobe Commerce 2.2.x à 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Pour Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Enregistrez le fichier. Ne validez ou n’envoyez pas encore de modifications à l’environnement distant.

1. Passez à la procédure de mise à niveau.

### composer.json

Avant de procéder à la mise à niveau, vérifiez toujours que les dépendances de la variable `composer.json` sont compatibles avec la version d’Adobe Commerce.

**Pour mettre à jour la variable `composer.json` pour Adobe Commerce version 2.4.4 et ultérieure**:

1. Ajoutez ce qui suit : `allow-plugins` à la fonction `config` section :

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Ajoutez le module externe suivant au `require` section :

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Ajoutez le composant suivant au `extra:component_paths` section :

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Enregistrez le fichier. Ne validez ou n’envoyez pas encore de modifications à votre branche.

1. Passez à la procédure de mise à niveau.

## Sauvegarde du projet

Nous vous recommandons de créer une sauvegarde de votre projet avant une mise à niveau. Procédez comme suit pour sauvegarder vos environnements d’intégration, d’évaluation et de production.

**Sauvegarde de la base de données et du code de votre environnement d’intégration**:

1. Créez une sauvegarde locale de la base distante.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >La variable `magento-cloud db:dump` exécute la commande [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) avec la commande `--single-transaction` qui permet de sauvegarder votre base de données sans verrouiller les tables.

1. Sauvegardez le code et le média.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Vous pouvez éventuellement omettre `[--media]` si vous disposez d’un grand nombre de fichiers statiques qui sont déjà dans le contrôle de code source.

**Pour sauvegarder votre base de données d’environnement d’évaluation ou de production avant le déploiement**:

1. Utilisez SSH pour vous connecter à l’environnement distant.

1. Créez un [vidage de base de données](../storage/database-dump.md). Pour choisir un répertoire cible pour le vidage DB, utilisez la méthode `--dump-directory` .

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   L’opération de vidage crée une `dump-<timestamp>.sql.gz` archivez le fichier dans votre répertoire de projet distant. Voir [Sauvegarde de la base](../storage/database-dump.md).

## Mise à niveau des applications

Consultez la section [versions de service](../services/services-yaml.md#service-versions) informations relatives aux dernières exigences en matière de version logicielle avant la mise à niveau de votre application.

**Mise à niveau de la version de l’application**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Définissez la version de mise à niveau à l’aide du [syntaxe de contrainte de version](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Vous devez utiliser la syntaxe de contrainte de version pour mettre à jour correctement la variable `ece-tools` module. Vous trouverez la contrainte de version dans la variable `composer.json` pour la version de [modèle d&#39;application](https://github.com/magento/magento-cloud/blob/master/composer.json) vous utilisez pour la mise à niveau.

1. Mettez à jour le projet.

   ```bash
   composer update
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` est nécessaire pour ajouter tous les fichiers modifiés au contrôle source en raison de la manière dont le compositeur marque les packages de base. Les deux `composer install` et `composer update` archiver les fichiers à partir du package de base (`magento/magento2-base` et `magento/magento2-ee-base`) dans la racine du module.

   Les fichiers marshals du compositeur appartiennent à la nouvelle version d’Adobe Commerce, pour remplacer la version obsolète de ces mêmes fichiers. Actuellement, la mise en grappe est désactivée dans Adobe Commerce. Vous devez donc ajouter les fichiers mis en grappe au contrôle source.

1. Attendez que le déploiement soit terminé.

1. Vérifiez la mise à niveau dans votre environnement d’intégration, d’évaluation ou de production en utilisant SSH pour vous connecter et vérifier la version.

   ```bash
   php bin/magento --version
   ```

### Créer un fichier config.php

Comme indiqué dans [Gestion des configurations](#configuration-management), après la mise à niveau, vous devez créer une mise à jour `config.php` fichier . Effectuez d’autres modifications de configuration par l’intermédiaire de l’administrateur de votre environnement d’intégration.

**Création d’un fichier de configuration spécifique au système**:

1. À partir du terminal, utilisez une commande SSH pour générer la variable `/app/etc/config.php` pour l’environnement.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Par exemple, pour Pro, pour exécuter la fonction `scd-dump` sur le `integration` branche :

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Transférez `config.php` à vos postes de travail locaux en utilisant `rsync` ou `scp`. Vous pouvez uniquement ajouter ce fichier à la branche localement.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Cette opération génère une mise à jour `/app/etc/config.php` avec une liste de modules et des paramètres de configuration.

>[!WARNING]
>
>Pour une mise à niveau, vous supprimez le `config.php` fichier . Une fois ce fichier ajouté à votre code, vous devez : **not** supprimez-le. Si vous devez supprimer ou modifier des paramètres, modifiez le fichier manuellement.

### Mettre à niveau les extensions

Passez en revue vos pages d’extension et de module tierces dans Marketplace ou d’autres sites d’entreprise et vérifiez la prise en charge d’Adobe Commerce et d’Adobe Commerce sur l’infrastructure cloud. Si vous devez mettre à niveau des extensions et modules tiers, Adobe recommande de travailler dans une nouvelle branche d’intégration avec vos extensions désactivées.

**Vérification et mise à niveau de vos extensions**:

1. Créez une branche sur votre poste de travail local.

1. Désactivez vos extensions selon vos besoins.

1. Lorsque disponible, téléchargez les mises à niveau d’extension.

1. Installez la mise à niveau comme indiqué dans la documentation tierce.

1. Activez et testez l’extension .

1. Ajoutez, validez et poussez les modifications de code sur la télécommande.

1. Poussez vers et testez dans votre environnement d’intégration.

1. Poussez vers l’environnement d’évaluation pour effectuer un test dans un environnement de pré-production.

Adobe recommande vivement de mettre à niveau votre environnement de production _before_ l’inclusion des extensions mises à niveau dans le processus de lancement de votre site.

>[!NOTE]
>
>Lorsque vous mettez à niveau la version de votre application, le processus de mise à niveau est mis à jour vers la dernière version de la [Module CDN rapide](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatiquement.

## Dépannage de la mise à niveau

En cas d’échec de la mise à niveau, un message d’erreur s’affiche dans le navigateur pour vous indiquer que vous ne pouvez pas accéder à votre vitrine ou au panneau d’administration :

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Pour résoudre l’erreur**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Ouvrez le `./app/var/report/<error number>` fichier .

1. [Examiner les logs](../test/log-locations.md) et déterminer la source du problème.

1. Ajout, validation et modification du code push.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
