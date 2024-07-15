---
title: Architecture mise à l’échelle
description: Découvrez l’architecture à plusieurs niveaux et comment elle s’adapte pour répondre à la demande.
feature: Cloud, Auto Scaling, Iaas, Logs
exl-id: c54d8772-b6cc-41cc-b1ab-bef7d6f13bf2
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Architecture évolutive

L’infrastructure Cloud s’adapte en fonction de vos besoins en ressources pour une efficacité accrue. Adobe Commerce sur l’infrastructure cloud surveille vos applications et peut ajuster la capacité pour maintenir des performances stables et prévisibles. La conversion vers cette architecture permet d’atténuer les problèmes, tels que la latence ou les pics de trafic importants.

>[!NOTE]
>
>L’architecture mise à l’échelle est disponible pour Adobe Commerce sur les comptes d’infrastructure cloud avec la grappe Pro 48 ou une version ultérieure.

## Architecture de niveau partagé

Historiquement, l’architecture Pro se composait de trois noeuds, chacun contenant un tech stack complet. Désormais, il existe une infrastructure évolutive qui fournit une architecture à niveaux avec un minimum de six noeuds : trois noeuds pour la base de données principale et les services, et trois noeuds pour le serveur web. Cette architecture à plusieurs niveaux permet de mettre à l’échelle les niveaux indépendamment afin d’obtenir un équilibre optimal des performances.

### Niveau de service

Il existe trois noeuds de service pour le stockage des données, le cache et les services : **OpenSearch** ou **Elasticsearch**, **MariaDB**, **Redis**, etc. Lorsque le niveau de service approche la capacité, le seul moyen d’augmenter la taille du serveur consiste à augmenter la puissance du processeur et la mémoire, par exemple. La capacité est limitée à la taille du noeud disponible. La grappe de base de données étant conçue pour une haute disponibilité, vous ne pouvez pas la mettre à l’échelle horizontalement de manière fiable avec les technologies utilisées.

![Mise à l’échelle du niveau de service](../../assets/scaling-service.png)

Supposons que le type d’instance de noeud de service soit _m5.2xlarge_ avec une mémoire vive de 32 Go. Un service, comme la base de données, utilise une quantité considérable de mémoire (30 Go). La mise à l’échelle à la prochaine taille d’instance disponible _m5.4xlarge_ fournit de la mémoire RAM de 64 Go, ce qui double la mémoire et prend en charge les besoins croissants de la base de données.

Vous pouvez optimiser davantage les performances du niveau de service en acheminant le trafic en fonction du type de noeud. Par défaut, le noeud de la base de données est isolé du trafic web. Par exemple, vous pouvez choisir de diffuser le trafic web sur le noeud de base de données.

### Niveau web

Il existe trois noeuds web pour les demandes de traitement et le trafic web : **php-fpm** et **NGINX**. En plus de la mise à l’échelle verticale en augmentant la puissance et la mémoire, le niveau web peut évoluer horizontalement en ajoutant des serveurs web à une grappe existante lorsqu’il est limité au niveau PHP. Voir [Mise à l’échelle automatique](autoscaling.md) pour découvrir comment les noeuds web se mettent automatiquement à l’échelle.

![Mise à l’échelle de niveau web](../../assets/scaling-web.png)

Cela complète la mise à l’échelle verticale fournie par le niveau de service. À mesure que le niveau de service évolue en taille et en puissance pour s’adapter à une utilisation croissante de la base de données et des services, le niveau web évolue en taille, puissance et instances afin de répondre à une augmentation des demandes de processus et à des exigences de trafic plus élevées.

Prenons l’exemple suivant : le type d’instance de noeud web est _C5.2xlarge avec huit processeurs et 16 Go de RAM_. Le nombre de requêtes sur le site a considérablement augmenté. Vous pouvez ajouter un noeud C5.2xlarge pour gérer l’augmentation des processus php-fpm ou vous pouvez remplacer chaque type d’instance par _C5.4xlarge avec 16 processeurs et 32 Go de RAM_. L’ajout d’un noeud réduit le risque d’insuffisance de capacité de montée en puissance.

## Structure du projet

Au minimum, les projets Pro avec l’architecture mise à l’échelle disposent de six noeuds.

- 3 noeuds web c5.2xlarge (8 processeurs, 16 Go de RAM)

- 3 noeuds de service m5.2xlarge (8 processeurs, 32 Go de RAM)

Cependant, chaque projet est unique et nécessite un suivi des performances pour analyser correctement la gestion des ressources. Chaque compte comprend le [service New Relic](../monitor/new-relic-service.md), qui se connecte automatiquement aux données de l’application et à l’analyse des performances afin de fournir une surveillance dynamique du serveur. Plus précisément, vous pouvez utiliser le service New Relic pour surveiller l’utilisation du processeur et de la mémoire vive afin de déterminer les noeuds qui nécessitent des ressources supplémentaires. Lorsqu’une ressource atteint sa capacité ou que vous constatez une dégradation des performances en fonction des analyses, vous pouvez créer une requête pour adapter votre infrastructure à la demande.

### Accès SSH

Certains fichiers et journaux, tels que le répertoire `/app/<project-id>/var/log`, ne sont pas partagés entre les noeuds. Chaque noeud dispose d’un accès SSH unique. Vous ne pouvez pas utiliser l’interface de ligne de commande `magento-cloud` pour vous connecter au service ou aux noeuds web, mais vous pouvez trouver les adresses de noeud dans la liste d’accès SSH de votre [!DNL Cloud Console].

```bash
ssh <node>.<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
```

- `node` 1 à 3 : adresses d’accès aux noeuds de service

- `node` 4 à _n_ : adresses pour accéder aux noeuds web

>[!TIP]
>
>Une fois connecté, vous pouvez confirmer l’ID du serveur et le rôle : les noeuds de service utilisent le rôle _unified_ et les noeuds web utilisent le rôle _web_.

L’exemple de réponse lors de la connexion à un **noeud de service** inclut le rôle _unifié_ :

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:unified.

project-id@server-id:~$
```

L’exemple de réponse lors de la connexion à un **noeud web** inclut le rôle _web_ :

```terminal
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:web.

project-id@server-id:~$
```

### Emplacements des journaux

L’emplacement du journal varie légèrement en fonction du noeud. Par exemple, un journal de base de données, tel que **MySQL error log**, est disponible sur un noeud de service (`/var/log/mysql/mysql-error.log`), mais il n’est pas disponible sur un noeud web.

Chaque compte Pro comprend le [service de journaux New Relic](../monitor/new-relic-service.md), qui se connecte automatiquement aux données de journal de l’application pour offrir une gestion dynamique des journaux. Les données de journal agrégées de tous les noeuds s’affichent dans l’application New Relic Logs afin que vous puissiez résoudre les problèmes de performances sur des noeuds spécifiques à partir d’un seul tableau de bord.
