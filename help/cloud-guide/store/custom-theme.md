---
title: Thème personnalisé
description: Découvrez comment installer un thème personnalisé avec Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Themes
exl-id: f08134ab-daea-471d-a927-02531d36a809
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Thème personnalisé

Vous pouvez installer un ou plusieurs thèmes à utiliser pour l’un ou l’ensemble de vos magasins et sites dans votre projet. Les thèmes comprennent plusieurs fichiers statiques, notamment des images, des polices, des fichiers CSS, JavaScript, PHP, etc., pour concevoir entièrement vos magasins. Vous pouvez ajouter le thème en extrayant son code dans le système de fichiers ou à l’aide du compositeur.

## Installer manuellement un thème

Pour installer manuellement un thème, vous devez disposer du code du thème dans une archive compressée ou dans une structure de répertoire similaire à celle-ci :

```text
<VendorName>
  ├── composer.json
      ├── etc
      │   └── view.xml
      ├── media
      ├── registration.php
      ├── theme.xml
      └── web
          ├── css
          │   └── source
          ├── fonts
          ├── images
          └── js
```

**Pour installer un thème manuellement** :

1. Copiez le code du thème sous `<Project root dir>/app/design/frontend` pour un thème de vitrine ou `<Project root dir>/app/design/adminhtml` pour un thème d’administrateur. Vérifiez que le répertoire de niveau supérieur est `<VendorName>` ; dans le cas contraire, le thème ne s’installe pas correctement.

   ```bash
   cp -r ExampleTheme <project-root>/app/design/frontend
   ```

1. Confirmez que le thème est copié au bon endroit.

   * Thème Storefront : `ls <project-root>/app/design/frontend`
   * Thème d’administration : `ls <project-root>/app/design/adminhtml`

   Voici un exemple :

   ExempleThème Adobe Commerce

1. Ajoutez et validez des fichiers.

   ```bash
   git add -A && git commit -m "Add theme"
   ```

1. Placez les fichiers dans votre branche.

   ```bash
   git push origin <branch name>
   ```

1. Attendez que le déploiement soit terminé.
1. Connectez-vous à l’administrateur.
1. Cliquez sur **Contenu** > Conception > **Thèmes**.

   Le thème s’affiche dans le volet de droite.

## Installation d’un thème à l’aide du compositeur

L’installation d’un thème à l’aide du compositeur est identique à l’installation de toute autre extension à l’aide du compositeur. Voir [Installation, gestion et mise à niveau des modules](extensions.md) pour plus d’informations.

Pour installer un thème à l’aide du compositeur :

1. Achetez le thème à partir du Commerce Marketplace .
1. Obtenez le nom du compositeur du thème.
1. Modifiez le répertoire racine Adobe Commerce et saisissez la commande :

   ```bash
   composer require <vendor>/<name>:<version>
   ```

   Par exemple,

   ```bash
   composer require zero1/theme-fashionista-theme:1.0.0
   ```

1. Attendez la mise à jour des dépendances.
1. Saisissez les commandes suivantes :

   ```bash
   git add -A && git commit -m "Add theme"
   ```

   ```bash
   git push origin <branch name>
   ```

1. Connectez-vous à l’administrateur.
1. Cliquez sur **Contenu** > Conception > **Thèmes**.

   Le thème s’affiche dans le volet de droite.

## Thèmes multiples

Lors de l’utilisation de plusieurs thèmes, tels que différents thèmes par langue, passez en revue la variable d’environnement `SCD_MATRIX` pour personnaliser le déploiement des thèmes. Voir les étapes [build](../environment/variables-build.md#scd_matrix) ou [deploy](../environment/variables-deploy.md#scd_matrix) dans la [configuration d&#39;environnement](../environment/configure-env-yaml.md).
