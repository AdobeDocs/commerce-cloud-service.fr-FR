---
title: Gestion de l’accès des utilisateurs
description: Découvrez comment gérer l’accès des utilisateurs à Adobe Commerce sur les projets et environnements d’infrastructure cloud.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: 5e4be034a392716ea55e2878d336cb9ecac1e052
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---

# Gestion de l’accès des utilisateurs

Les projets Adobe Commerce sur l’infrastructure cloud utilisent un accès basé sur les rôles. Deux rôles sont disponibles au niveau du projet :

- **Administrateur de projet** : accédez en écriture à tous les environnements de projet et pouvez gérer les utilisateurs, envoyer du code et mettre à jour les paramètres du projet. (Antérieurement appelé **Super administrateur**)
- **Visionneuse de projet** : accès en lecture seule à tous les environnements de projet.

Les visionneuses de projets ne peuvent pas effectuer de tâches sur un environnement, mais vous pouvez accorder aux visionneuses de projets l’accès en écriture à un type d’environnement spécifique.

L’accès au niveau de l’environnement est basé sur le type d’environnement : production, évaluation et développement. Octroyer une autorisation _viewer_ à un utilisateur pour _les environnements de développement_ signifie qu’il peut afficher **tous les** environnements de développement dans le projet. Le tableau suivant clarifie les fonctionnalités accordées à chaque niveau d’autorisation :

| Niveau d’autorisation | Accès | Accès SSH |
| ------------------ | ----------- | :----------: |
| **Admin** | Effectuez les tâches de l’administrateur, telles que les paramètres de modification, le code push, les tâches et la gestion des branches, y compris la fusion avec l’environnement parent. | Oui |
| **Contributeur** | code push et branche l’environnement ; ne peut pas modifier les paramètres ni exécuter des actions. | Oui |
| **Visionneuse** | Accès en lecture seule au type d&#39;environnement | Non |
| **Aucun accès** | Accès au type d&#39;environnement interdit | Non |

{style="table-layout:auto"}

Vous pouvez ajouter des utilisateurs et attribuer des rôles à l’aide de l’interface de ligne de commande `magento-cloud` ou de [!DNL Cloud Console].

>[!BEGINSHADEBOX]

**Conditions préalables :**

