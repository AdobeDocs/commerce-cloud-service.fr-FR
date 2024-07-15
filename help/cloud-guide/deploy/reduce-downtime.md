---
title: Déploiement sans interruption
description: Découvrez comment réduire le temps d’arrêt global lors du déploiement d’Adobe Commerce sur des projets d’infrastructure cloud.
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Déploiement sans interruption

Adobe Commerce sur l’infrastructure cloud exécute l’application en [_mode de maintenance_](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) pendant la phase de déploiement, qui met votre site hors ligne jusqu’à la fin du déploiement. La durée pendant laquelle votre site de production est en mode de maintenance dépend de la taille du site, du nombre de modifications appliquées au cours du déploiement et de la configuration pour le déploiement de contenu statique. Il est possible de configurer votre projet de sorte qu’il se déploie avec un effet d’interruption **zéro**.

Pendant le processus de déploiement, toutes les connexions restent en file d’attente jusqu’à 5 minutes, préservant les sessions actives et les actions en attente, telles que l’ajout au panier ou l’extraction. Après le déploiement, la file d’attente est libérée et les connexions se poursuivent sans interruption. Pour utiliser cette _connexion hold_ à votre avantage et réduire le temps d’arrêt du déploiement à _zero_, vous devez configurer votre projet pour utiliser la stratégie de déploiement la plus efficace.

Procédez comme suit pour réduire le temps nécessaire au déploiement d’une mise à jour vers Production dans votre boutique :

1. [ Effectuez la mise à niveau vers le `ece-tools` package](../dev-tools/install-package.md) ou [mettez à jour la `ece-tools` version](../dev-tools/update-package.md)
Votre projet d’infrastructure cloud Adobe Commerce sur doit comporter le dernier package `ece-tools` afin que vous disposiez des outils pour configurer un déploiement optimal. Si vous disposez du dernier `ece-tools`, passez à l’étape suivante.

   >[!NOTE]
   >
   >Même s’il est recommandé d’utiliser le dernier package `ece-tools`, la méthode de déploiement sans interruption fonctionne avec `ece-tools` [version 2002.0.13](../release-notes/cloud-release-archive.md#v2002013) et versions ultérieures.

1. [Configuration du déploiement de contenu statique](static-content.md)
Si le déploiement de contenu statique échoue en phase de déploiement, votre site reste bloqué en mode de maintenance. Lorsqu’un échec se produit pendant la phase de création, le processus évite les temps d’arrêt car il ne commence jamais la phase de déploiement. [La génération de contenu statique lors de la phase de création avec un HTML minimisé ](static-content.md#setting-the-scd-on-build), également appelé état idéal, est la configuration optimale pour les déploiements sans interruption et _évite_ temps d’arrêt en cas d’échec.

1. [Configuration du crochet de post-déploiement](../application/hooks-property.md)
Vous devez configurer le crochet de post-déploiement pour nettoyer et réchauffer le cache. Par défaut, le nettoyage du cache se produit pendant la phase de déploiement lorsque le site est hors service. Le déplacement du nettoyage du cache vers la phase de post-déploiement signifie que votre cache reste actif jusqu’à la fin de la phase de déploiement, puis que vous pouvez nettoyer le cache en toute sécurité.

   Personnalisez la liste des pages utilisées pour précharger le cache avec la variable d&#39;environnement [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages).

1. [Réduire les fichiers de thème](../environment/variables-deploy.md#scdmatrix)
Vous pouvez réduire le nombre de fichiers de thème inutiles en configurant la variable d’environnement SCD\_MATRIX.

1. [Accélérer le déploiement de contenu statique](../environment/variables-deploy.md#scdthreads)
Vous pouvez accélérer le processus de déploiement en mettant à jour la variable d’environnement SCD\_THREADS afin d’augmenter le nombre de threads pour le déploiement de contenu statique.

>[!NOTE]
>
>Vous pouvez valider la configuration de votre projet pour un déploiement optimal en [exécutant l’assistant d’état idéal](smart-wizards.md#verifying-an-ideal-configuration).
