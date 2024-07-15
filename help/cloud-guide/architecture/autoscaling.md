---
title: Mise à l’échelle automatique
description: Découvrez comment Adobe Commerce sur l’infrastructure cloud peut évoluer pour répondre aux besoins en ressources.
feature: Cloud, Auto Scaling
topic: Architecture
exl-id: 2ba49c55-d821-4934-965f-f35bd18ac95f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Mise à l’échelle automatique

La mise à l’échelle automatique ajoute ou supprime automatiquement des ressources à l’infrastructure cloud pour maintenir des performances optimales et des coûts raisonnables. Actuellement, cette fonctionnalité n’est disponible que pour les projets configurés avec une [architecture mise à l’échelle](scaled-architecture.md).

## Noeuds de serveur web

Le [niveau web](scaled-architecture.md#web-tier) est mis à l’échelle pour répondre à une augmentation des requêtes de processus et à des exigences de trafic plus élevées. Actuellement, la fonction de mise à l’échelle automatique ne se met à l’échelle qu’horizontalement en ajoutant ou en supprimant des noeuds de serveur web.

Un événement de mise à l’échelle automatique se produit lorsque l’utilisation du processeur et le trafic atteignent un seuil prédéfini :

- **Noeuds ajoutés** : les processeurs/coeurs sur tous les noeuds web actifs ont une capacité de 75 % pendant 1 minute et le trafic augmente de 20 % pour 5 minutes consécutives.
- **Nodes supprimés** : les processeurs/coeurs de tous les noeuds web actifs sont chargés à 60 % pendant 20 minutes. Les noeuds sont supprimés dans l’ordre dans lequel ils ont été ajoutés.

Les seuils minimal et maximal sont déterminés et définis en fonction des limites de ressources contractuelles de chaque commerçant, ce qui réduit le risque d’une mise à l’échelle infinie.

## Surveiller les seuils avec New Relic

Vous pouvez utiliser le [service New Relic](../monitor/new-relic-service.md) pour surveiller certains seuils, tels que le nombre d’hôtes et l’utilisation du processeur. Les requêtes New Relic suivantes utilisent une notation de variable pour `cluster-id` à des fins d’exemple uniquement.

>[!TIP]
>
>Pour une référence sur la création de requêtes, voir [Syntaxe NRQL, clauses et fonctions](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) dans la documentation _New Relic_.
>Utilisez vos requêtes pour créer un [tableau de bord New Relic](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### Nombre d’hôtes

L’exemple de requête New Relic suivant montre le nombre d’hôtes dans l’environnement :

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

Dans la capture d’écran suivante, **Hôtes APM vus** fait référence au nombre d’hôtes avec des transactions enregistrées pendant la période sélectionnée.

![Nombre d’hôtes New Relic](../../assets/new-relic/host-count.png)

### Utilisation du processeur

L’exemple de requête New Relic suivant montre l’utilisation du processeur pour les noeuds web :

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![Utilisation du processeur des noeuds web New Relic](../../assets/new-relic/web-node-cpu-usage.png)

## Activation de la mise à l’échelle automatique

Pour activer ou désactiver la mise à l’échelle automatique pour votre projet Adobe Commerce sur l’infrastructure cloud, [ envoyez un ticket d’assistance Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Sélectionnez les raisons suivantes dans le ticket :

- **Raison de contact** : demande de changement d’infrastructure
- **Raison de contact de l’infrastructure Adobe Commerce** : autre demande de modification de l’infrastructure

>[!IMPORTANT]
>
>La fonction de mise à l’échelle automatique capture les événements imprévus. Même si la mise à l’échelle automatique est activée, Adobe vous recommande de continuer à [Soumettre un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) si vous prévoyez un événement à venir.

### Test de chargement

Adobe active d’abord la mise à l’échelle automatique sur votre grappe _staging_ de projet Cloud. Une fois les tests de chargement effectués dans votre environnement, Adobe active la mise à l’échelle automatique sur votre grappe de production. Pour plus d’informations sur les tests de chargement, voir [Test de performance](../launch/checklist.md#performance-testing).

### LISTE AUTORISÉE IP

Après avoir activé la mise à l’échelle automatique, le trafic du noeud web sortant provient des adresses IP des noeuds de service. Si vous utilisez une liste autorisée avec un service tiers qui n’est pas fourni avec votre projet d’infrastructure cloud Adobe Commerce, vérifiez les adresses IP dans la liste autorisée de service tiers.

Par exemple :

- Si la liste autorisée contient les adresses IP de vos noeuds de service (1, 2 et 3), aucune action n’est requise.
- Si la liste autorisée contient les adresses IP de vos noeuds de service (1, 2 et 3) et des noeuds web (4, 5 et 6), dans ce cas les six noeuds, aucune action n’est requise.
- Si la liste autorisée contient les adresses IP _only_ pour vos noeuds web (4, 5 et 6), vous devez mettre à jour la liste autorisée afin d’inclure les adresses IP pour les noeuds de service.
