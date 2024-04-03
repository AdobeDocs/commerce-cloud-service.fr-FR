---
title: Interface de ligne de commande du cloud
description: Découvrez l’interface de ligne de commande de Magento-cloud et comment elle vous aide à gérer les environnements de développement locaux pour votre projet d’infrastructure cloud Adobe Commerce.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Interface de ligne de commande du cloud

La variable `magento-cloud` L’outil d’interface de ligne de commande permet aux développeurs et aux administrateurs système de gérer les projets et environnements cloud, d’exécuter des routines et d’exécuter des tâches d’automatisation. La variable `magento-cloud` L’interface de ligne de commande étend les fonctionnalités de [[!DNL Cloud Console]](../../get-started/cloud-console.md). Après avoir installé la variable `magento-cloud` Interface en ligne de commande sur votre poste de travail local, vous pouvez l’utiliser pour gérer votre Adobe Commerce dans les environnements d’intégration Starter et Pro de l’infrastructure cloud.

**Pour installer le `magento-cloud` CLI**:

1. Sur votre poste de travail local, modifiez le répertoire dans lequel vous avez l’intention de cloner le projet Cloud et où le [propriétaire du système de fichiers](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) has _write_ accès.

1. Installez le `magento-cloud` Interface de ligne de commande.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Ajouter `magento-cloud` Interface de ligne de commande du profil bash.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Rechargez le profil bash mis à jour.

   ```bash
   . ~/.bash_profile
   ```

1. Pour lancer l’interface de ligne de commande, appelez `magento-cloud` et saisissez les informations d’identification de votre compte Cloud lorsque vous y êtes invité.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Vérifiez les `magento-cloud` est dans votre chemin d’accès. L’exemple suivant répertorie les commandes disponibles.

   ```bash
   magento-cloud list
   ```

## Commandes courantes

Adobe a conçu ces commandes pour gérer les environnements d’intégration Cloud et vous recommande d’exécuter la `magento-cloud` Interface de ligne de commande d’un répertoire de projet afin que vous puissiez omettre la variable `-p <project-ID>` .

La liste suivante des `magento-cloud` Les commandes de l’interface de ligne de commande incluent uniquement les options requises. Vous pouvez utiliser la variable `--help` avec n’importe quelle commande pour afficher plus d’informations.

| Commande | Description |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Connectez-vous au projet. |
| `magento-cloud list` | Liste des commandes disponibles pour l’outil d’interface de ligne de commande. |
| `magento-cloud environment:list` | Liste des environnements du projet en cours. |
| `magento-cloud environment:checkout` | Extrayez un environnement existant. |
| `magento-cloud environment:merge -e` | Fusionner les modifications dans cet environnement avec son parent. |
| `magento-cloud variables` | Variables de liste dans cet environnement. |
| `magento-cloud ssh` | Utilisez SSH pour vous connecter à l’environnement distant. |
| `magento-cloud url` | Ouvrez le storefront Adobe Commerce dans un navigateur. |
| `magento-cloud web` | Ouvrez le [!DNL Cloud Console]. |

## Commandes d’environnement

L&#39;environnement _name_ est différent de l’environnement _ID_ uniquement si vous utilisez des espaces ou des majuscules dans le nom de l’environnement. Un ID d’environnement se compose de toutes les lettres minuscules, de tous les nombres et de tous les symboles autorisés. Les majuscules d’un nom d’environnement sont converties en minuscules dans l’identifiant ; les espaces d’un nom d’environnement sont convertis en tirets.

Un nom d’environnement _cannot_ incluez des caractères réservés à votre shell Linux ou à des expressions régulières. Les caractères interdits incluent des accolades (`{ }`), parenthèses, astérisque (`*`), chevrons (`< >`), esperluette (`&`), pourcentage (`%`), et autres caractères.

La variable `magento-cloud environment:list` affiche des hiérarchies d’environnement, alors que `git branch` ne le fait pas. Si vous disposez d’environnements imbriqués, utilisez les méthodes suivantes :

```bash
magento-cloud environment:list
```

### Redéployer l’environnement

Déclenchez un redéploiement sans utiliser de notification push. Vérifiez et confirmez l’environnement à redéployer. N’utilisez pas le redéploiement en cas de version en attente.

```bash
magento-cloud environment:redeploy
```

Exemple de réponse :

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Commandes Git

Vous remarquerez peut-être que certaines de ces commandes sont similaires aux commandes Git. La variable `magento-cloud` Les commandes se connectent directement au projet Cloud basé sur Git avec des fonctionnalités supplémentaires. Si vous créez une branche sans utiliser la variable `magento-cloud` Interface en ligne de commande, elle n’est pas &quot;activée&quot; et ne se génère pas automatiquement lorsque vous placez des modifications dans l’environnement distant. La variable `magento-cloud` La commande d’interface de ligne de commande inclut l’activation.

Pour créer une branche, utilisez la méthode `magento-cloud` pour activer la branche.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Pour l’état de la branche :

- Utilisez la variable `magento-cloud env` pour afficher la liste des branches de l&#39;environnement et leur état : actif ou inactif.
- Utilisez la variable `magento-cloud environment:activate` pour activer une branche d’environnement.

Envoyez une validation Git vide pour déclencher un déploiement. Par exemple :

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Certaines actions, telles que l’ajout d’un utilisateur, n’entraînent pas de déploiement.

### Création d’une branche d’environnement

Les étapes suivantes montrent comment gérer votre environnement local à l’aide des commandes d’interface de ligne de commande et Git :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Basculez vers le [propriétaire du système de fichiers](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Connectez-vous à votre projet.

   ```bash
   magento-cloud login
   ```

1. Liste de vos projets.

   ```bash
   magento-cloud project:list
   ```

1. Liste des environnements du projet. Chaque environnement comprend une branche Git active qui contient votre code, votre base de données, vos variables d’environnement, vos configurations et vos services.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >Il est important d’utiliser la variable `magento-cloud environment:list` , car elle affiche des hiérarchies d’environnement, tandis que la fonction `git branch` ne l’est pas.

1. Récupérez les branches d’origine pour obtenir le code le plus récent.

   ```bash
   git fetch origin
   ```

1. Extrayez ou basculez vers une branche et un environnement spécifiques.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Les commandes Git extraient uniquement la branche Git. La variable `magento-cloud checkout` extrait la branche et bascule vers l’environnement actif.

   >[!TIP]
   >
   >Vous pouvez créer une branche d’environnement à l’aide de la fonction `magento-cloud environment:branch <environment-name> <parent-environment-ID>` syntaxe de commande. La création et l’activation d’une branche d’environnement peuvent prendre du temps.

1. Utilisez l’ID d’environnement pour extraire le code mis à jour dans votre environnement local. Cela n’est pas nécessaire si la branche d’environnement est nouvelle.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Facultatif_) Créez un [instantané](../storage/snapshots.md) de l’environnement en tant que sauvegarde.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## Mise à jour de l’interface de ligne de commande

La variable `magento-cloud` L’interface en ligne de commande recherche les mises à jour disponibles lorsque vous vous connectez, mais vous pouvez les rechercher à l’aide de la variable `self:update` . Si une mise à jour est disponible, suivez les instructions pour mettre à jour l’interface de ligne de commande.

Si votre `magento-cloud` L’interface en ligne de commande est à jour. La réponse suivante s’affiche :

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
