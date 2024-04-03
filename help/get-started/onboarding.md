---
title: '[!DNL Onboarding] à Commerce'
description: Accédez à votre compte cloud et configurez un projet d’infrastructure cloud Adobe Commerce.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] vers Commerce

Une fois qu’Adobe a activé un abonnement Commerce sur l’infrastructure cloud, le projet initial et l’accès au code ne sont disponibles que pour la personne désignée comme propriétaire de licence (propriétaire du compte).

Le propriétaire de la licence est la personne au sein de votre entreprise ou de votre organisation financière qui gère les paiements et autres transactions liées à l’entreprise pour le compte d’infrastructure cloud d’Adobe Commerce. Cette personne sert de point de contact avec l’Adobe. Si vous devez modifier le propriétaire de la licence sur votre compte, vous devez contacter votre équipe de compte d’Adobe.

Pour intégrer rapidement votre projet, afin de pouvoir commencer à développer votre site pour un déploiement en direct, vous devez effectuer la configuration requise et [!DNL onboarding] tâches. En règle générale, le propriétaire de la licence commence le processus en sécurisant l’accès administrateur et en créant des utilisateurs administrateurs techniques qui peuvent vous aider à configurer, personnaliser et travailler sur le développement.

## S’inscrire à un compte Cloud

Si vous ne disposez pas d’un compte Adobe Commerce sur l’infrastructure cloud, contactez [Ventes]. Lorsque vous vous inscrivez, Adobe crée votre compte et vous envoie un e-mail de bienvenue qui explique comment accéder à l’interface du projet. L’e-mail contient un lien qui vous permet de vous connecter à votre compte et de terminer la configuration initiale du projet.

### Cloud [!DNL Onboarding] Interface utilisateur

La page Adobe Commerce sur le projet d’infrastructure cloud dans ([!DNL Onboarding] (IU) fournit une liste de contrôle Prise en main pour configurer votre projet et vos services, déterminer l’accès et commencer à développer. À partir de l’API, vous pouvez :

- Ajoutez un administrateur technique, un super-utilisateur qui peut gérer votre projet et vos branches.
- Accédez à votre environnement de projet, y compris un lien vers la [!DNL Cloud Console]
- Remplissez une liste de contrôle de test d’acceptation rapide des utilisateurs avec des liens vers d’autres tests.

**Pour ouvrir la page du projet**:

1. Connectez-vous à [Compte client Adobe Commerce](https://account.magento.com/customer/account/login).

1. Sur le _Mon compte_ , cliquez sur **[!UICONTROL Commerce]** pour afficher les projets dans votre compte.

1. Cliquez sur **Afficher la page du projet** dans le [Section Projets](https://cloud.magento.com/cloud/project/).

1. Cliquez sur le nom du projet et ouvrez la page Projet cloud ([!DNL Onboarding] ).

   ![Page du projet OBUI](../assets/onboarding-ui.png)

   Parcourez le portail pour obtenir des informations et des options utiles afin de commencer à planifier votre projet, à développer du code et à préparer le lancement du site et de l’UAT.

## Accès au projet et ajout d’utilisateurs

Le propriétaire de la licence peut ajouter des comptes d’utilisateurs pour permettre l’accès au code, gérer les branches, saisir des tickets et des environnements de support. Ces comptes d’utilisateurs peuvent inclure des spécialistes du développement interne, des consultants et des solutions.

En règle générale, le seul utilisateur que le propriétaire de la licence doit créer est le _Administrateur technique_. L’administrateur technique doit disposer d’un compte utilisateur disposant d’un accès administrateur pour créer des comptes utilisateur pour les développeurs, définir des autorisations d’environnement et gérer toutes les branches et tous les environnements. L’administrateur technique peut être un développeur, un consultant, un [Partenaire en solutions Adobe](https://business.adobe.com/products/magento/partners.html)ou vous-même.

Vous pouvez créer un administrateur technique via le portail de projet, à partir du [!DNL Cloud Console]ou à partir de la ligne de commande à l’aide de la fonction `magento-cloud` Interface de ligne de commande.

### Enregistrement d’utilisateur

Vous pouvez uniquement ajouter des utilisateurs enregistrés à votre Adobe Commerce sur des projets et des environnements d’infrastructure cloud. Si vous disposez d’un nouvel utilisateur, demandez-lui de [enregistrement d’un compte](https://account.magento.com/customer/account/login/) et pour indiquer l’adresse électronique associée à leur profil de compte.

### Accès au compte partagé

Le propriétaire de la licence peut configurer l’accès partagé pour le compte. L’accès partagé permet aux employés et aux fournisseurs de services de confiance d’utiliser le centre d’aide pour envoyer et suivre les tickets d’assistance associés à votre Adobe Commerce sur les projets d’infrastructure cloud. Pour obtenir des instructions sur la configuration, voir [Accès partagé] dans le centre d’aide.

### [!DNL Cloud Console]

Vous pouvez utiliser la variable [[!DNL Cloud Console]](cloud-console.md) pour gérer votre projet, ajoutez des comptes d’utilisateurs et commencez à développer votre magasin. Le propriétaire de la licence, les utilisateurs administrateurs techniques et les développeurs peuvent utiliser la variable [!DNL Cloud Console] pour gérer tous les environnements et branches, variables d’environnement, paramètres d’environnement et itinéraires.

**Pour accéder au[!DNL Cloud Console]**:

1. Connexion à [Mon compte](https://account.magento.com/customer/account/login).

1. Sur le _Mon compte_ , cliquez sur **[!UICONTROL Commerce]** pour afficher les projets dans votre compte.

1. Cliquez sur le bouton **Projets** et sélectionnez un projet.

1. Cliquez sur **Accès aux infrastructures**, puis cliquez sur **Accès au projet (interface utilisateur web)**.

   ![Portail de projet Cloud](../assets/obui-project-access.png)

## Inscrivez-vous au statut Adobe

Découvrez les mises à jour d’Adobe Commerce sur les environnements de plateforme d’infrastructure cloud et les services connexes à partir de [Page d’état].

La page fournit un état pour les composants et services Adobe Commerce, suivi de notifications sur les rapports d’incident, les mises à niveau de service, les pannes planifiées et la maintenance planifiée. Toute personne travaillant sur votre projet peut s’abonner au site d’état Adobe Commerce pour recevoir des notifications d’événement et des mises à jour par courrier électronique ou par Slack. Vous pouvez personnaliser l’abonnement à l’état de votre Adobe pour effectuer le suivi de produits spécifiques par régions et événements.

>[!TIP]
>
> Ouvrez le nouveau [!DNL Cloud Console] et afficher les activités de projet et d’environnement.
>
>**Étape suivante**: [Connectez-vous à la console LC[!DNL ]oud](cloud-console.md)

<!-- link definitions -->

[Ventes]: https://business.adobe.com/products/magento/get-demo.html
[Accès partagé]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Page d’état]: https://status.adobe.com/products/503473
