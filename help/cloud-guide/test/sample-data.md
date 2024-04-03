---
title: Exemples de données
description: Découvrez comment installer des exemples de données avec Adobe Commerce sur l’infrastructure cloud.
exl-id: 517e549f-15ba-47b3-9236-a1c4d24c917d
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Exemples de données

Si vous avez besoin de données d’exemple lors du développement de votre magasin, vous pouvez installer des données d’exemple. Ces données simulent un magasin Adobe Commerce actif avec des clients, des produits et d’autres données. Ces exemples de données fonctionnent mieux avec une nouvelle installation de modèle d’infrastructure cloud Adobe Commerce.

Il est recommandé d’installer des exemples de données dans les environnements de développement et d’intégration. Si vous utilisez des données d’exemple dans l’évaluation ou la production, vous devez [remove](#reset-or-uninstall-sample-data) les informations et les produits avant leur mise en ligne.

## Installer des exemples de données

Pour installer des exemples de données :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. À la racine, saisissez la commande suivante pour ajouter des exemples de données :

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Attendez la mise à jour des composants.

1. Validez et envoyez les modifications :

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Attendez que le projet soit déployé.

1. Vérifiez que l’installation a réussi en accédant à la page de storefront de l’environnement d’intégration. Vous pouvez localiser le lien de l’URL vers le storefront à l’aide du [!DNL Cloud Console].

1. Prenez un instantané de votre environnement :

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

Vous pouvez commencer à tester votre développement à l’aide de données en direct.

## Réinitialisation ou désinstallation d’exemples de données

Vous pouvez réinitialiser ou supprimer des données d’exemple selon la même procédure que celle utilisée pour installer les données d’exemple :

- Supprimer les exemples de données : `./bin/magento sampledata:remove`
- Réinitialiser les données d’exemple : `./bin/magento sampledata:reset`
