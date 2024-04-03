---
title: "Connexion à [!DNL Cloud Console]"
description: En savoir plus sur les [!DNL Cloud Console] pour l’infrastructure Adobe Commerce on Cloud.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Connexion à [!DNL Cloud Console]

La variable [!DNL Cloud Console] fournit des méthodes interactives pour créer, gérer et déployer le code Commerce. La variable [!DNL Cloud Console] est une expérience plus moderne et conviviale qui jette les bases d’améliorations futures de l’interface.

[Connectez-vous au [!DNL Cloud Console]](https://console.adobecommerce.com) pour afficher la liste de vos projets.

![Liste des projets](../assets/ui-allprojects-list.png)

## Fonctionnalités

Les fonctionnalités nouvelles ou améliorées sont les suivantes :

- Présentation claire des caractéristiques de projet et d’environnement
- Flux d’activité avec historique pouvant être trié
- Gestion et historique manuels des sauvegardes pour les projets de démarrage
- Amélioration des vues de journal
- Tri des listes
- Formulaires simples et conseils pour ajouter des intégrations
- Conformité aux règles WCAG (Web Content Accessibility Guidelines)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

Les fonctionnalités nouvelles ou améliorées sont les suivantes :

| Fonctionnalité | Améliorations |
| -------------- | ----------------------------------- |
| [Flux d’activité](../cloud-guide/project/activity-stream.md) | Interagissez avec une liste triable d’actions en cours, en attente ou historiques. Sélectionnez une activité et affichez les journaux ou annulez une version en cours d’exécution. |
| [Aperçu du projet et de l’environnement](../cloud-guide/project/overview.md#project-overview) | Ouvrez votre projet et affichez l’aperçu des détails du projet et de la liste de l’environnement. La présentation de l’environnement fournit des détails supplémentaires sur l’état de l’environnement, l’accès aux applications et les activités récentes. |
| [Formulaires d’intégration](../cloud-guide/integrations/overview.md) | Utilisez des formulaires simples et des conseils pour ajouter des intégrations, telles que des notifications Bitbucket ou Slack. |
| [Liste des projets](../cloud-guide/project/overview.md#cloud-console) | La variable _Tous les projets_ affiche la liste de tous les projets auxquels vous êtes autorisé à accéder. Cliquez sur **[!UICONTROL Show filters]** et filtrez votre liste de projets par type, région ou plan. |
| [Options de visibilité variable](../cloud-guide/environment/variable-levels.md) | Limitez la visibilité d’une variable au niveau du projet ou de l’environnement lors de la création ou de l’exécution. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Questions relatives à la console

**_Où puis-je trouver la fonction Instantanés ?_**?

Pour [!DNL Starter] projets, la fonction Instantanés est désormais appelée _Sauvegardes_. Vous pouvez créer une sauvegarde manuelle de votre [!DNL Starter] de l’environnement [!DNL Cloud Console] ou créez un instantané à partir de l’interface de ligne de commande de Cloud. Vous devez disposer d’un rôle d’administrateur pour l’environnement.

Sélectionnez un environnement dans la barre de navigation du projet. L’environnement doit être actif. Sélectionnez la variable **[!UICONTROL Backups]** . Actuellement, cette option n’est pas disponible pour les environnements Pro.

**_Où est la liste des itinéraires configurés pour l’environnement_**?

Vous trouverez la liste des itinéraires configurés sur la page _Services_ pour un environnement.

Sélectionnez un environnement dans la barre de navigation du projet. Sélectionnez la variable **[!UICONTROL Services]** . La variable **Routeur** La vue d’ensemble affiche les itinéraires configurés. Actuellement, vous ne pouvez pas ajouter d’itinéraire à partir de la nouvelle [!DNL Cloud Console].

## Menu Compte

Le menu Compte se trouve dans le coin supérieur droit. Cliquez sur la flèche vers le bas du menu, puis sélectionnez **[!UICONTROL My Profile]**. Dans le _Mon profil_ afficher, vous pouvez contrôler les détails de votre utilisateur et afficher les paramètres, gérer [authentification de sécurité](../cloud-guide/project/user-access.md#user-authentication-requirements), [Jetons API](../cloud-guide/project/user-access.md#create-an-api-token), et [Clés SSH](../cloud-guide/development/secure-connections.md).
