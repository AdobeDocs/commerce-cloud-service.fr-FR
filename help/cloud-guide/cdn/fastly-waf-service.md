---
title: Web Application Firewall (WAF)
description: Découvrez comment le service WAF Fastly détecte, consigne et bloque le trafic de requêtes malveillantes avant qu’il puisse endommager le réseau ou les sites Adobe Commerce.
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Web Application Firewall (WAF)

Optimisé par Fastly, le service de pare-feu d’application web (WAF) pour Adobe Commerce sur l’infrastructure cloud détecte, consigne et bloque le trafic de requêtes malveillantes avant qu’il puisse endommager vos sites ou votre réseau. Le service WAF est disponible uniquement dans les environnements de production.

Le service WAF offre les avantages suivants :

- **Conformité PCI**: l’activation de WAF garantit que les vitrines Adobe Commerce dans les environnements de production répondent aux exigences de sécurité PCI DSS 6.6.
- **Stratégie WAF par défaut**: la stratégie WAF par défaut, configurée et gérée de manière rapide, fournit un ensemble de règles de sécurité personnalisées pour protéger vos applications web Adobe Commerce contre un large éventail d’attaques, y compris les attaques par injection, les entrées malveillantes, les scripts intersites, l’exfiltration de données, les violations de protocole HTTP et d’autres types d’attaques. [OWASP Top 1](https://owasp.org/www-project-top-ten/) menaces à la sécurité.
- **Intégration et activation du mode WAF**: Adobe déploie et active la stratégie WAF par défaut dans votre environnement de production dans les 2 à 3 semaines suivant la fin de la mise en service.
- **Support opérationnel et de maintenance**—
   - Adobe et configurez et gérez rapidement vos journaux et alertes pour le service WAF.
   - Adobe trie les tickets d’assistance clientèle en rapport avec les problèmes de service WAF qui bloquent le trafic légitime en tant que problèmes de priorité 1.
   - Les mises à niveau automatisées de la version du service WAF assurent une couverture immédiate pour les nouveaux projets ou les projets en cours d’évolution. Voir [Maintenance et mises à niveau du WAF](#waf-maintenance-and-updates).

>[!TIP]
>
>Pour plus d’informations sur la maintenance de la conformité PCI pour votre Adobe Commerce sur les magasins d’infrastructure cloud, voir [Conformité PCI](https://business.adobe.com/products/magento/pci-compliance.html).

## Activation de la fonction WAF

Adobe active le service WAF sur les nouveaux comptes dans les 2 à 3 semaines suivant la fin de l’approvisionnement. Le WAF est mis en oeuvre par le biais du service de CDN Fastly. Vous n’avez pas besoin d’installer ni de gérer du matériel ou des logiciels.

>[!NOTE]
>
>Avant de pouvoir utiliser le service WAF, vous devez acheminer tout le trafic externe vers votre Adobe Commerce sur le projet d’infrastructure cloud via le service Fastly. Voir [Configuration rapide](fastly-configuration.md).

## Fonctionnement

Le service WAF s’intègre à Fastly et utilise la logique de cache du service Fastly CDN pour filtrer le trafic sur les noeuds globaux Fastly. Nous activons le service WAF dans votre environnement de production avec une stratégie WAF par défaut basée sur [Règles de sécurité Mod de Trustwave SpiderLabs](https://github.com/owasp-modsecurity/ModSecurity) et les dix principales menaces de sécurité de l&#39;OWASP.

Le service WAF filtre le trafic HTTP et HTTPS (demandes de GET et de POST) par rapport à l’ensemble de règles WAF et bloque le trafic malveillant ou non conforme à des règles spécifiques. Le service filtre uniquement le trafic lié à l’origine qui tente d’actualiser le cache. Par conséquent, nous arrêtons la plupart du trafic d’attaques au niveau du cache Fastly, ce qui protège votre trafic d’origine des attaques malveillantes. En traitant uniquement le trafic d’origine, le service WAF conserve les performances du cache, en introduisant uniquement une estimation de 1,5 millisecondes à 20 millisecondes de latence pour chaque requête non mise en cache.

## Dépannage des requêtes bloquées

Lorsque le service WAF est activé, il filtre tout le trafic web et administrateur par rapport aux règles WAF et bloque toute requête web qui déclenche une règle. Lorsqu’une demande est bloquée, le demandeur voit une valeur par défaut `403 Forbidden` page d’erreur contenant un identifiant de référence pour l’événement de blocage.

![Page d’erreur WAF](../../assets/cdn/fastly-waf-403-error.png)

Vous pouvez personnaliser cette page de réponse aux erreurs à partir de l’administrateur. Voir [Personnalisation de la page de réponse WAF](fastly-custom-response.md#customize-the-waf-error-page).

Si votre page d’administration ou storefront Adobe Commerce renvoie une `403 Forbidden` en réponse à une demande d’URL légitime, envoyez une [ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Copiez l’ID de référence de la page de réponse d’erreur et collez-le dans la description du ticket.

## Maintenance et mises à jour du WAF

Instaurer et mettre à jour rapidement l’ensemble de règles WAF à partir de mises à jour de règles de tiers commerciaux, de recherches rapides et de sources ouvertes. Met rapidement à jour les règles publiées dans une stratégie selon les besoins ou lorsque des modifications apportées aux règles sont disponibles à partir de leurs sources respectives. En outre, Fastly peut ajouter des règles qui correspondent aux classes de règles publiées dans l’instance WAF de n’importe quel service une fois le service WAF activé. Ces mises à jour assurent une couverture immédiate des exploits nouveaux ou en évolution.

Adobe et gestion rapide du processus de mise à jour pour vous assurer que les règles WAF nouvelles ou modifiées fonctionnent efficacement dans votre environnement de production avant le déploiement des mises à jour en mode de blocage.

## Limites

Le service WAF standard, optimisé à la vitesse, ne prend pas en charge les fonctionnalités suivantes :

- Protection contre les logiciels malveillants ou la limitation des robots : envisagez d’utiliser [listes de contrôle d’accès](./fastly-vcl-allowlist.md) ou un service tiers.
- Limite de débit - Voir [Limite de taux](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) dans la documentation Fastly, ou reportez-vous à la section [Limite de débit](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) dans le _API Web Commerce_ section de sécurité.
- Configuration d’un point de fin de journalisation pour le client : voir [Service PrivateLink](../development/privatelink-service.md) comme alternative.

Bien que le service WAF ne vous permette pas de bloquer ou d’autoriser le trafic basé sur les adresses IP, vous pouvez ajouter des listes de contrôle d’accès (ACL) et des fragments de code VCL personnalisés à votre service Fastly afin de spécifier les adresses IP et la logique VCL pour bloquer ou autoriser le trafic. Voir [Fragments de code VCL personnalisés](fastly-vcl-custom-snippets.md).

Le filtrage des requêtes TCP, UDP ou ICMP n’est pas pris en charge par le service WAF. Toutefois, cette fonctionnalité est fournie par la protection intégrée de DDoS incluse avec le service de CDN Fastly. Voir [Protection DDoS](fastly.md#ddos-protection).
