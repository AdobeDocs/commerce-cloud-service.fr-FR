---
title: Mettre à niveau le projet pour utiliser les outils de la CEE
description: Découvrez comment mettre à niveau votre projet Adobe Commerce sur l'infrastructure cloud pour utiliser le package ECE-Tools et tirer parti des derniers correctifs et fonctionnalités.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: bcdb59f0d2a17e55e8b0479ee69fac06c710638f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Mise à niveau du projet pour utiliser le package ECE-Tools

Adobe de l’obsolescence de `magento/magento-cloud-configuration` et `magento/ece-patches` packages en faveur de la `ece-tools` , qui simplifie de nombreux processus cloud. Si vous utilisez un ancien projet d’infrastructure cloud Adobe Commerce qui : _non_ contiennent les éléments suivants : `ece-tools` package, puis vous devez effectuer une opération manuelle unique _mettre à niveau_ à votre projet.

>[!WARNING]
>
>Si votre projet contient le `ece-tools` , vous pouvez ignorer la mise à niveau suivante. Pour vérifier, récupérez le [!DNL Commerce] version utilisant `php vendor/bin/ece-tools -V` dans votre répertoire racine de projet local.

Ce processus de mise à niveau du projet nécessite la mise à jour du `magento/magento-cloud-metapackage` contrainte de version dans `composer.json` dans le répertoire racine. Cette contrainte permet de mettre à jour Adobe Commerce sur les métapaquets d’infrastructure cloud (y compris la suppression des packages obsolètes) sans mettre à niveau votre version actuelle d’Adobe Commerce.

{{upgrade-tip}}

## Supprimer les packages obsolètes

Avant d’effectuer une mise à niveau pour utiliser `ece-tools` package, vérifiez le `composer.lock` fichier pour les packages obsolètes suivants :

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Mettre à jour le métapaquet

Chaque version d’Adobe Commerce nécessite une contrainte différente basée sur les éléments suivants :

```terminal
>=current_version <next_version
```

- Pour `current_version`, spécifiez la version d’Adobe Commerce à installer.
- Pour `next_version`, spécifiez la version de correctif suivante après la valeur spécifiée dans `current_version`.

Pour installer Adobe Commerce : `2.3.5-p2`, set `current_version` vers `2.3.5` et le `next_version` vers `2.3.6`. La contrainte `">=2.3.5 <2.3.6"` installe le dernier package disponible pour 2.3.5.

Vous pouvez toujours trouver la dernière contrainte de métapaquet dans le [`magento-cloud` modèle](https://github.com/magento/magento-cloud/blob/master/composer.json).

L’exemple suivant place une contrainte pour le métapaquet Adobe Commerce sur l’infrastructure cloud sur toute version supérieure ou égale à la version actuelle 2.4.7 et inférieure à la version suivante 2.4.8 :

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Mettre à niveau le projet

Pour mettre à niveau votre projet afin d’utiliser le `ece-tools` , vous devez mettre à jour le métapaquet et le `.magento.app.yaml` connecte les propriétés et effectue une mise à jour du compositeur ;

**Pour mettre à niveau le projet afin d’utiliser les outils électroniques**:

1. Mettre à jour `magento/magento-cloud-metapackage` contrainte de version dans `composer.json` fichier .

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Mettez à jour le métapaquet .

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Modifier les commandes de hook dans `magento.app.yaml` fichier .

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

1. Recherchez et supprimez [packages obsolètes](#remove-deprecated-packages). Les packages obsolètes peuvent empêcher une mise à niveau réussie.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Il peut être nécessaire de mettre à jour le `ece-tools` package.

   ```bash
   composer update magento/ece-tools
   ```

1. Ajouter et valider les modifications de code. Dans cet exemple, les fichiers suivants ont été mis à jour :

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Envoyez vos modifications de code au serveur distant et fusionnez cette branche avec le `integration` branche.

   ```bash
   git push origin <branch-name>
   ```
