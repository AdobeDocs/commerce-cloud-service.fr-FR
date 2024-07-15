---
title: Présentation des options de magasin et de la gestion de configuration
description: Personnalisez votre boutique Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, Services
exl-id: 06d477e4-02de-4742-8495-541458400e93
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Présentation des options de magasin et de la gestion de configuration

Il existe de nombreuses façons de personnaliser votre magasin, comme l’ajout d’un thème personnalisé, l’installation d’une extension ou l’application d’une configuration spécifique dans les environnements d’infrastructure cloud. Vous pouvez configurer les paramètres de services spécifiques directement dans les environnements d’évaluation et de production. Vous pouvez configurer plusieurs sites Web et magasins. La configuration Boutique vous permet de configurer ces options dans votre poste de travail local et de déployer des paramètres spécifiques dans tous les environnements.

Pour accéder à votre vitrine, utilisez la commande `magento-cloud url` et répondez aux invites. Vous pouvez également trouver l’URL dans le [!DNL Cloud Console] sous **Site d’accès**.

## Configuration des options de magasin

Les options de magasin sont les suivantes :

* [Module Entreprise à entreprise (B2B)](b2b-module.md)
* [Thèmes personnalisés](custom-theme.md)
* [Extensions](extensions.md)
* [Plusieurs sites](multiple-sites.md)
* [Services de paiement](paypal.md)

## Configuration des services et des intégrations

Il existe des [fichiers de configuration](../environment/overview.md) spécifiques qui gèrent certains comportements de déploiement dans des environnements distants. Vous pouvez passer en revue ces rubriques séparément :

* [Déploiement des applications](../application/configure-app-yaml.md)
* [Création et déploiement d’actions d’environnement](../environment/configure-env-yaml.md)
* [Itinéraires des requêtes entrantes](../routes/routes-yaml.md)
* [Services pris en charge](../services/services-yaml.md)

## Gestion des configurations

Après avoir configuré les options, services et intégrations du magasin, utilisez la gestion des configurations pour déployer ces configurations dans tous les environnements de manière cohérente et avec un temps d’arrêt minimal. Voir [Configuration Management](store-settings.md).
