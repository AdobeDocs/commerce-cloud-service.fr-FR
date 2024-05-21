---
title: Notes de mise à jour de la suite Cloud Tools
description: Découvrez les dernières améliorations apportées à la suite Cloud Tools pour Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: e04a9de8f0e31098f0cc2e47112f206c11a0e23b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# Notes de mise à jour de Commerce Cloud Tools Suite

Les informations de cette version détaillent les dernières améliorations apportées aux modules Cloud Tools Suite for Commerce , conçus pour déployer et gérer les installations et mises à niveau Adobe Commerce sur la plateforme Cloud.

| Notes de mise à jour | Version | Description | Source |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package](ece-tools-package.md) | 2002.1.19 | Ensemble de scripts et d’outils conçus pour gérer et déployer des projets cloud | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Correctifs cloud pour Commerce](cloud-patches.md) | 1.0.27 | Ensemble de correctifs qui améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud. Ce package comprend les correctifs Adobe Commerce et les correctifs disponibles qui sont appliqués lorsque vous utilisez `ece-tools` pour déployer | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker pour Commerce](cloud-docker.md) | 1.3.7 | Fonctionnalités et fichiers de configuration pour les images Docker permettant de déployer Adobe Commerce dans un environnement cloud local | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Composants cloud de Commerce](cloud-components.md) | 1.0.14 | Extension des fonctionnalités de base d’Adobe Commerce pour les sites déployés sur l’infrastructure cloud | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

Lorsque vous effectuez une mise à jour vers la version 2002.1.0 ou ultérieure de CEE-Tools, vous effectuez automatiquement une mise à jour vers les versions les plus récentes des autres packages, qui sont des dépendances pour la variable `ece-tools` module. Voir [Métappackage cloud](../development/overview.md#cloud-metapackage) pour une liste de dépendances.
