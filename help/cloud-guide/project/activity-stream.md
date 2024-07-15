---
title: Flux d’activité
description: Découvrez comment lire le flux d’activités dans l’interface de ligne de commande de  [!DNL Cloud Console] ou dans l’interface de ligne de commande de Cloud pour Adobe Commerce sur l’infrastructure cloud.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ffef5ab4-ef40-4073-adc8-a44c61c0d77b
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Flux d’activité

La vue principale de chaque environnement affiche une liste **Activité** d’événements historiques similaires à un journal Git. La liste des activités est un flux des événements récents pour les environnements actifs. Voici une liste des types d’activité et de leurs icônes qui s’affichent dans le flux d’activité :

![Types d’activité](../../assets/activity-types.svg){width="500" align="center"}

## Afficher les journaux

Dans la liste Activité , cliquez sur l’icône d’état d’une activité pour afficher le journal. Vous pouvez également cliquer sur le menu ![Plus](../../assets/icon-more.png){width="32"} (_plus_) pour accéder à d’autres options de gestion de l’activité. Vous trouverez ci-dessous un court journal pour créer une sauvegarde. Vous pouvez [utiliser l’interface de ligne de commande de Cloud](#activity-stream-with-cloud-cli) pour afficher le même journal.

![Affichage du journal](../../assets/log-view.png)

## Gestion d’une activité

Certaines activités sont à l’état _en cours d’exécution_ ou _en attente_ . Vous pouvez agir sur une activité en cours d’exécution, comme l’annulation d’un déploiement en cours d’exécution. Les onglets suivants présentent deux méthodes d’annulation d’une activité : [!DNL Cloud Console] ou l’interface de ligne de commande du cloud.

>[!BEGINTABS]

>[!TAB Console]

**Pour annuler une activité dans[!DNL Cloud Console]** :

Vous pouvez agir sur une activité en cours d’exécution en accédant au menu ![Plus](../../assets/icon-more.png){width="32"} (_plus_) et en sélectionnant une action, telle que `Cancel` ou `View log`. Pour cet exemple, sélectionnez l’option **Annuler** pour arrêter l’activité en cours d’exécution.

Toutes les activités n&#39;ont pas la possibilité d&#39;annuler. Par exemple, l’option d’annulation du déploiement de l’application s’affiche uniquement pendant la phase _build_. Une fois que l’application est passée à la phase _deploy_, vous ne pouvez plus annuler l’activité. Voir [Processus de déploiement](../deploy/process.md) à propos des différentes phases.

![Annuler l’activité](../../assets/activity-icons/cancel-activity.png){width="450" align="center"}

Si un terminal exécute l’activité de déploiement, l’annulation dans le [!DNL Cloud Console] entraîne l’annulation dans le terminal :

![Activité annulée dans le terminal](../../assets/activity-icons/activity-cancelled.png){width="300"}

>[!TAB CLI]

**Pour annuler une activité dans l’interface de ligne de commande de Cloud** :

1. Identifiez les activités en cours et sélectionnez un ID d’activité.

   ```bash
   magento-cloud activity:list --state=in_progress
   ```

1. Annuler l’activité à l’aide de l’ID d’activité :

   ```bash
   magento-cloud activity:cancel wvl5wm7s5vkhy
   ```

>[!ENDTABS]

## Filtrage du flux d’activités

La possibilité de filtrer la liste des activités est utile lorsque vous recherchez quelque chose de spécifique, tel qu’une sauvegarde ou un événement de fusion.

**Pour filtrer la liste des activités dans le[!DNL Cloud Console]** :

1. Sélectionnez un environnement et choisissez la vue Activité **[!UICONTROL All]** pour inclure l’historique complet des événements.

1. Cliquez sur ![Filtrer par](../../assets/icon-filterby.png){width="32"} et sélectionnez les options **[!UICONTROL Filter by]** :

   ![Filtrer les activités](../../assets/activity-filter.png)

1. Sélectionnez la vue Activité **[!UICONTROL Recent]** et réinitialisez la liste.

## Afficher le flux avec l’interface de ligne de commande de Cloud

L’interface de ligne de commande `magento-cloud` fournit la plupart des mêmes fonctionnalités que [!DNL Cloud Console]. La commande `activity` peut :

- `list` flux d’activités pour un environnement
- `get` détails sur une activité spécifique
- afficher le `log` pour une activité spécifique ;
- `cancel` une activité

**Pour afficher le flux d’activités avec l’interface de ligne de commande de Cloud** :

1. Répertorier les activités de l’environnement actuel.

   ```bash
   magento-cloud activity:list
   ```

1. Chaque activité possède un identifiant unique. Sélectionnez un ID dans la liste précédente et affichez les détails de cette activité.

   ```bash
   magento-cloud activity:get wvl5wm7s5vkhy
   ```

1. Afficher le journal complet de cette activité.

   ```bash
   magento-cloud activity:log wvl5wm7s5vkhy
   ```

   Exemple de réponse :

   ```bash
   Activity ID: wvl5wm7s5vkhy
   Type: environment.backup
   Description: User created a backup of Master
   Created: 2023-09-08T14:03:33+00:00
   State: complete
   Log:
   Creating backup of master
   Created backup eg5pu63egt2dcojkljalzjdopa
   ```
