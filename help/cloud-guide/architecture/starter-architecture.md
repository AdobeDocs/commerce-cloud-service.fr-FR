---
title: Architecture de démarrage
description: Découvrez les environnements pris en charge par l’architecture de démarrage.
feature: Cloud, Paas
exl-id: 03365d32-4eb4-42d4-82a7-771df5e7b3da
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Architecture de démarrage

Votre architecture Adobe Commerce on cloud infrastructure Starter prend en charge jusqu’à **quatre** environnements, y compris un environnement `master` qui contient le code de projet initial, l’environnement d’évaluation et jusqu’à deux environnements d’intégration.

Tous les environnements se trouvent dans des conteneurs PaaS (Platform as a service). Ces conteneurs sont déployés dans des conteneurs soumis à des restrictions importantes sur une grille de serveurs. Ces environnements sont en lecture seule et acceptent les modifications de code déployées à partir des branches transférées à partir de votre espace de travail local. Chaque environnement fournit une base de données et un serveur web.

Vous pouvez utiliser n’importe quelle méthodologie de développement et d’embranchement de votre choix. Lorsque vous obtenez un accès initial à votre projet, créez un environnement `staging` à partir de l’environnement `master`. Créez ensuite l’environnement `integration` en créant un embranchement à partir de `staging`.

## Architecture de l’environnement de démarrage

Le diagramme suivant montre les relations hiérarchiques des environnements de démarrage.

![Affichage de haut niveau du projet Starter](../../assets/starter/architecture.png)

## Environnement de production

L’environnement de production fournit le code source permettant de déployer Adobe Commerce sur l’infrastructure cloud qui exécute vos vitrines à site unique et multisite destinées au public. L’environnement de production utilise le code de la branche `master` pour configurer et activer le serveur web, la base de données, les services configurés et le code de votre application.

Comme l’environnement `production` est en lecture seule, utilisez l’environnement `integration` pour apporter des modifications au code, déployez l’ensemble de l’architecture de `integration` à `staging`, et enfin vers l’environnement `production`. Voir [Déployer votre boutique](../deploy/staging-production.md) et [Lancement de site](../launch/overview.md).

Adobe recommande d’effectuer des tests complets dans votre branche `staging` avant de passer à la branche `master`, qui se déploie sur l’environnement `production`.

## Environnement d’évaluation

Adobe recommande de créer une branche appelée `staging` à partir de `master`. La branche `staging` déploie le code dans l’environnement d’évaluation afin de fournir un environnement de pré-production pour tester le code, les modules et les extensions, les passerelles de paiement, l’expédition, les données de produit, etc. Cet environnement fournit la configuration de tous les services pour qu’ils correspondent à l’environnement de production, y compris Fastly, New Relic APM et search.

Les sections supplémentaires de ce guide fournissent des instructions pour les déploiements de code final et le test des interactions au niveau de la production dans un environnement d’évaluation sécurisé. Pour optimiser les performances et les tests de fonctionnalités, répliquez votre base de données dans l’environnement d’évaluation.

>[!WARNING]
>
>Adobe recommande de tester chaque interaction client et commerciale dans l’environnement d’évaluation avant son déploiement dans l’environnement de production. Voir [Déployer votre boutique](../deploy/staging-production.md) et [Déploiement de tests](../test/staging-and-production.md).

## Environnement d’intégration

Les développeurs utilisent l’environnement `integration` pour développer, déployer et tester :

- Code de l’application Adobe Commerce

- Code personnalisé

- Extensions

- Services

**Cas d’utilisation recommandés :**

Les environnements d’intégration sont conçus pour un test et un développement limités. Par exemple, vous pouvez utiliser l’environnement d’intégration pour effectuer les tâches suivantes :

- Assurez-vous que les modifications apportées aux processus d’intégration continue (CI) sont compatibles avec le cloud

- Tester les workflows critiques sur les pages clés telles que Accueil, Catégorie, Page de détails des produits (PDP), Passage en caisse et Administration

Pour de meilleures performances dans l’environnement d’intégration, suivez les bonnes pratiques suivantes :

- Limitation de la taille du catalogue

- Limiter l’utilisation à un ou deux utilisateurs simultanés

- Désactivez les tâches cron et exécutez-les manuellement si nécessaire.

