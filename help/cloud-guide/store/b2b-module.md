---
title: Activation du module B2B
description: Découvrez comment activer le module business-to-business pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Activation du module B2B

Si vos clients sont des entreprises, vous pouvez installer le module B2B pour Adobe Commerce afin d’étendre votre projet Adobe Commerce sur l’infrastructure cloud Pro pour l’adapter à un modèle business-to-business. Bien que cette rubrique fournisse des informations spécifiques à l’installation et à la configuration du module B2B pour Adobe Commerce sur l’infrastructure cloud, vous trouverez des informations B2B supplémentaires dans les guides suivants :

- [Guide du développeur d’Adobe Commerce B2B](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Guide de l’utilisateur d’Adobe Commerce B2B](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Dans la mesure où B2B est un module d’Adobe Commerce sur l’infrastructure cloud, Adobe vous recommande de déployer votre application Adobe Commerce dans un environnement d’intégration ou d’évaluation avant de commencer.

## Installation du module B2B

Adobe recommande de travailler dans une branche de développement lors de l’ajout du module B2B à votre projet. Si vous ne disposez pas d’une branche, voir [Création d’une branche pour le développement](../development/cli-branches.md#create-a-branch-for-development). Lors de l’installation du module B2B, la variable `Magento_B2b` Le nom du module est automatiquement inséré dans la fonction `app/etc/config.php` fichier . Il n’est pas nécessaire de modifier directement le fichier.

**Pour installer le module B2B**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Créez ou extrayez une branche de développement.

1. Ajoutez le module B2B au `require` de la `composer.json` fichier .

   ```bash
   composer require magento/extension-b2b --no-update
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
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Une fois la création et le déploiement terminés, utilisez SSH pour vous connecter à l’environnement distant et vérifier que le module B2B est installé.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   Un nom d’extension utilise le format suivant : `<VendorName>_<ComponentName>`.

   Exemple de réponse :

   ```terminal
   Magento_B2b : Module is enabled
   ```

   Si vous rencontrez des erreurs de déploiement, voir [Récupération de l’échec du composant](../deploy/recover-failed-deployment.md).

## Activation du module B2B

Lorsque vous installez le module B2B à l’aide du compositeur, le processus de déploiement active automatiquement le module. Si le module B2B est déjà installé, vous pouvez activer ou désactiver ce module à l’aide de l’interface en ligne de commande.

Activez le module B2B :

```bash
bin/magento module:enable Magento_B2b
```

Exemple de réponse :

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

Voir [Gestion des extensions](extensions.md).

## Configuration du module B2B

Après avoir installé le module B2B pour Adobe Commerce, vous devez [Démarrez le message aux consommateurs](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) pour activer la variable _Catalogue partagé_ et vous devez [activation des fonctionnalités B2B](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
