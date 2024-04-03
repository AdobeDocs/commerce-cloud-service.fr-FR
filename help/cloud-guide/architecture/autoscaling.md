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

La mise à l’échelle automatique ajoute ou supprime automatiquement des ressources à l’infrastructure cloud pour maintenir des performances optimales et des coûts raisonnables. Actuellement, cette fonctionnalité n’est disponible que pour les projets configurés avec une [Architecture mise à l’échelle](scaled-architecture.md).

## Noeuds de serveur web

La variable [niveau web](scaled-architecture.md#web-tier) s’adapte à une augmentation des demandes de processus et à des exigences de trafic plus élevées. Actuellement, la fonction de mise à l’échelle automatique ne se met à l’échelle qu’horizontalement en ajoutant ou en supprimant des noeuds de serveur web.

Un événement de mise à l’échelle automatique se produit lorsque l’utilisation du processeur et le trafic atteignent un seuil prédéfini :

- **Noeuds ajoutés**: la capacité des processeurs/coeurs sur tous les noeuds web actifs est de 75 % pendant 1 minute et le trafic augmente de 20 % pendant 5 minutes consécutives.
- **Noeuds supprimés**: les processeurs/coeurs sur tous les noeuds web actifs sont chargés à 60 % pendant 20 minutes. Les noeuds sont supprimés dans l’ordre dans lequel ils ont été ajoutés.

Les seuils minimal et maximal sont déterminés et définis en fonction des limites de ressources contractuelles de chaque commerçant, ce qui réduit le risque d’une mise à l’échelle infinie.

## Surveiller les seuils avec New Relic

Vous pouvez utiliser la variable [Service New Relic](../monitor/new-relic-service.md) pour surveiller certains seuils, tels que le nombre d’hôtes et l’utilisation du processeur. Les requêtes New Relic suivantes utilisent une notation de variable pour `cluster-id` par exemple, à des fins uniquement.

>[!TIP]
>
>Pour une référence sur la création de requêtes, voir [Syntaxe, clauses et fonctions NRQL](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) dans le _New Relic_ la documentation.
>Utilisez vos requêtes pour créer une [Tableau de bord New Relic](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### Nombre d’hôtes

L’exemple de requête New Relic suivant montre le nombre d’hôtes dans l’environnement :

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

Dans la capture d&#39;écran suivante, **Hôtes APM vus** fait référence au nombre d’hôtes avec des transactions enregistrées au cours de la période sélectionnée.

![Nombre d’hôtes New Relic](../../assets/new-relic/host-count.png)

### Utilisation du processeur

L’exemple de requête New Relic suivant montre l’utilisation du processeur pour les noeuds web :

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![Utilisation du processeur des noeuds web New Relic](../../assets/new-relic/web-node-cpu-usage.png)

## Activation de la mise à l’échelle automatique

Pour activer ou désactiver la mise à l’échelle automatique pour votre projet Adobe Commerce sur l’infrastructure cloud, [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Sélectionnez les raisons suivantes dans le ticket :

- **Raison du contact**: demande de changement d’infrastructure
- **Raison de contact pour l’infrastructure Adobe Commerce**: autre demande de changement d’infrastructure

>[!IMPORTANT]
>
>La fonction de mise à l’échelle automatique capture les événements imprévus. Même si la mise à l’échelle automatique est activée, Adobe vous recommande de continuer. [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) si vous attendez un événement à venir.

### Test de chargement

Adobe active la mise à l’échelle automatique sur votre projet Cloud _staging_ d’abord la grappe. Une fois les tests de chargement effectués dans votre environnement, Adobe active la mise à l’échelle automatique sur votre grappe de production. Pour plus d’informations sur le test de chargement, voir [Test de performance](../launch/checklist.md#performance-testing).

### LISTE AUTORISÉE IP

Après avoir activé la mise à l’échelle automatique, le trafic du noeud web sortant provient des adresses IP des noeuds de service. Si vous utilisez une liste autorisée avec un service tiers qui n’est pas fourni avec votre projet d’infrastructure cloud Adobe Commerce, vérifiez les adresses IP dans la liste autorisée de service tiers.

Par exemple :

- Si la liste autorisée contient les adresses IP de vos noeuds de service (1, 2 et 3), aucune action n’est requise.
- Si la liste autorisée contient les adresses IP de vos noeuds de service (1, 2 et 3) et des noeuds web (4, 5 et 6), dans ce cas les six noeuds, aucune action n’est requise.
- Si la liste autorisée contient des adresses IP _only_ pour vos noeuds web (4, 5 et 6), vous devez mettre à jour la liste autorisée afin d’inclure les adresses IP des noeuds de service.
