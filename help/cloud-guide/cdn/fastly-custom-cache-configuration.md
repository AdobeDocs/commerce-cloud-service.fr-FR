---
title: Personnalisation de la configuration du cache
description: Découvrez comment passer en revue et personnaliser les paramètres de configuration du cache une fois la configuration du service Fastly terminée.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# Personnalisation de la configuration du cache

Après avoir configuré et testé le service Fastly dans vos environnements d’évaluation et de production, passez en revue et personnalisez les paramètres de configuration du cache. Par exemple, vous pouvez mettre à jour les paramètres pour forcer TLS à rediriger les requêtes HTTP vers Fastly, mettre à jour les paramètres de purge et activer l’authentification de base pour protéger par mot de passe votre site pendant le développement.

Les sections suivantes présentent un aperçu et des instructions de configuration de certains paramètres du cache. Pour plus d’informations sur les options de configuration disponibles, voir [Module CDN rapide pour Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) la documentation.

## Forcer TLS

La fonction _Forcer TLS_ option permettant de rediriger les requêtes non chiffrées (HTTP) vers Fastly. Une fois que votre environnement d’évaluation ou de production a été configuré avec un [certificat SSL/TLS valide](fastly-configuration.md#provision-ssltls-certificates), vous pouvez mettre à jour la configuration Fastly de votre boutique afin d’activer l’option Forcer TLS . Voir la section [Guide Forcer TLS](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) dans le _Module CDN rapide pour Magento 2_ la documentation.

>[!NOTE]
>
>L’activation de l’option Forcer TLS est une bonne pratique pour Adobe Commerce sur les magasins d’infrastructure cloud.

## Étendre le délai d’expiration rapide

La configuration de service Fastly spécifie un délai d’expiration par défaut de 180 secondes pour les demandes HTTPS à l’administrateur. Tout traitement de requête qui dépasse le délai d’expiration renvoie une erreur 503. Par conséquent, vous pouvez recevoir 503 erreurs en réponse à des demandes qui nécessitent un traitement long ou lorsque vous essayez d’effectuer des opérations en bloc.

Pour terminer des actions en bloc qui prennent plus de 3 minutes, modifiez la variable _Délai du chemin d’accès administrateur_ value_ pour éviter les erreurs 503.

>[!NOTE]
>
>Pour étendre les paramètres de délai d’expiration rapides à d’autres utilisateurs que l’administration dans l’interface utilisateur de Fastly, voir [Augmentation des dépassements de délai pour les tâches longues](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**Pour prolonger le délai d’expiration le plus court pour l’administrateur**:

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** et développer **Cache de page complète**.

1. Dans le _Configuration rapide_ , développez **Configuration avancée**.

1. Définissez la variable **Délai du chemin d’accès administrateur** en secondes. Cette valeur ne peut pas dépasser 10 minutes (600 secondes).

1. Cliquez sur **Enregistrer la configuration** en haut de la page.

1. Après le rechargement de la page, sélectionnez **Chargement rapide de VCL** dans le _Configuration rapide_ .

Récupère rapidement le chemin d’accès d’administrateur pour générer le fichier VCL à partir de la fonction `app/etc/env.php` fichier de configuration.

## Configuration des options de purge

Fournit rapidement plusieurs types d’options de purge sur votre page Gestion du cache du Magento, y compris des options pour purger la catégorie de produits, les ressources de produits et le contenu. Lorsque cette option est activée, recherchez rapidement les événements qui purgent automatiquement ces caches. Si vous désactivez une option de purge, vous pouvez purger manuellement les caches Fastly après avoir terminé les mises à jour via la page Gestion du cache.

Les options de purge incluent :

- **Catégorie de purge**-Purge le contenu des catégories de produits (et non le contenu des produits) lorsque vous ajoutez et mettez à jour un seul produit. Vous pouvez conserver cette option désactivée et activer la purge du produit, qui purge les produits et les catégories de produits.
- **Purge du produit**-Purge tout le contenu des produits et catégories de produits lors de l’enregistrement d’une seule modification sur un produit. L’activation de la purge de produit peut s’avérer utile pour obtenir immédiatement des mises à jour des clients lors de la modification d’un prix, de l’ajout d’une option de produit et lorsque l’inventaire des produits est en rupture de stock.
- **Purge de la page CMS**-Purge le contenu des pages lors de la mise à jour et de l’ajout de pages au CMS Adobe Commerce. Par exemple, vous pouvez effectuer une purge lors de la mise à jour de vos conditions générales ou de votre stratégie de retour. Si vous apportez rarement ces modifications, vous pouvez désactiver la purge automatique.
- **Purge douce**-Définit le contenu modifié sur obsolète et le purge selon le calendrier obsolète. Outre les horodatages obsolètes, le contenu obsolète est présenté aux clients tout en le mettant à jour rapidement en arrière-plan.

![Configuration des options de purge](../../assets/cdn/fastly-purge-options.png)

**Pour configurer les options de purge rapide**:

1. Dans le _Configuration rapide_ , développez **Configuration avancée** pour afficher les options de purge.

1. Pour chaque option de purge, sélectionnez **Oui** pour activer la purge automatique, ou **Non** pour désactiver la purge automatique.

   Lorsque vous désactivez une option de purge, vous devez purger manuellement le cache de cette catégorie à partir de la variable _Gestion du cache_ page.

1. Cliquez sur **Enregistrer la configuration** en haut de la page.

1. Après le rechargement de la page, sélectionnez **Chargement rapide de VCL** dans le _Configuration rapide_ .

Pour plus d’informations, voir [les options de configuration rapides ;](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## Configuration de la gestion des géoadresses IP

Le module Fastly inclut la gestion de la géolocalisation pour rediriger automatiquement les visiteurs ou fournir une liste de magasins correspondant au code de pays obtenu. Si vous utilisez déjà une extension pour la gestion des adresses géoIP, vous devrez peut-être vérifier les fonctionnalités avec les options Fastly.

**Pour configurer la gestion des géoadresses IP**:

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** et développer **Cache de page complète**.

1. Dans le _Configuration rapide_ , développez **Configuration avancée**.

1. Faites défiler la page vers le bas et sélectionnez **Oui** to **Activer GeoIP**. D’autres options de configuration s’affichent.

1. Pour l’action GéoIP, sélectionnez si le visiteur est automatiquement redirigé avec **Rediriger** ou fourni une liste de magasins avec lesquels effectuer un choix **Boîte de dialogue**.

1. Pour **Mappage des pays**, sélectionnez **Ajouter** pour saisir un code de pays à deux lettres à mapper avec un magasin Adobe Commerce spécifique d’une liste.

   ![Ajout de cartes de pays géoIP](/help/assets/cdn/fastly-geo-code.png)

1. Cliquez sur **Enregistrer la configuration** en haut de la page.

1. Après le rechargement de la page, sélectionnez **Chargement rapide de VCL** dans le _Configuration rapide_ .

>[!NOTE]
>
>L’implémentation actuelle du module GéoIP Adobe Commerce Fastly ne prend pas en charge les redirections entre plusieurs sites web.

Fastly propose également une série de [fonctions VCL liées à la géolocalisation](https://developer.fastly.com/reference/vcl/variables/geolocation/) pour le codage de géolocalisation personnalisé.

## Activation des modules Edge Fastly

Fastly Edge Modules est un framework flexible qui permet de définir des composants d’interface utilisateur et du code VCL associé par le biais d’un modèle. Ces modules facilitent la personnalisation et l’extension de la configuration de service Fastly par le biais de l’interface utilisateur au lieu d’utiliser des fragments de code VCL personnalisés.

Les modules Edge vous permettent d’activer des fonctionnalités spécifiques telles que les en-têtes CORS, les réécritures de plan de site cloud et de configurer l’intégration entre votre boutique Adobe Commerce et d’autres systèmes de gestion de contenu ou back-end.

Pour accéder au menu des modules Edge afin d’afficher, de configurer et de gérer les modules disponibles, activez la fonction _Activation des modules Edge Fastly_ . Voir [Modules Edge Fastly](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) dans la documentation du module CDN Fastly.

## Configuration des back-ends et du blindage d’origine

Les paramètres principaux permettent d’affiner les performances pour accélérer les performances grâce au blindage et aux délais d’expiration d’origine. A _back end_ est un emplacement spécifique (IP ou domaine) avec des paramètres de protection de l’origine et de délai d’expiration configurés pour vérifier et fournir du contenu mis en cache.

_Protection d&#39;origine_ achemine toutes les requêtes de votre magasin vers un point de présence spécifique (POP). Lorsqu’une demande est reçue, le POP recherche le contenu mis en cache et le fournit. S’il n’est pas mis en cache, il continue sur le Protocole POP du Bouclier, puis sur le serveur d’origine qui met le contenu en cache. Les boucliers réduisent le trafic directement à l’origine.

Le code VCL par défaut, Fastly, spécifie les valeurs par défaut de protection et d’expiration d’origine pour votre Adobe Commerce sur les sites d’infrastructure cloud. Dans certains cas, vous devrez peut-être modifier les valeurs par défaut. Par exemple, si vous obtenez des erreurs de type Temps jusqu’au premier octet (TTF), vous devrez peut-être ajuster la variable _délai du premier octet_ .

>[!NOTE]
>
>Si votre site nécessite une intégration serveur principal, comme [Wordpress](fastly-vcl-wordpress.md), personnalisez votre configuration de service Fastly afin d’ajouter le serveur principal et de gérer les redirections de votre boutique Adobe Commerce vers Wordpress. Pour plus d’informations, voir [Modules Edge rapides - Autres intégrations CMS/backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) dans la documentation du module Fastly.

**Pour vérifier la configuration des paramètres du serveur principal**:

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** et développer **Cache de page complète**.

1. Développez l’objet **Configuration rapide** .

1. Développer **Paramètres du serveur principal** et sélectionnez l’engrenage pour vérifier le serveur principal par défaut. Une fenêtre modale s’ouvre. Elle affiche les paramètres actuels avec des options permettant de les modifier.

   ![Modification du serveur principal](../../assets/cdn/fastly-backend.png)

1. Sélectionnez la variable **Shield** emplacement (ou centre de données).

   La configuration Fastly par défaut de votre projet définit l’emplacement le plus proche de votre région de service Cloud. Si vous devez le modifier, sélectionnez un emplacement proche de l’emplacement par défaut.

1. Modifiez les valeurs de délai d’expiration (en microsecondes) pour la connexion à la protection, le temps entre les octets et le temps pour le premier octet. Nous vous recommandons de conserver les paramètres de délai d’expiration par défaut.

1. Si vous le souhaitez, sélectionnez **Activer le serveur principal et le bouclier après modification ou enregistrement**.

1. Cliquez sur **Télécharger** pour enregistrer vos modifications et les télécharger sur les serveurs Fastly.

1. Dans l’onglet Admin, sélectionnez **Enregistrer la configuration**.

Pour plus d’informations, voir [Guide des paramètres du serveur principal](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) dans la documentation du module Fastly.

## Authentification de base

L’authentification de base est une fonctionnalité permettant de protéger chaque page et ressource de votre site avec un nom d’utilisateur et un mot de passe. We **ne pas recommander** activation de l’authentification de base sur votre environnement de production. Vous pouvez le configurer sur l’évaluation pour protéger votre site pendant le processus de développement. Voir [Guide d’authentification de base](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) dans la documentation du module CDN Fastly.

Si vous ajoutez un accès utilisateur et activez l’authentification de base sur l’évaluation, vous pouvez toujours accéder à l’administrateur sans avoir besoin d’informations d’identification supplémentaires.

## Création de fragments de code VCL personnalisés

Prise en charge rapide d’une version personnalisée du langage de configuration de vernis (VCL) pour personnaliser la configuration de service Fastly. Par exemple, vous pouvez autoriser, bloquer ou rediriger l’accès d’utilisateurs ou d’adresses IP spécifiques à l’aide de blocs de code VCL avec des dictionnaires Edge et Access Control List (ACL).

Pour obtenir des instructions sur la création de fragments de code VCL personnalisés, de dictionnaires de périphérie et de listes ACL, voir [Fragments de code VCL personnalisés](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Avant d’ajouter du code VCL personnalisé, des dictionnaires de périphérie et des listes de contrôle d’accès à votre configuration de module Fastly, vérifiez que le service de mise en cache Fastly fonctionne avec la configuration par défaut. Voir [Configuration rapide](fastly-configuration.md).

## Gestion des domaines

Pour les projets Starter et Pro, vous pouvez utiliser la variable [!UICONTROL Domains] pour ajouter et gérer la configuration de domaine Fastly pour votre magasin.

- Pour les projets de démarrage, accédez à l’URL du projet sous [!UICONTROL Domains] dans le [!DNL Cloud Console] pour ajouter l’URL du projet.

- Pour les projets Pro, envoyez une [ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour ajouter le domaine à votre configuration de projet cloud. L’équipe d’assistance met également à jour la configuration du compte Adobe Commerce Fastly afin d’ajouter le domaine.

**Gestion rapide de la configuration des domaines à partir de l’administrateur**:

{{admin-login-step}}

1. Sélectionner **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** et développer **Cache de page complète**.

1. Dans l’administrateur _Configuration rapide_ , sélectionnez **Domaines**.

1. Cliquez sur **Gestion des domaines** pour ouvrir la page Domaines .

1. Ajoutez les noms de niveau supérieur et de sous-domaine pour les magasins de l’environnement cloud.

   Vous pouvez uniquement spécifier les domaines qui ont déjà été ajoutés à la configuration de votre infrastructure cloud.

   ![Ajout d’une configuration de domaine rapide pour le démarrage](../../assets/cdn/fastly-starter-activate-domain.png)

1. Cliquez sur **Activer** pour mettre à jour la configuration de domaine Fastly.

>[!NOTE]
>
>Si le même domaine a été configuré sur un autre compte Fastly, vous devez envoyer un ticket d’assistance Adobe Commerce pour demander la délégation de domaine avant de pouvoir ajouter le domaine à Adobe Commerce. Voir [Plusieurs comptes et domaines attribués à la date](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Activation du mode de maintenance

Utilisez la variable _Mode de maintenance_ pour autoriser l’accès administratif à votre site à partir d’adresses IP spécifiées tout en renvoyant une page d’erreur pour toutes les autres requêtes.

**Pour activer le mode Maintenance avec l’accès administratif**:

1. Ouvrez le _Configuration rapide_ dans la section Admin.

1. Dans le _ACL Edge_ , mettez à jour la section `maint_allow` liste de contrôle d’accès (ACL) avec les adresses IP administratives pouvant accéder à votre magasin lorsqu’il est en mode de maintenance.

   ![Mettre à jour la liste autorisée du mode de maintenance IP](../../assets/cdn/fastly-maint-allowlist.png)

1. Dans le _Mode de maintenance_ , sélectionnez **Activation du mode de maintenance**.

   Une fois le mode de maintenance activé, tout le trafic est bloqué, à l’exception des demandes provenant des adresses IP du `maint_allowlist` ACL. Vous pouvez mettre à jour la variable `maint_allowlist` pour modifier les adresses IP dans la liste de contrôle d’accès.

   Pour obtenir des instructions de configuration détaillées, voir [Guide du mode de maintenance](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) dans la documentation du module Fastly CDN pour Magento 2 .
