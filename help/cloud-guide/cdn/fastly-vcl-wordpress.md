---
title: Rétablir les requêtes vers le serveur principal CMS
description: Découvrez comment réacheminer les requêtes entrantes d’un magasin Adobe Commerce vers un site WordPress distinct à l’aide du module Fastly Edge.
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Rétablir les requêtes vers le serveur principal CMS

Déplacez les requêtes entrantes d’un magasin Adobe Commerce vers un site WordPress distinct à l’aide du module Edge Fastly _Autre intégration CMS/back-end_ avec un dictionnaire Edge. Vous pouvez suivre un processus similaire pour dédiriger les requêtes vers d’autres serveurs principaux de CMS.

Utilisez des modules Edge rapides pour créer et charger du code VCL personnalisé à partir de l’administrateur au lieu d’écrire manuellement le code VCL et de le charger à l’aide de l’API Fastly.

>[!NOTE]
>
>Nous vous recommandons d’ajouter des configurations VCL personnalisées à un environnement d’évaluation dans lequel vous pouvez les tester avant de mettre à jour la configuration de service Fastly dans l’environnement de production.

**Conditions préalables**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Pour faire dévier des requêtes d’Adobe Commerce vers WordPress** :

1. Activez les modules Edge rapides dans l’environnement d’évaluation ou de production.

   - Connectez-vous à l’administrateur.

   - Accédez à **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** > **Cache de page complet** > **Configuration rapide** > **Configuration avancée**.

   - Définissez la valeur de **Fastly Edge Modules** sur **Yes**.

   - Enregistrez la configuration.

1. Identifiez les chemins d’URL à rediriger vers le serveur principal WordPress.

1. Effectuez les tâches suivantes pour configurer le service Fastly et créer le code VCL personnalisé pour la redirection des requêtes vers le serveur principal WordPress.

   - Créez un dictionnaire Edge qui spécifie les chemins d’accès à faire défiler de la boutique Adobe Commerce vers le serveur principal.

   - Ajoutez le serveur principal WordPress à la configuration de service Fastly et joignez la condition de demande pour les réécritures d’URL.

   - Configurez le module Edge _Autre intégration CMS/serveur principal_ pour gérer les réécritures d’URL d’Adobe Commerce vers le serveur principal WordPress.

     Pour obtenir des instructions détaillées, reportez-vous à la section [Modules Edge Fastly - Autres intégrations CMS/backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) dans la documentation _Module CDN Fastly pour Magento 2_ .

1. Après avoir mis à jour la configuration du service Fastly, testez votre boutique Adobe Commerce pour vous assurer que les requêtes d’URL spécifiées pour WordPress sont correctement redirigées.
