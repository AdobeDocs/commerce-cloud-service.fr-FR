---
title: Mettre à niveau la version de Commerce
description: Découvrez comment mettre à niveau la version d’Adobe Commerce dans le projet d’infrastructure cloud.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Mettre à niveau la version de Commerce

Vous pouvez mettre à niveau la base de code Adobe Commerce vers une version plus récente. Avant de mettre à niveau votre projet, consultez la [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) du guide _Installation_ pour connaître les dernières exigences en matière de version logicielle.

Selon la configuration de votre projet, les tâches de mise à niveau peuvent inclure les éléments suivants :

- Les services de mise à jour, tels que MariaDB (MySQL), OpenSearch, RabbitMQ et Redis, sont compatibles avec les nouvelles versions d’Adobe Commerce.
- Convertissez un ancien fichier de gestion de configuration.
- Mettez à jour le fichier `.magento.app.yaml` avec de nouveaux paramètres pour les hooks et les variables d’environnement.
- Mettez à niveau les extensions tierces vers la dernière version prise en charge.
- Mettez à jour le fichier `.gitignore`.

{{upgrade-tip}}

{{pro-update-service}}

## Mise à niveau à partir d’anciennes versions

Si vous commencez une mise à niveau à partir d’une version de Commerce antérieure à 2.1, certaines restrictions dans la base de code Adobe Commerce peuvent affecter votre capacité à _mettre à jour_ vers une version spécifique de CEE-Outils ou à _mettre à niveau_ vers la prochaine version de Commerce prise en charge. Utilisez le tableau suivant pour déterminer le meilleur chemin d’accès :

