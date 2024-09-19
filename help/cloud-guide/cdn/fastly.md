---
title: Présentation des services rapides
description: Découvrez comment les services Fastly inclus dans Adobe Commerce sur l’infrastructure cloud vous aident à optimiser et sécuriser les opérations de diffusion de contenu pour vos sites Adobe Commerce.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: dc4500bf-f037-47f0-b7ec-5cd1291f73a1
source-git-commit: dc331df378074af8a8776a33784b73082a39cf10
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 0%

---

# Présentation des services rapides

>[!WARNING]
>
>Pour maintenir la conformité PCI pour les sites Adobe Commerce déployés sur la plateforme Cloud, configurez Fastly sur votre branche principale Starter, les environnements Pro Production et Pro Staging. Si vous utilisez Adobe Commerce dans un déploiement sans interface utilisateur graphique, il est vivement recommandé d’utiliser Fastly pour mettre en cache les réponses GraphQL. Reportez-vous à la section [Mise en cache avec Fastly](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) dans le *Guide du développeur de GraphQL*.

Fournit rapidement les services suivants afin d’optimiser et de sécuriser les opérations de diffusion de contenu pour Adobe Commerce sur les projets d’infrastructure cloud. Ces services sont inclus avec Adobe Commerce sur l’infrastructure cloud sans frais supplémentaires.

- **Réseau de diffusion de contenu (CDN)** : service de marque qui met en cache vos pages de site, ressources, CSS, etc. dans les centres de données principaux que vous avez configurés. À mesure que les clients accèdent à votre site et stockent, les demandes atteignent Fastly afin de charger plus rapidement les pages mises en cache. Le service CDN fournit les fonctionnalités suivantes :

