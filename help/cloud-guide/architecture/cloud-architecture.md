---
title: Architecture cloud pour Commerce
description: Découvrez le contraste des architectures de projet Starter et Pro pour l’infrastructure Commerce on Cloud.
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
exl-id: 37cd6733-c10a-4d06-b784-171da576f9fc
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Architecture cloud pour Commerce

Adobe Commerce sur l’infrastructure cloud comporte un forfait Starter et Pro. Chaque plan dispose d’une architecture unique pour piloter votre processus de développement et de déploiement Adobe Commerce. Le plan de démarrage et l’architecture du plan Pro déploient des bases de données, des serveurs web et des serveurs de mise en cache dans plusieurs environnements pour des tests de bout en bout tout en prenant en charge l’intégration continue.

À titre de comparaison, chaque plan comprend les fonctionnalités d’infrastructure et les produits pris en charge suivants.

|          | Starter | Pro |
| -------- | --------------------| ------------------ |
| Fonctionnalités principales | <ul><li>[Toutes les fonctionnalités d’Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>Outil d’intégration PayPal</li><li>[Rapports Commerce](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li></ul> | <ul><li>[Toutes les fonctionnalités d’Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html)</li><li>Outil d’intégration PayPal</li><li>[Rapports Commerce](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209)</li><li>[Module B2B](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| Infrastructure et déploiement | <ul><li>Outils d’intégration continue dans le cloud avec un nombre illimité d’utilisateurs</li><li>Réseau de diffusion de contenu rapide (CDN), optimisation d’image (IO), et ajout de sécurité avec de généreuses bande passante. Le service Web Application Firewall (WAF) est disponible uniquement dans les environnements de production.</li><li>[New Relic](../monitor/new-relic-service.md) APM (Performance Monitoring) sur 3 branches : `master` et 2 de votre choix<br>Environnements de production, d’évaluation et de développement Platform as a service (PaaS) (4 environnements actifs au total) optimisés pour Adobe Commerce</li><li>Filtrage sortant (pare-feu sortant)</li></ul> | <ul><li>Outils d’intégration continue dans le cloud avec un nombre illimité d’utilisateurs</li><li>Réseau de diffusion de contenu rapide (CDN), optimisation d’image (IO), et ajout de sécurité avec de généreuses bande passante. Le service Web Application Firewall (WAF) est disponible uniquement dans les environnements de production.</li><li>[New Relic](../monitor/new-relic-service.md) Infrastructure en production + APM (Performance Monitoring) en évaluation et en production. La variable [Stratégie d’alertes gérées](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) pour la stratégie Adobe Commerce, mettez en oeuvre les bonnes pratiques de surveillance afin de vous avertir de manière proactive des problèmes d’application et d’infrastructure affectant les performances du site.</li><li>Plateforme en tant que service (PaaS) [Développement de l’intégration](pro-architecture.md#integration-environment) Environnements (2 environnements actifs au total) optimisés pour Adobe Commerce</li><li>Infrastructure as a service (IaaS) : infrastructure virtuelle dédiée aux environnements d’évaluation et de production</li></ul> |
| Infrastructure à haute disponibilité | | [Architecture en haute disponibilité](pro-architecture.md#redundant-hardware) avec une configuration à trois serveurs dans l’infrastructure sous-jacente en tant que service (IaaS) pour offrir une fiabilité et une disponibilité de niveau entreprise |
| Matériel dédié | | Matériel isolé et dédié dans l’infrastructure sous-jacente en tant que service (IaaS) pour offrir des niveaux de fiabilité et de disponibilité encore plus élevés |
| Prise en charge de la messagerie 24h/24, 7j/7 | Surveillance 24h/24, 7j/7 et prise en charge des courriers électroniques pour l’application principale et l’infrastructure cloud | Surveillance 24h/24, 7j/7 et prise en charge des courriers électroniques pour l’application principale et l’infrastructure cloud |
| Un conseiller technique client dédié | | Gestion de compte technique dédiée pour la période de lancement initiale, en commençant par votre abonnement jusqu’au lancement initial du site. |
| Modules complémentaires\* | <ul><li>[Module B2B](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _Disponible pour des frais supplémentaires_

## Projets de démarrage

La variable [Architecture du plan de démarrage](starter-architecture.md) comporte quatre environnements :

- **Intégration**: l’environnement d’intégration fournit deux environnements testables. Chaque environnement comprend une branche Git active, une base de données, un serveur web, une mise en cache, certains services, des variables d’environnement et des configurations.

- **Évaluation**: lorsque le code et les extensions réussissent vos tests, vous pouvez fusionner votre `integration` se branche à l’environnement d’évaluation, qui devient votre environnement de test de pré-production. Il comprend la variable `staging` branche active, base de données, serveur web, mise en cache, services tiers, variables d’environnement, configurations et services, tels que Fastly et New Relic.

- **Production**: lorsque le code est prêt et testé, tout le code est fusionné en `master` pour le déploiement sur le site en direct de production. Cet environnement inclut votre `master` branche, base de données, serveur web, mise en cache, services tiers, variables d’environnement et configurations.

- **Inactif**: vous disposez d’un nombre illimité de branches inactives.

## Projets Pro

La variable [Architecture Pro Formule](pro-architecture.md) a une dimension globale `master` avec trois environnements :

- **Intégration**: l’environnement d’intégration fournit un environnement testable qui comprend une base de données, un serveur web, une mise en cache, certains services, des variables d’environnement et des configurations. Vous pouvez développer, déployer et tester votre code avant de le fusionner dans l’environnement d’évaluation.

   - _Inactif_: vous pouvez avoir un nombre illimité de branches inactives en fonction de la variable `integration` mais une seule branche active (sans inclure `integration` ).

- **Évaluation**: l’environnement d’évaluation est destiné aux tests de pré-production et comprend une base de données, un serveur web, une mise en cache, des services tiers, des variables d’environnement, des configurations et des services, tels que Fastly.

- **Production**: l’environnement de production comprend une architecture à trois noeuds haute disponibilité pour vos données, services, mise en cache et stockage. La production est votre environnement de magasin public actif avec des variables d’environnement, des configurations et des services tiers.

## Logiciels et services pris en charge

Adobe Commerce sur l’infrastructure cloud utilise :

- Système d’exploitation : Debian GNU/Linux
- Serveur web : Nginx
- Base de données : MySQL (MariaDB)
- Réseau de diffusion de contenu (CDN) : Réseau de diffusion de contenu (CDN) Fastly

Vous pouvez configurer les services suivants :

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>Voir [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Guide d’installation_ pour les versions recommandées.

Le module CDN Fastly est utilisé pour le CDN et la mise en cache des services dans les environnements d’évaluation et de production. Voir [Configuration des services Fastly](../cdn/fastly.md).

Pour plus d’informations sur la configuration des versions de logiciels à utiliser dans votre mise en oeuvre, voir Adobe Commerce sur les fichiers de configuration de l’infrastructure cloud suivants :

- [Configuration de l’application (.magento.app.yaml)](../application/configure-app-yaml.md)
- [Configuration de l’environnement (.magento.env.yaml)](../environment/configure-env-yaml.md)
- [Configuration des itinéraires (routes.yaml)](../routes/routes-yaml.md)
- [Configuration des services (services.yaml)](../services/services-yaml.md)
