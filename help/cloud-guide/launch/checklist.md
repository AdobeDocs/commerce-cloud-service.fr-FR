---
title: Liste de contrôle de lancement
description: Consultez les éléments de liste de contrôle pour le lancement du site.
exl-id: 4525742e-18c5-40d1-975d-00ba3f3a51a0
source-git-commit: 6ac23cbcf7ab48d09b494ebe8c7136518d213c4e
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Liste de contrôle de lancement

Avant de procéder au déploiement dans l’environnement de production, téléchargez la [liste de contrôle de Launch](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf) et utilisez-la avec ces instructions pour confirmer que vous avez terminé tous les tests et la configuration requis. Consultez un aperçu du processus de déploiement complet pour Starter et Pro à l’adresse [Déployer votre boutique](../deploy/staging-production.md).

## Test complet en production

Voir [Test du déploiement](../test/staging-and-production.md) pour tester tous les aspects de vos sites, magasins et environnements. Ces tests incluent la vérification rapide, les tests d’acceptation utilisateur (UAT) et les tests de performances.

## TLS et Fastly

Adobe fournit un certificat SSL/TLS à chiffrer pour chaque environnement. Ce certificat est requis pour qu’il puisse servir du trafic sécurisé via HTTPS.

Pour utiliser ce certificat, vous devez mettre à jour votre configuration DNS afin que l’Adobe puisse terminer la validation du domaine et appliquer le certificat à votre environnement. Chaque environnement dispose d’un certificat unique qui couvre les domaines d’Adobe Commerce sur les sites d’infrastructure cloud déployés dans cet environnement. Nous vous recommandons d’effectuer et de mettre à jour la configuration pendant le [processus de configuration rapide](../cdn/fastly-configuration.md).

## Mise à jour de la configuration DNS avec les paramètres de production

Lorsque vous êtes prêt à lancer votre site, vous devez mettre à jour la configuration DNS pour acheminer le trafic depuis votre environnement de production par le biais du service Fastly.

**Conditions préalables :**

