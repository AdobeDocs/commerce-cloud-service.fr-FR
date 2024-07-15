---
title: Correctifs cloud pour Commerce
description: Consultez la liste des dernières améliorations apportées au module Correctifs Cloud .
recommendations: noDisplay, catalog
last-substantial-update: 2024-05-21T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 61c42a1bd1d5a28f90b8756032ee6f45be4565b2
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 0%

---

# Correctifs cloud pour Commerce

Le package [ Correctifs de cloud ](https://github.com/magento/magento-cloud-patches) fournit un ensemble de correctifs requis qui améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud et prend en charge la livraison rapide de correctifs critiques.

Le package Cloud Patches for Commerce est une dépendance du package CEE-Outils. Il est installé et mis à jour lorsque vous installez ou mettez à jour le package CEE-Outils. Vous pouvez également utiliser et gérer des correctifs Cloud pour Commerce sous la forme d’un module autonome afin d’appliquer des correctifs à un projet Adobe Commerce qui ne se trouve pas sur la plateforme Cloud. Ces notes de mise à jour décrivent les dernières améliorations apportées à ce module.

>[!TIP]
>
>Pour vous assurer que votre projet comporte tous les correctifs requis, mettez à jour vers la [dernière version de ece-tools](../dev-tools/update-package.md).

>[!NOTE]
>
>Voir [Application de correctifs](../development/apply-patches.md) pour obtenir des instructions sur l’application de correctifs à vos projets.

Le package `magento/magento-cloud-patches` utilise la séquence de version suivante : `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.27 {#latest}

Date de publication : 21 mai 2024

- **Prise en charge de PHP 8.3** : ce correctif résout les erreurs de compatibilité entre php 8.3 et la version du package de compositeur.

## v1.0.26

Date de publication : 8 avril 2024

- ![nouvelle icône](../../assets/new.svg) **PHP** — Prise en charge de PHP 8.3.

## v1.0.25

Date de publication : 16 janvier 2024

- **Améliorations du cache** - Ce correctif améliore l’efficacité du cache de mise en page, réduisant considérablement l’utilisation de la mémoire, pour Adobe Commerce versions 2.4.4 et ultérieures.<!-- MCLOUD-11514 -->
- **Améliorations des tâches CRON** - Ce correctif corrige le problème en raison duquel les tâches manquées attendent inutilement des verrous de tâche cron pour Adobe Commerce versions 2.4.4 et ultérieures.<!-- MCLOUD-11329 -->

## v1.0.24

Date de publication : 15 septembre 2023

- **Amélioration des performances** - Ce correctif corrige un problème affectant les performances en réduisant le nombre de fois que les mêmes configurations de déploiement sont chargées pour Adobe Commerce 2.4.6 à 2.4.6-p1<!-- MCLOUD-10604 -->.

## v1.0.23

Date de publication : 31 juillet 2023

- **Suppression du correctif MCLOUD-10604** - Ce correctif a été déplacé vers QPT.<!-- MCLOUD-10736 -->

## v1.0.22

Date de publication : 19 juin 2023

- **Assistant/sortie d’interface de ligne de commande améliorée QPT** : ajout d’un avertissement à l’assistant/la sortie d’interface de ligne de commande QPT qui vous rappelle de vérifier les détails et les exigences du correctif s’il existe des dépendances.<!-- ACP2E-1963 -->
- **Correctifs ajoutés pour Commerce 2.4.6 :**
   - Correction de la validation `regexp cache tag`.<!-- MCLOUD-10226 -->
   - Amélioration des performances en réduisant le nombre de chargements des mêmes configurations de déploiement.<!-- MCLOUD-10604 -->
- **Ajout de correctifs pour Commerce 2.3.7 à 2.4.6** : correction d’un problème qui provoquait un incrément par une valeur aléatoire au lieu d’un incrément par 1 pour les tables `catalog_product_entity_*`.<!-- MCLOUD-10032 -->
- **Ajout de correctifs pour Commerce 2.4.0 à 2.4.6** : correction d’une erreur stipulant que `The file can't be deleted. Warning!unlink: No such file or directory`, qui se produisait lors du vidage du cache JS/CSS de l’administrateur.<!-- MCLOUD-10279 -->

## v1.0.21

Date de publication : 10 mars 2023

- **Amélioration de la prise en charge de PHP 8.2** : correction de problèmes de compatibilité avec certaines versions de PHP 8.2.x afin de prendre en charge Commerce 2.4.6.

## v1.0.20

Date de publication : 27 octobre 2022

- **Ajout de l’amélioration du cache L2 correctif** : ce correctif corrige un problème de vidage du cache L2 local pour Commerce versions 2.4.0 et 2.4.1.<!-- MCLOUD-7845 -->

## v1.0.19

Date de publication : 13 septembre 2022

- **Prise en charge améliorée de PHP 8.1** : correction de problèmes de compatibilité avec certaines versions de PHP 8.1.x.

## v1.0.18

Date de publication : 11 août 2022

Correctif critique pour Adobe Commerce 2.4.5 :

- **Problème lié aux commandes utilisant des paiements de Braintree** : ce correctif résout un problème critique empêchant les administrateurs de passer de nouvelles commandes ou de nouvelles commandes.<!-- MCLOUD-9137 -->

Voir [L’administrateur ne peut pas créer de commande/réorganisation lorsque le paiement du Braintree est activé](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Date de publication : 24 mai 2022

Correction des contraintes relatives aux correctifs de sécurité dans le fichier `patches.json`.

## v1.0.16

Date de publication : 31 mars 2022

Correctif critique pour Adobe Commerce 2.3.3-p1 et versions ultérieures :

Mise à jour de correctifs pour résoudre une vulnérabilité **critique** résultant en une exécution de code distant non authentifiée.<!-- MCLOUD-8479 -->

Voir [Bulletin de sécurité Adobe APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Date de publication : 10 mars 2022

- **Prise en charge de PHP 8.1** : ajout de la prise en charge de PHP 8.1 et abandon de la prise en charge de PHP 7.0 et 7.1.
- **Ajout d’un correctif pour Adobe Commerce 2.3.3** : correction de l’affichage de la devise sur la page du produit.

## v1.0.14

Date de publication : 13 février 2022

Correctif critique pour Adobe Commerce 2.3.3-p1 et versions ultérieures :

Ajout d&#39;un correctif pour résoudre une vulnérabilité **critical** résultant en une exécution de code distant non authentifiée.<!-- MCLOUD-8461 -->

Voir [Bulletin de sécurité Adobe APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Date de publication : 25 octobre 2021

- **Mettre à jour Monolog** : mise à jour de la version minimale requise pour le package `monolog` vers `^2.3`.<!-- ACMP-1263 -->
- **Méthode PHP incompatible** : correction d’une méthode PHP incompatible pour les versions 2.4.3 et 2.3.7-p1 d’Adobe Commerce.<!-- AC-384 -->
- **Erreur PHP** : correction d’une erreur `PHP error 'Undefined variable: errorMessage' ...` qui se produisait lors de la tentative d’application d’un correctif.<!-- ACP2E-138 -->

## v1.0.12

Date de publication : 12 août 2021

Correctif critique pour Adobe Commerce 2.4.3 et 2.3.7-p1 :

- **Problème lié à la limitation du débit de l’API** : ce correctif corrige une limite de débit par défaut qui empêchait les API Web de traiter les demandes comportant plus de 20 éléments dans un tableau. Ce correctif augmente la valeur par défaut de la limite de taux. Voir les [ notes de mise à jour 2.4.3 d’Adobe Commerce ](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) et les [ notes de mise à jour 2.3.7](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Date de publication : 29 juillet 2021

- **Correction d’un problème provoqué par l’application du correctif de navigation à couche B2B**. Pour les clients qui ont appliqué le correctif de navigation à couche B2B, ce correctif résout une erreur `Undefined offset` qui s’affiche sur la page de recherche après le changement de vue de magasin.<!--MCLOUD-5287-->

- **Correctif Paypal Checkout** : corrige un problème Adobe Commerce 2.3.7 avec PayPal Express où le prix de commande précédemment placé s’affiche.<!--MC-42674-->

- **Prise en charge de la catégorie de correctifs** : ajout de la prise en charge des catégories de correctifs de traitement et des sources d’origine affectées aux correctifs de qualité. Les catégories permettent aux clients d’utiliser des filtres et un tri pour trouver plus rapidement les correctifs lors de l’utilisation de l’[ outil de correctifs de qualité](https://github.com/magento/quality-patches) et de l’outil d’analyse à l’échelle du site (SWAT). <!--MC-38577-->

## v1.0.10

Date de publication : 10 mai 2021

- **Compatibilité avec Adobe Commerce 2.3.7** : résolution d’un conflit de dépendances de compositeur pour l’installation sur Adobe Commerce 2.3.7.<!--MC-42131-->
- **Correction d’un problème en raison duquel un correctif groupé était appliqué plusieurs fois**. L’application d’un correctif groupé (un qui inclut d’autres correctifs obsolètes) pouvait rétablir les packages obsolètes inclus. Tous les correctifs sont désormais appliqués une seule fois. Tenter d&#39;appliquer à nouveau le même package affiche un message indiquant que le correctif a déjà été appliqué.<!--MC-41912-->
- **Correctif de navigation en couches B2B** : correction d’un autre problème qui empêchait la navigation en couches d’afficher toutes les options de produit lorsque l’utilisateur activait le catalogue partagé B2B.<!--MCLOUD-7742-->

## v1.0.9

Date de publication : 1 février 2021

- **Correctif de navigation en couches B2B** : correction du problème qui empêchait la navigation en couches d’afficher toutes les options de produit lorsque le catalogue partagé B2B était activé.<!--MCLOUD-6923-->
- **Compatibilité avec PHP 7.4** : correction d’un problème de compatibilité des correctifs cloud avec PHP 7.4.<!--MCLOUD-7367-->
- **Les correctifs obsolètes deviennent visibles** : correction d’un problème lié aux correctifs de cloud, en raison duquel les correctifs obsolètes apparaissent dans la table des correctifs après l’application d’un correctif de remplacement contenant l’intégralité du contenu du correctif obsolète. Cela peut se produire si vous appliquez un correctif qui combine plusieurs autres correctifs.<!--MC-40626-->
- **Échec silencieux lors de l’application de correctifs** : correction d’un problème de correctifs cloud dans lequel la commande `git apply` ne parvenait pas à appliquer des correctifs dans certains environnements.<!--MC-40529-->

## v1.0.8

Date de publication : 14 octobre 2020

- **Mises à jour de compatibilité pour les correctifs Magento/magento-cloud** : mise à jour des contraintes de version `symfony` et `semver` dans le fichier `composer.json` à des fins de compatibilité avec Adobe Commerce 2.4.1 et les versions ultérieures.<!--MCLOUD-7111-->

## v1.0.7

Date de publication : 14 octobre 2020

- **Redis les correctifs pour Adobe Commerce 2.3.0 à 2.3.5, 2.4.0** : mise à jour des correctifs Redis pour prendre en charge l’ajout de produits à une catégorie lors de l’implémentation d’un cache de niveau 2. <!--MCLOUD-6659-->

- **Correctif VBE Braintree** : corrige un problème qui générait une erreur lorsqu’un administrateur tentait d’afficher un rapport de règlement Braintree. <!--MCLOUD-6684-->

- Désormais, la commande `ece-patches apply` utilise la commande Unix `patch` pour appliquer des correctifs si Git n’est pas disponible sur le système hôte. <!--MCLOUD-7069-->

## v1.0.6

Date de publication :

- **Redis les correctifs pour Adobe Commerce 2.3.0 - 2.3.4** : optimisez la communication et améliorez les performances.
   - Réduction de la taille des transferts réseau entre Redis et Adobe Commerce
   - Correction des conditions de concurrence sur les opérations de chargement et d’écriture Redis
   - Réécrire l’adaptateur de cache de base pour gérer les erreurs lors de l’enregistrement
   - Réduire la consommation du processeur Redis<!--MCLOUD-6139-->

- **Redis les correctifs pour Adobe Commerce 2.3.0 - 2.3.5** : amélioration des performances et correction des erreurs
   - Correction de l’implémentation du verrouillage du cache pour empêcher les verrous infinis
   - Amélioration du mécanisme de verrouillage actuel
   - Implémentation de verrous signés pour empêcher le déverrouillage à partir de requêtes parallèles
   - Corrigez l’erreur suivante qui se produit lors de l’opération d’écriture Redis : `OOM command not allowed when used memory > maxmemory`
   - Correction du traitement du cache propre par la balise `cat_p` qui s’exécute lors des mises à jour du produit<!--MCLOUD-6110-->

- Correction d’un problème qui provoquait une erreur lors de l’application du correctif `amzn/amazon-pay-module` requis à Adobe Commerce sur les projets d’infrastructure cloud avec Adobe Commerce v2.2.6 ou 2.3.5, qui n’incluent pas ce module. Désormais, le processus de correction ignore le correctif `amzn/amazon-pay-module` si le module n&#39;est pas installé.<!--MCLOUD-6588-->

## v1.0.5

Date de publication : 26 juin 2020

- **Améliorations des performances Redis** : ajoute des fonctionnalités d’optimisation Redis aux versions 2.3.3 et 2.3.4 d’Adobe Commerce. Ces correctifs ont été inclus dans la version 2.3.5 d’Adobe Commerce. Voir [Améliorations des performances](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) dans les _notes de mise à jour d’Adobe Commerce 2.3.5_.<!--MCLOUD-5771-->

- **New Relic Log Enricher** : ajoute l’interface de processeur Monolog requise pour prendre en charge les améliorations des fonctionnalités de journalisation New Relic introduites dans les composants Cloud de Commerce version 1.0.4. Ce correctif est nécessaire pour déployer Adobe Commerce 2.1.x. Si le correctif n&#39;est pas appliqué, la version échoue pendant le processus `di:compile`.<!--MCLOUD-6029-->

## v1.0.4

Date de publication : 12 mai 2020

- **Passage en caisse Amazon** : résolution d’un problème lié au widget de paiement payant Amazon qui empêchait les clients de modifier le mode de paiement à l’étape _Révision et paiements_ pendant le processus de paiement.<!--MCLOUD-5930-->

- **Affichage des produits sur la page Catégorie** : corrige un problème qui empêchait l’affichage des produits sur la page de catégorie dans la vue _Afficher toutes les pages_.<!--MCLOUD-5684-->

- **Téléchargement d’image du générateur de pages** : résolution d’un problème d’interface du créateur de pages qui provoquait parfois l’erreur suivante lors du téléchargement d’images vers la galerie d’images : `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Supprimer les avertissements de génération de plan de site inutiles** : ajoute une tentative de reprise lorsque des erreurs se produisent lors de la génération du plan de site et ignore la notification par e-mail du client dans les cas où les erreurs peuvent être récupérées automatiquement.<!--MCLOUD-3025-->

- **Amélioration des performances du site** : résolution d’un problème de performances avec la fonction `Magento\Framework\App\DeploymentConfig\Reader::load`, qui a connu périodiquement de longs temps de chargement qui ont affecté les performances du site. <!--MCLOUD-5650-->

- Mise à jour de l’affectation des correctifs pour les correctifs de méthode de paiement afin de cibler les modules de paiement au lieu du package de base du Magento (magento/magento2-base), de sorte que les correctifs de paiement ne soient appliqués que si les modules de paiement existent.<!--MCLOUD-5666-->

- Mise à jour des correctifs pour la compatibilité avec Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Date de publication : 28 avril 2020

- Ajout d’un correctif pour le correctif &quot;FPC est désactivé pendant les déploiements&quot; afin de prendre en charge Adobe Commerce 2.3.5.

## v1.0.2

Date de publication : 27 février 2020

Cette version comprend les correctifs et correctifs critiques suivants :

- **Mises à jour de compatibilité pour magento/magento-cloud-patches**

   - Mise à jour des contraintes de version `symfony` et `semver` dans le fichier `composer.json` pour assurer la compatibilité avec Adobe Commerce 2.4 et les versions ultérieures.<!--MAGECLOUD-5127-->

   - Mise à jour des contraintes dans `composer.json` pour la compatibilité avec les versions `ece-tools` 2002.0.22 et ultérieures 2002.0.x.

- **PayPal Express Checkout** : publié le 12 février 2020, ce correctif résout un problème qui affecte les commandes passées avec PayPal Express Checkout où l’adresse d’expédition de la commande spécifie une région de pays qui a été saisie manuellement dans le champ de texte plutôt que sélectionnée dans le menu déroulant de la page Expédition. Consultez la description complète du correctif sur la page de téléchargement des correctifs.

- **Correctif de déploiement d’application** : ajout d’un correctif pour résoudre un problème qui désactivait le cache de page entière pendant le processus de déploiement. Ce correctif s’applique à Adobe Commerce 2.3.2 et versions ultérieures.

- **Paramètre d’étendue pour l’API asynchrone/en bloc** : mise à jour de ce correctif pour corriger une erreur de syntaxe dans le fichier `composer.json`. Ce correctif s’applique à Magento Open Source 2.3.1 et 2.3.2. Consultez la description complète du correctif sur la page de téléchargement des correctifs.

## v1.0.1

Date de publication : 6 février 2020

Nous avons inclus tous les correctifs Magento Open Source 2.x de la page de téléchargement des logiciels dans la version magento/magento-cloud-Correctifs v1.0.1. Si vous avez copié des correctifs dans votre projet précédemment, supprimez-les pour éviter les conflits.

Cette version comprend les correctifs et correctifs critiques suivants :

- **Correction des blocages cron et amélioration du verrouillage cron**—

   - Correction d’un problème en raison duquel certaines tâches cron ne s’exécutaient pas en raison d’une valeur d’état incorrecte dans la table `cron_schedule`. Désormais, nous utilisons la structure de verrouillage Adobe Commerce pour vérifier et mettre à jour l’état de la tâche cron au lieu d’utiliser la table `cron_schedule`. Les tâches Cron qui se sont terminées avec un état d’erreur sont reprises lors de la prochaine exécution cron au lieu d’attendre 24 heures.

   - Ajoute une opération _retry_ pour éviter un blocage lors des mises à jour des données de la table `cron_schedule`.

- **Mise à jour de `magento/magento-cloud-patches` afin d’inclure tous les correctifs disponibles pour Magento Open Source 2.x**. Mise à jour du package magento/magento-cloud-Correctifs pour inclure tous les correctifs Magento Open Source 2.x disponibles sur la page de téléchargement des logiciels. Si vous avez copié des correctifs Magento Open Sources dans votre projet d’infrastructure cloud Adobe Commerce précédemment, supprimez-les pour éviter les conflits.<!--MAGECLOUD-4606-->

- **Correctif de pagination de catalogue Elasticsearch** : remplacement du correctif de pagination de catalogue Elasticsearch fourni dans Magento/magento-cloud-Correctifs v1.0 par un correctif plus efficace.<!--MAGECLOUD-4847-->

- **Correctifs de Page Builder** : dans les correctifs cloud pour Commerce 1.0.0, nous avons regroupé les correctifs de Page Builder pour répondre à une vulnérabilité d’exécution de code à distance de Page Builder (RCE) connue, avec le correctif initial basé sur Adobe Commerce 2.3.3. Nous avons mis à jour ces correctifs avec une mise en oeuvre plus stable basée sur Adobe Commerce 2.3.4, qui inclut plusieurs optimisations pour résoudre le problème.<!--MAGECLOUD-4884-->

  Si vous disposez du package magento/magento-cloud-Correctifs 1.0.0, vous êtes toujours protégé des problèmes de vulnérabilité du RCE de Page Builder. Si vous effectuez une mise à jour vers la version 1.0.1 ou ultérieure, vous disposez d’une meilleure mise en oeuvre du même correctif.

## v1.0.0

Date de publication : 14 novembre 2019

Il s’agit de la première version du package [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches), qui est une nouvelle dépendance pour la version 2002.0.22 du package `ece-tools` ou version ultérieure.

Cette version comprend les correctifs et correctifs critiques suivants :

- **Correctifs de sécurité de Page Builder pour les versions 2.3.1.x et 2.3.2.x** : corrige un problème dans l’aperçu de Page Builder qui permet aux utilisateurs non authentifiés d’accéder à certaines méthodes de modèle qui peuvent être utilisées pour déclencher l’exécution arbitraire du code sur le réseau (RCE), ce qui entraîne des fuites d’informations globales. Ce problème peut se produire lors de l’utilisation de versions de Page Builder non prises en charge avec Adobe Commerce versions 2.3.1 et 2.3.2.<!--MAGECLOUD-4649-->

- **Correctifs MSI** : corrige les problèmes qui provoquaient des erreurs d’indexation et des problèmes de performances lors de l’utilisation des paramètres de stock par défaut pour la gestion du stock.<!--MAGECLOUD-4428-->

- **Compatibilité descendante des nouvelles interfaces de messagerie** - Correction d’un problème d’incompatibilité ascendante provoqué par l’interface PHP `Magento\Framework\Mail\EmailMessageInterface` introduite dans Adobe Commerce v2.3.3. Dans la portée de ce correctif, le nouvel `EmailMessageInterface` hérite de l’ancien `MessageInterface` et les modules principaux Adobe Commerce sont restaurés pour dépendre de `MessageInterface`.<!--MAGECLOUD-4422-->

- **La pagination du catalogue ne fonctionne pas sur Elasticsearch 6.x** : corrige un problème critique lié à la pagination des résultats de recherche qui affecte les clients utilisant Elasticsearch 6.x comme moteur de recherche de catalogue.<!--MAGECLOUD-4448-->
