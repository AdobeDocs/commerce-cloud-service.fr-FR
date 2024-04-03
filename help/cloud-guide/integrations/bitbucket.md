---
title: Intégration de Bitbucket
description: Découvrez comment intégrer votre projet d’infrastructure cloud Adobe Commerce à Bitbucket.
feature: Cloud, Integration
exl-id: cd3cffbe-268f-429b-a2ea-0306159f4a6b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Intégration de Bitbucket

Vous pouvez configurer votre référentiel Bitbucket pour créer et déployer automatiquement un environnement lorsque vous poussez des modifications de code. Cette intégration synchronise votre référentiel Bitbucket avec votre compte d’infrastructure cloud Adobe Commerce.

{{private-repository}}

## Conditions préalables

- Accès de l’administrateur au projet d’infrastructure cloud Adobe Commerce
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) outil dans votre environnement local
- Un compte Bitbucket
- Accès de l’administrateur au référentiel Bitbucket
- Clé d’accès SSH pour le référentiel Bitbucket

## Préparation de votre référentiel

Cloner votre projet Adobe Commerce sur un projet d’infrastructure cloud à partir d’un environnement existant et migrer les branches du projet vers un nouveau référentiel Bitbucket vide, en conservant les mêmes noms de branche. Il s’agit de **critique** pour conserver une arborescence Git identique, de sorte que vous ne perdiez pas d’environnements ou de branches existants dans votre projet d’infrastructure cloud Adobe Commerce.

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

