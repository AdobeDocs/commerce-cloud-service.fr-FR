---
title: Test d’évaluation et de production
description: Découvrez comment tester dans les environnements d’évaluation et de production.
exl-id: 5b762d59-04c5-4e89-a637-719141759158
source-git-commit: c6d4128792e688485e021bad75d9814a9f4d3b4f
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Test d’évaluation et de production

Après une migration réussie de votre code, fichiers et données vers l’environnement d’évaluation ou de production, utilisez les URL d’environnement pour tester vos sites et magasins. Vous trouverez ci-dessous des informations sur la vérification des journaux, le test de configurations rapides, le test d’acceptation utilisateur (UAT), etc.

{{second-staging}}

## Fichiers de log

Si vous rencontrez des erreurs lors du déploiement ou d’autres problèmes lors du test, vérifiez les fichiers journaux. Les fichiers journaux se trouvent sous le répertoire `var/log`.

Le journal de déploiement se trouve dans `/var/log/platform/<prodject-ID>/deploy.log`. La valeur de `<project-ID>` dépend de l’ID de projet et de si l’environnement est intermédiaire ou de production. Par exemple, avec un ID de projet de `yw1unoukjcawe`, l’utilisateur d’évaluation est `yw1unoukjcawe_stg` et l’utilisateur de production est `yw1unoukjcawe`.

