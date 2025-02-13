---
title: Service New Relic
description: Découvrez le service New Relic disponible avec votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: b53d5a8d06e0ed249bd44b6f38f837a257cbd315
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Présentation du service New Relic

Tous les projets Adobe Commerce sur l’infrastructure cloud incluent l’accès au service New Relic pour surveiller les performances et enquêter sur les événements de l’application [!DNL Commerce] et de l’infrastructure cloud.

Les fonctionnalités New Relic suivantes peuvent être utilisées avec les environnements de production et d’évaluation :

- [New Relic APM](#new-relic-apm) (Pro and Starter)
- [New Relic Infrastructure](#new-relic-infrastructure) (Pro uniquement)
- [Gestion des journaux New Relic](#new-relic-log-management) (Pro uniquement)

>[!INFO]
>
>D’autres fonctionnalités New Relic ne sont pas disponibles sur les projets Adobe Commerce.

## NEW RELIC APM

[New Relic for application Performance Management (APM)](https://docs.newrelic.com/introduction-apm/) est un produit d’analyse logicielle qui vous aide à analyser et à améliorer les interactions de l’application. New Relic APM est disponible pour tous les projets d’infrastructure cloud d’Adobe Commerce et offre les fonctionnalités suivantes :

- **Concentrez-vous sur des transactions spécifiques** : marquez et surveillez activement les actions clés des clients sur votre site, comme l’ajout au panier, l’extraction ou le traitement d’un paiement.
- **Surveillance des requêtes de base de données** : localisez et surveillez les requêtes de base de données affectant les performances.
- **App Map** : affiche toutes les dépendances de l’application au sein de votre site, des extensions et des services externes.
- **[!DNL Apdex]scores** : évaluez les performances et créez des alertes qui identifient les problèmes et vous avertissent lorsqu’ils se produisent, comme les performances du site affectées par une vente flash ou un événement web. Voir [Score d’application](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Alertes gérées pour Adobe Commerce** - Utilisez cette stratégie d’alerte New Relic pour surveiller les performances de l’application et de l’infrastructure en fonction des bonnes pratiques du secteur. Voir [Surveillance des performances avec la stratégie d’alerte Gestion des alertes pour Adobe Commerce](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **Suivi des déploiements** : surveillez les événements de déploiement et analysez l’impact du déploiement sur les performances globales. Voir [Suivi des déploiements](track-deployments.md).

Votre projet d’infrastructure de cloud Adobe Commerce comprend le logiciel du service New Relic APM, ainsi qu’une clé de licence. Vous n’avez pas besoin d’acheter ou d’installer des logiciels supplémentaires.

## Infrastructure New Relic

Les projets Pro incluent le service [New Relic Infrastructure (NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/), qui se connecte automatiquement aux données d’application et à l’analyse des performances pour fournir une surveillance dynamique du serveur. Ce service est disponible dans les environnements Pro Production et Test.

## Gestion des journaux New Relic

Tous les projets d’infrastructure de cloud comprennent [ la gestion des journaux New Relic](log-management.md). Le service est préconfiguré pour agréger toutes les données de journal de vos environnements d’évaluation et de production et les afficher dans un tableau de bord de gestion des journaux centralisé.
