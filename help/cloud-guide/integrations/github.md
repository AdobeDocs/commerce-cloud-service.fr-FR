---
title: Intégration de GitHub
description: Découvrez comment intégrer votre projet d’infrastructure cloud Adobe Commerce à GitHub.
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: 5305452f-4c8d-438c-ac78-e2e1ec2f8cd9
source-git-commit: 4d32fc596064f01eaefe3ee509a655837fa846de
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Intégration de GitHub

L’intégration GitHub vous permet de gérer votre Adobe Commerce dans les environnements d’infrastructure cloud directement à partir de votre référentiel GitHub. L’intégration gère déjà le contenu dans GitHub et se synchronise avec votre référentiel de code d’infrastructure cloud Adobe Commerce. Par essence, le référentiel de code devient un miroir du référentiel GitHub.

{{private-repository}}

Cette intégration vous permet d’effectuer les opérations suivantes :

- Création d’un environnement lors de la création d’une branche
- Redéployer l’environnement lorsque vous fusionnez une requête de tirage
- Suppression de l’environnement lorsque vous supprimez la branche

Vous devez obtenir un jeton GitHub et un webhook pour continuer le processus.

## Conditions préalables

- Accès de l’administrateur au projet d’infrastructure cloud Adobe Commerce
- Référentiel GitHub
- Jeton d’accès personnel GitHub

## Génération d’un jeton GitHub

Créez un jeton d’accès personnel classique dans les paramètres du développeur GitHub. Vous devez être membre d’un groupe disposant d’un accès en écriture au référentiel GitHub afin que vous puissiez _push_ au référentiel. Incluez les portées suivantes lors de la création de votre jeton :

- `admin:repo_hook`—Création de hooks Web
- `repo`: intégration à votre référentiel
- `read:org`: intégration à votre référentiel d’organisation

