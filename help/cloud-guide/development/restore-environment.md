---
title: Restaurer un environnement
description: Découvrez comment désinstaller l’application Adobe Commerce à partir d’un projet d’infrastructure cloud et restaurer un environnement à un état stable.
role: Developer
topic: Development
exl-id: b76bd6c3-986e-4adc-abd0-5b27db0d8a3b
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Restaurer un environnement

Si vous rencontrez des problèmes dans l’environnement d’intégration et que vous ne disposez pas d’une [sauvegarde valide](../storage/snapshots.md), essayez de restaurer votre environnement à l’aide de l’une des méthodes suivantes :

- Réinitialiser ou rétablir le code dans la branche Git
- Désinstallation de l’application [!DNL Commerce]
- Forcer un redéploiement
- Réinitialisation manuelle de la base de données

{{stuck-deployment-tip}}

## Réinitialisation de la branche Git

La réinitialisation de votre branche Git rétablit l’état stable du code par le passé.

**Pour réinitialiser votre branche** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Examinez l’historique de validation Git. Utilisez `--oneline` pour afficher les validations abrégées sur une ligne :

   ```bash
   git log --oneline
   ```

   Exemple de réponse :

   ```
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Choisissez un hachage de validation qui représente le dernier état stable connu de votre code.

   Pour réinitialiser votre branche à son état initialisé d’origine, recherchez la première validation qui a créé votre branche. Vous pouvez utiliser `--reverse` pour afficher l’historique dans l’ordre chronologique inverse.

1. Utilisez l’option hard reset pour réinitialiser votre branche. Faites attention en utilisant cette commande, car elle ignore toutes les modifications depuis la validation choisie.

   ```bash
   git reset --hard <commit>
   ```

1. Envoyez vos modifications pour déclencher un redéploiement qui réinstalle Adobe Commerce.

   ```bash
   git push --force <origin> <branch>
   ```

## Désinstallation de Commerce

La désinstallation de l’application [!DNL Commerce] renvoie votre environnement à l’état d’origine en restaurant la base de données, en supprimant la configuration de déploiement et en effaçant les sous-répertoires `var/`. Cette directive réinitialise également votre branche git à un état stable antérieur. Si vous ne disposez pas d’une sauvegarde récente, mais que vous pouvez accéder à l’environnement distant à l’aide de SSH, procédez comme suit pour restaurer votre environnement :

- Désactivation de la gestion de la configuration
- Désinstallation d’Adobe Commerce
- Réinitialisation de la branche git

La désinstallation du logiciel Adobe Commerce supprime et restaure la base de données, supprime la configuration de déploiement et efface les sous-répertoires `var/`. Il est important de désactiver la [gestion de la configuration](../store/store-settings.md) afin qu’elle n’applique pas automatiquement les paramètres de configuration précédents lors du prochain déploiement. Assurez-vous que votre répertoire `app/etc/` ne contient pas le fichier `config.php`.

**Pour désinstaller le logiciel Adobe Commerce** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Supprimez le fichier de configuration.
   - Pour Adobe Commerce 2.2 et versions ultérieures :

     ```bash
     rm app/etc/config.php
     ```

   - Pour Adobe Commerce 2.1 :

     ```bash
     rm app/etc/config.local.php
     ```

1. Désinstallez l’application Adobe Commerce.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Vérifiez que Adobe Commerce a bien été désinstallé.

   Le message suivant s’affiche pour confirmer la désinstallation :

   ```
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Effacez les sous-répertoires `var/`.

   ```bash
   rm -rf var/*
   ```

1. Déconnectez-vous.

>[!TIP]
>
>En option, il est recommandé de nettoyer les caches de version.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Forcer un redéploiement

Si vous avez tenté de désinstaller Adobe Commerce et que votre déploiement continue d’échouer, vous pouvez essayer de forcer manuellement un redéploiement.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## Réinitialiser la base de données

Si vous avez tenté de désinstaller Adobe Commerce et que la commande a échoué ou n’a pas pu être effectuée, vous pouvez réinitialiser manuellement la base de données.

**Pour réinitialiser la base de données** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Connexion à la base de données.

   ```bash
   mysql -h database.internal
   ```

1. Déposez la base de données `main`.

   ```shell
   drop database main;
   ```

1. Créez une base de données `main` vide.

   ```shell
   create database main;
   ```

1. Supprimez les fichiers de configuration suivants.

   - `config.php`
   - `config.php.bak`
   - `env.php`
   - `env.php.bak`

1. Déconnectez-vous et déclenchez un redéploiement.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
