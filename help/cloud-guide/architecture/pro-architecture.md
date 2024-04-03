---
title: Architecture Pro
description: Découvrez les environnements pris en charge par l’architecture Pro.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: 6807b572366d28fd54fbec89e7c119ec158b5e10
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Architecture Pro

Votre architecture Adobe Commerce sur l’infrastructure cloud Pro prend en charge plusieurs environnements que vous pouvez utiliser pour développer, tester et lancer votre boutique.

- **Principal**—Fournit un `master` branche déployée sur les conteneurs Platform as a service (PaaS).
- **Intégration**: fournit une seule `integration` branche pour le développement, bien que vous puissiez créer une branche supplémentaire. Cela permet d’obtenir jusqu’à deux _active_ branches déployées sur les conteneurs Platform as a service (PaaS).
- **Évaluation**: fournit une seule `staging` branche déployée vers les conteneurs de services d’infrastructure dédiés (IaaS).
- **Production**: fournit une seule `production` branche déployée vers les conteneurs de services d’infrastructure dédiés (IaaS).

Le tableau suivant résume les différences entre les environnements :

|                                        | INTÉGRATION | STAGING | PRODUCTION |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| Prise en charge de la gestion des paramètres dans le [!DNL Cloud Console] | Oui | Limitée | Limitée |
| Prise en charge de plusieurs branches | Oui | Non (évaluation uniquement) | Non (production uniquement) |
| Utilise les fichiers YAML pour la configuration | Oui | Non | Non |
| S’exécute sur du matériel IaaS dédié | Non | Oui | Oui |
| Inclut un réseau de diffusion de contenu rapide | Non | Oui | Oui |
| Inclut le service New Relic | Non | APM | APM + NRI |
| Sauvegardes automatiques | Non | Oui | Oui |

>[!NOTE]
>
>Adobe fournit l’outil Cloud Docker for Commerce pour le déploiement dans un environnement Cloud Docker local afin que vous puissiez développer et tester des projets Adobe Commerce. Voir [Développement de Docker](../dev-tools/cloud-docker.md).

## Architecture de l’environnement

Votre projet est un référentiel Git unique avec trois branches d’environnement principales : `integration`, `staging`, et `production`. Le diagramme suivant illustre la relation hiérarchique des environnements Pro :

![Vue de haut niveau de l’architecture de l’environnement Pro](../../assets/pro-branch-architecture.png)

### Environnement de Principal

Sur les projets Pro, la variable `master` branche fournit un environnement PaaS actif avec votre environnement de production. Envoyez toujours une copie du code de production à la variable `master` afin que vous puissiez déboguer l’environnement de production sans interrompre les services.

**Avertissements :**

- Do **not** créer une branche en fonction de la variable `master` branche. Utilisez l’environnement d’intégration pour créer des branches actives pour le développement.

- N’utilisez pas la variable `master` environnement pour le développement, l’UAT ou les tests de performance

### Environnement d’intégration

L’environnement d’intégration s’exécute dans un conteneur Linux (LXC) sur une grille de serveurs appelée PaaS. Chaque environnement comprend un serveur web et une base de données pour tester votre site. Voir [Adresses IP régionales](../project/regional-ip-addresses.md) pour obtenir une liste des adresses IP AWS et Azure.

**Cas d’utilisation recommandés :**

Les environnements d’intégration sont conçus pour des tests et un développement limités avant de déplacer les modifications vers les environnements d’évaluation et de production. Par exemple, vous pouvez utiliser l’environnement d’intégration pour effectuer les tâches suivantes :

- Assurez-vous que les modifications apportées aux processus d’intégration continue (CI) sont compatibles avec le cloud

- Tester les workflows critiques sur les pages clés telles que Accueil, Catégorie, Page de détails des produits (PDP), Passage en caisse et Administration

Pour de meilleures performances dans l’environnement d’intégration, suivez les bonnes pratiques suivantes :

- Limitation de la taille du catalogue

- Limiter l’utilisation à un ou deux utilisateurs simultanés

- Désactivez les tâches cron et exécutez-les manuellement si nécessaire.

**Avertissements :**

- Les services CDN et New Relic rapides ne sont pas accessibles dans un environnement d’intégration

- L’architecture de l’environnement d’intégration ne correspond pas à l’architecture intermédiaire et de production.

- N’utilisez pas la variable `integration` environnement pour les tests de développement, de performance ou d’acceptation utilisateur (UAT)

