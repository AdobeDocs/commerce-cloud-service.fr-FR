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

Adobe Commerce sur les infrastructures cloud les environnements distants sont les suivants : **Lecture seule**, y compris tous les environnements de démarrage et tous les environnements d’intégration, d’évaluation et de production Pro. Dans un environnement de développement local, vous pouvez écrire et tester le code avant de le transmettre à un environnement d’intégration pour des tests et un déploiement supplémentaires dans les environnements d’évaluation et de production.

Avant de préparer votre espace de travail local, vérifiez que vous disposez de vos [informations d’identification](../../get-started/prepare-workspace.md). Le développement local nécessite l&#39;installation de PHP et du compositeur, sauf si vous choisissez d&#39;utiliser [Cloud Docker pour Commerce](#docker-environment).

## Packages requis

Adobe Commerce sur l’infrastructure cloud utilise le compositeur pour gérer les dépendances et les mises à niveau des projets. Pour le développement local, vous devez installer les versions PHP et Composer compatibles avec votre projet Cloud. Par exemple, si vous utilisez [!DNL Commerce] 2.4.7 modèle de cloud, vous pouvez voir que le [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) le fichier de configuration utilise **PHP 8.3** et **Compositeur 2.7.2**.

Le compositeur installe les bibliothèques et les dépendances requises pour votre projet dans le `vendor` répertoire. Les fichiers Composer requis suivants se trouvent dans le répertoire racine du projet :

- `composer.json`: utilisez le `composer.json` pour gérer les installations et les mises à niveau de produits.
- `composer.lock`—Le `composer.lock` Le fichier stocke un ensemble de dépendances de version exactes qui répondent aux contraintes de version de chaque exigence pour chaque package dans l’arborescence des dépendances du projet.

**Commandes courantes :**

| Commande | Description |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Mises à jour vers les dernières versions des dépendances reflétées dans le `composer.json` fichier . Cette action met à jour le `composer.lock` fichier . |
| `composer install` | Lit le `composer.lock` fichier pour télécharger les dépendances. Il est recommandé de conserver une copie à jour des `composer.lock` dans le référentiel de votre projet. |

{style="table-layout:auto"}

Une fois que vous avez ajouté, validé et envoyé le code mis à jour, le processus de déploiement exécute automatiquement le `composer install` commande pendant [phase de création](../deploy/process.md#build-phase-build-phase).

### Métapaquet cloud

Adobe Commerce sur l’infrastructure cloud utilise un métapaquet qui nécessite `magento/product-enterprise-edition`. Pour obtenir les dernières mises à jour de la dernière version de Commerce, utilisez la syntaxe de contrainte suivante :

```text
>=current_version <next_version
```

Par exemple, pour utiliser la dernière version d’Adobe Commerce 2.4.7, définissez `2.4.7` comme la version « actuelle » ; et `2.4.8` comme version « suivante » dans `composer.json` fichier :

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Les principaux packages de ce métapaquet sont les suivants :

- **fournisseur/magento/ece-tools**—Le `ece-tools` Le package est compatible avec les versions 2.1.4 et ultérieures d’Adobe Commerce. Il fournit un large éventail de fonctionnalités que vous pouvez utiliser pour gérer votre projet d’infrastructure Adobe Commerce sur cloud. Il contient des scripts et des commandes d’Adobe Commerce sur l’infrastructure cloud conçus pour vous aider à gérer votre code et à créer et déployer automatiquement vos projets. Voir la [`ece-tools` présentation du package](../dev-tools/package-overview.md).
- **édition fournisseur/magento/product-enterprise**: ce métapaquet nécessite des composants d’application, notamment des modules, des structures, des thèmes, etc.
- **fournisseur/fastly2/magento2**: ce module gère le réseau CDN Fastly et les services pour les environnements d’évaluation et de production Pro et de production de démarrage. Voir [Services Fastly](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **fournisseur/magento/module-paypal-on-boarding**—Ce module permet de passer en caisse avec la passerelle de paiement PayPal en se connectant à votre compte marchand PayPal. Voir [Outil d’intégration PayPal](../store/paypal.md).

>[!TIP]
>
>Voir [Packages cloud pour Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) dans le _Notes de mise à jour de Commerce_ pour obtenir une liste des dépendances et des licences tierces.

## Environnement Docker

Vous pouvez utiliser l’outil Cloud Docker for Commerce pour émuler Adobe Commerce sur les environnements de production et de développement d’infrastructure cloud pour le développement local. Cloud Docker for Commerce ne nécessite pas l’installation locale de PHP et du compositeur.

- [Développement local avec Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) sur le site Adobe Developer
- [Architecture Docker et commandes courantes](../dev-tools/cloud-docker.md)
- [Notes de mise à jour de Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Pour plus d’informations sur l’utilisation des services d’hébergement basés sur Git avec Adobe Commerce sur les infrastructures cloud, voir [Intégrations](../integrations/overview.md).