- Un utilisateur enregistré avec une Adobe ID. Un utilisateur doit [s’enregistrer pour un compte d’Adobe](https://account.adobe.com), puis [ initialiser son compte Cloud](https://console.adobecommerce.com) avant de pouvoir les ajouter à un projet Cloud.
- Un utilisateur qui se voit attribuer le rôle **Admin** ne peut pas gérer les utilisateurs avec l’interface de ligne de commande `magento-cloud`. Seuls les utilisateurs qui se voient accorder le rôle **Propriétaire du compte** peuvent gérer les utilisateurs.

>[!ENDSHADEBOX]

## Gestion des utilisateurs à l’aide de l’interface en ligne de commande

Utilisez l’interface de ligne de commande `magento-cloud` pour gérer les utilisateurs et les intégrer aux systèmes automatisés :

- `magento-cloud user:add`-ajouter un utilisateur au projet
- `magento-cloud user:delete`-supprimer un utilisateur
- `magento-cloud user:list [users]`-list project users
- `magento-cloud user:role`-afficher ou modifier le rôle de l’utilisateur
- `magento-cloud user:update` : rôle utilisateur de mise à jour sur un projet

Les exemples suivants utilisent l’interface de ligne de commande `magento-cloud` pour ajouter un utilisateur, configurer des rôles, modifier des affectations de projet et affecter des rôles utilisateur.

**Pour ajouter un utilisateur et attribuer des rôles** :

1. Utilisez l’interface de ligne de commande `magento-cloud` pour ajouter l’utilisateur.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >L’utilisateur doit disposer d’un Adobe ID ; voir les [conditions préalables](#add-users-and-manage-access).

1. Suivez les invites : spécifiez l’adresse électronique de l’utilisateur, définissez les rôles de type projet et environnement, puis ajoutez l’utilisateur.

   > Exemples de invites

   ```
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   Une fois l’utilisateur ajouté, Adobe envoie un courrier électronique à l’adresse spécifiée avec des instructions pour accéder au projet d’infrastructure cloud Adobe Commerce.

### Affichage du rôle de projet d’un utilisateur

```bash
magento-cloud user:get alice@example.com
```

>Exemple de réponse :

```
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Ajout d’un utilisateur à plusieurs environnements

Pour ajouter un utilisateur en tant que `viewer` dans un environnement `Production` et en tant que `contributor` dans un environnement `Integration` :

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Mise à jour des autorisations d’environnement utilisateur

Pour mettre à jour les autorisations d’environnement utilisateur vers `admin` sur l’environnement `Production` :

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Gestion des utilisateurs à partir de [!DNL Cloud Console]

Vous pouvez utiliser le [[!DNL Cloud Console]](../../get-started/cloud-console.md) pour ajouter des autorisations et utiliser la fonction _Modifier_ pour modifier les autorisations d’un utilisateur existant.

>[!IMPORTANT]
>
>L’utilisateur doit disposer d’un Adobe ID ; voir les [conditions préalables](#add-users-and-manage-access).

### Ajout d’un utilisateur au projet

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com/).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Dans le tableau de bord du projet, cliquez sur l’icône de configuration en haut à droite.

1. Sous _Paramètres du projet_, cliquez sur **[!UICONTROL Access]**.

1. Dans la vue _Accès_, cliquez sur **[!UICONTROL Add]**.

1. Remplissez le formulaire _[!UICONTROL Add User]_:

   - Saisissez l’adresse électronique de l’utilisateur.

   - **[!UICONTROL Project admin]** : accordez des droits d’administrateur à tous les paramètres et types d’environnements.

   - **[!UICONTROL Environment types and permissions]** : accordez l’accès et des niveaux d’autorisation spécifiques à certains types d’environnements. _Aucun accès_, _Admin_ (modifier les paramètres, exécuter une action, fusionner le code), _Contributor_ (code push) ou _Observateur_ (affichage uniquement).

   >[!TIP]
   >
   >Seul un **administrateur de projet** peut gérer les utilisateurs dans n’importe quel environnement. Pour accorder à un utilisateur l’accès à l’onglet **Accès**, un autre **administrateur de projet** ou le **propriétaire de compte** doit affecter à cet utilisateur le rôle **administrateur de projet**.

1. Cliquez sur **[!UICONTROL Add User]**.

   >[!IMPORTANT]
   >
   >L’ajout d’un utilisateur ne déclenche pas automatiquement un déploiement.

1. Après avoir ajouté des utilisateurs, redéployez tous les environnements pour appliquer les modifications. L’ajout d’un utilisateur ne déclenche pas automatiquement un déploiement. Le redéploiement est une étape importante pour s’assurer que l’utilisateur peut accéder à un environnement à l’aide de SSH ou effectuer des tâches d’administrateur.

Une fois l’utilisateur ajouté, Adobe envoie un courrier électronique à l’adresse spécifiée avec des instructions pour accéder au projet d’infrastructure cloud Adobe Commerce.

## Exigences d’authentification des utilisateurs

Pour plus de sécurité, Adobe fournit une application d’authentification multifactorielle au niveau du projet (MFA) qui nécessite une authentification à deux facteurs (TFA) pour l’accès SSH à Adobe Commerce sur le code source et les environnements du projet d’infrastructure cloud. Voir [Activation de MFA pour SSH](multi-factor-authentication.md).

Lorsque l’application MFA est activée sur un projet d’infrastructure cloud Adobe Commerce, tous les utilisateurs disposant d’un accès SSH à un environnement dans ce projet doivent activer TFA sur leur compte d’infrastructure cloud Adobe Commerce. Pour les processus automatisés, vous pouvez créer un utilisateur de machine et un jeton API pour vous authentifier à partir de la ligne de commande.

Après avoir ajouté un utilisateur à un projet Cloud, demandez à l’utilisateur de vérifier les paramètres de sécurité de son compte et d’ajouter les configurations de sécurité suivantes, le cas échéant :

- **Activer TFA** : répondez aux normes de sécurité et de conformité en configurant une authentification à deux facteurs. Les projets configurés avec l’ [application MFA](multi-factor-authentication.md) nécessitent TFA sur les comptes qui utilisent SSH pour accéder aux projets.

- **Activer les clés SSH** : les utilisateurs qui ont besoin d’accéder à Adobe Commerce sur les référentiels de code source de l’infrastructure cloud doivent activer les clés SSH sur leur compte. Voir [Connexions sécurisées](../development/secure-connections.md).

- **Créer un jeton API** : les utilisateurs doivent générer un jeton API utilisé pour accéder à un environnement SSH. Vous avez besoin du jeton pour activer les workflows d’authentification pour les processus automatisés.

  Sur les projets pour lesquels l’application de la loi MFA est activée, vous devez utiliser le jeton API pour authentifier les demandes d’accès SSH provenant de comptes automatisés. Le jeton permet aux processus automatisés de contourner les workflows d’authentification qui nécessitent TFA.

### Activation de TFA pour les comptes cloud

Adobe Commerce sur l’infrastructure cloud prend en charge TFA à l’aide de l’une des applications suivantes :

- [Authentificateur Google (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Auteur (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [Authentificateur GAuth (Firefox OS, bureau, autres)](https://github.com/gbraad-apps/gauth)

Les instructions d’installation de l’application d’authentification et d’activation de TFA sont disponibles sur la page _Paramètres du compte_ dans [!DNL Cloud Console].

**Pour activer TFA sur votre compte utilisateur** :

1. Connectez-vous à [votre compte](https://console.adobecommerce.com).

1. Dans le menu supérieur droit du compte, cliquez sur **[!UICONTROL My Profile]**.

1. Sur l&#39;onglet _Sécurité_, cliquez sur **[!UICONTROL Set up application]**.

1. Si vous ne disposez pas d’une application d’authentification approuvée sur votre périphérique mobile, utilisez les instructions associées pour l’installer.

1. Ajoutez votre compte Adobe Commerce sur l’infrastructure cloud à l’application d’authentification.

   - Sur votre périphérique mobile, ouvrez l’application d’authentification. Ajoutez ensuite le code de configuration à l’application.

   - Sur la page [!UICONTROL **[!UICONTROL TFA set up - Application]**], saisissez le code TFA de votre appareil mobile dans le champ **[!UICONTROL Application verification code]** .

   - Cliquez sur **[!UICONTROL Verify and save]**.

     Si le code est valide, Adobe envoie une notification à l’adresse électronique du compte confirmant que le compte dispose désormais de TFA.

1. Facultatif. Activez les paramètres _Navigateur approuvé_ pour mettre en cache le code d’authentification dans le navigateur pendant 30 jours.

   Cette configuration réduit le nombre de problèmes d’authentification lors de la connexion au projet.

1. Cliquez sur **Enregistrer** ou **Ignorer**.

1. Enregistrez les codes de récupération.

   - Sur la page _Configuration TFA - Codes de récupération_ , copiez et enregistrez les codes de récupération afin que vous puissiez vous connecter à votre projet d’infrastructure cloud Adobe Commerce lorsque vous ne pouvez pas accéder à votre appareil mobile ou à votre application d’authentification.

   - Copiez les codes de récupération à un autre emplacement ou notez-les si vous ne pouvez plus accéder à votre périphérique ou application d’authentification.

   - Cliquez sur **Enregistrer** pour enregistrer les codes dans votre compte afin de pouvoir les afficher et les gérer à partir des paramètres de sécurité de votre compte.

     >[!WARNING]
     >
     >Si vous n’avez plus accès à un compte avec TFA et que vous ne disposez pas de la liste des codes de récupération, vous devez contacter votre administrateur de projet ou [Soumettre un ticket de support Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour réinitialiser l’application TFA.

1. Une fois la configuration TFA terminée, cliquez sur **Enregistrer** pour mettre à jour votre compte.

1. Authentifiez la session en cours avec TFA.

   - Déconnectez-vous de votre compte.
   - Connectez-vous avec votre nom d’utilisateur et votre mot de passe.
   - Lorsque vous y êtes invité, saisissez le code TFA pour l’entrée `accounts.magento.cloud` de l’application d’authentification sur votre appareil mobile.

### Gestion des codes de configuration et de récupération TFA

Vous pouvez gérer la configuration TFA d’un compte Adobe Commerce sur l’infrastructure cloud à partir de la section _Sécurité_ de la page _Mon profil_.

1. Connectez-vous à [votre compte](https://console.adobecommerce.com).

1. Dans le menu supérieur droit du compte, cliquez sur **[!UICONTROL My Profile]**.

1. Sur la page _My Profile_, cliquez sur l’onglet **[!UICONTROL Security]** .

1. Utilisez les liens disponibles pour mettre à jour les paramètres TFA de votre compte Adobe Commerce sur l’infrastructure cloud :

   - Désactiver TFA
   - Réinitialisation de l’application d’authentification
   - Ajout ou suppression de navigateurs approuvés
   - Afficher ou actualiser les codes de récupération TFA sur votre compte

### Création d’un jeton API

Un jeton API peut être échangé contre un jeton d’accès OAuth 2, qui peut ensuite être utilisé pour authentifier les requêtes.

Sur les projets pour lesquels l’application de la loi MFA est activée, vous devez disposer d’un jeton API pour activer l’accès SSH pour les utilisateurs de la machine et les processus automatisés.

>[!IMPORTANT]
>
>Valeurs de jeton API Protect pour votre compte. N’exposez pas la valeur dans des exemples de code, des captures d’écran ou des communications client-serveur non sécurisées. De plus, n’exposez pas la valeur dans le code source stocké dans des référentiels publics.

**Pour créer un jeton API** :

1. Connectez-vous à [votre compte](https://console.adobecommerce.com).

1. Dans le menu supérieur droit du compte, cliquez sur **[!UICONTROL My Profile]**.

1. Sur la page _My Profile_, cliquez sur l’onglet **[!UICONTROL API tokens]** .

1. Cliquez sur **[!UICONTROL Create API token]** et saisissez un nom, par exemple, qui correspond à l’utilisateur de la machine ou au processus automatisé qui utilise le jeton API.

   ![Jetons API](../../assets/api-token-name.png)

1. Cliquez sur **[!UICONTROL Create API token]**.