- N’utilisez pas la variable `integration` environnement de test B2B pour la fonctionnalité Adobe Commerce

- Vous ne pouvez pas restaurer la base de données dans l’environnement d’intégration à partir de la production ou de l’évaluation de la base de données.

{{enhanced-integration-envs}}

### Environnement d’évaluation

L’environnement d’évaluation fournit un environnement de quasi-production pour tester votre site. Cet environnement, qui est hébergé sur du matériel IaaS dédié, comprend tous les services, tels que Fastly CDN, New Relic APM et la recherche.

**Cas d’utilisation recommandés :**

L’environnement correspond à l’architecture de production. Il est conçu pour l’UAT, l’évaluation du contenu et la révision finale avant d’envoyer les fonctionnalités à la `production` environnement. Par exemple, vous pouvez utiliser la variable `staging` pour effectuer les tâches suivantes :

- Test de régression par rapport aux données de production

- Test de performance avec activation de la mise en cache rapide

- Test de nouvelles versions au lieu de l’application de correctifs dans l’environnement de production

- Test UAT pour les nouveaux builds

- Test B2B pour Adobe Commerce

- Personnalisation de la configuration cron et test des tâches cron

Voir [Workflow de déploiement](pro-develop-deploy-workflow.md#deployment-workflow) et [Test du déploiement](../test/staging-and-production.md).

**Avertissements :**

- Après le lancement du site de production, utilisez l’environnement d’évaluation principalement pour tester les correctifs de bogues critiques pour la production.

- Vous ne pouvez pas créer une branche à partir de la fonction `staging` branche. À la place, vous poussez les modifications de code depuis la variable `integration` vers la branche `staging` branche.

### Environnement de production

L’environnement de production exécute vos vitrines à site unique et multi-site destinées au public. Cet environnement s’exécute sur du matériel IaaS dédié, qui comprend des noeuds redondants haute disponibilité pour un accès continu et une protection contre le basculement pour vos clients. L’environnement de production comprend tous les services de l’environnement d’évaluation, plus le [Infrastructure New Relic (NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) qui se connecte automatiquement aux données de l’application et aux analyses des performances afin de fournir une surveillance dynamique du serveur.

**Avertissement :**

Vous ne pouvez pas créer une branche à partir de la fonction `production` branche. À la place, vous poussez les modifications de code depuis la variable `staging` vers la branche `production` branche.

### Pile de technologie de production

L&#39;environnement de production comporte trois machines virtuelles derrière un équilibreur de charge élastique géré par un HAProxy par VM. Chaque VM comprend les technologies suivantes :

- **Réseau de diffusion de contenu Fastly**—Mise en cache HTTP et CDN

- **NGINX**—serveur web avec PHP-FPM, une instance avec plusieurs programmes de travail

- **GlusterFS**—serveur de fichiers pour la gestion de tous les déploiements de fichiers statiques et la synchronisation avec quatre montages de répertoires :

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis**: un serveur par VM avec un seul actif et les deux autres comme réplicas

- **Elasticsearch**: recherchez Adobe Commerce sur l’infrastructure cloud 2.2 à 2.4.3-p2.

- **OpenSearch**: recherchez Adobe Commerce sur l’infrastructure cloud 2.3.7-p3, 2.4.3-p2, 2.4.4 et versions ultérieures.

- **Galera**: grappe de base de données avec une base de données MariaDB MySQL par noeud avec un paramètre d’incrémentation automatique de trois pour les identifiants uniques de chaque base de données

La figure suivante présente les technologies utilisées dans l’environnement de production :

![Pile de technologie de production](../../assets/az-stack-diagram.png)

## Matériel redondant

Plutôt que de diriger une `master` Pour une configuration primaire secondaire, Adobe Commerce sur l’infrastructure cloud exécute une _architecture redondante_ où les trois instances acceptent les lectures et écritures. Cette architecture n’offre aucun temps d’arrêt lors de la mise à l’échelle et offre une intégrité transactionnelle garantie.

En raison du matériel unique et redondant, Adobe peut fournir trois serveurs de passerelle. La plupart des services externes vous permettent d’ajouter plusieurs adresses IP à une liste autorisée. Par conséquent, avoir plusieurs adresses IP fixes n’est pas un problème. Les trois passerelles correspondent aux trois serveurs de votre grappe d’environnements de production et conservent les adresses IP statiques. Elle est entièrement redondante et hautement disponible à tous les niveaux :

- DNS
- Réseau de diffusion de contenu (CDN)
- Équilibreur de charge élastique (ELB)
- Grappe de trois serveurs comprenant tous les services Adobe Commerce, y compris la base de données et le serveur web

## Sauvegarde et reprise après sinistre

Adobe Commerce sur l’infrastructure cloud utilise une architecture haute disponibilité qui reproduit chaque projet Pro sur trois zones de disponibilité AWS ou Azure distinctes, chacune d’elles disposant d’un centre de données distinct. Outre cette redondance, les environnements d’évaluation et de production Pro reçoivent des sauvegardes en direct régulières, conçues pour être utilisées dans les cas où _échec catastrophique_.

**Sauvegardes automatiques** Incluez des données persistantes provenant de tous les services en cours d’exécution, comme la base de données MySQL et les fichiers stockés sur les volumes montés. Les sauvegardes sont enregistrées dans un stockage en bloc chiffré (EBS) dans la même région que l’environnement de production. Les sauvegardes automatiques ne sont pas accessibles publiquement car elles sont stockées dans un système distinct.

{{pro-backups}}

Vous pouvez créer un **sauvegarde manuelle** de la base de données pour vos environnements d’évaluation et de production à l’aide des commandes de l’interface de ligne de commande. Voir [Sauvegarde de la base](../storage/database-dump.md). Pour `integration` , Adobe recommande de créer une sauvegarde comme première étape après avoir accédé à votre projet d’infrastructure cloud Adobe Commerce et avant d’appliquer toute modification majeure. Voir [Gestion des sauvegardes](../storage/snapshots.md).

### Objectif du point de récupération

RPO est six heures au maximum pour terminer la dernière sauvegarde (par exemple à 6h00, puis à 12h00, puis 18h00). La fréquence des sauvegardes dépend du planning de sauvegarde de votre plan et du volume des modifications à écrire au service de stockage.

### Politique de rétention

Adobe conserve les sauvegardes automatiques, conformément à la politique de conservation des données suivante :

| Période | Stratégie de conservation des sauvegardes |
| ------------------ | ----------------------- |
| Jour 1 à 3 | Une sauvegarde par heure |
| Jours 4 à 7 | Une sauvegarde par jour |
| Semaines 2 à 6 | Une sauvegarde par semaine |
| Semaines 8 à 12 | Sauvegarde bi-hebdomadaire |
| Mois 3 à 5 | Une sauvegarde par mois |

Cette stratégie peut varier en fonction de votre plan d’infrastructure cloud.

### Objectif du temps de récupération

Le RTO dépend de la taille du stockage. Les gros volumes EBS nécessitent plus de temps pour être restaurés. Les temps de restauration peuvent varier en fonction de la taille de votre base de données :

- Une base de données volumineuse (200 Go ou plus) peut prendre 5 heures.
- Une base de données moyenne (150 Go) peut prendre 2 heures et demie.
- Une petite base de données (60 Go) peut prendre 1 heure

{{pro-backups}}

## Mise à l’échelle Pro

Redimensionnement de la grappe Pro _compute_ les configurations varient en fonction du fournisseur cloud sélectionné (AWS, Azure), de la région et des dépendances de service. L’infrastructure cloud d’Adobe peut mettre à l’échelle des grappes Pro pour répondre aux attentes en matière de trafic et aux besoins en matière de service au fur et à mesure que les demandes changent.

L’architecture redondante permet à l’infrastructure cloud d’Adobe d’évoluer sans temps d’arrêt. Lors de la mise à l’échelle, chacune des trois instances alterne pour mettre à niveau la capacité sans affecter le fonctionnement du site. Par exemple, vous pouvez ajouter des serveurs web supplémentaires à une grappe existante si la construction se fait au niveau PHP plutôt qu’au niveau de la base de données. Cette variable fournit les _mise à l’échelle horizontale_ pour compléter la mise à l’échelle verticale fournie par des processeurs supplémentaires au niveau de la base de données. Voir [Architecture mise à l’échelle](scaled-architecture.md).

Si vous prévoyez une augmentation importante du trafic pour un événement ou une autre raison, vous pouvez demander une augmentation temporaire de la capacité. Voir [Comment demander une modification temporaire](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) dans le _Centre d’aide Commerce_.
