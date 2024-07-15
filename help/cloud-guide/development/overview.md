---
title: Présentation du développement
description: Préparez-vous au développement local avec un projet d’infrastructure cloud Adobe Commerce.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Présentation du développement

Les environnements distants d’Adobe Commerce sur l’infrastructure cloud sont **en lecture seule**, y compris tous les environnements Starter et tous les environnements d’intégration, d’évaluation et de production Pro. Dans un environnement de développement local, vous pouvez écrire et tester du code avant de le transférer vers un environnement d’intégration pour effectuer d’autres tests et le déployer vers les environnements d’évaluation et de production.

Avant de préparer votre espace de travail local, vérifiez que vous disposez de vos [informations d’identification](../../get-started/prepare-workspace.md). Le développement local nécessite une installation PHP et du compositeur, sauf si vous optez pour l’utilisation de [Cloud Docker for Commerce](#docker-environment).

## Packages requis

Adobe Commerce sur l’infrastructure cloud utilise le compositeur pour gérer les dépendances et les mises à niveau des projets. Pour le développement local, vous devez installer les versions PHP et du compositeur compatibles avec votre projet Cloud. Par exemple, si vous utilisez le modèle cloud [!DNL Commerce] 2.4.7, vous pouvez constater que le fichier de configuration [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) utilise **PHP 8.3** et **Composer 2.7.2**.

Le compositeur installe les bibliothèques et dépendances requises pour votre projet dans le répertoire `vendor`. Les fichiers du compositeur requis suivants se trouvent dans le répertoire racine du projet :

- `composer.json` : utilisez le fichier `composer.json` pour gérer les installations et les mises à niveau de produit.
- `composer.lock` : le fichier `composer.lock` stocke un ensemble de dépendances de version exactes qui répondent aux contraintes de version de chaque exigence pour chaque module dans l’arborescence de dépendance du projet.

**Commandes courantes :**

| Commande | Description |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Mises à jour des dernières versions des dépendances reflétées dans le fichier `composer.json`. Cela met à jour le fichier `composer.lock`. |
| `composer install` | Lit le fichier `composer.lock` pour télécharger les dépendances. Il est recommandé de conserver une copie à jour de `composer.lock` dans votre référentiel de projet. |

{style="table-layout:auto"}

Une fois que vous avez ajouté, validé et envoyé le code mis à jour, le processus de déploiement exécute automatiquement la commande `composer install` pendant la [phase de création](../deploy/process.md#build-phase-build-phase).

### Métappackage cloud

Adobe Commerce sur l’infrastructure cloud utilise un métaphorage qui nécessite `magento/product-enterprise-edition`. Pour obtenir les dernières mises à jour de la dernière version de Commerce, utilisez la syntaxe de contrainte suivante :

```text
>=current_version <next_version
```

Par exemple, pour utiliser la dernière version d’Adobe Commerce 2.4.7, définissez `2.4.7` comme version &quot;actuelle&quot; et `2.4.8` comme version &quot;suivante&quot; dans le fichier `composer.json` :

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Les packages principaux de ce métapackage sont les suivants :

- **vendor/magento/ece-tools** : le package `ece-tools` est compatible avec Adobe Commerce version 2.1.4 et ultérieure pour fournir un riche ensemble de fonctionnalités que vous pouvez utiliser pour gérer votre Adobe Commerce sur le projet d’infrastructure cloud. Il contient des scripts et Adobe Commerce sur des commandes d’infrastructure cloud conçues pour vous aider à gérer votre code et à créer et déployer automatiquement vos projets. Voir la [`ece-tools` présentation du package](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition** : ce métappackage nécessite des composants d’application, notamment des modules, des structures, des thèmes, etc.
- **vendor/fastly2/magento2** : ce module gère le réseau de diffusion de contenu et les services Fastly pour les environnements d’évaluation et de production Pro, ainsi que les environnements de production Starter. Voir [Services rapides](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-paypal-on-boarding** : ce module fournit le passage en caisse de la passerelle de paiement PayPal en se connectant à votre compte marchand PayPal. Voir [Outil d’intégration PayPal](../store/paypal.md).

>[!TIP]
>
>Voir [Packages Cloud pour Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) dans les _Notes de mise à jour de Commerce_ pour obtenir une liste des dépendances et des licences tierces.

## Environnement Docker

Vous pouvez utiliser l’outil Cloud Docker pour Commerce pour émuler Adobe Commerce sur les environnements de production et de développement d’infrastructure cloud pour le développement local. Cloud Docker pour Commerce ne nécessite pas l’installation locale de PHP et du compositeur.

- [Développement local avec Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) dans le site Adobe Developer
- [Architecture de Docker et commandes courantes](../dev-tools/cloud-docker.md)
- [Notes de mise à jour de Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Pour plus d’informations sur l’utilisation des services d’hébergement Git avec Adobe Commerce sur l’infrastructure cloud, voir [Intégrations](../integrations/overview.md).
