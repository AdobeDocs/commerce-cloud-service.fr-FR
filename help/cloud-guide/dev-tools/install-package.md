---
title: Mettre à niveau le projet à l’aide des outils CEE-ONU
description: Découvrez comment mettre à niveau votre projet Adobe Commerce sur l’infrastructure cloud pour utiliser le package CEE-Outils et tirer parti des correctifs et fonctionnalités les plus récents.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Mettre à niveau le projet pour utiliser le package CEE-Outils

Adobe a abandonné les packages `magento/magento-cloud-configuration` et `magento/ece-patches` au profit du package `ece-tools`, ce qui simplifie de nombreux processus cloud. Si vous utilisez un projet d’infrastructure de cloud Adobe Commerce plus ancien qui ne contient _pas_ le package `ece-tools`, vous devez exécuter un processus manuel de _mise à niveau_ unique sur votre projet.

>[!WARNING]
>
>Si votre projet contient le package `ece-tools`, vous pouvez ignorer la mise à niveau suivante. Pour vérifier, récupérez la version [!DNL Commerce] à l’aide de la commande `php vendor/bin/ece-tools -V` dans le répertoire racine de votre projet local.

Ce processus de mise à niveau de projet nécessite que vous mettiez à jour la contrainte de version `magento/magento-cloud-metapackage` dans le fichier `composer.json` situé dans le répertoire racine. Cette contrainte active les mises à jour d’Adobe Commerce sur les modules d’infrastructure cloud (notamment la suppression des modules obsolètes) sans mettre à niveau votre version Adobe Commerce actuelle.

{{upgrade-tip}}

## Suppression de modules obsolètes

Avant d&#39;effectuer une mise à niveau pour utiliser le package `ece-tools`, vérifiez que le fichier `composer.lock` contient les packages obsolètes suivants :

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Mettre à jour le métappackage

Chaque version d’Adobe Commerce nécessite une contrainte différente basée sur les éléments suivants :

```
>=current_version <next_version
```

- Pour `current_version`, spécifiez la version Adobe Commerce à installer.
- Pour `next_version`, spécifiez la version de correctif suivante après la valeur spécifiée dans `current_version`.

Si vous souhaitez installer Adobe Commerce `2.3.5-p2`, définissez `current_version` sur `2.3.5` et `next_version` sur `2.3.6`. La contrainte `">=2.3.5 <2.3.6"` installe le dernier package disponible pour 2.3.5.

Vous pouvez toujours trouver la dernière contrainte de mise en forme de métappackage dans le modèle [`magento-cloud`](https://github.com/magento/magento-cloud/blob/master/composer.json).

L’exemple suivant place une contrainte pour Adobe Commerce sur le métappackage d’infrastructure cloud à toute version supérieure ou égale à la version actuelle 2.4.7 et inférieure à la version suivante 2.4.8 :

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Mettre à niveau le projet

Pour mettre à niveau votre projet afin d’utiliser le package `ece-tools`, vous devez mettre à jour le métapackage et les propriétés des hooks `.magento.app.yaml` et effectuer une mise à jour du compositeur.

**Pour mettre à niveau un projet afin d’utiliser les outils de l’environnement de travail citoyen** :

1. Mettez à jour la contrainte de version `magento/magento-cloud-metapackage` dans le fichier `composer.json`.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Mettez à jour le métapaquet.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Modifiez les commandes de crochet dans le fichier `magento.app.yaml`.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Recherchez et supprimez les [packages obsolètes](#remove-deprecated-packages). Les packages obsolètes peuvent empêcher une mise à niveau réussie.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Il peut être nécessaire de mettre à jour le package `ece-tools`.

   ```bash
   composer update magento/ece-tools
   ```

1. Ajoutez et validez les modifications du code. Dans cet exemple, les fichiers suivants ont été mis à jour :

   ```
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Poussez vos modifications de code sur le serveur distant et fusionnez cette branche avec la branche `integration`.

   ```bash
   git push origin <branch-name>
   ```
