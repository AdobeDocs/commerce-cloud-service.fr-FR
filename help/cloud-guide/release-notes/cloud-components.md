---
title: Composants cloud pour Commerce
description: Consultez la liste des dernières améliorations apportées au module Composants Cloud .
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Composants cloud pour Commerce

La variable [Composants cloud](https://github.com/magento/magento-cloud-components) Le module fournit des fonctionnalités de base Adobe Commerce étendues pour les sites déployés sur l’infrastructure cloud. Ce module est une dépendance pour le module Outils de la CEE. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui est un composant de [Suite d’outils cloud pour Commerce](cloud-tools-suite.md).

La variable `magento/magento-cloud-components` Le package utilise la séquence de versions suivante : `<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->

## v1.0.13 {#latest}

Date de publication : 10 mars 2023

- ![nouvelle icône](../../assets/new.svg) **Prise en charge améliorée de PHP 8.2**—Correction de problèmes de compatibilité avec certaines versions de PHP 8.2.x pour prendre en charge Commerce 2.4.6.

## v1.0.12

Date de publication : 13 septembre 2022

- ![icône de correctif](../../assets/fix.svg) **Erreurs lors du réchauffement**: correction d’un problème qui tentait de [chauffer](../environment/variables-post-deploy.md#warm_up_pages) lorsque la visibilité de la page est définie sur [**Non visible individuellement**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) dans l’administrateur, ce qui entraîne `ERROR: Warming up failed: <link to page>` erreurs dans le journal de déploiement.<!-- MCLOUD-9134 -->

## v1.0.11

Date de publication : 4 août 2022

- ![icône de correctif](../../assets/fix.svg) **Prise en charge de la compatibilité Symfony 5.4 ajoutée**: correctifs pour la compatibilité avec Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de PHP 8.1**: ajout de la prise en charge de PHP 8.1 et suppression de la prise en charge de PHP 7.1.

## v1.0.9

Date de publication : 25 octobre 2021

- ![icône de correctif](../../assets/fix.svg) **Mettre à jour Monolog**: mise à jour de la version minimale requise pour le `monolog` vers `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Date de publication : 29 juillet 2021

- ![icône de correctif](../../assets/fix.svg) **Suppression des barres obliques de fin des URL générées automatiquement**: suppression des barres obliques de fin des URL de page de catégorie générées lors du nettoyage du cache.<!--MCLOUD-7192-->

## v1.0.7

Date de publication : 9 septembre 2020

- ![nouvelle icône](../../assets/new.svg) **Amélioration de la journalisation**: réduisez la taille de la variable `cache.log` afin d’améliorer les performances.<!--MCLOUD-6859-->

- ![icône de correctif](../../assets/fix.svg) Correction d’une erreur de type dans les valeurs de configuration du cache qui provoquait l’erreur `php bin/magento cache:evict` La commande de l’interface de ligne de commande échoue.

## v1.0.6

Date de publication : 5 août 2020

- ![nouvelle icône](../../assets/new.svg) **Amélioration des performances Redis**: ajout de la propriété `./bin/magento cache:evict` pour supprimer les clés Redis expirées, ce qui réduit l’utilisation de la mémoire Redis pour améliorer les performances.<!--MCLOUD-6023-->

- ![icône de correctif](../../assets/fix.svg) Suppression de la prise en charge pour *Journaux New Relic en contexte* pour résoudre un problème de performances.<!--MCLOUD-6422-->

## v1.0.5

Date de publication : 25 juin 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème introduit dans la version 1.0.4 de magento/magento-cloud-components en raison duquel l’opération de vidage du cache échouait pendant la phase de déploiement, interrompant ainsi le processus de déploiement.

## v1.0.4

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Mise en oeuvre des journaux New Relic dans le contexte**: les journaux d’application générés par Adobe Commerce s’affichent désormais dans les traces dans New Relic afin d’améliorer les fonctionnalités de dépannage.<!--MCLOUD-6029-->

- ![nouvelle icône](../../assets/new.svg) **Journalisation améliorée**: ajout de la journalisation pour suivre les événements d’invalidation du cache et de réindexation complète.<!--MCLOUD-6157-->

## v1.0.3

Date de publication : 27 février 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de compatibilité pour la prise en charge de `ece-tools` Versions 2002.0.x qui utilisent des versions plus anciennes de PHP.

## v1.0.2

Date de publication : 6 février 2020

- ![nouvelle icône](../../assets/new.svg) Étendez les fonctionnalités de la fonction `WARM_UP_PAGES` pour prendre en charge le préchargement du cache pour des pages de produits spécifiques. Voir [variables post-déploiement](../environment/variables-post-deploy.md#warm_up_pages) rubrique pour obtenir une description détaillée des fonctionnalités.<!--MAGECLOUD-4444-->

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème en raison duquel une URL de magasin non valide provoquait l’échec du crochet de post-déploiement lors de l’utilisation de la variable `WARM_UP_PAGES` pour remplir le cache. Ce problème survenait uniquement lorsque les réécritures d’URL étaient désactivées.<!-- MAGECLOUD-4094 -->

## v1.0.1

Date de publication : 23 juillet 2019

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème affectant [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) qui utilise une URL de magasin par défaut. Maintenant, si la variable `config:show:default-url` ne peut pas récupérer une URL de base, alors l’URL de la variable MAGENTO_CLOUD_ROUTES est utilisée.<!-- MAGECLOUD-3866 -->

## v1.0.0

Date de publication : 12 juin 2019

Il s’agit de la première version de la [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) qui est une nouvelle dépendance pour `ece-tools` version de package 2002.0.20 et versions ultérieures.

- ![nouvelle icône](../../assets/new.svg) Ajout de la possibilité d’utiliser des modèles d’expression régulière pour configurer le **WARM_UP_PAGES** pour mettre en cache des pages uniques, plusieurs domaines et plusieurs pages. Voir [Variables de post-déploiement](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
