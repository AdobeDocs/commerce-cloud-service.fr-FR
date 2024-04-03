---
title: Surveillance New Relic
description: Découvrez comment accéder à votre tableau de bord New Relic et analyser les données de votre projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Observability
topic: Performance
exl-id: 8d1e2ad6-14d0-4754-9703-960d93e135a9
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Surveillance New Relic

New Relic se connecte et surveille votre infrastructure et [!DNL Commerce] à l’aide d’agents PHP. Une fois qu’un environnement Cloud se connecte à New Relic, vous pouvez vous connecter à votre compte New Relic pour consulter les données collectées par l’agent.

Sur le _APM &amp; Services_ , sélectionnez **Résumé** pour afficher des informations transactionnelles sur votre application. Cette vue vous permet d’identifier les échecs potentiels et de vérifier l’intégrité globale de votre application et de vos services.

![Page d’aperçu du projet Cloud New Relic](../../assets/new-relic/dashboard.png)

Dans cette vue, vous pouvez effectuer le suivi des transactions qui rencontrent des réponses lentes ou des goulets d’étranglement, le débit de l’application, les erreurs web, etc.

Examinez les données suivies :

- **Le plus long**: détermine la consommation de temps en suivant les demandes en parallèle. Par exemple, vous avez peut-être le temps de transaction le plus élevé passé dans les vues de produit et de catégorie. Si une page de compte client classe soudainement une consommation de temps élevée, votre application peut être affectée par un appel ou une performance de glissement de requête.

- **Débit le plus élevé**: identifiez les pages les plus consultées en fonction de la taille et de la fréquence des octets transmis.

Toutes les données collectées détaillent le temps passé sur les actions qui transmettent des données, des requêtes ou _Redis_ data. Si des requêtes entraînent des problèmes, New Relic fournit des informations pour effectuer le suivi de ces problèmes et y répondre.

>[!TIP]
>
>Pour plus d’informations sur l’utilisation de ces données pour résoudre les problèmes de performances de l’application, voir [Dépannage des performances à l’aide de New Relic](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) dans le _Centre d’aide Adobe Commerce_.

## Surveillance des performances à l’aide des alertes gérées

Adobe fournit la variable _Alertes gérées pour Adobe Commerce_ stratégie d’alerte pour effectuer le suivi des mesures de performances. La stratégie comprend un ensemble d’alertes qui définissent des seuils et déclenchent des avertissements et des notifications critiques lorsque des problèmes d’infrastructure ou d’application affectent les performances du site. La stratégie effectue le suivi des mesures suivantes dans les environnements de production :

| Mesure | Collecte de données | Disponibilité |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] score | APM | Pro et Starter |
| Utilisation du processeur | NRI | Pro |
| Espace disque | NRI | Pro |
| Taux d’erreur | APM | Pro et Starter |
| Utilisation de la mémoire | NRI | Pro |
| Chargement des requêtes MariaDB | NRI | Pro |
| Redis memory | NRI | Pro |

Lorsque l’infrastructure du site ou les conditions d’application déclenchent un seuil d’alerte, New Relic envoie des notifications d’alerte afin que vous puissiez résoudre le problème de manière proactive. Voir [Alertes gérées pour Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) dans le _Centre d’aide Adobe Commerce_ pour plus d’informations sur les seuils d’alerte et les étapes de résolution des problèmes qui ont déclenché l’alerte.

>[!TIP]
>
>Pour les environnements d’évaluation et d’intégration Pro et les environnements de démarrage, utilisez [Notifications d’intégrité](../integrations/health-notifications.md) pour surveiller l’espace disque.

