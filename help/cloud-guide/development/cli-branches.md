---
title: Gestion des branches à l’aide de l’interface de ligne de commande
description: Découvrez comment gérer les branches d’environnement pour Adobe Commerce sur l’infrastructure cloud à l’aide de l’interface de ligne de commande de Cloud.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Gestion des branches à l’aide de l’interface de ligne de commande

Pour installer le `magento-cloud` Interface en ligne de commande, voir [Référence de l’interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md). Après avoir installé la variable `magento-cloud` Interface de ligne de commande et configuration des clés SSH pour un accès à distance à votre infrastructure cloud, vous pouvez utiliser `magento-cloud` Commandes d’interface de ligne de commande pour gérer les environnements de vos projets. Pour plus d’informations sur l’architecture de l’environnement, voir [Architecture de démarrage](../architecture/starter-architecture.md) ou [Architecture Pro](../architecture/pro-architecture.md).

Pour gérer les branches et les environnements avec l’événement [!DNL Cloud Console], voir [Gestion des branches avec [!DNL Cloud Console]](../project/console-branches.md).

## Utilisation des commandes de l’interface de ligne de commande

La variable `magento-cloud` Les commandes de l’interface de ligne de commande sont similaires aux commandes Git. Vous pouvez les utiliser pour vous connecter à votre projet et gérer vos environnements. Bien que vous puissiez exécuter les commandes à partir de n’importe quel répertoire, il est recommandé de les exécuter à partir d’un répertoire de projet. Lorsque vous exécutez à partir d’un répertoire de projet, vous pouvez omettre l’événement `-p <project-ID>` . Voir [Référence de l’interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md).

## Cloner le projet

Les instructions suivantes utilisent une combinaison de `magento-cloud` Commandes d’interface de ligne de commande et commandes Git pour cloner votre projet sur votre poste de travail local. Pour afficher la liste complète de `magento-cloud` Commandes d’interface de ligne de commande, utilisez `magento-cloud list` .

>[!IMPORTANT]
>
>Certaines commandes Git ne peuvent pas effectuer d’action dans votre projet Adobe Commerce sur l’infrastructure cloud. Par exemple, vous pouvez créer une branche à l’aide d’une commande Git, mais vous ne pouvez pas créer ni activer un nouvel environnement. Vous devez créer un environnement à l’aide de la variable `magento-cloud environment:branch <branch-name>` pour que l’environnement devienne _active_. Vous pouvez également utiliser la variable [!DNL Cloud Console] pour créer des environnements actifs. Voir [Référence de l’interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md#git-commands).

**Pour cloner un projet `master` environnement**:

1. Connectez-vous à votre poste de travail local à l’aide d’un [propriétaire du système de fichiers](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) compte .

1. Modification du serveur web ou de l’hôte virtuel _docroot_ répertoire .

1. Connectez-vous à l’aide du `magento-cloud` Interface de ligne de commande.

   ```bash
   magento-cloud login
   ```

1. Liste de vos projets.

   ```bash
   magento-cloud project:list
   ```

1. Cloner un projet.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Lorsque vous y êtes invité, indiquez un nom de répertoire.

1. Changement de la `magento2` répertoire .

1. Liste des environnements disponibles pour le projet.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >La variable `magento-cloud environment:list` affiche des hiérarchies d’environnement, tandis que la fonction `git branch` ne l’est pas.

1. Récupérez les branches distantes.

   ```bash
   git fetch origin
   ```

1. Extrayez le code mis à jour.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Voir [Intégrations](../integrations/overview.md) pour plus d’informations sur l’utilisation des services d’hébergement Git avec Adobe Commerce sur l’infrastructure cloud.

## Création d’une branche pour le développement

Après avoir cloné votre projet et mis à jour la configuration du compte administrateur Adobe Commerce, vous pouvez créer une branche pour le développement. Comme indiqué précédemment, vous devez créer un environnement à l’aide de la variable `magento-cloud environment:branch <branch-name>` ou la fonction [!DNL Cloud Console] pour que l’environnement devienne _active_.

- Pour [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch), envisagez de créer une branche pour `staging`, puis créez une branche de développement basée sur la variable `staging` branche.
- Pour [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), créez des branches de développement en fonction des `Integration` branche.

**Pour créer une branche de développement**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Créez un environnement basé sur la branche recommandée pour votre workflow de projet.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Mise à jour des dépendances.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_facultatif_] Créez un [sauvegarde](../storage/snapshots.md) de l’environnement.

### Fusion d’une branche

Une fois le développement terminé, fusionnez cette branche avec le parent :

1. Validation et modification du code push :

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Fusionner avec l’environnement parent :

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Supprimer un environnement

Supprimez un environnement uniquement si vous êtes certain que vous n’en avez plus besoin. Une fois supprimé, vous ne pouvez pas récupérer un environnement.

>[!WARNING]
>
>Vous ne pouvez pas supprimer la variable `master` branche de n’importe quel projet.

Pour effectuer cette tâche, vous devez être un administrateur de projet, un administrateur d’environnement ou un propriétaire de compte. Voir [Gestion de l’accès des utilisateurs aux projets cloud](../project/user-access.md).

Lorsque vous supprimez un environnement, celui-ci est défini sur _inactive_. Le code est toujours disponible dans la branche Git, mais ne contient plus les services ni la base de données. Pour supprimer complètement l’environnement, vous devez également supprimer la branche Git distante correspondante.

**Pour supprimer un environnement**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Récupérez les mises à jour à partir du serveur distant.

   ```bash
   git fetch
   ```

1. Supprimez la branche d’environnement.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   Vous pouvez éventuellement supprimer plusieurs environnements à la fois en ajoutant plusieurs ID d’environnement à la commande de suppression.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Répondez aux invites pour supprimer l’environnement local et l’environnement distant correspondant.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   La suppression de l’environnement le place dans une _inactive_ état.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   La suppression de la branche Git distante supprime l’environnement du projet.

1. Attendez que l’environnement soit supprimé.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Pour activer un environnement inactif, utilisez la méthode `magento-cloud environment:activate` .

## Interaction avec les environnements distants

Après vous [configuration des clés SSH](../development/secure-connections.md), vous pouvez [connexion de votre espace de travail local à un environnement distant](../development/secure-connections.md#connect-to-a-remote-environment) et interagissez avec vos services de projet et modifiez les paramètres.