1. Ajoutez votre référentiel Bitbucket en tant que référentiel distant.

   ```bash
   git remote add origin git@bitbucket.org:<user-name>/<repo-name>.git
   ```

   Le nom par défaut de la connexion distante peut être `origin` ou `magento`. If `origin` existe, vous pouvez choisir un autre nom ou renommer ou supprimer la référence existante. Voir [documentation git-remote](https://git-scm.com/docs/git-remote).

1. Vérifiez que vous avez correctement ajouté la télécommande Bitbucket.

   ```bash
   git remote -v
   ```

   Réponse attendue :

   ```terminal
   origin git@bitbucket.org:<user-name>/<repo-name>.git (fetch)
   origin git@bitbucket.org:<user-name>/<repo-name>.git (push)
   ```

1. Placez les fichiers de projet dans votre nouveau référentiel Bitbucket. N’oubliez pas de conserver tous les noms de branche identiques.

   ```bash
   git push -u origin master
   ```

   Si vous commencez avec un nouveau référentiel Bitbucket, vous devrez peut-être utiliser la variable `-f` , car le référentiel distant ne correspond pas à votre copie locale.

1. Vérifiez que votre référentiel Bitbucket contient tous vos fichiers de projet.

## Création d’un consommateur OAuth

L’intégration de Bitbucket requiert une [consommateur OAuth](https://support.atlassian.com/bitbucket-cloud/docs/use-oauth-on-bitbucket-cloud/). Vous avez besoin du OAuth `key` et `secret` de ce client pour terminer la section suivante.

**Pour créer un consommateur OAuth dans Bitbucket**:

1. Connectez-vous à [Bitbucket](https://id.atlassian.com/login) compte .

1. Cliquez sur **Paramètres** > **Gestion des accès** > **OAuth**.

1. Cliquez sur **Ajouter un client** et configurez-le comme suit :

   ![Configuration du consommateur OAuth pour Bitbucket](../../assets/oauth-consumer-config.png)

   >[!WARNING]
   >
   >Un valide **URL de callback** n’est pas obligatoire, mais vous devez saisir une valeur dans ce champ pour terminer l’intégration.

1. Cliquez sur **Enregistrer**.

1. Cliquez sur le client **Nom** pour afficher votre OAuth `key` et `secret`.

1. Copiez votre OAuth `key` et `secret` pour configurer l’intégration.

## Configuration de l’intégration

1. Depuis le terminal, accédez à votre projet d’infrastructure cloud Adobe Commerce.

1. Créez un fichier temporaire appelé `bitbucket.json` et ajoutez ce qui suit en remplaçant les variables entre crochets par vos valeurs :

   ```json
   {
     "type": "bitbucket",
     "repository": "<bitbucket-user-name/bitbucket-repo-name>",
     "app_credentials": {
       "key": "<oauth-consumer-key>",
       "secret": "<oauth-consumer-secret>"
     },
     "prune_branches": true,
     "fetch_branches": true,
     "build_pull_requests": true,
     "resync_pull_requests": true
   }
   ```

   >[!TIP]
   >
   >Veillez à utiliser le nom de votre référentiel Bitbucket et non l’URL. L’intégration échoue si vous utilisez une URL.

1. Ajoutez l’intégration à votre projet à l’aide du `magento-cloud` Outil d’interface de ligne de commande.

   >[!WARNING]
   >
   >La commande suivante remplace _all_ code dans votre projet d’infrastructure cloud Adobe Commerce avec le code de votre référentiel Bitbucket. Cela inclut toutes les branches, y compris la variable `production` branche. Cette action se produit instantanément et ne peut pas être annulée. En règle générale, il est important de cloner toutes vos branches de votre projet Adobe Commerce sur l’infrastructure cloud et de les placer dans votre référentiel Bitbucket. **before** Ajout de l’intégration Bitbucket.

   ```bash
   magento-cloud project:curl -p '<project-ID>' /integrations -i -X POST -d "$(< bitbucket.json)"
   ```

   Cela renvoie une réponse HTTP longue avec des en-têtes. Une intégration réussie renvoie un code d’état 200 ou 201. Un état 400 ou supérieur indique qu’une erreur s’est produite.

1. Supprimer le `bitbucket.json` fichier .

1. Vérifiez l’intégration du projet.

   ```bash
   magento-cloud integrations -p <project-ID>
   ```

   ```terminal
   +----------+-----------+--------------------------------------------------------------------------------+
   | ID       | Type      | Summary                                                                        |
   +----------+-----------+--------------------------------------------------------------------------------+
   | <int-id> | bitbucket | Repository: bitbucket_Account/magento-int                                      |
   |          |           | Hook URL:                                                                      |
   |          |           | https://magento-url.cloud/api/projects/<project-id>/integrations/<int-id>/hook |
   +----------+-----------+--------------------------------------------------------------------------------+
   ```

   Notez que la variable **URL de crochet** pour configurer un webhook dans BitBucket.

### Ajouter un webhook dans BitBucket

Pour communiquer des événements (une notification push, par exemple) avec votre serveur Cloud Git, vous devez disposer d’un webhook pour votre référentiel BitBucket. La méthode de configuration d’une intégration Bitbucket détaillée sur cette page, lorsqu’elle est correctement suivie, crée automatiquement un webhook. Il est important de vérifier le webhook pour éviter de créer plusieurs intégrations.

1. Connectez-vous à [Bitbucket](https://id.atlassian.com/login) compte .

1. Cliquez sur **Référentiels** et sélectionnez votre projet.

1. Cliquez sur **Paramètres du référentiel** > **Workflow** > **Webhooks**.

1. Vérifiez le webhook avant de continuer.

   Si le point d’extension est actif, ignorez les étapes restantes et [Test de l’intégration](#test-the-integration). Le point d’extension doit avoir un nom similaire à **&quot;Adobe Commerce sur l’infrastructure cloud &lt;project_id>&quot;** et un format d’URL hook similaire à : `https://<zone>.magento.cloud/api/projects/<project_id>/integrations/<id>/hook`

1. Cliquez sur **Ajout d’un webhook**.

1. Dans le _Ajouter un webhook_ visualisez, modifiez les champs suivants :

   - **Titre**: intégration Adobe Commerce
   - **URL**: utilisez l’URL de crochet de votre `magento-cloud` liste d’intégration
   - **Triggers**: la valeur par défaut est un _Repository push_

1. Cliquez sur **Enregistrer**.

### Test de l’intégration

Après avoir configuré l’intégration de Bitbucket, vous pouvez vérifier que l’intégration est opérationnelle à l’aide de la variable `magento-cloud` Interface de ligne de commande :

```bash
magento-cloud integration:validate
```

Vous pouvez également le tester en envoyant une simple modification à votre référentiel Bitbucket.

1. Créez un fichier de test.

   ```bash
   touch test.md
   ```

1. Validez et envoyez la modification à votre référentiel Bitbucket.

   ```bash
   git add . && git commit -m "Testing Bitbucket integration" && git push
   ```

1. Connectez-vous au [[!DNL Cloud Console]](../project/overview.md) et vérifiez que votre message de validation s’affiche et que votre projet est déployé.

   ![Test de l’intégration de Bitbucket](../../assets/bitbucket-integration.png)

## Création d’une branche Cloud

L’intégration Bitbucket ne peut pas activer de nouveaux environnements dans votre projet d’infrastructure cloud Adobe Commerce. Si vous créez un environnement avec Bitbucket, vous devez activer l’environnement manuellement. Pour éviter cette étape supplémentaire, il est recommandé de créer des environnements à l’aide de la méthode `magento-cloud` l’outil d’interface en ligne de commande ou [!DNL Cloud Console].

**Pour activer une branche créée avec Bitbucket**:

1. Utilisez la variable `magento-cloud` Interface de ligne de commande pour pousser la branche.

   ```bash
   magento-cloud environment:push from-bitbucket
   ```

   ```terminal
   Pushing from-bitbucket to the new environment from-bitbucket
   Activate from-bitbucket after pushing? [Y/n] y
   Parent environment [master]: integration
   --- (Validation and activation messages)
   ```

1. Vérifiez que l’environnement est actif.

   ```bash
   magento-cloud environment:list
   ```

   ```terminal
   Your environments are:
   +---------------------+----------------+--------+
   | ID                  | Name           | Status |
   +---------------------+----------------+--------+
   | master              | Master         | Active |
   |  integration        | integration    | Active |
   |    from-bitbucket * | from-bitbucket | Active |
   +---------------------+----------------+--------+
   * - Indicates the current environment
   ```

Après avoir créé un environnement, vous pouvez envoyer la branche correspondante vers votre référentiel Bitbucket distant à l’aide de commandes Git standard. Les modifications suivantes apportées à votre branche dans Bitbucket créent et déploient automatiquement l’environnement.

## Suppression de l’intégration

Vous pouvez supprimer l’intégration Bitbucket de votre projet en toute sécurité sans affecter votre code.

**Suppression de l’intégration Bitbucket**:

1. Depuis le terminal, connectez-vous à votre projet d’infrastructure cloud Adobe Commerce.

1. Liste de vos intégrations. Vous avez besoin de l’ID d’intégration de Bitbucket pour terminer l’étape suivante.

   ```bash
   magento-cloud integration:list
   ```

1. Supprimez l’intégration.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Vous pouvez également supprimer l’intégration Bitbucket en vous connectant à votre compte Bitbucket et en révoquant l’octroi OAuth sur ce compte. _Paramètres_ page.

## Intégration du serveur Bitbucket

Pour utiliser l’intégration du serveur Bitbucket, vous avez besoin des éléments suivants :

- [Jeton d’accès au compartiment](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html): génère un jeton qui accorde le projet `read` accès et référentiel `admin` access
- [URL du serveur Bitbucket](https://confluence.atlassian.com/bitbucketserver/specify-the-bitbucket-base-url-776640392.html): ajoutez l’URL de base de votre instance Bitbucket.

Bien que vous puissiez utiliser l’interface de ligne de commande Cloud pour parcourir les étapes d’intégration du serveur Bitbucket, la commande complète ressemble à ce qui suit :

```bash
magento-cloud integration:add --type=bitbucket_server --base-url=<bitbucket-url> --username=<username> --token=<bitbucket-access-token> --project=<project-ID>
```

Utilisez la commande d’aide pour plus d’exigences d’utilisation et d’options : `magento-cloud integration:add --help`
