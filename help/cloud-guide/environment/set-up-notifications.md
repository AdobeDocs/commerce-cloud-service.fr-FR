---
title: Configuration des notifications
description: Découvrez comment configurer des notifications pour Adobe Commerce dans des environnements d’infrastructure cloud.
feature: Cloud, Configuration, Logs
exl-id: be48abcd-4753-4e89-83fe-0aadfb0415c2
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Configuration des notifications

Par défaut, Adobe Commerce sur l’infrastructure cloud écrit et déploie les actions sur le fichier `app/var/log/cloud.log` dans le répertoire d’application racine Adobe Commerce. Vous pouvez éventuellement envoyer des journaux à un système de messagerie, tel que Slack et courrier électronique, pour recevoir des notifications en temps réel.

Par exemple, vous pouvez envoyer un message d’alerte à un groupe de personnes en cas d’échec d’un déploiement et demander une enquête sur les problèmes.

## Planification des notifications

Avant de configurer des notifications, tenez compte des points suivants :

- Quel type de notification souhaitez-vous recevoir (messages du Slack, email, les deux) ?
- Combien de détails voulez-vous voir dans les logs ?
- Où souhaitez-vous configurer des notifications (intégration, évaluation, production) ?

Par exemple, lors du développement initial, vous préférez peut-être recevoir des notifications par e-mail qui affichent des journaux détaillés sur votre environnement d’intégration afin de vous aider à déboguer les problèmes avant de procéder au déploiement dans l’environnement d’évaluation. Lorsque vous êtes prêt à effectuer un déploiement dans l’environnement d’évaluation ou de production, vous préférez peut-être un message de Slack contenant des informations moins détaillées.

>[!NOTE]
>
>Le fichier de configuration utilisé pour configurer les notifications se trouve à la racine de votre répertoire de projet. Il s’applique donc lorsque vous poussez des modifications dans n’importe quel environnement. Si vous souhaitez personnaliser les notifications par environnement, vous devez modifier le fichier de configuration avant de le transférer dans cet environnement.

## Configurer les notifications

Pour configurer les notifications :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.
1. Dans le fichier `.magento.env.yaml` de la racine de votre projet, ajoutez les paramètres de votre système de messagerie, y compris la notification préférée [Niveaux de journal](log-handlers.md#log-levels).

   Par exemple, pour configurer les configurations de courrier électronique des Slack _et_, utilisez les éléments suivants :

   ```yaml
   log:
     slack:
       token: "<your-slack-token>"
       channel: "<your-slack-channel>"
       username: "SlackHandler"
       min_level: "info"
     email:
       to: <your-email>
       from: <your-email>
       subject: "Log notification from Adobe Commerce"
       min_level: "notice"
   ```

   >[!NOTE]
   >
   >Adobe Commerce sur l’infrastructure cloud envoie uniquement des emails pendant la phase de déploiement.

1. Validez et envoyez vos modifications au serveur distant.

   ```bash
   git -A && git commit -m "Configure build/deploy notifications"
   ```

   ```bash
   git push origin <branch-name>
   ```

### Exemple de configuration de Slack

L’exemple suivant illustre une configuration réservée aux Slack :

```yaml
log:
  slack:
    token: "<your-slack-token>"
    channel: "<your-slack-channel>"
    username: "SlackHandler"
    min_level: "info"
```

- `token` : votre Slack [jeton utilisateur](https://api.slack.com/docs/token-types#user). Votre jeton utilisateur autorise Adobe Commerce sur l’infrastructure cloud pour envoyer des messages.
- `channel` : nom du canal Slack Adobe Commerce sur l’infrastructure cloud envoie des notifications.
- `username` : nom d’utilisateur Adobe Commerce sur l’infrastructure cloud utilise pour envoyer des messages de notification dans Slack.
- `min_level` : niveau de journalisation minimal pour les messages de notification. Nous vous recommandons d’utiliser `info`.

### Exemple de configuration de courrier électronique

L’exemple suivant illustre une configuration par email uniquement :

>[!NOTE]
>
>Adobe Commerce sur l’infrastructure cloud envoie uniquement des emails pendant la phase de déploiement.

```yaml
log:
  email:
    to: <your-email>
    from: <your-email>
    subject: "Log notification from Adobe Commerce"
    min_level: "notice"
```

- `to` : l’adresse électronique Adobe Commerce sur l’infrastructure cloud envoie des messages de notification.
- `from` : adresse électronique pour envoyer des messages de notification aux destinataires.
- `subject` : description de l’email.
- `min_level` : niveau de journalisation minimal pour les messages de notification. Nous vous recommandons d’utiliser `notice` ou `warning`.