>[!PREREQUISITES]
>
>- **Informations d’identification New Relic**: informations d’identification pour se connecter au compte New Relic de votre projet Cloud.
>- **Intégration de New Relic active**: vérifiez que votre environnement cloud est connecté à New Relic.
>- **Notification de workflow**—Configurez au moins un [workflow](#set-up-a-workflow-for-notifications) recevoir les notifications d’alerte

**Pour consulter la stratégie Alertes gérées pour Adobe Commerce**:

1. Connectez-vous à [Compte New Relic](https://login.newrelic.com/login).

1. Recherchez la variable _Alertes gérées pour Adobe Commerce_ policy :

   - Dans le menu de navigation de l’Explorateur, cliquez sur **[!UICONTROL Alerts & AI]**.

   - Sous _Détecter_, cliquez sur **[!UICONTROL Alert Conditions & Policies]**.

   - Vérifiez que votre compte est sélectionné en haut de la page _Conditions et stratégies d’alerte_ vue.

   - Dans le _Stratégie_ list, select **Alertes gérées pour Adobe Commerce** stratégie.

     ![Stratégies d’alerte générées](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Si la variable _Alertes gérées pour Adobe Commerce_ la stratégie n’est pas disponible, voir [Alertes gérées pour Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) dans le _Centre d’aide Adobe Commerce_.

1. Cliquez sur le bouton **[!UICONTROL Alert conditions]** pour consulter les conditions d’alerte définies dans la stratégie.

## Création de stratégies d’alerte

Ne modifiez aucune alerte incluse dans la stratégie Alertes gérées pour Adobe Commerce. Adobe met à jour et améliore les conditions d’alerte de cette stratégie au fil du temps, ce qui remplace toutes les personnalisations que vous ajoutez à la stratégie.

Au lieu de modifier une alerte existante, vous pouvez créer une stratégie d’alerte. Copiez ensuite les conditions d’alerte dans la nouvelle stratégie. Voir [Mise à jour de stratégies ou de conditions](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) dans le _New Relic_ la documentation.

>[!TIP]
>
>Voir [Présentation des alertes](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) dans le _New Relic_ documentation pour plus d’informations sur les alertes, les stratégies d’alerte et les workflows.

## Configuration d’un workflow pour les notifications

Vous pouvez désormais configurer une _workflow_, auparavant appelé canal de notification, pour recevoir des notifications sur les performances de votre site en fonction de données filtrées, telles qu’une stratégie d’alerte. Les notifications relatives aux problèmes de performances sont envoyées à tous les workflows associés à une stratégie d’alerte lorsque des conditions de l’application ou de l’infrastructure déclenchent une alerte. Vous recevez également des notifications lorsqu’un problème est reconnu et fermé.

New Relic fournit des modèles pour la configuration de différents types de notifications de workflow, notamment les e-mails, les Slack, les pagerDuty, les webhooks, etc.

**Pour configurer un workflow**:

1. Connectez-vous à [Compte New Relic](https://login.newrelic.com/login).

1. Créez un workflow.

   - Dans le menu de navigation de l’Explorateur, cliquez sur **[!UICONTROL Alerts & AI]**.

   - Dans la navigation de gauche sous _Enrichir et informer_, cliquez sur **[!UICONTROL Workflows]**.

   - Cliquez sur **[!UICONTROL Add a workflow]** sur la droite.

     ![Ajout d’un workflow par New Relic](../../assets/new-relic/add-a-workflow.png)

   - Sur le _Configuration de votre workflow_ , saisissez un nom pour le workflow.

   - Dans le _Filtrage des données_ , sélectionnez **[!UICONTROL Managed Alerts for Adobe Commerce]** de la **[!UICONTROL Policy]** liste déroulante.

   - Dans le _Notifier_ , sélectionnez un canal et suivez les instructions.

   - Cliquez sur **[!UICONTROL Test workflow]** pour vérifier votre configuration.

1. Cliquez sur **[!UICONTROL Activate workflow]**.

Reportez-vous à la documentation de New Relic à propos de [Workflows](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>Les workflows par défaut des alertes de la stratégie Alertes gérées pour Adobe Commerce sont configurés pour avertir les équipes d’Adobe qui prennent en charge Adobe Commerce sur les clients de l’infrastructure cloud. Ne modifiez pas la configuration de ces canaux par défaut et ne supprimez aucune stratégie d’alerte qui leur est affectée.
