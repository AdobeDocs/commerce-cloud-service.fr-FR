---
title: Notes de mise à jour de la suite Cloud Tools
description: Découvrez les dernières améliorations apportées à la suite Cloud Tools pour Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: f294370379ec2216ec32ccc606b77453211aa50a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 1%

---

# Notes de mise à jour de Commerce Cloud Tools Suite

Les informations de cette version détaillent les dernières améliorations apportées aux modules Cloud Tools Suite for Commerce , conçus pour déployer et gérer les installations et mises à niveau Adobe Commerce sur la plateforme Cloud.

| Notes de mise à jour | Version | Description | Source |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package](ece-tools-package.md) | 2002.2.0 | Ensemble de scripts et d’outils conçus pour gérer et déployer des projets cloud | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.2.0) |
| [Correctifs cloud pour Commerce](cloud-patches.md) | 1.1.0 | Ensemble de correctifs qui améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud. Ce package comprend les correctifs Adobe Commerce et les correctifs disponibles qui sont appliqués lorsque vous utilisez `ece-tools` pour déployer | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.1.0) |
| [Cloud Docker pour Commerce](cloud-docker.md) | 1.4.0 | Fonctionnalités et fichiers de configuration pour les images Docker permettant de déployer Adobe Commerce dans un environnement cloud local | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Composants cloud de Commerce](cloud-components.md) | 1.1.0 | Extension des fonctionnalités de base d’Adobe Commerce pour les sites déployés sur l’infrastructure cloud | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.1.0) |

Lorsque vous effectuez une mise à jour vers la version 2002.1.0 ou ultérieure d’ECE-Tools, vous effectuez automatiquement une mise à jour vers les dernières versions des autres packages, qui sont des dépendances du package `ece-tools`. Voir [Métapackage cloud](../development/overview.md#cloud-metapackage) pour obtenir une liste des dépendances.

La nouvelle version de `ece-tools` (2002.2.0) est disponible avec PHP version 8.1 et ultérieure (8.2, 8.3) uniquement. Les anciennes versions de PHP étaient obsolètes (7.4, 7.3, 7.2). Vous pouvez utiliser les versions précédentes de `ece-tools` avec d’anciennes versions PHP.