- [Configuration et test rapides dans votre environnement de développement](../cdn/fastly-configuration.md#)

- Mise à jour de la configuration de l’environnement de production avec tous les domaines requis

  En règle générale, vous collaborez avec votre conseiller technique client pour ajouter tous les domaines et sous-domaines de niveau supérieur requis pour vos magasins. Pour ajouter ou modifier les domaines de votre environnement de production, [Envoyez un ticket d’assistance Adobe Commerce](https://support.magento.com/hc/en-us/articles/360019088251). Attendez la confirmation que la configuration de votre projet a été mise à jour.

  Sur les projets de démarrage, vous devez ajouter les domaines à votre projet. Voir [Gestion des domaines](../cdn/fastly-custom-cache-configuration.md#manage-domains).

- Certificat SSL/TLS configuré pour vos environnements de production.

  Si vous avez ajouté les enregistrements de défi ACME pour vos domaines de production lors du processus de configuration rapide, Adobe télécharge automatiquement le certificat SSL/TLS vers votre environnement de production lorsque vous mettez à jour la configuration DNS pour acheminer le trafic vers le service Fastly. Si vous n’avez pas pré-configuré le certificat ou si vous avez mis à jour vos domaines, l’Adobe doit effectuer la validation du domaine et configurer le certificat, ce qui peut prendre jusqu’à 12 heures.

### Pour mettre à jour la configuration DNS pour le lancement du site :

1. Mettez à jour la configuration DNS suivante pour votre site de production :

   - Définissez toutes les redirections nécessaires, en particulier si vous effectuez une migration à partir d’un site existant.

   - Définissez l’enregistrement de ressource racine de la zone pour adresser le nom d’hôte.

   - Réduisez la valeur de la durée de vie (TTL) pour actualiser les informations DNS afin de diriger les clients vers le magasin de production approprié.

     Nous recommandons une valeur TTL nettement inférieure lors du changement d’enregistrement DNS. Cette valeur indique au DNS combien de temps mettre en cache l’enregistrement DNS. Une fois raccourci, le DNS est actualisé plus rapidement. Par exemple, vous pouvez modifier la valeur TTL de trois jours à 10 minutes lorsque vous mettez votre site à jour. Notez que le raccourcissement de la valeur TTL ajoute de la charge à l’infrastructure DNS. Restaurez la valeur précédente plus élevée après le lancement du site.


1. Ajoutez des enregistrements CNAME pour pointer les sous-domaines de votre environnement de production vers le service Fastly `prod.magentocloud.map.fastly.net`, par exemple :

   | Domaine ou sous-domaine | CNAME |
   | ----------------------- | -------------------------------- |
   | `www.<domain-name>.com` | prod.magentocloud.map.fastly.net |
   | `mystore.<domain-name>.com` | prod.magentocloud.map.fastly.net |

1. Si nécessaire, ajoutez des enregistrements A pour mapper le domaine apex (`<domain-name>.com`) aux adresses IP Fastly suivantes :

   | Domaine d’application | ANAME |
   | --------------- | ----------------- |
   | `<domain-name>.com` | `151.101.1.124` |
   | `<domain-name>.com` | `151.101.65.124` |
   | `<domain-name>.com` | `151.101.129.124` |
   | `<domain-name>.com` | `151.101.193.124` |

>[!IMPORTANT]
>
>Les instructions DNS de [RFC1034](https://www.rfc-editor.org/rfc/rfc1912) (**section 2.4**) indiquent que :
>_Un enregistrement CNAME n’est pas autorisé à coexister avec d’autres données. En d’autres termes, si suzy.podunk.xx est un alias pour sue.podunk.xx, vous ne pouvez pas non plus avoir d’enregistrement MX pour suzy.podunk.edu, ou un enregistrement A, ni même un enregistrement TXT._
>
>Pour cette raison, les enregistrements DNS doivent être de type `CNAME` pour les sous-domaines et de type `A` pour les domaines d’application (domaines racine). L’abandon de cette règle peut entraîner des interruptions de votre service de messagerie ou de la propagation DNS, car vous ne pouvez plus ajouter d’autres enregistrements, tels que MX ou NS. Certains fournisseurs DNS peuvent contourner ce problème en utilisant des personnalisations internes, mais le respect de la norme garantit stabilité et flexibilité (comme le changement du fournisseur DNS).

1. Mettez à jour l’URL de base.

   - Utilisez SSH pour vous connecter à l’environnement de production.

     ```bash
     magento-cloud ssh -e production
     ```

   - Utilisez l’interface en ligne de commande pour modifier l’URL de base de votre magasin.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://www.<domain-name>.com/"
     ```

   **REMARQUE** : vous pouvez également mettre à jour l’URL de base à partir de l’administrateur. Voir [Stocker les URL](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html) dans le _Guide des magasins Adobe Commerce et de l’expérience d’achat_.

1. Patientez quelques minutes pour que le site soit mis à jour.

1. Testez votre site.

## Vérification de la configuration de production

Effectuez une dernière passe pour valider la configuration Production pour un ou plusieurs magasins. Vous pouvez mettre à jour la configuration dans l’environnement Production. Si les paramètres sont en lecture seule, vous devrez peut-être ouvrir une connexion SSH et utiliser les commandes de l’interface de ligne de commande pour modifier la configuration ou apporter des modifications à la configuration dans votre environnement local. Une fois les mises à jour effectuées, vous pouvez déployer les modifications dans les environnements d’évaluation et de production.

Les modifications et vérifications suivantes sont recommandées :

- [Fin du test des emails sortants](../project/outgoing-emails.md)

- [ Configuration sécurisée pour les informations d’identification d’administrateur et URL d’administrateur de base](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin)

- [Optimiser toutes les images pour le web](../cdn/fastly-image-optimization.md)

- [Vérification des paramètres de minimisation pour HTML, JavaScript et CSS](../deploy/static-content.md)

## Vérification de la mise en cache rapide

- Vérifiez que la mise en cache rapide fonctionne correctement sur le site de production. Pour des tests et des vérifications détaillés, voir [Test rapide](../test/staging-and-production.md#check-fastly-caching).

- [Assurez-vous que la dernière version du module CDN Fastly pour Commerce est installée dans votre environnement de production.](../cdn/fastly-configuration.md#upgrade-the-fastly-module)

- [Assurez-vous que la version la plus récente du code VCL Fastly a été téléchargée.](../cdn/fastly-configuration.md#upload-vcl-to-fastly)

## Test de performance

Nous vous recommandons de passer en revue les options [Performance Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) dans le cadre de votre processus de préparation avant le lancement.

Vous pouvez également tester à l’aide des options tierces suivantes :

- [Siège](https://www.joedog.org/siege-home/) : logiciel de modélisation et de test du trafic pour pousser votre magasin à la limite. Accédez à votre site avec un nombre configurable de clients simulés. Le siège prend en charge l’authentification de base, les cookies, les protocoles HTTP, HTTPS et FTP.

- [Jmètre](https://jmeter.apache.org/) : excellent test de charge pour permettre d’évaluer les performances du trafic en pointe, comme pour les ventes Flash. Créez des tests personnalisés à exécuter sur votre site.

- [New Relic](https://support.newrelic.com/s/) (fourni) : aide à localiser les processus et les zones du site, ce qui entraîne des performances ralenties avec le temps passé par action suivi comme la transmission de données, de requêtes, de Redis, etc.

- [WebPageTest](https://www.webpagetest.org/) et [Pingdom](https://www.pingdom.com/) : analyse en temps réel du temps de chargement des pages de votre site avec différents emplacements d’origine. Le royaume peut coûter des frais. WebPageTest est un outil gratuit.

## Configuration de la sécurité

- [Configuration de votre analyse de sécurité](overview.md#set-up-the-security-scan-tool)

- [Configuration sécurisée pour l’utilisateur administrateur](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin)

- [Configuration sécurisée pour l’URL d’administration](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url)

- [Supprimer tous les utilisateurs qui ne se trouvent plus dans Adobe Commerce sur le projet d’infrastructure cloud](../project/user-access.md)

- [Configuration de l’authentification à deux facteurs](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/)

## Suivi des performances

Vous pouvez utiliser les services New Relic pour la surveillance des performances dans les environnements Pro et Starter. Sur les comptes Pro, nous fournissons la stratégie d’alerte Géré pour Adobe Commerce afin de surveiller les performances des applications et de l’infrastructure à l’aide des agents API et d’infrastructure New Relic. Pour plus d’informations sur l’utilisation de ces services, voir [Surveillance des performances avec les alertes gérées](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

### Étape suivante

[Étapes de lancement](steps.md)
