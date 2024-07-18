---
title: Gestion des sauvegardes
description: Découvrez comment créer et restaurer manuellement une sauvegarde pour votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Gestion des sauvegardes

Vous pouvez effectuer une sauvegarde manuelle des environnements de démarrage actifs à tout moment à l’aide du bouton **[!UICONTROL Backup]** dans [!DNL Cloud Console] ou à l’aide de la commande `magento-cloud snapshot:create`.

Une sauvegarde ou _instantané_ est une sauvegarde complète des données de l’environnement qui inclut toutes les données persistantes des services en cours d’exécution (base de données MySQL) et tous les fichiers stockés sur les volumes montés (var, pub/media, app/etc). L’instantané n’inclut _pas_ du code, puisque le code est déjà stocké dans le référentiel basé sur Git. Vous ne pouvez pas télécharger une copie d’un instantané.

La fonction de sauvegarde/instantané ne s’applique **pas** aux environnements d’évaluation et de production Pro, qui reçoivent par défaut des sauvegardes régulières à des fins de reprise après sinistre. Pour plus d’informations, voir [Sauvegarde et reprise sur sinistre Pro](../architecture/pro-architecture.md#backup-and-disaster-recovery) . Contrairement aux sauvegardes en direct automatiques sur les environnements d’évaluation et de production Pro, les sauvegardes sont **et non** automatiques. Il est de _votre responsabilité de créer manuellement une sauvegarde ou de configurer une tâche cron afin de créer périodiquement une sauvegarde de vos environnements d’intégration Starter ou Pro._

## Création d’une sauvegarde manuelle

Vous pouvez créer une sauvegarde manuelle de n’importe quel environnement Starter actif et environnement Integration Pro à partir de [!DNL Cloud Console] ou créer un instantané à partir de l’interface de ligne de commande de Cloud. Vous devez disposer d’un [rôle d’administrateur](../project/user-access.md) pour l’environnement.

**Pour créer une sauvegarde de tout environnement de lancement à l’aide de[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Sélectionnez un environnement dans la barre de navigation du projet. L’environnement doit être actif.
1. Dans la vue _Sauvegardes_, cliquez sur **[!UICONTROL Backup]**. Cette option n’est pas disponible pour un environnement Pro.

   ![Sauvegarde](../../assets/button-backup.png){width="150"}

**Pour créer une sauvegarde d’un environnement d’intégration à l’aide de[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Sélectionnez un environnement d’intégration/de développement dans la barre de navigation du projet. L’environnement doit être actif.
1. Sélectionnez l’option **[!UICONTROL Backup]** dans le menu supérieur droit. Cette option est disponible pour les environnements Starter et Pro.
1. Cliquez sur le bouton **[!UICONTROL Yes]** .

**Pour créer un instantané à l’aide de l’interface de ligne de commande `magento-cloud`** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.
1. Consultez la branche d’environnement pour obtenir un instantané.
1. Créez l’instantané.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Vous pouvez également utiliser la commande courte `magento-cloud backup`. L’option `--live` laisse l’environnement en cours d’exécution pour éviter les temps d’arrêt. Pour obtenir la liste complète des options, saisissez `magento-cloud snapshot:create --help`.

   Exemple de réponse :

   ```
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Vérifiez les instantanés les plus récents.

   ```bash
   magento-cloud snapshot:list
   ```

   La liste renvoie des informations sur l’état de l’instantané :

   ```
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Restauration d’une sauvegarde manuelle

Vous devez disposer de l’ [accès administrateur](../project/user-access.md) à l’environnement. Vous avez jusqu&#39;à **sept jours** pour _restaurer_ une sauvegarde manuelle. La restauration d’une sauvegarde ne modifie pas le code de la branche git actuelle. La restauration d’une sauvegarde de cette manière ne s’applique pas aux environnements d’évaluation et de production Pro ; voir [Sauvegarde et reprise sur sinistre Pro](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Les délais de restauration varient en fonction de la taille de votre base de données :

- une base de données volumineuse (200 Go ou plus) peut prendre 5 heures.
- La base de données moyenne (150 Go) peut prendre 2 heures et demie
- La petite base de données (60 Go) peut prendre 1 heure

>[!TIP]
>
>Restauration sans sauvegarde :
>
>- Pour restaurer le code précédent ou supprimer les extensions ajoutées dans un environnement, voir [Restaurer le code](#roll-back-code).
>- Pour restaurer un environnement instable qui _n&#39;a pas_ de sauvegarde, voir [Restaurer un environnement](../development/restore-environment.md).

**Pour restaurer une sauvegarde à l’aide de[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Sélectionnez un environnement dans la barre de navigation du projet.
1. Dans la vue _Sauvegardes_, choisissez une sauvegarde dans la liste _Stockée_. La fonction de sauvegarde ne s’applique pas **aux environnements Pro.**
1. Dans le menu ![Plus](../../assets/icon-more.png){width="32"} (_plus_), cliquez sur **Restaurer**.
1. Passez en revue les informations Restaurer à partir de la sauvegarde et cliquez sur **Oui, restaurer**.

**Pour restaurer un instantané à l’aide de l’interface de ligne de commande de Cloud** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.
1. Extrayez la branche d’environnement à restaurer.
1. Répertorier tous les instantanés disponibles.

   ```bash
   magento-cloud snapshot:list
   ```

   La liste renvoie des informations sur les instantanés disponibles :

   ```
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Restaurez un instantané à l’aide de l’ID d’instantané de la liste.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Restauration d’un instantané de reprise sur sinistre

Pour restaurer l’instantané de reprise sur sinistre dans les environnements d’évaluation et de production Pro, [Importez le vidage de base de données directement à partir du serveur](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3).

## Restaurer le code

Les sauvegardes et les instantanés incluent _not_ une copie de votre code. Votre code est déjà stocké dans le référentiel basé sur Git. Vous pouvez donc utiliser des commandes basées sur Git pour restaurer (ou rétablir) le code. Par exemple, utilisez `git log --oneline` pour parcourir les validations précédentes, puis utilisez [`git revert`](https://git-scm.com/docs/git-revert) pour restaurer le code à partir d’une validation spécifique.

Vous pouvez également choisir de stocker le code dans une branche _inactive_. Utilisez des commandes git pour créer une branche au lieu d’utiliser des commandes `magento-cloud`. Voir à propos des [commandes Git](../dev-tools/cloud-cli-overview.md#git-commands) dans la rubrique d’interface de ligne de commande Cloud.
