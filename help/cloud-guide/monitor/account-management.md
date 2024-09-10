---
title: Gestion de compte New Relic
description: Découvrez comment accéder à votre compte New Relic et gérer l’accès, les intégrations et l’utilisation des outils pour votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 1fc488d7e13952ad70d4c864327899f38ea48af1
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Gestion des comptes New Relic

Lorsqu’Adobe fournit votre projet d’infrastructure cloud, le propriétaire de la licence reçoit un courrier électronique de New Relic avec des informations d’identification et des instructions pour accéder au compte New Relic. Si vous n’avez pas reçu le courrier électronique, utilisez l’adresse électronique du propriétaire de la licence pour réinitialiser le mot de passe New Relic.

## Gestion de l’accès des utilisateurs

>[!NOTE]
>
>Accordez uniquement un accès complet aux utilisateurs qui ont strictement besoin d’un accès à l’ensemble des fonctionnalités.

**Pour accéder à la gestion des utilisateurs dans New Relic** :

1. Connectez-vous à votre [compte New Relic](https://login.newrelic.com/login).

1. Sélectionnez votre nom d’utilisateur dans le volet de navigation inférieur gauche.

1. Cliquez sur **[!UICONTROL Administration]** et sélectionnez l’une des options suivantes dans la liste :

   - **[!UICONTROL User management]** pour ajouter un utilisateur et gérer les utilisateurs actifs et les invitations en attente.

   - **[!UICONTROL Access management]** pour gérer les groupes d’utilisateurs, les rôles et les comptes.

Voir [Gestion des utilisateurs](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) dans la documentation _New Relic_.

## Configuration de New Relic pour l’environnement de démarrage

>[!NOTE]
>
>Les **environnements Pro** sont préconfigurés pour utiliser les services New Relic et peuvent ignorer les instructions d’activation et de connexion. Si l’APM New Relic n’est pas installé sur les environnements d’évaluation et de production ou si l’infrastructure New Relic n’est pas disponible dans l’environnement de production, [ envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander l’installation.

Pour les environnements de démarrage, vous devez vérifier que le fichier `.magento.app.yaml` contient l’extension New Relic dans la section `runtime`. Si l’extension n’a pas été configurée, ajoutez les éléments suivants :

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Appliquer la clé de licence

Pour connecter un environnement Cloud à New Relic, ajoutez la clé de licence New Relic à l’environnement.

- Pour les **projets Pro**, Adobe ajoute la clé de licence à vos environnements de production et d’évaluation pendant le processus d’approvisionnement. Vous pouvez vous connecter à votre [compte New Relic](https://login.newrelic.com/login) pour vérifier la connectivité entre votre Adobe Commerce sur le site d’infrastructure cloud et New Relic.

- Pour les **projets de démarrage**, vous disposez d’une clé de licence New Relic qui prend en charge jusqu’à _trois_ environnements. Vous devez ajouter manuellement la clé à vos configurations d’environnement. Les environnements de démarrage ne sont pas préconfigurés pour utiliser le service New Relic.

Pour les environnements de démarrage, activez l’intégration de New Relic en ajoutant la clé de licence New Relic à la configuration de l’environnement. Ajoutez la clé aux environnements d’évaluation et de production, ainsi qu’à un autre environnement de votre choix. Seule la clé de licence New Relic est requise pour la configuration. Vous trouverez des informations sur d’autres options de configuration dans la rubrique [Rapports New Relic](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) du _Guide de l’utilisateur d’Adobe Commerce_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Identifiants de connexion pour la page de compte Adobe Commerce ou pour la licence New Relic associée à votre projet
>- [Accès de niveau administrateur](../project/user-access.md) aux environnements de démarrage à configurer
>- Informations d’identification pour accéder à l’[administrateur](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) pour l’environnement

**Pour configurer New Relic pour les environnements de démarrage** :

1. Recherchez votre clé de licence New Relic à partir de l’interface de ligne de commande [!DNL Cloud Console] ou de Cloud.

   **[!DNL Cloud Console]method** :

   - Ouvrez votre projet cloud [page de compte](https://accounts.magento.cloud/user).

   - Dans l’onglet _Projets_, recherchez votre projet.

   - Cliquez sur **Afficher les détails** pour obtenir des informations sur l’infrastructure du projet.

   - Développez la section **Service New Relic** pour afficher la clé de licence.

   - Copiez la clé de licence.

   **Méthode d’interface de ligne de commande cloud** :

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Ajoutez la clé de licence New Relic à un environnement à l’aide de l’interface de ligne de commande `magento-cloud`.

   - Modifiez l’environnement qui a besoin de la clé de licence.
   - Mettez à jour la valeur de la variable à l’aide de la commande d’interface de ligne de commande `magento-cloud` suivante :

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Vous pouvez éventuellement l’ajouter à partir de l’ [administrateur Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Connectez-vous à votre [compte New Relic](https://login.newrelic.com/login) pour vérifier que vous pouvez afficher les données de l’environnement Adobe Commerce. Voir [Performance d&#39;investigation](investigate-performance.md).

### Supprimer la clé de licence

Vous ne pouvez utiliser votre clé de licence New Relic que dans trois environnements actifs. Si la clé est utilisée dans trois environnements, vous devez la supprimer de l’un des environnements avant de pouvoir l’ajouter à un autre environnement.

**Pour supprimer une clé de licence d’un environnement** :

1. Variables d’environnement de liste.

   ```bash
   magento-cloud variable:list
   ```

   Exemple de réponse :

   ```
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Si vous avez ajouté la clé de licence en tant que variable _project_ , vous devez supprimer cette variable au niveau du projet. Une variable de projet ajoute la licence à _chaque_ branche d’environnement créée, ce qui peut consommer ou dépasser la limite de licence. Pour répertorier les variables de projet : `magento-cloud variable:list --level project`

1. Supprimez la variable de licence.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