Lors de l’accès aux journaux dans les environnements de production ou d’évaluation, utilisez SSH pour vous connecter à chacun des trois noeuds afin de localiser les journaux. Vous pouvez également utiliser la [gestion des journaux New Relic](../monitor/log-management.md) pour afficher et interroger les données de journaux agrégées de tous les noeuds. Voir [Afficher les journaux](log-locations.md#application-logs).

## Vérifier la base de code

Vérifiez que votre base de code est correctement déployée dans les environnements d’évaluation et de production. Les environnements doivent avoir des bases de code identiques.

## Vérification des paramètres de configuration

Vérifiez les paramètres de configuration dans le panneau Admin, y compris l’URL de base, l’URL d’administration de base, les paramètres multisite, etc. Si vous devez apporter d’autres modifications, effectuez les modifications dans votre branche Git locale et passez à la branche `master` dans Intégration, Évaluation et Production.

## Vérification de la mise en cache rapide

[ La configuration rapide ](../cdn/fastly-configuration.md) nécessite une attention particulière aux détails : l’utilisation de l’identifiant de service Fastly correct et des informations d’identification du jeton API Fastly, le téléchargement du code VCL Fastly, la mise à jour de la configuration DNS et l’application des certificats SSL/TLS à vos environnements. Après avoir effectué ces tâches de configuration, vous pouvez vérifier la mise en cache rapide dans les environnements d’évaluation et de production.

**Pour vérifier la configuration de service Fastly** :

1. Connectez-vous à l’administrateur pour l’évaluation et la production à l’aide de l’URL avec `/admin` ou de l’ [ URL d’administration mise à jour](../environment/variables-admin.md#admin-url).

1. Accédez à **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**. Faites défiler l’écran et cliquez sur **Full Page Cache**.

1. Assurez-vous que la valeur **Application de mise en cache** est définie sur _Fastly CDN_ .

1. Testez les informations d’identification Fastly.

   - Cliquez sur **Configuration Fastly**.

   - Vérifiez que les valeurs de l’identifiant de service Fastly et des informations d’identification du jeton API Fastly. Voir [Obtenir des informations d’identification rapides](/help/cloud-guide/cdn/fastly-configuration.md#get-fastly-credentials).

   - Cliquez sur **Tester les informations d’identification**.

   >[!WARNING]
   >
   >Assurez-vous d’avoir saisi l’ID de service et le jeton d’API corrects dans les environnements d’évaluation et de production. Les informations d’identification les plus rapides sont créées et mappées par environnement de service. Si vous saisissez des informations d’identification d’évaluation dans votre environnement de production, vous ne pouvez pas charger vos fragments de code VCL, la mise en cache ne fonctionne pas correctement et votre configuration de mise en cache pointe vers le serveur et les magasins incorrects.

**Pour vérifier rapidement le comportement de mise en cache** :

1. Recherchez des en-têtes utilisant l’utilitaire de ligne de commande `dig` pour obtenir des informations sur la configuration du site.

   Vous pouvez utiliser n’importe quelle URL avec la commande `dig`. Les exemples suivants utilisent des URL Pro :

   - Évaluation : `dig https://mcstaging.<your-domain>.com`
   - Production : `dig https://mcprod.<your-domain>.com`

   Pour des tests `dig` supplémentaires, voir [Tests avant de modifier le DNS](https://docs.fastly.com/en/guides/working-with-domains).

1. Utilisez `cURL` pour vérifier les informations de l’en-tête de la réponse.

   ```bash
   curl https://mcstaging.<your-domain>.com -H "host: mcstaging.<your-domain.com>" -k -vo /dev/null -H Fastly-Debug:1
   ```

   Voir [Vérifier les en-têtes de réponse](../cdn/fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) pour plus d’informations sur la vérification des en-têtes.

1. Une fois que vous êtes actif, utilisez `cURL` pour vérifier votre site actif.

   ```bash
   curl https://<your-domain> -k -vo /dev/null -H Fastly-Debug:1
   ```

## Terminer le test UAT

Test complet de l’acceptation utilisateur (UAT) lors de l’évaluation et de la production. Les tests suivants répertorient rapidement les tâches et les domaines possibles à tester en tant que commerçant et client. Votre liste peut être plus longue et inclure des tests supplémentaires pour les modules personnalisés, les extensions et les intégrations tierces. Lors du test, utilisez des ordinateurs de bureau, des ordinateurs portables et des appareils mobiles.

Si vous rencontrez des problèmes, enregistrez les étapes de reproduction, les messages d’erreur, les captures d’écran étranges et les liens. Utilisez ces informations pour enquêter et résoudre les problèmes dans le code de l’environnement d’intégration, les configurations ou les paramètres d’environnement.

<table>
<tr>
<td style="width:150px">Gestion des utilisateurs</td>
<td>
<ul>
<li>Créer et modifier des comptes clients, vérifier des emails</li>
<li>Création de rôles d’administrateur pour les marchands</li>
<li>Création de comptes de commerce avec des rôles spécifiques</li>
<li>Test de l’accès au compte commercial par rôle</li>
</ul>
</td>
</tr>
<tr>
<td>Catalogues et produits</td>
<td>
<ul>
<li>Création d’un catalogue avec les produits associés</li>
<li>Créez des produits pour votre vitrine, y compris tous les types de produits : simples, configurables, regroupés.</li>
<li>Ajout d’images de produit, d’échantillons, de vidéos et d’autres options multimédias</li>
<li>Configurer les prix, les remises et les règles de prix </li>
<li>Configurer des fonctionnalités avancées, notamment des plages de prix, des produits proposés et des dates de disponibilité</li>
<li>Modifier l’inventaire et vérifier que les valeurs correctes s’affichent et changent par augmentation et par achat terminé</li>
</ul>
</td>
</tr>
<tr>
<td>Paniers et passages en caisse</td>
<td>
<ul>
<li>Rechercher des produits et sélectionner des options de filtrage</li>
<li>Ajout de produits au panier à partir des résultats de recherche, des pages de catégories et des pages de produits</li>
<li>Test de tous les types de produits</li>
<li>Afficher le panier et modifier le contenu en supprimant ou en modifiant les montants </li>
<li>Passage en caisse pour vérifier les montants de la commande par rapport au panier et aux informations sur le produit</li>
<li>Vérifier que la taxe calcule correctement pour le panier</li>
<li>Effectuez un achat avec différentes options : ajoutez un coupon, sélectionnez l’expédition, saisissez les informations d’expédition et de facturation, ainsi que les informations de paiement.</li>
<li>Vérifier les passerelles et options de paiement lors du passage en caisse</li>
<li>Rechercher des notifications à l’écran, des commandes répertoriées dans le compte client et des notifications par e-mail</li>
<li>Test de l’extraction des invités et des clients</li>
</ul>
</td>
</tr>
<tr>
<td>Order Management</td>
<td>
<ul>
<li>Création d’une commande pour un client</li>
<li>Recherche et affichage des commandes</li>
<li>Modifier une commande en ajoutant et en supprimant des produits, en modifiant les montants, en modifiant les informations d’expédition et de facturation</li>
<li>Gérer un remboursement</li>
<li>Annuler une commande</li>
<li>Appliquer les codes coupon et les remises</li>
</ul>
</td>
</tr>
<tr>
<td>Contenu du site</td>
<td>
<ul>
<li>Vérifier correctement le chargement de tous les thèmes et ressources</li>
<li>Vérifier que CSS s’affiche correctement, y compris les tailles de médias réactifs</li>
<li>Vérifier les conditions générales, la politique de remboursement et d’autres informations de politique</li>
<li>Vérifiez les coordonnées, les liens et plus sur votre société.</li>
<li>Rechercher des produits et du contenu, vérifier le filtrage des résultats</li>
<li>Vérification du bloc de pied de page et des blocs de navigation supérieurs</li>
<li>Test des pages 404 et Maintenance</li>
</ul>
</td>
</tr>
<tr>
<td>Extensions</td>
<td>
<ul>
<li>Vérifiez tous les paramètres d’extension, en particulier pour tous les modules de taxes, d’expédition et de paiement (exemple : commande envoyée à l’entrepôt et au système de gestion financière).</li>
<li>Test de toutes les interactions de module personnalisé et d’extension installée</li>
<li>Vérifier les données de toute interaction qui doit se terminer (paiements, commandes, notifications électroniques)</li>
<li>Vérifier les configurations par environnement pour vos extensions</li>
<li>Vérifier le fonctionnement des dépendances entre les modules et les extensions</li>
<li>Vérifier toutes les actions en tant que commerçant et client</li>
</ul>
</td>
</tr>
<tr>
<td>Intégrations tierces</td>
<td>
<ul>
<li>Vérifiez que les données sont correctement enregistrées dans Adobe Commerce et exportent, envoient ou sont accessibles par le service tiers (exemple : les commandes s’affichent dans le système de gestion des commandes tiers).</li>
<li>Vérification des configurations et interactions par intégration</li>
<li>Effectuez des tests en boucle à partir d’Adobe Commerce et de votre service tiers.</li>
<li>Vérification de la fin de l’authentification</li>
<li>Recherchez les problèmes consignés pour mettre à jour les intégrations de code ou les messages d’erreur dans les panneaux de contrôle.</li>
</ul>
</td>
</tr>
<tr>
<td>Test principal</td>
<td>
<ul>
<li>Test et effacement du cache </li>
<li>Réindexation et vérification des résultats</li>
<li>Vérifier les tâches cron, rechercher les erreurs cron_schedule</li>
<li>Vérifier et vérifier les éventuels problèmes de script shell</li>
<li>Recherchez les problèmes consignés : journaux d’application, journaux PHP, journaux MySQL, journaux d’email.</li>
</ul>
</td>
</tr>
</table>

## Test de charge et de stress

Avant le lancement, il est préférable d’effectuer des tests de trafic et de performances étendus sur vos environnements d’évaluation et de production. Pensez aux tests de performance pour vos processus front-end et back-end.

Avant de commencer le test, saisissez un ticket avec support pour informer les environnements que vous testez, les outils que vous utilisez et la période. Mettez à jour le ticket avec les résultats et les informations pour suivre les performances. Une fois le test terminé, ajoutez les résultats mis à jour et notez que le test du ticket est terminé avec une date et un horodatage.

Passez en revue les options [Performance Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) dans le cadre de votre processus de préparation avant le lancement.

Pour de meilleurs résultats, utilisez les outils suivants :

- [Test de performance de l’application](../environment/variables-post-deploy.md#ttfb_tested_pages) : testez les performances de l’application en configurant la variable d’environnement `TTFB_TESTED_PAGES` pour tester le temps de réponse du site.
- [Siège](https://www.joedog.org/siege-home/) : logiciel de modélisation et de test du trafic pour pousser votre boutique jusqu’à la limite. Accédez à votre site avec un nombre configurable de clients simulés. Le siège prend en charge l’authentification de base, les cookies, les protocoles HTTP, HTTPS et FTP.
- [Jmètre](https://jmeter.apache.org) : excellent test de charge pour permettre d’évaluer les performances du trafic en pointe, comme pour les ventes Flash. Créez des tests personnalisés à exécuter sur votre site.
- [New Relic](../monitor/new-relic-service.md) (fourni) : aide à localiser les processus et les zones du site, ce qui entraîne des performances ralenties avec le temps passé par action suivi, comme la transmission de données, de requêtes, de Redis, etc.
- [WebPageTest](https://www.webpagetest.org) et [Pingdom](https://www.pingdom.com) : analyse en temps réel du temps de chargement des pages de votre site avec différents emplacements d’origine. Le royaume peut avoir besoin d&#39;un tribut. WebPageTest est un outil gratuit.

## Tests fonctionnels

Vous pouvez utiliser le MFTF (Magento Funcational Testing Framework) pour terminer les tests fonctionnels pour Adobe Commerce à partir de l’environnement Cloud Docker. Voir [Test d’application](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) dans le _guide Cloud Docker for Commerce_.

## Configuration de l’outil d’analyse de sécurité

Il existe un outil d’analyse de sécurité gratuit pour vos sites. Pour ajouter vos sites et exécuter l’outil, voir [Outil d’analyse de sécurité](../launch/overview.md#set-up-the-security-scan-tool).
