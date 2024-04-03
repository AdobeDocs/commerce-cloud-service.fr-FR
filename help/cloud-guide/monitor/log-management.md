---
title: Gestion des journaux New Relic
description: Découvrez comment utiliser le journal New Relic
feature: Cloud, Logs, Observability
exl-id: d8afb5c0-9727-4123-8944-81cd6ad7cbb7
source-git-commit: ebe1746ee9fd08480da5ad07d7f1f8299ad9af7e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Gestion des journaux New Relic

Tous les projets d’infrastructure cloud incluent : [Gestion des journaux New Relic](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). Le service est préconfiguré pour agréger toutes les données de journal de vos environnements d’évaluation et de production et les afficher dans un tableau de bord de gestion des journaux centralisé.

Les données agrégées incluent des informations provenant des journaux suivants :

- Tous `ece-tools` et des journaux d’application à partir de `~/var/log` directory
- Journaux des services cloud de la `var/log/platform/<project-ID>` directory
- Réseau de diffusion de contenu et WAF rapides

Lorsque votre projet est connecté à New Relic, vous pouvez utiliser le service New Relic Logs pour effectuer les tâches suivantes :

- Utilisation de requêtes New Relic pour rechercher des données de journal agrégées
- Visualisation des données de journal à l’aide de l’application New Relic Logs
- Créer des graphiques, des tableaux de bord et des alertes personnalisés
- Résolution des problèmes de performances d’un seul tableau de bord

## Afficher et analyser les données du journal

Utilisez l’application New Relic Logs pour effectuer des recherches dans les données de journal agrégées et résoudre les problèmes liés à l’application, à l’infrastructure, au réseau de diffusion de contenu et aux erreurs WAF. Vous pouvez créer des graphiques, des tableaux de bord et des alertes à l’aide des données de journal collectées auprès des services New Relic APM et d’infrastructure.

**Pour utiliser l’application New Relic Logs**:

1. Connectez-vous à [Compte New Relic](https://login.newrelic.com/login).

1. Sélectionner **Journaux** dans le menu de navigation de l’Explorateur.

1. Vérifiez que votre compte est sélectionné en haut de la page _Tous les journaux_ vue.

1. Sélectionnez une période pour la requête Journaux.

1. Pour examiner les données de journal d’infrastructure pour les services cloud (journaux depuis `~/var/log/`), saisissez la chaîne de requête `has: "filePath"` dans le _Recherche de journaux_ champ . Cliquez ensuite sur **[!UICONTROL Query logs]**.

   Les noms des fichiers journaux sont stockés dans la variable `filePath` avec des chemins complets vers le fichier journal.

   ![Données du journal du service New Relic de projet Cloud](../../assets/new-relic/var-log-query.png)

1. Pour examiner les données de journal Fastly, saisissez la chaîne de requête. `has: "client_ip"` dans le _Recherche de journaux_ champ . Cliquez ensuite sur **[!UICONTROL Query logs]**.

1. Pour filtrer les résultats du journal Fastly par code de pays, cliquez sur **[!UICONTROL Add column]**, puis sélectionnez **[!UICONTROL geo_country_code]**.

   ![Filtre d’attribut de journal du réseau de diffusion de contenu New Relic du projet cloud](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>Vous pouvez enregistrer la vue de requête à partir du _Vues enregistrées_ menu déroulant. Cliquez sur **[!UICONTROL Create new]**, attribuez un nom, sélectionnez des options, puis cliquez sur **[!UICONTROL Save view]**.
>
>Voir [Prise en main de la gestion des logs](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) et [Présentation du langage de requête New Relic](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) sur le _Documents New Relic_ site.
