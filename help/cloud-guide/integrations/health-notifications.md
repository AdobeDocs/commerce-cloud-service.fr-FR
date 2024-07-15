---
title: Notifications d’intégrité
description: Découvrez comment configurer des notifications Slack, email et PagerDuty pour l’utilisation de l’espace disque sur votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Observability, Integration
exl-id: d3173098-78ed-42a8-aeb3-9ccbaccc4d32
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Notifications d’intégrité

Adobe Commerce sur l’infrastructure cloud surveille l’utilisation de l’espace disque sur toutes les applications et tous les services de votre environnement de démarrage ou de votre environnement d’intégration Pro. Un disque de base de données qui manque d’espace peut entraîner une corruption des données. La vérification de l’état d’intégrité a lieu toutes les 5 minutes et peut vous en informer par e-mail ou par un autre service externe. Il existe trois avertissements de faible disque pour les notifications d’intégrité :

- **Warning** : l’espace disque disponible chute en dessous de 20 %
- **Critique** : l’espace disque disponible chute sous 10 %
- **All-clear** : l’espace disque disponible renvoie plus de 20 %, après un événement de faible disque

>[!NOTE]
>
>Dans les environnements Pro Production, vous pouvez utiliser la stratégie d’alerte Gestion des alertes pour Adobe Commerce pour New Relic afin de surveiller l’espace disque. Voir [Surveillance des performances avec des alertes gérées](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

## Notifications par e-mail

L’intégration des courriers électroniques d’intégrité requiert une adresse d’origine et au moins une adresse de destinataire. Vous pouvez utiliser la même adresse électronique pour l’adresse `from-address` et l’adresse `recipients`. L’exemple suivant enregistre une intégration d’email d’intégrité avec deux destinataires :

```bash
magento-cloud integration:add --type health.email --from-address you@example.com --recipients them@example.com --recipients others@example.com
```

## Notifications des canaux Slack

Slack est un service externe qui utilise des applications interactives appelées robots pour publier des messages dans une salle de conversation. Avant de pouvoir recevoir des notifications d’intégrité en Slack, vous devez créer un [utilisateur de robot](https://api.slack.com/bot-users) personnalisé pour votre groupe de Slack. Après avoir configuré l’utilisateur de robot pour votre canal ou canaux, enregistrez le [jeton de robot](https://api.slack.com/docs/token-types#bot) fourni par le Slack pour enregistrer votre intégration. L’exemple suivant enregistre des notifications d’intégrité dans un canal de Slack :

```bash
magento-cloud integration:add --type health.slack --token SLACK_BOT_TOKEN --channel '#slack-channel-name'
```

## Notifications PagerDuty

PagerDuty est un service externe qui peut avertir les membres de l’équipe d’appel de problèmes importants. Avant de pouvoir recevoir des notifications d’intégrité dans PagerDuty, vous devez créer une [intégration PagerDuty](https://developer.pagerduty.com/v2/docs/integrating) qui utilise l’API d’événement version 2. Utilisez la clé d&#39;intégration, ou _clé de routage_, pour enregistrer votre intégration. L’exemple suivant enregistre des notifications pour PagerDuty à l’aide d’une clé de routage :

```bash
magento-cloud integration:add --type health.pagerduty --routing-key PAGERDUTY_ROUTING_KEY
```
