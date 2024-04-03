---
title: Optimisation du déploiement cloud
description: Découvrez comment optimiser le processus de déploiement d’Adobe Commerce sur les projets d’infrastructure cloud, notamment la réduction des temps d’arrêt, le déploiement de contenu statique, le déploiement basé sur des scénarios et les assistants intelligents.
feature: Cloud, Deploy, SCD
exl-id: 62e5eccb-6919-4a4b-9f50-6105f9d0f3af
source-git-commit: 5c47c8bf9c97fac70ef249f76ecc905df07e4437
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Optimisation du déploiement

Les performances du site peuvent en pâtir pendant le processus de déploiement. La durée du déploiement d’un site en mode de maintenance dépend de nombreux facteurs, tels que la configuration de l’environnement et la quantité de contenu qu’il contient. La première bonne pratique pour optimiser le déploiement en mode cloud consiste à [mettre à niveau pour utiliser `ece-tools`](../dev-tools/install-package.md) pour bénéficier des fonctionnalités du package, telles que les commandes permettant de créer une sauvegarde de la base de données et de vérifier la configuration de l’environnement.

Les rubriques suivantes peuvent vous aider à mieux comprendre comment optimiser le processus de déploiement :

- [Processus de déploiement dans le cloud](process.md)
Le processus de déploiement en cloud comporte trois phases. Vous pouvez tirer parti des forces et des faiblesses de chaque phase.

- [Déploiement sans interruption](reduce-downtime.md)
Découvrez ce qui se passe pendant le déploiement et comment réduire le temps d’arrêt de vos expériences de magasin lors d’une mise à jour de l’environnement de production.

- [Déploiement de contenu statique](static-content.md)
La meilleure façon d’optimiser votre déploiement en cloud consiste à contrôler comment et à quel moment générer du contenu statique.

- [Assistant dynamique](smart-wizards.md)
La variable `ece-tools` Le module fournit les commandes de l’assistant dynamique pour évaluer rapidement la configuration de votre projet.

- [Suivi des déploiements avec New Relic](../monitor/track-deployments.md)
Utilisez le service New Relic pour surveiller les événements de déploiement et analyser l’impact du déploiement sur les performances globales.
