---
title: Pile de technologie
description: Voir la pile de technologies qui forme l’infrastructure Commerce on Cloud.
feature: Cloud, Iaas, Paas
exl-id: e456db25-c44b-4053-b96d-517d3d1606d0
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Pile de technologie

Considérez Adobe Commerce sur l’infrastructure cloud comme cinq couches fonctionnelles, comme illustré ci-dessous :

![Pile cloud](../../assets/CloudStack.svg)

1. [**Cloud Infrastructure**](pro-architecture.md) : sélectionnez Amazon Web Services (AWS) ou Microsoft Azure comme base d’infrastructure en tant que service (IaaS) pour vos projets Adobe Commerce on cloud infrastructure Pro.

   Adobe analyse régulièrement votre utilisation de la ressource de calcul virtuelle (vCPU) et alloue automatiquement des ressources afin d’optimiser votre utilisation à long terme et d’atténuer le risque de dépasser la limite de journée annuelle de la vCPU. Si vous prévoyez une augmentation du trafic sur le site pour des périodes spécifiques, vous devez continuer à ouvrir un ticket d’ assistance pour [demander une modification temporaire de la taille](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html).

1. [**Platform as a Service**](cloud-architecture.md) : chaque projet d’infrastructure cloud d’Adobe Commerce fournit un environnement d’intégration Platform as a Service (PaaS) pour le développement, le test et l’intégration des services.
1. [**Adobe Commerce**](../project/overview.md) : Adobe Commerce sur l’infrastructure cloud fournit une infrastructure préconfigurée qui comprend des technologies PHP, MySQL (MariaDB), Redis, [!DNL RabbitMQ] et des moteurs de recherche prises en charge.
1. [**Outils de performances**](../monitor/new-relic-service.md) : les outils de performances de New Relic vous permettent de déboguer, de surveiller et de gérer vos applications et votre infrastructure en collectant, analysant et affichant des données de votre Adobe Commerce sur des projets d’infrastructure cloud.
1. [**Réseau de diffusion de contenu (CDN), pare-feu d’applications web ([!DNL WAF]) et optimisation des images (IO)**](../cdn/fastly.md) :

   * [Réseau de diffusion de contenu Fastly](../cdn/fastly.md#ddos-protection) : fournit des services de réseau de diffusion de contenu sécurisés avec une protection intégrée contre les attaques par déni de service distribué (DDoS) telles que [!DNL Ping of Death], les attaques [!DNL Smurf] et les autres attaques par inondation basées sur le protocole ICMP (Internet Control Message Protocol).
   * [Web Application Firewall (WAF)](../cdn/fastly-waf-service.md) : les services WAF garantissent la conformité PCI pour les storefronts Adobe Commerce dans les environnements de production et les stratégies WAF qui protègent vos applications web Adobe Commerce contre les attaques par injection, les entrées malveillantes, les scripts intersites, l’exfiltration de données, les violations de protocole HTTP et d’autres [[!DNL OWASP] Dix principales menaces de sécurité](https://owasp.org/www-project-top-ten/).
   * [Optimisation des images (IO)](../cdn/fastly-image-optimization.md) : fournit une manipulation et une optimisation d’images en temps réel pour accélérer la diffusion des images et simplifier la maintenance des visionneuses de sources d’images pour les applications web réactives. Une E/S rapide décharge le traitement et le redimensionnement des images, libérant ainsi les serveurs pour traiter efficacement les commandes et les conversions.

Les applications monolithiques sont gourmandes en ressources et difficiles à mettre à l’échelle et à servir rapidement. Grâce à l’infrastructure cloud, les clients Commerce bénéficient d’un accès inégalé aux microservices basés sur SaaS, qui sont riches, intelligents et performants. Voir [Logiciels et services pris en charge](cloud-architecture.md#supported-software-and-services).

Utilisez le [guide de prise en main de Commerce](../../get-started/overview.md) pour configurer votre nouveau programme Cloud et commencer à gérer votre application [!DNL Commerce] dans un environnement natif dans le cloud.
