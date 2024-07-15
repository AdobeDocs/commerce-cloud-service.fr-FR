---
title: "Connectez-vous à [!DNL Cloud Console]"
description: Découvrez l’ [!DNL Cloud Console]  pour l’infrastructure Adobe Commerce on Cloud.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Connectez-vous à [!DNL Cloud Console]

[!DNL Cloud Console] fournit des méthodes interactives pour créer, gérer et déployer le code Commerce. [!DNL Cloud Console] est une expérience plus moderne et conviviale qui jette les bases d’améliorations futures de l’interface.

[Connectez-vous à  [!DNL Cloud Console]](https://console.adobecommerce.com) pour afficher la liste de vos projets.

![Liste de projets](../assets/ui-allprojects-list.png)

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
| [Flux d’activités](../cloud-guide/project/activity-stream.md) | Interagissez avec une liste triable d’actions en cours, en attente ou historiques. Sélectionnez une activité et affichez les journaux ou annulez une version en cours d’exécution. |
| [Présentation du projet et de l’environnement](../cloud-guide/project/overview.md#project-overview) | Ouvrez votre projet et affichez l’aperçu des détails du projet et de la liste de l’environnement. La présentation de l’environnement fournit des détails supplémentaires sur l’état de l’environnement, l’accès aux applications et les activités récentes. |
| [Formulaires d’intégration](../cloud-guide/integrations/overview.md) | Utilisez des formulaires simples et des conseils pour ajouter des intégrations, telles que des notifications Bitbucket ou Slack. |
| [Liste de projets](../cloud-guide/project/overview.md#cloud-console) | La vue _Tous les projets_ répertorie tous les projets auxquels vous êtes autorisé à accéder. Vous pouvez cliquer sur **[!UICONTROL Show filters]** et filtrer la liste de vos projets par type, région ou plan. |
| [ Options de visibilité variable ](../cloud-guide/environment/variable-levels.md) | Limitez la visibilité d’une variable au niveau du projet ou de l’environnement lors de la création ou de l’exécution. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Questions relatives à la console

**_Où puis-je trouver la fonction Instantanés_** ?

Pour les projets [!DNL Starter], la fonction Instantanés est désormais appelée _Sauvegardes_. Vous pouvez créer une sauvegarde manuelle de votre environnement [!DNL Starter] à partir de [!DNL Cloud Console] ou créer un instantané à partir de l’interface de ligne de commande du cloud. Vous devez disposer d’un rôle d’administrateur pour l’environnement.

Sélectionnez un environnement dans la barre de navigation du projet. L’environnement doit être actif. Sélectionnez l’onglet **[!UICONTROL Backups]** . Actuellement, cette option n’est pas disponible pour les environnements Pro.

**_Où se trouve la liste des itinéraires configurés pour l’environnement_** ?

Vous trouverez la liste des itinéraires configurés sur l’onglet _Services_ pour un environnement.

Sélectionnez un environnement dans la barre de navigation du projet. Sélectionnez l’onglet **[!UICONTROL Services]** . La présentation de **routeur** affiche les itinéraires configurés. Actuellement, vous ne pouvez pas ajouter d’itinéraire à partir du nouvel [!DNL Cloud Console].

## Menu Compte

Le menu Compte se trouve dans le coin supérieur droit. Cliquez sur la flèche vers le bas du menu et sélectionnez **[!UICONTROL My Profile]**. Dans la vue _My Profile_, vous pouvez contrôler les détails de l’utilisateur et les paramètres d’affichage, gérer l’ [authentification de sécurité](../cloud-guide/project/user-access.md#user-authentication-requirements), les [jetons d’API](../cloud-guide/project/user-access.md#create-an-api-token) et les [clés SSH](../cloud-guide/development/secure-connections.md).
