---
title: Mettre à niveau la version de Commerce
description: Découvrez comment mettre à niveau la version d’Adobe Commerce dans le projet d’infrastructure cloud.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Mettre à niveau la version de Commerce

Vous pouvez mettre à niveau la base de code Adobe Commerce vers une version plus récente. Avant de mettre à niveau votre projet, passez en revue les [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Installation_ guide des dernières exigences en matière de version logicielle.

Selon la configuration de votre projet, les tâches de mise à niveau peuvent inclure :

- Mettez à jour les services tels que MariaDB (MySQL), OpenSearch, RabbitMQ et Redis pour des raisons de compatibilité avec les nouvelles versions d’Adobe Commerce.
- Convertissez un fichier de gestion de configuration plus ancien.
- Mettre à jour `.magento.app.yaml` avec les nouveaux paramètres pour les hooks et les variables d’environnement.
- Mettez à niveau les extensions tierces vers la dernière version prise en charge.
- Mettre à jour `.gitignore` fichier .

{{upgrade-tip}}

{{pro-update-service}}

## Mise à niveau à partir de versions plus anciennes

Si vous commencez une mise à niveau à partir d’une version de Commerce antérieure à la version 2.1, certaines restrictions de la base de code d’Adobe Commerce peuvent affecter votre capacité à : _mettre à jour_ à une version spécifique des outils de la CEE ou à _mettre à niveau_ à la prochaine version de Commerce prise en charge. Utilisez le tableau suivant pour déterminer le meilleur chemin d’accès :

| Version actuelle | Chemin de mise à niveau |
| ----------------- | ------------ |
| 2.1.3 et versions antérieures | Mettez à niveau Adobe Commerce vers la version 2.1.4 ou une version ultérieure avant de continuer. Effectuez ensuite une [mise à niveau ponctuelle pour l&#39;installation des outils ECE](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [Mise à jour des outils de la CEE](../dev-tools/update-package.md) package.<br>Voir les notes de mise à jour pour [2002.0.9](../release-notes/cloud-release-archive.md#v200209) et versions ultérieures 2002.0.x. |
| 2.1.15 - 2.1.16 | [Mise à jour des outils de la CEE](../dev-tools/update-package.md) package.<br>Voir les notes de mise à jour pour[2002.0.9](../release-notes/cloud-release-archive.md#v200209) et plus tard. |
| 2.2.x et versions ultérieures | [Mise à jour des outils de la CEE](../dev-tools/update-package.md) package.<br>Voir les notes de mise à jour pour[2002.0.8](../release-notes/cloud-release-archive.md#v200208) et plus tard. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Gestion de la configuration

Les anciennes versions d’Adobe Commerce, telles que la version 2.1.4 ou ultérieure à la version 2.2.x ou ultérieure, utilisaient un `config.local.php` fichier pour la gestion de la configuration. Adobe Commerce version 2.2.0 et ultérieure utilise `config.php` , qui fonctionne exactement comme le `config.local.php` , mais il comporte différents paramètres de configuration qui incluent une liste de vos modules activés et des options de configuration supplémentaires.

Lors de la mise à niveau à partir d’une ancienne version, vous devez migrer le `config.local.php` fichier pour utiliser le plus récent `config.php` fichier . Pour sauvegarder votre fichier de configuration et en créer un, procédez comme suit.

**Pour créer un fichier temporaire `config.php` fichier**:

1. Créer une copie de `config.local.php` fichier et le nommer `config.php`.

1. Ajouter ce fichier au `app/etc` du projet.

1. Ajoutez et validez le fichier dans votre branche.

1. Envoyez le fichier vers votre branche d’intégration.

1. Poursuivez le processus de mise à niveau.

>[!WARNING]
>
>Après la mise à niveau, vous pouvez supprimer le `config.php` et générer un nouveau fichier complet. Vous ne pouvez supprimer ce fichier que pour le remplacer cette fois-ci. Après avoir généré un nouveau fichier, terminez `config.php` fichier, vous ne pouvez pas supprimer le fichier pour en générer un nouveau. Voir [Gestion de la configuration et déploiement du pipeline](../store/store-settings.md).

### Vérifier les dépendances du compositeur de structure d&#39;envoi

Lors de la mise à niveau vers **2.3.x ou version ultérieure à partir de 2.2.x**, vérifiez que les dépendances de la structure d’envoi ont été ajoutées au `autoload` propriété du `composer.json` fichier pour prendre en charge Laminas. Ce plug-in prend en charge les nouvelles exigences du framework Zend, qui a migré vers le projet Laminas. Voir [Migration de Zend Framework vers le projet Laminas](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) le _DevBlog du Magento_.

**Pour vérifier le `auto-load:psr-4` configuration**:

1. Sur votre station de travail locale, accédez au répertoire du projet.

1. Consultez votre branche d’intégration.

1. Ouvrez le . `composer.json` dans un éditeur de texte.

1. Vérifier le `autoload:psr-4` pour l’implémentation du gestionnaire de plug-ins Zend pour la dépendance des contrôleurs.

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

1. Si la dépendance Envoyer est manquante, mettez à jour le `composer.json` fichier :

   - Ajoutez la ligne suivante au `autoload:psr-4` section.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Mettez à jour les dépendances du projet.

     ```bash
     composer update
     ```

   - Ajout, validation et modifications de code push.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Fusionner les modifications apportées à l’environnement d’évaluation, puis à la production.

## Fichiers de configuration

Avant de mettre à niveau l’application, vous devez mettre à jour les fichiers de configuration de votre projet afin de tenir compte des modifications apportées aux paramètres de configuration par défaut d’Adobe Commerce sur l’infrastructure cloud ou l’application. Les dernières valeurs par défaut se trouvent dans le [référentiel GitHub magento-cloud](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Toujours vérifier les valeurs contenues dans [.magento.app.yaml](../application/configure-app-yaml.md) fichier pour la version installée, car il contrôle la manière dont votre application se crée et se déploie sur l’infrastructure cloud. L’exemple suivant concerne la version 2.4.7 et utilise le compositeur 2.7.2. Le `build: flavor:` La propriété n’est pas utilisée pour le compositeur 2.x ; voir [Installation et utilisation du compositeur 2](../application/properties.md#installing-and-using-composer-2).

**Pour mettre à jour le `.magento.app.yaml` fichier**:

1. Sur votre station de travail locale, accédez au répertoire du projet.

1. Ouvrez et modifiez le `magento.app.yaml` fichier .

1. Mettez à jour les options PHP.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Modifier le `hooks` propriété `build` et `deploy` commandes.

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

1. Ajoutez les variables d’environnement suivantes à la fin du fichier .

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

1. Enregistrez le fichier. Ne validez pas et n’envoyez pas encore les modifications à l’environnement distant.

1. Poursuivez le processus de mise à niveau.

### composer.json

Avant la mise à niveau, vérifiez toujours que les dépendances dans le `composer.json` Les fichiers sont compatibles avec la version Adobe Commerce.

**Pour mettre à jour le `composer.json` fichier pour Adobe Commerce version 2.4.4 et ultérieure**:

1. Ajoutez les éléments suivants : `allow-plugins` vers le `config` section :

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

1. Enregistrez le fichier. Ne validez pas et ne transmettez pas encore les modifications à votre branche.

1. Poursuivez le processus de mise à niveau.

## Sauvegarde du projet

Nous vous recommandons de créer une sauvegarde de votre projet avant une mise à niveau. Suivez les étapes ci-après pour sauvegarder vos environnements d’intégration, d’évaluation et de production.

**Pour sauvegarder la base de données et le code de votre environnement d’intégration**:

1. Créez une sauvegarde locale de la base de données distante.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Le `magento-cloud db:dump` La commande exécute le [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) avec la commande `--single-transaction` indicateur , qui permet de sauvegarder la base de données sans verrouiller les tables.

1. Sauvegardez le code et le média.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Vous pouvez éventuellement omettre `[--media]` si vous avez un grand nombre de fichiers statiques qui se trouvent déjà dans le contrôle de code source.

**Pour sauvegarder la base de données de l’environnement d’évaluation ou de production avant le déploiement**:

1. Utilisez SSH pour vous connecter à l’environnement distant.

1. Création d’un [vidage de base de données](../storage/database-dump.md). Pour choisir un répertoire cible pour l’image mémoire de la base de données, utilisez `--dump-directory` option.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   L’opération de vidage crée une `dump-<timestamp>.sql.gz` archivez le fichier dans votre répertoire de projet distant. Voir [Sauvegarde de la base de données](../storage/database-dump.md).

## Mise à niveau de l’application

Vérifier le [versions de service](../services/services-yaml.md#service-versions) informations sur les dernières exigences en matière de version logicielle avant la mise à niveau de votre application.

**Pour mettre à niveau la version de l’application**:

1. Sur votre station de travail locale, accédez au répertoire du projet.

1. Définissez la version de mise à niveau à l’aide de [syntaxe de contrainte de version](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Vous devez utiliser la syntaxe de contrainte de version pour mettre à jour le `ece-tools` package. La contrainte de version est disponible dans `composer.json` fichier pour la version de [modèle d&#39;application](https://github.com/magento/magento-cloud/blob/master/composer.json) vous utilisez pour la mise à niveau.

1. Mettez à jour le projet.

   ```bash
   composer update
   ```

1. Ajout, validation et modifications de code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` est nécessaire pour ajouter tous les fichiers modifiés au contrôle de code source en raison de la manière dont le compositeur marshale les packages de base. Les deux `composer install` et `composer update` rassembler les fichiers du package de base (`magento/magento2-base` et `magento/magento2-ee-base`) dans la racine du package.

   Les fichiers que le compositeur marshale appartiennent à la nouvelle version d’Adobe Commerce, afin de remplacer la version obsolète de ces mêmes fichiers. Actuellement, le marshalling est désactivé dans Adobe Commerce, vous devez donc ajouter les fichiers marshalés au contrôle de code source.

1. Attendez la fin du déploiement.

1. Vérifiez la mise à niveau dans votre environnement d’intégration, d’évaluation ou de production à l’aide de SSH pour vous connecter et vérifier la version.

   ```bash
   php bin/magento --version
   ```

### Créer un fichier config.php

Comme mentionné dans [Gestion de la configuration](#configuration-management), après la mise à niveau, vous devez créer une mise à jour `config.php` fichier . Effectuez toutes les modifications de configuration supplémentaires via l’Administration dans votre environnement d’intégration.

**Pour créer un fichier de configuration spécifique au système**:

1. À partir du terminal, utilisez une commande SSH pour générer le `/app/etc/config.php` pour l’environnement.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Par exemple, pour Pro, pour exécuter le `scd-dump` le `integration` branche :

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Transférer le `config.php` fichier sur vos stations de travail locales à l’aide de `rsync` ou `scp`. Vous pouvez uniquement ajouter ce fichier à la branche localement.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Ajout, validation et modifications de code push.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Cela génère une mise à jour `/app/etc/config.php` avec une liste de modules et des paramètres de configuration.

>[!WARNING]
>
>Pour une mise à niveau, vous devez supprimer le `config.php` fichier . Une fois ce fichier ajouté à votre code, vous devez : **non** Supprimez-le. Si vous devez supprimer ou modifier des paramètres, modifiez le fichier manuellement.

### Mettre à niveau les extensions

Passez en revue vos pages d’extension et de module tiers sur la Marketplace ou d’autres sites d’entreprise et vérifiez la prise en charge d’Adobe Commerce et d’Adobe Commerce sur l’infrastructure cloud. Si vous devez mettre à niveau des extensions et modules tiers, Adobe recommande de travailler dans une nouvelle branche d’intégration avec vos extensions désactivées.

**Pour vérifier et mettre à niveau vos extensions**:

1. Créez une branche sur votre station de travail locale.

1. Désactivez vos extensions selon vos besoins.

1. Lorsqu’elles sont disponibles, téléchargez les mises à niveau d’extension.

1. Installez la mise à niveau comme indiqué dans la documentation tierce.

1. Activez et testez l’extension.

1. Ajoutez, validez et envoyez les modifications de code à la télécommande.

1. Envoyez et testez dans votre environnement d’intégration.

1. Effectuez un transfert vers l’environnement d’évaluation pour effectuer des tests dans un environnement de pré-production.

Adobe recommande vivement de mettre à niveau votre environnement de production _avant_ inclusion des extensions mises à niveau dans le processus de lancement de votre site.

>[!NOTE]
>
>Lorsque vous mettez à niveau votre version de l’application, le processus de mise à niveau se met à jour vers la dernière version de [Module Fast CDN](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatiquement.

## Résolution des problèmes de mise à niveau

Si la mise à niveau a échoué, vous recevez un message d’erreur dans le navigateur indiquant que vous ne pouvez pas accéder à votre storefront ou au panneau d’administration :

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Pour résoudre l’erreur**:

1. Sur votre station de travail locale, accédez au répertoire du projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Ouvrez le . `./app/var/report/<error number>` fichier .

1. [Examiner les logs](../test/log-locations.md) et déterminez la source du problème.

1. Ajout, validation et modifications de code push.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
