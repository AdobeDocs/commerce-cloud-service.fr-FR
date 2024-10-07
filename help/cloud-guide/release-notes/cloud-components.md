---
title: Composants cloud pour Commerce
description: Consultez la liste des dernières améliorations apportées au module Composants Cloud .
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: 30eafa856aaa57bb2fd2ce26e3be2a69aee726e2
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Composants cloud pour Commerce

Le package [ Composants cloud](https://github.com/magento/magento-cloud-components) fournit des fonctionnalités de base Adobe Commerce étendues pour les sites déployés sur l’infrastructure cloud. Ce module est une dépendance pour le module Outils de la CEE. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module, qui est un composant de la [suite d’outils cloud pour Commerce](cloud-tools-suite.md).

Le package `magento/magento-cloud-components` utilise la séquence de version suivante : `<major>.<minor>.<patch>`

Les notes de mise à jour incluent :

- ![nouvelle icône](../../assets/new.svg) Nouvelles fonctionnalités
- ![Icône de correctif](../../assets/fix.svg) Correctifs et améliorations

<!--Add release notes below-->

## v1.1.0 {#latest}

Date de publication : 7 octobre 2024

- ![Icône de correctif](../../assets/fix.svg) **Code restructuré**—Suppression de la prise en charge des anciennes versions de PHP 7.4, 7.3, 7.2 et des bibliothèques associées.<!-- MCLOUD-9278 - -->
- ![Icône de correctif](../../assets/fix.svg) **Mise à niveau de la version monolog**—Ajout de la prise en charge de monolog 3.6.<!-- MCLOUD-12855 - -->

## v1.0.14

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** : prise en charge de PHP 8.3.

## v1.0.13

Date de publication : 10 mars 2023

- ![nouvelle icône](../../assets/new.svg) **Prise en charge améliorée de PHP 8.2** : correction de problèmes de compatibilité avec certaines versions de PHP 8.2.x pour prendre en charge Commerce 2.4.6.

## v1.0.12

Date de publication : 13 septembre 2022

- ![icône de correctif](../../assets/fix.svg) **Erreurs lors du réchauffement** : correction d’un problème qui tentait de [réchauffer](../environment/variables-post-deploy.md#warm_up_pages) lorsque la visibilité de la page était définie sur [**Non visible individuellement**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) dans l’administrateur, ce qui entraînait des erreurs `ERROR: Warming up failed: <link to page>` dans le journal de déploiement.<!-- MCLOUD-9134 -->

## v1.0.11

Date de publication : 4 août 2022

- ![icône de correctif](../../assets/fix.svg) **Ajout de la prise en charge de la compatibilité Symfony 5.4**—Correctifs pour la compatibilité avec Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Date de publication : 10 mars 2022

- ![nouvelle icône](../../assets/new.svg) **Prise en charge de PHP 8.1** : ajout de la prise en charge de PHP 8.1 et abandon de la prise en charge de PHP 7.1.

## v1.0.9

Date de publication : 25 octobre 2021

- ![Icône de correctif](../../assets/fix.svg) **Mise à jour de monolog**—Mise à jour de la version minimale requise pour le package `monolog` vers `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Date de publication : 29 juillet 2021

- ![Icône de correctif](../../assets/fix.svg) **Suppression des barres obliques de fin des URL générées automatiquement**—Suppression des barres obliques de fin des URL de page de catégorie générées lors du nettoyage du cache.<!--MCLOUD-7192-->

## v1.0.7

Date de publication : 9 septembre 2020

- ![nouvelle icône](../../assets/new.svg) **Améliorations de la journalisation**—Réduisez la taille du fichier `cache.log` pour améliorer les performances.<!--MCLOUD-6859-->

- ![icône de correction](../../assets/fix.svg) Correction d’une erreur de type dans les valeurs de configuration du cache qui provoquait l’échec de la commande d’interface de ligne de commande `php bin/magento cache:evict`.

## v1.0.6

Date de publication : 5 août 2020

- ![nouvelle icône](../../assets/new.svg) **Améliorer les performances Redis**—Ajout de la commande `./bin/magento cache:evict` pour supprimer les clés Redis expirées, ce qui réduit l’utilisation de la mémoire Redis pour améliorer les performances.<!--MCLOUD-6023-->

- ![icône de correctif](../../assets/fix.svg) Suppression de la prise en charge des *journaux New Relic dans le contexte* pour résoudre un problème de performances.<!--MCLOUD-6422-->

## v1.0.5

Date de publication : 25 juin 2020

- ![icône de correction](../../assets/fix.svg) Correction d’un problème introduit dans la version 1.0.4 de magento/magento-cloud-components en raison duquel l’opération de vidage du cache échouait pendant la phase de déploiement, interrompant le processus de déploiement.

## v1.0.4

Date de publication : 25 juin 2020

- ![nouvelle icône](../../assets/new.svg) **Journaux New Relic implémentés dans le contexte** : les journaux d’application générés par Adobe Commerce s’affichent désormais dans les traces dans New Relic pour améliorer les fonctionnalités de dépannage.<!--MCLOUD-6029-->

- ![nouvelle icône](../../assets/new.svg) **Journalisation améliorée** : ajout de la journalisation pour suivre l’invalidation du cache et les événements de réindexation complète.<!--MCLOUD-6157-->

## v1.0.3

Date de publication : 27 février 2020

- ![icône de correctif](../../assets/fix.svg) Correction d’un problème de compatibilité afin de prendre en charge les versions `ece-tools` 2002.0.x qui utilisent d’anciennes versions de PHP.

## v1.0.2

Date de publication : 6 février 2020

- ![nouvelle icône](../../assets/new.svg) Extension de la fonctionnalité de la variable d’environnement `WARM_UP_PAGES` pour la prise en charge du préchargement du cache pour des pages de produits spécifiques. Pour obtenir une description détaillée des fonctionnalités, reportez-vous à la rubrique [Variables de post-déploiement](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-4444-->

- ![icône de correction](../../assets/fix.svg) Correction d’un problème en raison duquel une URL de magasin non valide provoquait l’échec du crochet de post-déploiement lors de l’utilisation de la fonctionnalité `WARM_UP_PAGES` pour remplir le cache. Ce problème se produisait uniquement lorsque les réécritures d’URL étaient désactivées.<!-- MAGECLOUD-4094 -->

## v1.0.1

Date de publication : 23 juillet 2019

- ![Icône de correctif](../../assets/fix.svg) Correction d’un problème affectant la fonctionnalité [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) qui utilise une URL de magasin par défaut. Désormais, si la commande `config:show:default-url` ne parvient pas à récupérer une URL de base, l&#39;URL de la variable MAGENTO_CLOUD_ROUTES est utilisée.<!-- MAGECLOUD-3866 -->

## v1.0.0

Date de publication : 12 juin 2019

Il s’agit de la première version du package [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components), qui est une nouvelle dépendance pour le package `ece-tools` version 2002.0.20 et ultérieure.

- ![nouvelle icône](../../assets/new.svg) Ajout de la possibilité d’utiliser des modèles regex pour configurer la variable d’environnement **WARM_UP_PAGES** afin de mettre en cache des pages uniques, plusieurs domaines et plusieurs pages. Voir [Variables de post-déploiement](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
