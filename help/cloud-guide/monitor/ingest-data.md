---
title: Ingestion des données
description: Découvrez comment afficher et gérer l’ingestion de données Commerce dans New Relic.
feature: Cloud, Observability
exl-id: f88bf20c-604b-4986-b71c-bb726b2f00b8
source-git-commit: bf3debc5986d51a721537b52ffced58b2ee521ea
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Ingestion des données

New Relic dépend de données riches pour fournir une surveillance et une analyse efficaces, mais des jeux de données volumineux peuvent affecter les résultats, les performances et la conformité en temps voulu. Cette rubrique fournit des conseils sur la gestion de l’ingestion des données et des stratégies pour affiner vos données afin qu’elles soient les plus efficaces.

New Relic fournit une vue _Data Management_ qui résume l’utilisation de votre plan par source de données.

**Pour afficher vos données d’ingestion et vos sources** :

1. Dans le menu utilisateur de New Relic, cliquez sur **[!UICONTROL Manage your data]**.
1. Cliquez sur **[!UICONTROL Data management]** dans la liste _Administration_.

   ![Gestion des données](../../assets/new-relic/data-ingestion.png)

   L’onglet **[!UICONTROL Data ingestion]** affiche les données ingérées pour le jour et la source des données.
L’onglet Conservation des données affiche et contrôle la durée de stockage des données.

1. Sélectionnez l’onglet **[!UICONTROL Limits]** et affichez les limites de votre compte.

Les sources de données pour Adobe Commerce incluent :

- **événements APM** : données d’événement utilisées dans les graphiques et les tableaux de bord
- **Infrastructure** : processus et mesures d’hôte telles que le processeur, le stockage, la mise en réseau
- **Journalisation** : journaux pour CDN, APM et serveur d’applications

Les données de journal contribuent à une grande partie de l’ingestion. Découvrez comment [afficher et analyser les données de journal](log-management.md#view-and-analyze-log-data) et travailler avec votre représentant d’Adobe pour former une stratégie pour l’ingestion et la conservation des données. Pour en savoir plus sur la [gestion de l’ingestion de données](https://docs.newrelic.com/docs/data-apis/manage-data/manage-data-coming-new-relic/), consultez la _documentation de New Relic_.
