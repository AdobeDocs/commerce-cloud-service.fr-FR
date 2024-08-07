---
title: Intégration de GitLab
description: Découvrez comment intégrer votre projet d’infrastructure cloud Adobe Commerce à GitLab.
feature: Cloud, Integration
exl-id: 37fda8a0-7274-422f-9049-243f2e409f26
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Intégration de GitLab

Vous pouvez configurer un référentiel GitLab pour créer et déployer automatiquement un environnement lorsque vous poussez des modifications de code. Cette intégration synchronise votre référentiel GitLab avec votre compte Adobe Commerce sur l’infrastructure cloud.

{{private-repository}}

Cette intégration vous permet d’effectuer les opérations suivantes :

- Création d’un environnement lors de la création d’une branche
- Redéployer l’environnement lorsque vous fusionnez une requête de tirage
- Suppression de l’environnement lorsque vous supprimez la branche

Vous devez obtenir un jeton GitLab et un webhook pour continuer le processus.

## Conditions préalables

- Accès de l’administrateur au projet d’infrastructure cloud Adobe Commerce
- Outil [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) dans votre environnement local
- Compte GitLab
- Jeton d’accès personnel GitLab avec accès en écriture au référentiel GitLab. Les portées sélectionnées doivent être au moins : `api` et `read_repository`.

## Préparation de votre référentiel

Cloner votre projet Adobe Commerce sur un projet d’infrastructure cloud à partir d’un environnement existant et migrer les branches du projet vers un nouveau référentiel GitLab vide, en conservant les mêmes noms de branche. Il est **essentiel** de conserver un arbre Git identique afin de ne pas perdre d’environnements ou de branches existants dans votre Adobe Commerce sur le projet d’infrastructure cloud.

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
   magento-cloud project:get <project-id>
   ```

1. Ajoutez votre référentiel GitLab en tant que référentiel distant (en supposant que GitLab soit utilisé dans sa version SaaS).

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   Le nom par défaut de la connexion distante peut être `origin` ou `magento`. Si `origin` existe, vous pouvez choisir un autre nom ou renommer ou supprimer la référence existante. Voir la [documentation git-remote](https://git-scm.com/docs/git-remote).

1. Vérifiez que vous avez correctement ajouté la télécommande GitLab.

   ```bash
   git remote -v
   ```

   Réponse attendue :

   ```
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. Placez les fichiers de projet dans votre nouveau référentiel GitLab. N’oubliez pas de conserver tous les noms de branche identiques.

   ```bash
   git push -u origin master
   ```

   Si vous commencez avec un nouveau référentiel GitLab, vous devrez peut-être utiliser l’option `-f`, car le référentiel distant ne correspond pas à votre copie locale.

1. Vérifiez que votre référentiel GitLab contient tous vos fichiers de projet.

## Activation de l’intégration GitLab

Utilisez la commande `magento-cloud integration` pour activer l’intégration GitLab et obtenir l’URL de payload du webhook GitLab pour envoyer des mises à jour de GitLab à votre Adobe Commerce sur le projet d’infrastructure cloud.

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| Option | Description |
| ------ | ----------- |
| `<project-ID>` | Votre identifiant de projet Adobe Commerce on Cloud Infrastructure |
| `<your-GitLab-token>` | Jeton d’accès personnel généré pour GitLab |
| `--base-url` | URL de GitLab (`https://gitlab.com/` si GitLab est utilisé dans sa version SaaS) |
| `--server-project` | Nom du projet dans GitLab (partie après l’URL de base) |
| `--build-merge-requests` | Un paramètre _facultatif_ qui demande à Adobe Commerce sur l’infrastructure cloud de créer un environnement pour chaque demande de fusion (`true` par défaut) |
| `--merge-requests-clone-parent-data` | Un paramètre _facultatif_ qui demande à Adobe Commerce sur l’infrastructure cloud de cloner les données de l’environnement parent pour les demandes de fusion (`true` par défaut) |
| `--fetch-branches` | Un paramètre _facultatif_ qui entraîne Adobe Commerce sur l’infrastructure cloud à récupérer toutes les branches de la distante (en tant qu’environnements inactifs) (`true` par défaut) |
| `--prune-branches` | Paramètre _optionnel_ qui indique à Adobe Commerce sur l’infrastructure cloud de supprimer les branches qui n’existent pas sur le site distant (`true` par défaut) |

>[!WARNING]
>
>La commande `magento-cloud integration` remplace le code _all_ de votre projet d’infrastructure cloud Adobe Commerce par le code de votre référentiel GitLab. Cela inclut toutes les branches, y compris la branche `production`. Cette action se produit instantanément et ne peut pas être annulée. En règle générale, il est important de cloner toutes vos branches à partir d’Adobe Commerce sur un projet d’infrastructure cloud et de les placer dans votre référentiel GitLab avant d’ajouter l’intégration GitLab.

**Pour activer l’intégration GitLab** :

1. Depuis le terminal, ajoutez l’intégration GitLab à votre projet d’infrastructure cloud Adobe Commerce :

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. Lorsque vous y êtes invité, saisissez `y` pour ajouter l’intégration.

   ```
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. Copiez l’ **URL du crochet** affiché par la sortie de retour.

   ```
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### Ajout du webhook dans GitLab

Pour communiquer des événements, tels qu’une requête push ou de fusion, avec votre serveur Cloud Git, vous devez [ créer un webhook](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) pour votre référentiel GitLab.

1. Dans votre référentiel GitLab, cliquez sur l’onglet **Paramètres**.

1. Dans la barre de navigation de gauche, cliquez sur **Webhooks**.

1. Dans le formulaire _Webhooks_, modifiez les champs suivants :

   - **URL** : saisissez le `Hook URL` renvoyé lorsque vous avez activé l’intégration GitLab.
   - **Jeton secret** : saisissez un secret de vérification si nécessaire.
   - **Déclencheur** : cochez `Merge request events` et/ou `Push events` en fonction de vos besoins.
   - **Activer la vérification SSL** : vous devez sélectionner cette option.

1. Cliquez sur **Ajouter webhook**.

### Test de l’intégration

Après avoir configuré l’intégration GitLab, vous pouvez vérifier que l’intégration fonctionne à l’aide de l’interface de ligne de commande `magento-cloud` :

```bash
magento-cloud integration:validate
```

Vous pouvez également le tester en envoyant une simple modification à votre référentiel GitLab.

1. Créez un fichier de test.

   ```bash
   touch test.md
   ```

1. Validez et envoyez la modification à votre référentiel GitLab.

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. Connectez-vous à [[!DNL Cloud Console]](../project/overview.md) et vérifiez que votre message de validation s’affiche et que votre projet est en cours de déploiement.

## Création d’une branche Cloud

Utilisez la commande `magento-cloud` CLI `environment:push` pour créer et activer un nouvel environnement. Voir [Création d’une branche de cloud](bitbucket.md#create-a-cloud-branch).

## Suppression de l’intégration

Utilisez la commande `magento-cloud` CLI `integration:delete` pour supprimer l’intégration. Voir [Suppression de l’intégration](bitbucket.md#remove-the-integration).
