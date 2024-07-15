---
title: Préparation au développement
description: Rassemblez les informations d’identification et découvrez les outils disponibles pour configurer un espace de travail de développement à utiliser avec votre projet d’infrastructure cloud Commerce.
recommendations: noDisplay, catalog
exl-id: 8f88161f-3580-453b-b977-2c6e3824cc02
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Préparation au développement

Que vous soyez nouveau dans Commerce ou propriétaire de Commerce que vous passiez vers l’infrastructure cloud, procédez comme suit pour préparer un espace de travail de développement pour votre projet Cloud. Si vous avez déjà terminé certaines de ces étapes ou si vous disposez d’un environnement de développement Adobe Commerce existant, passez en revue les résultats attendus ci-après et passez à l’étape suivante. Certaines configurations et certains workflows diffèrent d’une installation classique sur site.

## Informations d’identification

Avant de configurer un espace de travail, réunissez les clés et l’accès au compte suivants :

- **Clés d’authentification (clés du compositeur)**

  Les clés d’authentification sont des jetons d’authentification à 32 caractères qui permettent un accès sécurisé au référentiel du compositeur d’Adobe Commerce (`repo.magento.com`) et à tout autre service Git requis pour le développement d’applications telles que GitHub. Votre compte peut comporter plusieurs clés d’authentification. Pour la configuration de l’espace de travail, commencez par une clé spécifique pour votre référentiel de code. Si vous ne disposez d’aucune clé, contactez le propriétaire du projet ou créez vous-même les [clés d’authentification](../cloud-guide/development/authentication-keys.md).

- **Compte de projet cloud**

  Le propriétaire du projet doit vous inviter à rejoindre Adobe Commerce sur le projet d’infrastructure cloud. Lorsque vous recevez l’invitation par courrier électronique, cliquez sur le lien et suivez les invites pour créer votre compte. Voir [Intégration](onboarding.md).

- **Clé de chiffrement Adobe Commerce**

  Lors de l’importation d’un système existant uniquement, capturez la clé de chiffrement utilisée pour protéger votre accès et vos données pour la base de données. Pour plus d’informations sur cette clé, voir [Résolution des problèmes liés à la clé de chiffrement](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html)

## Outils de développement

- **Installation de l’interface de ligne de commande de Cloud**

  Installez l’interface de ligne de commande `magento-cloud` afin de pouvoir gérer les environnements cloud et exécuter des tâches d’automatisation. Voir [Interface en ligne de commande de Cloud](../cloud-guide/dev-tools/cloud-cli-overview.md) pour obtenir des instructions d’installation.

- **Installer Docker pour le développement et le test locaux**

  Si vous le souhaitez, utilisez l’environnement Docker pour émuler l’environnement Commerce sur l’infrastructure cloud `integration` pour le développement local. Il existe trois composants essentiels : un modèle Adobe Commerce v2, un composant Docker et un package `ece-tools`.

   - [Architecture de Docker et commandes courantes](../cloud-guide/dev-tools/cloud-docker.md)
   - [ Environnement de développement Launch Docker ](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
   - [Package de outils CEE](../cloud-guide/dev-tools/package-overview.md)

- **Intégrer des services basés sur Git**

  Vous pouvez éventuellement intégrer un service d’hébergement basé sur Git, tel que GitHub ou GitLab, à Adobe Commerce sur l’infrastructure cloud. Voir [Intégrations](../cloud-guide/integrations/overview.md).

## Code du projet

Une connexion sécurisée est essentielle pour interagir avec les environnements distants. Pour un nouveau projet, [ connectez-vous à  [!DNL Cloud Console]](https://console.adobecommerce.com) et cliquez sur **[!UICONTROL No SSH key]**. Cette icône est située à droite du champ de commande et est visible lorsque le projet ne contient pas de clé SSH. Voir [Connexions sécurisées](../cloud-guide/development/secure-connections.md#add-an-ssh-public-key-to-your-account).

**Pour cloner votre base de code vers votre poste de travail local** :

1. Dans [[!DNL Cloud Console]](https://console.adobecommerce.com), cliquez sur **[!UICONTROL code]** et sélectionnez l’onglet **[!UICONTROL Git]** .

   ![Cloner votre code](../assets/ui-git-code.png){width="450"}

1. Copiez la commande `git clone ...` fournie.

1. Dans un terminal, créez et modifiez votre répertoire de travail.

1. Collez et exécutez la commande `git clone ...`.

>[!TIP]
>
>Adobe fournit votre environnement de projet initial à l’aide d’un référentiel de modèles contenant des instructions de package pour une version spécifique d’Adobe Commerce. Passez en revue la rubrique [structure de fichier de projet](../cloud-guide/project/file-structure.md) et découvrez les fichiers de projet importants et les modèles cloud.
