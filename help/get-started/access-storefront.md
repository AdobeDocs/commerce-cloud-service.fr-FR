---
title: Accès à votre panneau d’administration Commerce
description: Découvrez comment accéder à votre panneau d’administration Commerce.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 3ca09243dc0a714c1d86cccf9f0620a8a39fd1e1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Accès à votre panneau d’administration Commerce

Les utilisateurs disposant d’un accès administratif au panneau d’administration de Commerce peuvent ajouter des utilisateurs, configurer les services de magasin, terminer la configuration et la personnalisation du magasin, etc.

Pour un nouveau projet, la première étape après réception de l’e-mail de bienvenue consiste à sécuriser l’accès administrateur au projet en modifiant le mot de passe sur le compte du propriétaire de la licence. Le nom d’utilisateur par défaut de ce compte est l’adresse électronique du propriétaire de la licence.

Vous pouvez envoyer une demande de modification de mot de passe en utilisant l’une des méthodes suivantes :

- Recherchez l’e-mail de bienvenue envoyé à l’adresse électronique du propriétaire de la licence, suivez le lien et modifiez votre mot de passe.

- Copiez l’URL du magasin de [[!DNL Cloud Console]](../cloud-guide/project/overview.md) dans un navigateur. Ensuite, ajoutez `/admin` à la fin de l’URL pour ouvrir la page de connexion. Cliquez sur le **mot de passe oublié ?** pour envoyer une demande de modification de mot de passe à l’adresse électronique du propriétaire de la licence.

Une fois que vous avez envoyé la demande de modification de mot de passe, vérifiez que vous avez reçu la notification de réinitialisation du mot de passe par courrier électronique. Si vous n’obtenez pas l’email, vérifiez votre dossier de messages indésirables.

>[!TIP]
>
>Si la réinitialisation du mot de passe échoue ou si vous ne pouvez pas vous connecter au panneau d’administration, un utilisateur disposant d’un accès administrateur peut se connecter au projet à l’aide du SSH et ajouter un utilisateur administrateur à l’aide de la commande d’interface de ligne de commande `admin:user:create`. Voir [Créer, modifier ou déverrouiller un compte administrateur](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) dans le _Guide d&#39;installation_.

## Surveillance de l’intégrité du site

L’ [outil d’analyse à l’échelle du site](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) est un outil en libre-service proactif et un référentiel central qui comprend des informations détaillées sur le système et des recommandations pour garantir la sécurité et la maniabilité de votre installation Adobe Commerce. Il fournit 24/7 surveillance des performances, rapports et conseils en temps réel afin d’identifier les problèmes potentiels et d’améliorer la visibilité sur l’intégrité, la sécurité et les configurations d’application du site. Cela permet de réduire le temps de résolution et d’améliorer la stabilité et les performances du site. Vous pouvez accéder à l’outil d’analyse à l’échelle du site directement à partir du [panneau d’administration](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-2-logging-in-to-your-site-wide-analysis-tool-dashboard-from-your-stores-admin-panel) ou du [ domaine dédié](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/access#option-1-logging-in-to-your-site-wide-analysis-tool-dashboard-directly-from-the-site-wide-analysis-tool-domain-for-adobe-commerce-on-cloud-infrastructure-only) (Adobe Commerce sur les projets d’infrastructure cloud uniquement).