| Version actuelle | Chemin de mise à niveau |
| ----------------- | ------------ |
| 2.1.3 et versions antérieures | Effectuez la mise à niveau d’Adobe Commerce vers la version 2.1.4 ou ultérieure avant de continuer. Effectuez ensuite une [mise à niveau unique pour installer les outils ECG](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [ Mettre à jour le package CEE-Outils](../dev-tools/update-package.md).<br>Voir les notes de mise à jour pour les versions [2002.0.9](../release-notes/cloud-release-archive.md#v200209) et ultérieures 2002.0.x. |
| 2.1.15 - 2.1.16 | [ Mettre à jour le package CEE-Outils](../dev-tools/update-package.md).<br>Voir les notes de mise à jour pour[2002.0.9](../release-notes/cloud-release-archive.md#v200209) et versions ultérieures. |
| 2.2.x et versions ultérieures | [ Mettre à jour le package CEE-Outils](../dev-tools/update-package.md).<br>Voir les notes de mise à jour de [2002.0.8](../release-notes/cloud-release-archive.md#v200208) et versions ultérieures. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Gestion des configurations

Les versions plus anciennes d’Adobe Commerce, telles que la version 2.1.4 ou ultérieure à la version 2.2.x ou ultérieure, utilisaient un fichier `config.local.php` pour la gestion de la configuration. Adobe Commerce version 2.2.0 et ultérieure utilise le fichier `config.php`, qui fonctionne exactement comme le fichier `config.local.php`, mais qui comporte différents paramètres de configuration qui incluent une liste de vos modules activés et d’autres options de configuration.

Lors de la mise à niveau à partir d’une ancienne version, vous devez migrer le fichier `config.local.php` pour utiliser le fichier `config.php` plus récent. Procédez comme suit pour sauvegarder votre fichier de configuration et en créer un.

**Pour créer un fichier `config.php` temporaire** :

1. Créez une copie du fichier `config.local.php` et nommez-la `config.php`.

1. Ajoutez ce fichier au dossier `app/etc` de votre projet.

1. Ajoutez et validez le fichier dans votre branche.

1. Envoyez le fichier à votre branche d’intégration.

1. Passez à la procédure de mise à niveau.

>[!WARNING]
>
>Après la mise à niveau, vous pouvez supprimer le fichier `config.php` et générer un nouveau fichier complet. Vous ne pouvez supprimer ce fichier que pour le remplacer cette fois-ci. Après avoir généré un nouveau fichier `config.php`, vous ne pouvez pas supprimer le fichier pour en générer un nouveau. Voir [ Configuration Management et déploiement de pipeline ](../store/store-settings.md).

### Vérification des dépendances du compositeur Zend Framework

Lors de la mise à niveau vers **2.3.x ou version ultérieure à partir de 2.2.x**, vérifiez que les dépendances Zend Framework ont été ajoutées à la propriété `autoload` du fichier `composer.json` pour prendre en charge Laminas. Ce module externe prend en charge de nouvelles exigences pour Zend Framework, qui a migré vers le projet Laminas. Voir [Migration de Zend Framework vers le projet Laminas](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) sur le _Magento DevBlog_.

**Pour vérifier la configuration `auto-load:psr-4`** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Extrayez votre branche d’intégration.

1. Ouvrez le fichier `composer.json` dans un éditeur de texte.

1. Consultez la section `autoload:psr-4` de l’implémentation du gestionnaire de modules externes Zend pour connaître la dépendance des contrôleurs.

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

1. Si la dépendance Zend est manquante, mettez à jour le fichier `composer.json` :

   - Ajoutez la ligne suivante à la section `autoload:psr-4` .

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

Avant de mettre à niveau l’application, vous devez mettre à jour les fichiers de configuration de votre projet afin de tenir compte des modifications apportées aux paramètres de configuration par défaut d’Adobe Commerce sur l’infrastructure cloud ou l’application. Les derniers paramètres par défaut sont disponibles dans le [référentiel GitHub magento-cloud](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Vérifiez toujours les valeurs contenues dans le fichier [.magento.app.yaml](../application/configure-app-yaml.md) pour votre version installée, car il contrôle la manière dont votre application crée et se déploie vers l’infrastructure cloud. L’exemple suivant concerne la version 2.4.7 et utilise Composer 2.7.2. La propriété `build: flavor:` n’est pas utilisée pour le compositeur 2.x ; voir [Installation et utilisation du compositeur 2](../application/properties.md#installing-and-using-composer-2).

**Pour mettre à jour le fichier `.magento.app.yaml`** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Ouvrez et modifiez le fichier `magento.app.yaml`.

1. Mettez à jour les options PHP.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Modifiez les commandes `hooks` property `build` et `deploy` .

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

Avant de procéder à la mise à niveau, vérifiez toujours que les dépendances du fichier `composer.json` sont compatibles avec la version Adobe Commerce.

**Pour mettre à jour le fichier `composer.json` pour Adobe Commerce version 2.4.4 et ultérieure** :

1. Ajoutez le `allow-plugins` suivant à la section `config` :

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Ajoutez le module externe suivant à la section `require` :

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Ajoutez le composant suivant à la section `extra:component_paths` :

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

**Pour sauvegarder votre base de données et votre code d’environnement d’intégration** :

1. Créez une sauvegarde locale de la base distante.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >La commande `magento-cloud db:dump` exécute la commande [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) avec l’indicateur `--single-transaction`, ce qui vous permet de sauvegarder votre base de données sans verrouiller les tables.

1. Sauvegardez le code et le média.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Vous pouvez éventuellement omettre `[--media]` si vous disposez d’un grand nombre de fichiers statiques qui sont déjà dans le contrôle de code source.

**Pour sauvegarder votre base de données d’environnement d’évaluation ou de production avant le déploiement** :

1. Utilisez SSH pour vous connecter à l’environnement distant.

1. Créez un [vidage de base de données](../storage/database-dump.md). Pour choisir un répertoire cible pour le vidage DB, utilisez l’option `--dump-directory`.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   L’opération de vidage crée un fichier d’archive `dump-<timestamp>.sql.gz` dans votre répertoire de projet distant. Voir [Sauvegarde de la base de données](../storage/database-dump.md).

## Mise à niveau des applications

Passez en revue les [versions de service](../services/services-yaml.md#service-versions) pour connaître les dernières exigences en matière de version logicielle avant de mettre à niveau votre application.

**Pour mettre à niveau la version de l’application** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Définissez la version de mise à niveau à l’aide de la [syntaxe de contrainte de version](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Vous devez utiliser la syntaxe de contrainte de version pour mettre à jour le package `ece-tools` avec succès. Vous pouvez trouver la contrainte de version dans le fichier `composer.json` pour la version du [modèle d’application](https://github.com/magento/magento-cloud/blob/master/composer.json) que vous utilisez pour la mise à niveau.

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

   `git add -A` est nécessaire pour ajouter tous les fichiers modifiés au contrôle de code source en raison de la manière dont le compositeur d’expérience associe les packages de base. `composer install` et `composer update` stockent les fichiers du package de base (`magento/magento2-base` et `magento/magento2-ee-base`) dans la racine du package.

   Les fichiers marshals du compositeur appartiennent à la nouvelle version d’Adobe Commerce, pour remplacer la version obsolète de ces mêmes fichiers. Actuellement, la mise en grappe est désactivée dans Adobe Commerce. Vous devez donc ajouter les fichiers mis en grappe au contrôle source.

1. Attendez que le déploiement soit terminé.

1. Vérifiez la mise à niveau dans votre environnement d’intégration, d’évaluation ou de production en utilisant SSH pour vous connecter et vérifier la version.

   ```bash
   php bin/magento --version
   ```

### Créer un fichier config.php

Comme mentionné dans [Gestion de la configuration](#configuration-management), après la mise à niveau, vous devez créer un fichier `config.php` mis à jour. Effectuez d’autres modifications de configuration par l’intermédiaire de l’administrateur de votre environnement d’intégration.

**Pour créer un fichier de configuration spécifique au système** :

1. Depuis le terminal, utilisez une commande SSH pour générer le fichier `/app/etc/config.php` pour l’environnement.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Par exemple, pour Pro, exécutez `scd-dump` sur la branche `integration` :

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Transférez le fichier `config.php` vers vos postes de travail locaux à l’aide de `rsync` ou `scp`. Vous pouvez uniquement ajouter ce fichier à la branche localement.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Cela génère un fichier `/app/etc/config.php` mis à jour avec une liste de modules et des paramètres de configuration.

>[!WARNING]
>
>Pour une mise à niveau, vous supprimez le fichier `config.php`. Une fois ce fichier ajouté à votre code, vous devez le supprimer **et non**. Si vous devez supprimer ou modifier des paramètres, modifiez le fichier manuellement.

### Mettre à niveau les extensions

Passez en revue vos pages d’extension et de module tierces dans Marketplace ou d’autres sites d’entreprise et vérifiez la prise en charge d’Adobe Commerce et d’Adobe Commerce sur l’infrastructure cloud. Si vous devez mettre à niveau des extensions et modules tiers, Adobe recommande de travailler dans une nouvelle branche d’intégration avec vos extensions désactivées.

**Pour vérifier et mettre à niveau vos extensions** :

1. Créez une branche sur votre poste de travail local.

1. Désactivez vos extensions selon vos besoins.

1. Lorsque disponible, téléchargez les mises à niveau d’extension.

1. Installez la mise à niveau comme indiqué dans la documentation tierce.

1. Activez et testez l’extension .

1. Ajoutez, validez et poussez les modifications de code sur la télécommande.

1. Poussez vers et testez dans votre environnement d’intégration.

1. Poussez vers l’environnement d’évaluation pour effectuer un test dans un environnement de pré-production.

Adobe recommande vivement de mettre à niveau votre environnement de production _avant_, y compris les extensions mises à niveau dans le processus de lancement de votre site.

>[!NOTE]
>
>Lorsque vous mettez à niveau la version de votre application, le processus de mise à niveau se met automatiquement à jour vers la dernière version du [module CDN Fastly](../cdn/fastly.md#fastly-cdn-module-for-magento-2).

## Dépannage de la mise à niveau

En cas d’échec de la mise à niveau, un message d’erreur s’affiche dans le navigateur pour vous indiquer que vous ne pouvez pas accéder à votre vitrine ou au panneau d’administration :

```
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Pour résoudre l’erreur** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Ouvrez le fichier `./app/var/report/<error number>`.

1. [Examinez les journaux](../test/log-locations.md) et déterminez la source du problème.

1. Ajout, validation et modification du code push.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
