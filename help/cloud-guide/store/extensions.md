---
title: Gestion des extensions
description: Découvrez comment installer et gérer des extensions dans Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Extensions, Upgrade
exl-id: 9c6e98ca-85da-4342-8402-d576eb382ba2
source-git-commit: f8fb9d4d43c85f91ff87686160bcddb7cd417635
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Gestion des extensions

Vous pouvez étendre les fonctionnalités de votre application Adobe Commerce en ajoutant une extension du [Commerce Marketplace](https://marketplace.magento.com). Par exemple, vous pouvez ajouter un thème pour modifier l’aspect de votre vitrine, ou vous pouvez ajouter un module de langue pour localiser votre vitrine et votre administrateur.

>[!NOTE]
>
>Pour éviter des problèmes d’installation, tous les achats Marketplace doivent être effectués à l’aide du même compte (MAGEID) propriétaire du projet cloud.

## Nom du compositeur d’une extension

Bien que cette section explique comment obtenir le nom et la version du compositeur d’une extension depuis Commerce Marketplace, vous trouverez le nom et la version du module _any_ dans le fichier du compositeur du module. Ouvrez le fichier `composer.json` dans un éditeur de texte et notez les valeurs `"name"` et `"version"` .

**Pour obtenir le nom du compositeur d’un module à partir du Commerce Marketplace** :

1. Connectez-vous à [Commerce Marketplace](https://marketplace.magento.com) avec le nom d’utilisateur et le mot de passe que vous avez utilisés pour acheter le composant.

1. Dans le coin supérieur droit, cliquez sur votre nom d’utilisateur et sélectionnez **Mon profil**.

   ![Accéder à votre compte Marketplace](../../assets/marketplace/my-profile.png)

1. Sur la page _Mon compte_, cliquez sur **Mes achats**.

   ![Historique des achats Marketplace](../../assets/marketplace/my-purchases.png)

1. Sur la page _Mes achats_, sélectionnez un module que vous avez acheté, puis cliquez sur **Détails techniques**.

1. Cliquez sur **Copier** pour copier l’ [!UICONTROL Component name] dans le Presse-papiers.

1. Ouvrez un éditeur de texte, collez le nom du composant et ajoutez un caractère deux-points (`:`).

1. Dans **Technical Details**, cliquez sur **Copier** pour copier l’élément [!UICONTROL Component version] dans le Presse-papiers.

1. Dans l’éditeur de texte, ajoutez le numéro de version au nom du composant après le signe deux-points. Par exemple :

   ```text
   extension-name/magento2:1.0.1
   ```

## Installer une extension

Adobe recommande de travailler dans une branche de développement lors de l’ajout d’une extension à votre mise en oeuvre. Lors de l’installation d’une extension, le nom de l’extension (`<VendorName>_<ComponentName>`) est automatiquement inséré dans le fichier [`app/etc/config.php`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html). Il n’est pas nécessaire de modifier directement le fichier.

**Pour installer une extension** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Créez ou extrayez une branche de développement. Voir [branchement](../development/cli-branches.md).

1. À l’aide du nom et de la version du compositeur, ajoutez l’extension à la section `require` du fichier `composer.json`.

   ```bash
   composer require <extension-name>:<version> --no-update
   ```

1. Mettez à jour les dépendances du projet.

   ```bash
   composer update
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install <extension-name>"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!WARNING]
   >
   >Lors de l’installation d’une extension, vous devez inclure le fichier `composer.lock` lorsque vous poussez les modifications de code dans l’environnement distant. La commande `composer install` lit le fichier `composer.lock` pour activer les dépendances définies dans l’environnement distant.

1. Une fois la création et le déploiement terminés, utilisez un SSH pour vous connecter à l’environnement distant et vérifier que l’extension est installée.

   ```bash
   bin/magento module:status <extension-name>
   ```

   Un nom d’extension utilise le format : `<VendorName>_<ComponentName>`.

   Exemple de réponse :

   ```terminal
   Module is enabled
   ```

   Si vous rencontrez des erreurs de déploiement, reportez-vous à la section [échec du déploiement de l&#39;extension](../deploy/recover-failed-deployment.md).

## Gestion des extensions

Lorsque vous ajoutez une extension à l’aide de Composer, le processus de déploiement active automatiquement l’extension. Si l’extension est déjà installée, vous pouvez l’activer ou la désactiver à l’aide de l’interface de ligne de commande. Lors de la gestion des extensions, utilisez le format : `<VendorName>_<ComponentName>`

Ne jamais activer ou désactiver une extension lors de la connexion aux environnements distants.

**Pour activer ou désactiver une extension** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Activez ou désactivez un module. La commande `module` met à jour le fichier `config.php` avec l’état demandé du module.

   >Activez un module.

   ```bash
   bin/magento module:enable <module-name>
   ```

   >Désactivez un module.

   ```bash
   bin/magento module:disable <module-name>
   ```

1. Si vous avez activé un module, utilisez `ece-tools` pour actualiser la configuration.

   ```bash
   ./vendor/bin/ece-tools module:refresh
   ```

1. Vérifiez l’état d’un module.

   ```bash
   bin/magento module:status <module-name>
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Disable <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

## Mettre à niveau une extension

Avant de poursuivre, vous avez besoin du nom et de la version du compositeur pour l’extension. Vérifiez également que l’extension est compatible avec votre projet et la version d’Adobe Commerce. En particulier, [vérifiez la version PHP requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) avant de commencer.

**Pour mettre à jour une extension** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Créez ou extrayez une branche de développement. Voir [branchement](../development/cli-branches.md).

1. Ouvrez le fichier `composer.json` dans un éditeur de texte.

1. Recherchez votre extension et mettez à jour la version.

1. Enregistrez vos modifications et quittez l’éditeur de texte.

1. Mettez à jour les dépendances du projet.

   ```bash
   composer update
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

Si vous rencontrez des erreurs, reportez-vous à la section [Récupération de l’échec du composant](../deploy/recover-failed-deployment.md). Pour plus d’informations sur l’utilisation des extensions avec Adobe Commerce, voir [Extensions](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/extensions.html) dans le _Guide de l’administrateur_.