- **Gestion du cache** : mettez en cache vos pages de site, ressources, CSS, etc. dans les centres de données principaux que vous configurez pour réduire la charge et les coûts liés à la bande passante.

   - Utilisez les [ fragments de code VCL personnalisés (conformes à la version 2.1 de Varnish) ](fastly-vcl-custom-snippets.md) pour modifier la manière dont la mise en cache répond aux requêtes.

   - Configuration de la [prise en charge du service GeoIP](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Forcer les requêtes non chiffrées sur TLS](fastly-custom-cache-configuration.md#force-tls)

   - [Personnaliser les paramètres de délai d’expiration rapide](fastly-custom-cache-configuration.md#extend-fastly-timeout) pour empêcher 503 réponses aux demandes d’opérations en bloc

   - Créer [ pages de réponse d’erreur personnalisées](fastly-custom-response.md)

- **Sécurité** : une fois que vous avez activé les services rapides pour les sites Adobe Commerce, des fonctionnalités de sécurité supplémentaires sont disponibles pour protéger vos sites et votre réseau :

   - [Pare-feu d’applications web](fastly-waf-service.md) (WAF) : service de pare-feu d’applications web géré qui fournit une protection conforme PCI afin de bloquer le trafic malveillant avant qu’il puisse endommager votre Adobe Commerce de production sur les sites et le réseau d’infrastructure cloud. Le service WAF est disponible uniquement dans les environnements Pro et Starter Production.

   - [Protection par déni de service distribué (DDoS)](#ddos-protection) : protection par déni de service intégrée contre les attaques courantes telles que Ping of Death, les attaques à Smurf et d’autres attaques par inondation basées sur l’ICMP.

   - [Certificats SSL/TLS](fastly-configuration.md#provision-ssltls-certificates) : le service Fastly nécessite un certificat SSL/TLS pour servir le trafic sécurisé via HTTPS.

     Adobe Commerce fournit un certificat SSL/TLS Encrypt validé par le domaine pour chaque environnement d’évaluation et de production. Adobe Commerce procède à la validation des domaines et à la mise en service des certificats lors du processus de configuration rapide.

- **Cloaking d’origine** : empêche le trafic de contourner le WAF Fastly et masque les adresses IP de vos serveurs d’origine pour les protéger contre les attaques d’accès direct et de DDoS.

  Le cloaking d’origine est activé par défaut sur Adobe Commerce sur les projets d’infrastructure cloud Pro Production. Pour activer le cloaking d’origine sur Adobe Commerce dans les projets de production de démarrage de l’infrastructure cloud, envoyez un [ticket de support Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Si le trafic ne nécessite pas de mise en cache, vous pouvez personnaliser la configuration du service Fastly afin d’autoriser les requêtes à [contourner le cache Fastly](fastly-vcl-bypass-to-origin.md).

- **[Optimisation d’image](fastly-image-optimization.md)** : décharge le traitement des images et redimensionne la charge vers le service Fastly afin que les serveurs puissent traiter les commandes et les conversions plus efficacement.

- **[Journaux CDN et WAF rapides](../monitor/new-relic-service.md#new-relic-log-management)** : pour les projets Adobe Commerce sur l’infrastructure cloud Pro, vous pouvez utiliser le service New Relic Logs pour examiner et analyser rapidement les données du réseau de diffusion de contenu et des journaux WAF.

## Module CDN rapide pour Magento 2

Les services rapides pour Adobe Commerce sur l’infrastructure cloud utilisent le module [Fastly CDN pour Magento 2] installé dans les environnements suivants : Pro Staging and Production, Starter Production (`master` branche).

Lors de la mise en service ou de la mise à niveau initiale de votre projet Adobe Commerce, Adobe installe la dernière version du module CDN Fastly dans vos environnements d’évaluation et de production. Lorsque vous publiez rapidement des mises à jour de module, vous recevez des notifications dans l’Admin de vos environnements. Adobe vous recommande de mettre à jour vos environnements afin d’utiliser la dernière version. Voir [Mise à niveau rapide](fastly-configuration.md#upgrade-the-fastly-module).

## Compte de service et informations d’identification rapides

Adobe Commerce sur les projets d’infrastructure cloud ne reçoit pas de compte Fastly dédié. Le service Fastly est géré dans un compte centralisé enregistré dans Adobe et le tableau de bord de gestion n’est accessible que par l’équipe de support cloud.

À la place, chaque environnement d’évaluation et de production dispose d’informations d’identification Fastly uniques (jeton API et ID de service) pour configurer et gérer les services Fastly à partir de l’administrateur Commerce. L’API Fastly est disponible pour une gestion avancée du service Fastly, qui nécessite les informations d’identification pour envoyer ces requêtes.

Pendant la mise en service du projet, Adobe ajoute votre projet au compte de service Fastly d’Adobe Commerce sur l’infrastructure cloud et ajoute les informations d’identification Fastly à la configuration des environnements d’évaluation et de production. Voir [Obtenir des informations d’identification rapides](fastly-configuration.md#get-fastly-credentials).

### Modification du jeton API Fastly

Envoyez un ticket d’assistance Adobe Commerce pour modifier les informations d’identification du jeton API Fastly. Lorsque vous recevez le nouveau jeton, mettez à jour votre environnement d’évaluation ou de production pour utiliser le nouveau jeton.

**Pour modifier les informations d’identification du jeton API Fastly** :

1. [Envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) demandant de nouvelles informations d’identification d’API Fastly.

   Incluez votre Adobe Commerce à l’identifiant de projet d’infrastructure cloud et aux environnements nécessitant de nouvelles informations d’identification.

1. Une fois que vous avez reçu le nouveau jeton API, mettez à jour la valeur du jeton API dans la [configuration des informations d’identification rapides](fastly-configuration.md#test-the-fastly-credentials) dans l’administrateur ou à partir des [[!DNL Cloud Console]  variables d’environnement](../project/overview.md#configure-environment).

1. [Testez les nouvelles informations d’identification](fastly-configuration.md#test-the-fastly-credentials).

1. Après avoir mis à jour les informations d’identification, envoyez un ticket d’assistance Adobe Commerce pour supprimer l’ancien jeton API.

### Plusieurs comptes et domaines attribués à la date

Fastly vous permet uniquement d’affecter un domaine apex et des sous-domaines associés à un service et à un compte Fastly. Si vous disposez d’un compte Fastly qui lie les mêmes apex et sous-domaines utilisés pour votre site Adobe Commerce, vous disposez des options suivantes :

- Supprimez les apex et les sous-domaines du compte existant avant de demander des informations d’identification de service Fastly pour votre Adobe Commerce dans les environnements de projet d’infrastructure cloud. Voir [Utilisation de domaines] dans la documentation Fastly.

  Utilisez cette option pour lier le domaine apex et tous les sous-domaines au compte de service Fastly d’Adobe Commerce sur l’infrastructure cloud.

- Envoyez un ticket d’assistance Adobe Commerce pour demander la délégation de domaine afin que les apex et les sous-domaines puissent être liés à différents comptes.

  Utilisez cette option si vous disposez d’un domaine hexadécimal qui comporte plusieurs sous-domaines pour les sites Adobe Commerce et non Adobe Commerce et que vous souhaitez lier ces sous-domaines à différents comptes Fastly.

#### Délégation de domaine de demande

*Scénario 1 :*

Le domaine apex (`testweb.com` et `www.testweb.com`) est lié à un compte Fastly existant. Un projet d’infrastructure de cloud Adobe Commerce est configuré avec les sous-domaines suivants : `mcstaging.testweb.com` et `mcprod.testweb.com`. Vous ne souhaitez pas déplacer le domaine apex vers le compte de service Fastly d’Adobe Commerce sur l’infrastructure cloud.

Envoyez un [ ticket de support Fastly] demandant que les sous-domaines soient délégués du compte Fastly existant au compte Fastly d’Adobe Commerce sur l’infrastructure cloud. Incluez votre ID de projet Adobe Commerce dans le ticket.

Une fois la délégation terminée, vos sous-domaines de projet peuvent être ajoutés au compte de service Fastly d’Adobe Commerce sur l’infrastructure cloud. Voir [Obtenir des informations d’identification rapides](fastly-configuration.md#get-fastly-credentials).

*Scénario 2 :*

Le domaine apex (`testweb.com` et `www.testweb.com`) est lié au compte de service Fastly d’Adobe Commerce sur l’infrastructure cloud. Vous souhaitez gérer les services Fastly pour les sous-domaines `service.testweb.com` et `product-updates.testweb.com` à partir d’un autre compte Fastly.

Envoyez un ticket d’assistance Adobe Commerce demandant que les sous-domaines soient délégués d’Adobe Commerce sur l’infrastructure cloud Compte de service Fastly au compte Fastly. Incluez l’identifiant du service pour le compte Fastly dans le ticket.

## Protection DDoS

La protection DOS est intégrée au service de diffusion de contenu Fastly. Une fois que vous avez activé les services Fastly pour vos sites Adobe Commerce, Filtre Fastly tout le trafic web et administrateur afin de détecter et bloquer les attaques potentielles.

- Pour les attaques ciblant la couche 3 ou 4, le service Fastly filtre le trafic en fonction du port et du protocole, en examinant uniquement les requêtes HTTP ou HTTPS. ICMP, UDP et d’autres attaques initiées par le réseau sont larguées sur notre périphérie réseau. Cela inclut les attaques par réflexion et amplification, qui utilisent des services UDP comme SSDP ou NTP. En fournissant ce niveau de protection, nous bloquons efficacement les multiples attaques courantes comme Ping of Death, les attaques Smurf et d&#39;autres inondations basées sur l&#39;ICMP.

  Gère rapidement les attaques au niveau TCP sur la couche de cache. Cette stratégie fournit l’échelle et le contexte nécessaires par client pour gérer une attaque par inondation SYN et ses nombreuses variantes, y compris la pile TCP, les attaques par ressources et les attaques TLS dans les systèmes Fastly.

- Elle assure également une protection rapide contre les attaques de la couche 7. Si votre magasin rencontre des problèmes de performances et que vous pensez qu’il y a une attaque par déni de service (DDoS) de la couche 7, soumettez un ticket d’assistance Adobe Commerce. Adobe peut créer et appliquer des règles personnalisées au service Fastly afin d’examiner et d’éliminer les requêtes malveillantes en fonction de l’en-tête, de la charge utile ou d’une combinaison d’attributs qui identifient le trafic d’attaque. Voir [Recherche d’attaques DDoS] et [Comment bloquer le trafic malveillant] dans le *Centre d’aide Adobe Commerce*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Recherche d’attaques DDoS]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Module CDN rapide pour Magento 2]: https://github.com/fastly/fastly-magento2

[ticket de prise en charge rapide]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[Comment bloquer le trafic malveillant]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Utilisation des domaines]: https://docs.fastly.com/en/guides/working-with-domains
