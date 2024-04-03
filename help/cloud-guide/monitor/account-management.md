---
title: Gestion de compte New Relic
description: Découvrez comment accéder à votre compte New Relic et gérer l’accès, les intégrations et l’utilisation des outils pour votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Gestion des comptes New Relic

Lorsqu’Adobe fournit votre projet d’infrastructure cloud, le propriétaire de la licence reçoit un courrier électronique de New Relic avec des informations d’identification et des instructions pour accéder au compte New Relic. Si vous n’avez pas reçu le courrier électronique, utilisez l’adresse électronique du propriétaire de la licence pour réinitialiser le mot de passe New Relic.

## Gestion de l’accès des utilisateurs

Une seule personne peut être affectée à un compte New Relic au rôle Propriétaire. Si vous devez modifier le propriétaire du compte, attribuez le rôle d’administrateur au propriétaire actuel, puis le rôle de propriétaire à un autre utilisateur. Voir [Mettre à jour le propriétaire du compte](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) dans le _Documentation New Relic_ pour obtenir des instructions.

Instructions pour gérer l’accès à New Relic :

- Les propriétaires de projet et les administrateurs peuvent ajouter et supprimer des utilisateurs du compte New Relic.
- Ne créez pas plus de cinq accès complets **Utilisateurs**.
- Accordez uniquement un accès complet aux utilisateurs qui ont strictement besoin d’un accès à l’ensemble des fonctionnalités.
- Il n’existe pas de conseils spécifiques sur la gratuité **Restricted** utilisateurs.

>[!TIP]
>
>Avant d’affecter le rôle Propriétaire à un utilisateur, vérifiez que l’utilisateur existe sur le compte New Relic pour Adobe Commerce sur l’infrastructure cloud. Si vous devez ajouter l’utilisateur à ce compte et qu’un propriétaire ou un administrateur de compte existant ne peut pas vous aider, tout utilisateur ayant accès à la variable [Compte propriétaire du partenariat Adobe](https://account.newrelic.com/accounts/1311131/users) pour New Relic peut ajouter des utilisateurs au nom du client.

Ajouter au moins un **Administration** de votre compte New Relic qui peut gérer tous les accès, intégrations et utilisation des outils.

**Pour accéder à la gestion des utilisateurs dans New Relic**:

1. Connectez-vous à [Compte New Relic](https://login.newrelic.com/login).

1. Sélectionnez votre nom d’utilisateur dans le volet de navigation inférieur gauche.

1. Cliquez sur **[!UICONTROL Administration]** et sélectionnez l’une des options suivantes dans la liste :

   - **[!UICONTROL User management]** pour ajouter un utilisateur et gérer les utilisateurs actifs et les invitations en attente.

   - **[!UICONTROL Access management]** pour gérer les groupes d’utilisateurs, les rôles et les comptes.

Voir [Gestion des utilisateurs](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) dans le _New Relic_ la documentation.

## Configuration de New Relic pour l’environnement de démarrage

>[!NOTE]
>
>**Environnements professionnels** sont préconfigurés pour utiliser les services New Relic et peuvent ignorer les instructions d’activation et de connexion. Si le New Relic APM n’est pas installé sur les environnements d’évaluation et de production ou si l’infrastructure New Relic n’est pas disponible dans l’environnement de production, [envoyer un ticket d’assistance Adobe Commerce ;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander l’installation.

Pour les environnements de démarrage, vous devez cocher la case `.magento.app.yaml` pour vérifier que la variable `runtime` comprend l’extension New Relic. Si l’extension n’a pas été configurée, ajoutez les éléments suivants :

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Appliquer la clé de licence

Pour connecter un environnement Cloud à New Relic, ajoutez la clé de licence New Relic à l’environnement.

- Pour **Projets Pro**, Adobe ajoute la clé de licence à vos environnements de production et d’évaluation pendant le processus d’approvisionnement. Vous pouvez vous connecter à votre [Compte New Relic](https://login.newrelic.com/login) pour vérifier la connectivité entre votre Adobe Commerce sur le site d’infrastructure cloud et New Relic.

- Pour **Projets de démarrage**, vous disposez d’une clé de licence New Relic qui prend en charge jusqu’à _trois_ des environnements. Vous devez ajouter manuellement la clé à vos configurations d’environnement. Les environnements de démarrage ne sont pas préconfigurés pour utiliser le service New Relic.

Pour les environnements de démarrage, activez l’intégration de New Relic en ajoutant la clé de licence New Relic à la configuration de l’environnement. Ajoutez la clé aux environnements d’évaluation et de production, ainsi qu’à un autre environnement de votre choix. Seule la clé de licence New Relic est requise pour la configuration. Vous trouverez des informations sur les options de configuration supplémentaires dans la section [Rapports New Relic](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) dans la section _Guide de l’utilisateur d’Adobe Commerce_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Identifiants de connexion pour la page de compte Adobe Commerce ou pour la licence New Relic associée à votre projet
>- [Accès de niveau administrateur](../project/user-access.md) aux environnements de démarrage à configurer.
>- Informations d’identification pour accéder au [Administration](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) pour l’environnement

**Configuration de New Relic pour les environnements de démarrage**:

1. Recherchez votre clé de licence New Relic à partir du [!DNL Cloud Console] ou l’interface de ligne de commande de Cloud.

   **[!DNL Cloud Console]method**:

   - Ouvrez votre projet cloud. [page de compte](https://accounts.magento.cloud/user).

   - Sur le _Projets_ recherchez votre projet.

   - Cliquez sur **Afficher les détails** pour obtenir des informations sur l’infrastructure du projet.

   - Développez l’objet **New Relic Service** pour afficher la clé de licence.

   - Copiez la clé de licence.

   **Méthode d’interface de ligne de commande cloud**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Ajoutez la clé de licence New Relic à un environnement à l’aide du `magento-cloud` Interface de ligne de commande.

   - Modifiez l’environnement qui a besoin de la clé de licence.
   - Mettez à jour la valeur de la variable à l’aide de ce qui suit : `magento-cloud` Commande de l’interface de ligne de commande :

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Vous pouvez éventuellement l’ajouter à partir du [Administrateur Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Connectez-vous à [Compte New Relic](https://login.newrelic.com/login) pour vérifier que vous pouvez afficher les données de l’environnement Adobe Commerce. Voir [Explorer les performances](investigate-performance.md).

### Supprimer la clé de licence

Vous ne pouvez utiliser votre clé de licence New Relic que dans trois environnements actifs. Si la clé est utilisée dans trois environnements, vous devez la supprimer de l’un des environnements avant de pouvoir l’ajouter à un autre environnement.

**Pour supprimer une clé de licence d’un environnement**:

1. Variables d’environnement de liste.

   ```bash
   magento-cloud variable:list
   ```

   Exemple de réponse :

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Si vous avez ajouté la clé de licence en tant que _project_ , vous devez supprimer cette variable au niveau du projet. Une variable de projet ajoute la licence à _each_ branche d’environnement créée, qui peut consommer ou dépasser la limite de licence. Pour répertorier les variables de projet : `magento-cloud variable:list --level project`

1. Supprimez la variable de licence.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