Vous pouvez avoir jusqu’à **deux** environnements d’intégration actifs. Vous créez un environnement d’intégration en créant une branche à partir de la branche `staging`. Lorsque vous créez un environnement d’intégration, le nom de l’environnement correspond au nom de la branche. Un environnement d’intégration comprend un serveur web et une base de données. Il n’inclut pas tous les services, par exemple, un réseau de diffusion de contenu Fastly et New Relic ne sont pas disponibles.

Vous pouvez avoir un nombre illimité de branches inactives pour le stockage du code. Pour accéder, afficher et tester une branche inactive, vous devez l’activer.

{{enhanced-integration-envs}}

## Pile de la technologie de production et d’évaluation

Les environnements de production et d’évaluation incluent les technologies suivantes. Vous pouvez modifier et configurer ces technologies par le biais du fichier [`.magento.app.yaml`](../application/configure-app-yaml.md).

- Fastly pour la mise en cache HTTP et CDN
- Serveur web Nginx parlant à PHP-FPM, une instance avec plusieurs programmes de travail
- Serveur Redis
- Elasticsearch pour la recherche catalogue pour Adobe Commerce 2.2 à 2.4.3-p2
- Recherchez dans le catalogue Adobe Commerce 2.3.7-p3, 2.4.3-p2 et 2.4.4 et versions ultérieures.
- Filtrage sortant (pare-feu sortant)

### Services

Adobe Commerce sur l’infrastructure cloud prend actuellement en charge les services suivants : PHP, MySQL (MariaDB), Elasticsearch (Adobe Commerce 2.2 à 2.4.3-p2), OpenSearch (2.3.7-p3, 2.4.3-p2, 2.4.4 et versions ultérieures), Redis et [!DNL RabbitMQ].

Chaque service s’exécute dans un conteneur sécurisé distinct. Les conteneurs sont gérés ensemble dans le projet. Certains services sont standard, par exemple :

- routeur HTTP (gestion des requêtes entrantes, mais aussi mise en cache et redirections)

- serveur d’applications PHP

- Git

- Shell sécurisé (SSH)

### Versions de logiciels

Adobe Commerce sur l&#39;infrastructure cloud utilise le système d&#39;exploitation Debian GNU/Linux et le serveur web NGINX. Vous ne pouvez pas mettre à niveau ce logiciel, mais vous pouvez configurer des versions pour les éléments suivants :

- [PHP](../application/php-settings.md)

- [MySQL](../services/mysql.md)

- [Redis](../services/redis.md)

- [RabbitMQ](../services/rabbitmq.md)

- [Elasticsearch](../services/elasticsearch.md)

- [OpenSearch](../services/opensearch.md)

Dans les environnements d’évaluation et de production, vous utilisez Fastly pour le réseau de diffusion de contenu et la mise en cache. La dernière version de l’extension CDN Fastly s’installe pendant la mise en service initiale de votre projet. Vous pouvez mettre à niveau l’extension pour obtenir les derniers correctifs et améliorations. Voir [Module CDN Fastly pour Magento 2](https://github.com/fastly/fastly-magento2). Vous avez également accès à [New Relic](../monitor/account-management.md) pour la surveillance des performances.

Utilisez les fichiers suivants pour configurer les versions de logiciels que vous souhaitez utiliser dans votre mise en oeuvre.

- [`.magento.app.yaml`](../application/configure-app-yaml.md)

- [`routes.yaml`](../routes/routes-yaml.md)

- [`services.yaml`](../services/services-yaml.md)

### Sauvegarde et reprise après sinistre

Vous pouvez créer une sauvegarde de votre base de données et de votre système de fichiers à l’aide de [!DNL Cloud Console] ou de l’interface de ligne de commande. Voir [Gestion des sauvegardes](../storage/snapshots.md).

## Préparation au développement

Le workflow suivant résume le processus de branche de votre code, de développement et de déploiement de votre magasin :

1. Configuration de votre environnement local

1. Cloner la branche `master` vers votre environnement local

1. Créez une branche `staging` à partir de `master`

1. Créer des branches pour le développement à partir de `staging`

1. Push code to Git qui crée et se déploie dans un environnement pour le test

Consultez les sections suivantes pour obtenir des instructions détaillées et des instructions détaillées sur le développement, le test et le déploiement de votre magasin :

- [Démarrer le workflow de développement et de déploiement](starter-develop-deploy-workflow.md)

- [Développement de Docker](../dev-tools/cloud-docker.md) (environnement de développement local activé par Cloud Docker pour Commerce)

- [Gestion des branches](../project/console-branches.md)

- [Déployer votre boutique](../deploy/staging-production.md)

- [Lancement du site](../launch/overview.md)