Voir [GitHub : Créer](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Préparation de votre référentiel

Cloner votre projet Adobe Commerce sur un projet d’infrastructure cloud à partir d’un environnement existant et migrer les branches du projet vers un nouveau référentiel GitHub vide, en conservant les mêmes noms de branche. Il s’agit de **critique** pour conserver une arborescence Git identique, de sorte que vous ne perdiez pas d’environnements ou de branches existants dans votre projet d’infrastructure cloud Adobe Commerce.

1. Depuis le terminal, connectez-vous à votre projet d’infrastructure cloud Adobe Commerce.

   ```bash
   magento-cloud login
   ```

1. Répertorier vos projets et copier l’ID de projet.

   ```bash
   magento-cloud project:list
   ```

1. Cloner le projet dans votre environnement local.

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. Ajoutez votre référentiel GitHub en tant que référentiel distant.

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   Le nom par défaut de la connexion distante peut être `origin` ou `magento`. If `origin` existe, vous pouvez choisir un autre nom ou renommer ou supprimer la référence existante. Voir [documentation git-remote](https://git-scm.com/docs/git-remote).

1. Vérifiez que vous avez correctement ajouté la télécommande GitHub.

   ```bash
   git remote -v
   ```

   Réponse attendue :

   ```terminal
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. Placez les fichiers de projet dans votre nouveau référentiel GitHub. N’oubliez pas de conserver tous les noms de branche identiques.

   ```bash
   git push -u origin master
   ```

   Si vous commencez avec un nouveau référentiel GitHub, vous devrez peut-être utiliser la variable `-f` , car le référentiel distant ne correspond pas à votre copie locale.

1. Vérifiez que votre référentiel GitHub contient tous vos fichiers de projet.

## Activation de l’intégration GitHub

Avant de commencer, le code et les environnements de votre projet doivent se trouver dans le référentiel GitHub. Après avoir activé l’intégration, le référentiel GitHub devient la source de code. Si vous poussez le code vers l’original `magento` , il est remplacé par l’intégration lorsque vous placez des modifications de code dans votre référentiel GitHub.

L’exemple suivant active l’intégration GitHub et fournit une URL de charge utile à utiliser lors de la création d’un webhook.

>[!WARNING]
>
>La commande suivante remplace _all_ code dans votre projet d’infrastructure cloud Adobe Commerce avec du code provenant de votre référentiel GitHub, qui comprend toutes les branches, y compris la variable `production` branche. Cette action se produit instantanément et ne peut pas être annulée. En règle générale, il est important de cloner toutes vos branches à partir d’Adobe Commerce sur un projet d’infrastructure cloud et de les transférer vers votre référentiel GitHub. **before** Ajout de l’intégration GitHub.

Vous pouvez choisir de parcourir les invites de l’interface de ligne de commande à l’aide de `magento-cloud integration:add` ou vous pouvez créer la commande d’intégration avec les options suivantes :

| Option | Obligatoire ? | Description |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | Oui | URL de base de l’installation du serveur, qui peut être `https://github.com/` ou une personnalisation. Omettez cette option si votre référentiel est hébergé avec Github public. |
| `--token` | Oui | Jeton d’accès personnel généré pour GitHub |
| `--repository` | Oui | Nom du référentiel : `owner-or-organisation/repository` |
| `--build-pull-requests` | Facultatif | Indique à Adobe Commerce sur l’infrastructure cloud de se déployer après la fusion d’une requête de tirage (`true` par défaut) |
| `--fetch-branches` | Facultatif | Permet à Adobe Commerce sur l’infrastructure cloud d’effectuer le suivi des branches et le déploiement après la mise à jour d’une branche (`true` par défaut) |
| `--prune-branches` | Facultatif | Supprimer les branches qui n’existent pas sur la télécommande (`true` par défaut) |

Il existe de nombreuses autres options, que vous pouvez voir à l’aide de l’option d’aide :

```bash
magento-cloud integration:add --help
```

**Pour activer l’intégration GitHub**:

1. Activez l’intégration.

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **Exemple 1**: activez l’intégration GitHub pour un référentiel privé personnel :

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **Exemple 2**: activez l’intégration GitHub pour un référentiel d’organisation :

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. Saisissez les informations requises lorsque vous y êtes invité.

1. Copiez le **URL de la payload** affiché par la sortie de retour.

   ```terminal
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## Ajout du webhook dans GitHub

Pour communiquer des événements (une notification push, par exemple) avec votre serveur Cloud Git, vous devez créer un webhook pour votre référentiel GitHub :

1. Dans votre référentiel GitHub, cliquez sur le **Paramètres** .

1. Dans la barre de navigation de gauche, cliquez sur **Webhooks**.

1. Dans le _Webhooks_ volet, cliquez sur **Ajout d’un webhook**.

1. Dans le _Webhooks/Add webhook_ modifiez les champs suivants du formulaire :

   - **URL de la payload**: saisissez l’URL renvoyée lorsque vous avez activé l’intégration GitHub.
   - **Type de contenu**: Choose **application/json** dans la liste.
   - **Secret**: saisissez un secret de vérification.
   - **Quels événements souhaitez-vous déclencher ce webhook ?**: sélectionnez **Envoyez-moi tout**.
   - Sélectionnez la variable **Actif** .

1. Cliquez sur **Ajout d’un webhook**.

## Test de l’intégration

Après avoir configuré l’intégration GitHub, vous pouvez vérifier que l’intégration fonctionne à l’aide de la variable `magento-cloud` Interface de ligne de commande :

```bash
magento-cloud integration:validate
```

Vous pouvez également le tester en envoyant une modification simple à votre référentiel GitHub.

1. Créez un fichier de test.

   ```bash
   touch test.md
   ```

1. Validez et envoyez la modification à votre référentiel GitHub.

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. Connectez-vous au [[!DNL Cloud Console]](../project/overview.md) et vérifiez que votre message de validation s’affiche et que votre projet est déployé.

## Suppression de l’intégration

Vous pouvez supprimer l’intégration GitHub de votre projet en toute sécurité sans affecter votre code.

**Pour supprimer l’intégration GitHub**:

1. Depuis le terminal, connectez-vous à votre projet d’infrastructure cloud Adobe Commerce.

1. Liste de vos intégrations. Vous avez besoin de l’identifiant d’intégration GitHub pour terminer l’étape suivante.

   ```bash
   magento-cloud integration:list
   ```

1. Supprimez l’intégration.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

En outre, vous pouvez supprimer l’intégration GitHub en vous connectant à votre compte GitHub et en supprimant le point d’extension web dans la variable _Webhooks_ onglet du référentiel _Paramètres_.
