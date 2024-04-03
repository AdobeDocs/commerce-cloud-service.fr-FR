---
title: Workflow du projet Pro
description: Découvrez comment utiliser les workflows de développement et de déploiement Pro.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Workflow du projet Pro

Le projet Pro comprend un seul référentiel Git avec une valeur globale. `master` branche et trois environnements principaux :

1. **Production** environnement de lancement et de maintenance du site actif
1. **Évaluation** environnement de test avec tous les services
1. **Intégration** environnement de développement et de test

![Liste des environnements Pro](../../assets/pro-environments.png)

Ces environnements sont `read-only`, acceptant les modifications de code déployées à partir des branches transférées à partir de votre espace de travail local. Voir [Architecture Pro](pro-architecture.md) pour une présentation complète des environnements Pro. Voir [[!DNL Cloud Console]](../project/overview.md#cloud-console) pour un aperçu de la liste des environnements Pro dans la vue du projet.

Le graphique suivant illustre le workflow de développement et de déploiement de Pro, qui utilise une approche simple d’embranchement git. You [development](#development-workflow) code à l’aide d’une branche active basée sur `integration` environnement, _pousser_ et _extraction_ Le code change pour et depuis votre branche distante active. Vous déployez du code vérifié par _fusion_ la branche distante vers la branche de base, qui active une [création et déploiement](#deployment-workflow) processus pour cet environnement.

![Vue de haut niveau du workflow de développement d’architecture Pro](../../assets/pro-dev-workflow.png)

## Workflow de développement

L’environnement d’intégration fournit une base unique. `integration` branche contenant votre Adobe Commerce sur le code d’infrastructure cloud. Vous pouvez créer une branche d’environnement active supplémentaire. Cela permet de déployer jusqu’à deux branches actives dans les conteneurs Platform as a service (PaaS). Le nombre d’environnements inactifs n’est pas limité.

{{enhanced-integration-envs}}

Les environnements de projet prennent en charge un processus d’intégration flexible et continu. Commencez par cloner la variable `integration` branche à votre dossier de projet local. Créez une branche ou plusieurs branches, développez de nouvelles fonctionnalités, configurez des modifications, ajoutez des extensions et déployez des mises à jour :

- **Récupérer** change depuis `integration`

- **Branche** de `integration`

- **Développer** code sur un poste de travail local, y compris [!DNL Composer] mises à jour

- **Push** modifications du code à distance et validation

- **Fusion** to `integration` et test

Avec une branche de code développée et les fichiers de configuration correspondants, vos modifications de code sont prêtes à être fusionnées dans la variable `integration` branche pour des tests plus complets. La variable `integration` L’environnement est également idéal pour :

- **Intégration de services tiers**: tous les services ne sont pas disponibles dans l’environnement PaaS.

- **Génération des fichiers de gestion de configuration**—Certains paramètres de configuration sont _Lecture seule_ dans un environnement déployé.

- **Configuration de votre boutique**: vous devez configurer entièrement tous les paramètres de magasin à l’aide de l’environnement d’intégration. Vous pouvez trouver la variable **Store Admin URL** sur le _integration_ vue d’environnement dans _[!DNL Cloud Console]_.

## Workflow de déploiement

Chaque fois que vous poussez le code de votre poste de travail local vers l’environnement distant ou que vous le fusionnez vers une branche d’environnement, les scripts de création et de déploiement génèrent un nouveau code et fournissent les services configurés à l’environnement distant.

Création d’actions de script :

- Le site de l’environnement cible continue de fonctionner pendant une génération

- Vérifier et exécuter Adobe Commerce sur les correctifs et correctifs de l’infrastructure cloud

- Compilation du code avec un journal de création et de déploiement

- Recherchez Configuration Management, le déploiement de contenu statique survient pendant cette phase.

- Créer ou utiliser une balise de code inchangé pour accélérer le processus

- Configuration de tous les services et applications principaux

Déployer des actions de script :

- Placez le site dans l’environnement cible dans un _Maintenance_ mode

- Déployer du contenu statique s’il n’est pas terminé pendant la génération

- Installation ou mise à jour d’Adobe Commerce sur l’infrastructure cloud

- Configuration du routage pour le trafic

Après le processus de création et de déploiement, votre magasin revient en ligne avec vos dernières modifications et configurations de code. Voir [Processus de déploiement](../deploy/process.md).

### Fusion vers l’intégration

Combinez toutes les modifications de code vérifiées en fusionnant votre branche de développement active dans la base `integration` branche. Vous pouvez tester toutes vos modifications sur la page `integration` avant de promouvoir des modifications dans l’environnement d’évaluation.

### Fusionner vers l’évaluation

L’évaluation est un environnement de pré-production qui fournit tous les services et paramètres aussi proches que possible de l’environnement de production. Envoyez toujours vos modifications de code à partir de la fonction `integration` à l’environnement `staging` afin que vous puissiez effectuer des tests approfondis avec tous les services. La première fois que vous utilisez l’environnement intermédiaire, vous devez configurer des services, tels que [Réseau de diffusion de contenu Fastly](../cdn/fastly.md) et [New Relic](../monitor/new-relic-service.md). Configurez les passerelles de paiement, l’expédition, les notifications et d’autres services essentiels avec un environnement de test ou des informations d’identification de test.

Il est préférable de tester minutieusement chaque service, de vérifier vos outils de test de performances et d’effectuer des tests UAT en tant qu’administrateur et client, jusqu’à ce que vous estimiez que votre boutique est prête pour l’environnement de production. Voir [Déployer votre boutique](../deploy/staging-production.md).

### Fusionner vers la production

Après des tests approfondis dans l’environnement d’évaluation, fusionnez-les dans l’environnement de production et testez-les minutieusement à l’aide des informations d’identification en direct. Le moment où vous lancez votre site de production, les clients doivent pouvoir effectuer des achats et les administrateurs doivent être en mesure de gérer la boutique en ligne. Consultez les rubriques suivantes pour obtenir une présentation détaillée et claire du déploiement de votre boutique et de sa mise en ligne :

- [Déployer votre boutique](../deploy/staging-production.md)
- [Lancement du site](../launch/overview.md)

### Fusionner vers le Principal global

Toujours envoyer une copie du code de production à la version globale `master` en cas de besoin émergent de déboguer l’environnement de production sans interrompre les services.

Do **not** créer une branche à partir de Global `master`. Utilisez la variable `integration` branche pour créer des branches actives pour le développement et les correctifs.
