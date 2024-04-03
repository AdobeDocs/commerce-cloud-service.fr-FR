---
title: Dépannage rapide
description: Découvrez comment résoudre les problèmes et gérer les services et le module CDN Fastly pour Adobe Commerce.
feature: Cloud, Configuration, Cache, Services
exl-id: e4c47035-cbad-4838-8d44-fa5eaaac42d1
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Dépannage rapide

Utilisez les informations suivantes pour résoudre et gérer le module CDN Fastly pour Magento 2 dans vos environnements de projet d’infrastructure cloud Adobe Commerce. Vous pouvez, par exemple, examiner les valeurs de l’en-tête de réponse et le comportement de mise en cache pour résoudre les problèmes de service et de performances rapides.

Dans les environnements de production et d’évaluation, vous pouvez utiliser des [Journaux New Relic](../monitor/log-management.md) pour afficher et analyser rapidement les données du journal CDN et WAF afin de résoudre les erreurs et les problèmes de performances.

>[!NOTE]
>
>Pour plus d’informations sur la configuration et la configuration rapides, voir [Configuration rapide](fastly.md).

## Localisation de l’ID de service Fastly

Vous avez besoin de l’identifiant de service Fastly pour effectuer une configuration Fastly à partir de l’administrateur ou pour envoyer des demandes d’API Fastly pour une configuration et un dépannage rapides avancés.

Si l’option Fastly est activée dans votre environnement de projet, vous pouvez obtenir l’ID de service auprès de l’administrateur. Voir [Obtention des informations d’identification rapides](fastly-configuration.md#get-fastly-credentials).

Les développeurs et les utilisateurs avancés de VCL peuvent utiliser un VCL personnalisé pour récupérer l’ID de service à l’aide de la variable Fastly . `req.service_id`. Par exemple, vous pouvez ajouter la variable `req.service_id` à la directive de journalisation personnalisée dans votre VCL pour capturer la valeur de l’ID de service :

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

Vous pouvez utiliser le même VCL pour les environnements de production et d’évaluation. Voir [Comment configurer vcl_log](https://support.fastly.com/hc/en-us/community/posts/360040447172-How-to-configure-vcl-log).

## Problèmes de performances, de purge et de cache du site

Utilisez la liste suivante pour identifier et résoudre les problèmes liés à la configuration de service Fastly pour votre environnement d’infrastructure cloud Adobe Commerce.

- **Le menu Boutique ne s’affiche ni ne fonctionne**: vous pouvez utiliser un lien ou un lien temporaire directement vers le serveur d’origine au lieu d’utiliser l’URL du site actif, ou vous avez utilisé `-H "host:URL"` dans [cURL, commande](#check-live-site-through-fastly). Si vous ignorez Fastly le serveur d’origine, le menu principal ne fonctionne pas et des en-têtes incorrects s’affichent qui permettent la mise en cache côté navigateur.

- **La navigation supérieure ne fonctionne pas**: la navigation supérieure repose sur le traitement ESI (Edge Side Includes), qui est activé lorsque vous chargez les fragments de code VCL fastly par défaut du Magento. Si la navigation ne fonctionne pas, [Téléchargement du fichier VCL Fastly](fastly-configuration.md#upload-vcl-to-fastly) et vérifiez à nouveau le site.

- **La géolocalisation/la géolocalisation ne fonctionne pas**— Les fragments de code VCL Fastly par défaut du Magento ajoutent le code pays à l’URL. Si le code pays ne fonctionne pas, [Téléchargement du fichier VCL Fastly](fastly-configuration.md#upload-vcl-to-fastly) et vérifiez à nouveau le site.

- **Les pages ne sont pas mises en cache**: par défaut, Fastly ne met pas en cache les pages avec l’événement `Set-Cookies` en-tête . Adobe Commerce définit les cookies même sur les pages pouvant être mises en cache (TTL > 0). Le Magento par défaut, Fastly VCL, supprime ces cookies sur les pages pouvant être mises en cache. Si les pages ne sont pas mises en cache, [Téléchargement du fichier VCL Fastly](fastly-configuration.md#upload-vcl-to-fastly) et vérifiez à nouveau le site.

  Ce problème peut également se produire si un bloc de page d’un modèle est marqué comme impossible à mettre en cache. Dans ce cas, le problème est probablement causé par un module tiers ou une extension bloquant ou supprimant les en-têtes Adobe Commerce. Pour résoudre le problème, voir [X-Cache contient uniquement MISS, aucun accès](#x-cache-contains-only-miss-no-hit).

- **Échec des requêtes de purge**—Fastly renvoie l’erreur suivante lorsque vous envoyez une requête de purge :

  ```text
  The purge request was not processed successfully.
  ```

  Ce problème peut être dû à l’un des problèmes suivants :

   - Informations d’identification Fastly non valides dans la configuration de service Fastly pour Adobe Commerce dans l’environnement de projet d’infrastructure cloud
   - Code non valide dans un fragment de code VCL personnalisé

  Pour résoudre le problème, voir [Purge rapide du cache dans le cloud](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) dans le centre d’aide d’Adobe Commerce.

## 503 erreurs de Fastly

Si Fastly renvoie des erreurs de délai d’expiration 503, vérifiez les journaux d’erreur et la page d’erreur 503 pour identifier la cause principale.

>[!NOTE]
>
>Si le délai d’expiration survient lors de l’exécution d’opérations en bloc, vous pouvez [Extension du délai d’expiration rapide pour l’administrateur](fastly-custom-cache-configuration.md#extend-fastly-timeout).

Si vous recevez une erreur 503, vérifiez le journal des erreurs de l’environnement de production ou d’évaluation et le journal des accès php pour résoudre le problème.

**Pour vérifier les logs d’erreur**:

- [Journal des erreurs](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  Ce journal contient des erreurs provenant de l’application ou du moteur PHP, par exemple : `memory_limit` ou `max_execution_time exceeded` erreurs. Si vous ne trouvez pas d&#39;erreur liée à Fastly, vérifiez le journal des accès PHP.

- journal des accès PHP

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  Recherchez dans le journal les réponses HTTP 200 pour connaître l’URL qui a renvoyé l’erreur 503. Si vous trouvez la réponse 200, cela signifie qu’Adobe Commerce a renvoyé la page sans erreur. Cela indique que le problème peut s’être produit après l’intervalle qui dépasse la valeur `first_byte_timeout` défini dans la configuration de service Fastly.

Lorsqu’une erreur 503 se produit, la fonction renvoie rapidement la raison sur la page d’erreur et de maintenance. Vous ne pourrez peut-être pas voir la raison si vous avez ajouté du code pour une [page de réponse personnalisée](fastly-custom-response.md). Pour afficher le code motif sur la page d’erreur par défaut, vous pouvez supprimer le code HTML de la page d’erreur personnalisée.

**Pour vérifier la page d’erreur Fastly 503**:

{{admin-login-step}}

1. Cliquez sur **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Dans le volet de droite, développez **Cache de page complète**.

1. Dans le **Configuration rapide** , développez **Pages synchrones personnalisées** comme le montre la figure suivante.

   ![Page d’erreur personnalisée 503](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Cliquez sur **Définir le HTML**.

1. Supprimez le code personnalisé. Vous pouvez l’enregistrer dans un programme de texte pour l’ajouter ultérieurement.

1. Cliquez sur **Télécharger** pour envoyer vos mises à jour à Fastly.

1. Cliquez sur **Enregistrer la configuration** en haut de la page.

1. rouvrez l’URL à l’origine de l’erreur 503. Renvoie rapidement une page d’erreur avec la raison, comme illustré dans l’exemple suivant.

   ![Erreur Fastly](../../assets/cdn/fastly-503-example.png)

## Apex et sous-domaines déjà associés à un compte Fastly

Si le domaine et les sous-domaines apex de votre projet d’infrastructure cloud Adobe Commerce sont déjà associés à un compte Fastly existant avec un ID de service affecté, vous ne pouvez pas le lancer tant que vous n’avez pas mis à jour votre configuration Fastly :

- Mettez à jour la configuration apex et sous-domaine sur le compte Fastly existant. Voir [Plusieurs comptes et domaines attribués à la date](fastly.md#domain).

- [Activation et configuration rapides](fastly-configuration.md#enable-fastly-caching) et exécutez le [Configuration DNS](../launch/checklist.md#update-dns-configuration-with-production-settings)

## Vérification ou débogage des services rapides

Vous pouvez résoudre les problèmes de performances ou de mise en cache d’un site d’infrastructure cloud Adobe Commerce en testant les URL du site et en examinant les valeurs d’en-tête renvoyées dans la réponse.

### Archivage rapide du site

Utilisez l’API Fastly pour vérifier la variable  `Fastly-Magento-VCL-Uploaded` et `X-Cache` en-têtes de réponse renvoyés par votre site actif.

Les demandes d’API rapides sont transmises via l’extension Fastly afin d’obtenir une réponse de vos serveurs d’origine. Si la réponse renvoie des en-têtes incorrects, testez la variable [Serveurs d’origine directement](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**Pour vérifier les en-têtes de réponse**:

1. Dans un terminal, utilisez les `curl` pour tester l’URL de votre site actif :

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   Si vous n’avez pas défini d’itinéraire statique ou terminé la configuration DNS pour les domaines de votre site actif, utilisez la variable `--resolve` qui contourne la résolution du nom DNS.

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >Pour utiliser cette commande avec la méthode `--resolve` , vous devez activer TLS avec Fastly via un certificat SSL/TLS et rechercher l’adresse IP du noeud de cache.

1. Dans la réponse, vérifiez la variable [en-têtes](#check-cache-hit-and-miss-response-headers) pour vous assurer que Fastly fonctionne. Vous devriez voir les en-têtes uniques suivants dans la réponse :

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Si les en-têtes ne comportent pas les valeurs correctes, reportez-vous aux informations suivantes :

- [Vérification du chargement VCL](#fastly-vcl-has-not-been-uploaded)

- [X-Cache contient uniquement MISS, aucun accès](#x-cache-contains-only-miss-no-hit)

### Contournement du cache rapide pour vérifier les sites Adobe Commerce

Si le service Fastly renvoie des en-têtes incorrects, vous pouvez créer un extrait de code VCL qui vous permet d’envoyer des requêtes qui contournent le cache Fastly. Voir [Contournement rapide du cache](fastly-vcl-bypass-to-origin.md).

Après avoir ajouté le fragment de code VCL, utilisez les commandes cURL pour envoyer des requêtes au serveur d’origine à partir de l’adresse IP spécifiée. Recherchez ensuite les erreurs dans les réponses.

### Vérifier les en-têtes de réponse HIT et MISS du cache

Vérifiez que la réponse renvoyée contient les informations suivantes :

- Inclut la variable `X-Magento-Tags` header

- La valeur de la variable `Fastly-Module-Enabled` header is `Yes` ou le numéro de version du module Fastly for CDN Magento 2 installé dans l’environnement du projet

- [Cache-Control: max-age](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) est supérieur à 0

- [Pragma](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) paramètre `cache`

L’extrait suivant de la sortie de la commande cURL affiche les valeurs correctes pour la variable `Pragma`, `X-Magento-Tags`, et `Fastly-Module-Enabled` headers :

```terminal
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>Pour plus d’informations sur les accès et les échecs, voir [Présentation des en-têtes d’accès au cache et MISS avec les services protégés](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) dans la documentation Fastly.

### Résoudre les erreurs détectées dans les en-têtes de réponse

Cette section fournit des suggestions pour résoudre les erreurs renvoyées lors de la vérification des en-têtes de réponse à l’aide de l’API Fastly.

#### Le module Fastly n’est pas activé

Si le module Fastly n’est pas activé (`Fastly-Module-Enabled: no`) ou si l’en-tête est manquant, [utiliser SSH pour se connecter ;](../development/secure-connections.md#connect-to-a-remote-environment) au projet. Exécutez ensuite la commande suivante pour vérifier l’état du module.

```bash
php bin/magento module:status Fastly_Cdn
```

En fonction de l’état renvoyé, suivez les instructions suivantes pour mettre à jour la configuration Fastly.

- `Module does not exist`: si le module n’existe pas [installation et configuration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) le module CDN Fastly pour Magento 2 dans une branche d’intégration. Une fois l’installation terminée, activez et configurez le module. Voir [Configuration rapide](fastly-configuration.md).

- `Module is disabled`: si le module Fastly est désactivé, mettez à jour la configuration de l’environnement sur un `integration` branche dans votre environnement local pour l’activer. Ensuite, appliquez les modifications à l’évaluation et à la production. Voir [Gestion des extensions](../store/extensions.md#install-an-extension).

  Si vous utilisez [Gestion des configurations](../store/store-settings.md#configure-store), vérifiez l’état du module CDN Fastly dans le `app/etc/config.php` fichier de configuration avant d’envoyer les modifications à l’environnement de production ou d’évaluation.

  Si le module n’est pas activé (`Fastly_CDN => 0`) dans la variable `config.php` , supprimez le fichier et exécutez la commande suivante pour mettre à jour : `config.php` avec les derniers paramètres de configuration.

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### Le fichier VCL Fastly n’a pas été chargé.

Si le fichier VCL Fastly n’a pas été chargé (`Fastly-Magento-VCL-Uploaded`: `false`), utilisez la variable *Télécharger VCL* dans l’option Admin pour la télécharger. Voir [Chargement rapide de fragments de code VCL](fastly-configuration.md#upload-vcl-to-fastly).

#### X-Cache contient uniquement MISS, aucun accès

Si la variable `X-Cache` L’en-tête contient `HIT` (`HIT, HIT` ou `HIT, MISS`), cela indique que le contenu mis en cache est renvoyé rapidement.

Si la variable `X-Cache` header is `MISS, MISS` et ne contient pas `HIT`, exécutez le `curl` pour vous assurer que la page n’a pas été récemment purgée du cache.

Si vous obtenez le même résultat, utilisez la variable [`curl` Commandes](#check-live-site-through-fastly) et vérifiez la variable [en-têtes de réponse](#check-cache-hit-and-miss-response-headers):

- `Pragma` is `cache`
- `X-Magento-Tags` existe
- `Cache-Control: max-age` est supérieur à 0

Si le problème persiste, une autre extension réinitialise probablement ces en-têtes. Répétez la procédure suivante dans l’environnement d’évaluation en désactivant toutes les extensions et en réactivant chacune d’elles pour déterminer l’extension qui réinitialise les en-têtes. Après avoir identifié l’extension à l’origine du problème, vous devez la désactiver dans l’environnement de production.

**Pour identifier une extension qui réinitialise les en-têtes de réponse :**

{{admin-login-step}}

1. Accédez à **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Avancé**.

1. Dans le *Désactiver la sortie des modules* dans le volet de droite, recherchez toutes vos extensions et désactivez-les.

1. Cliquez sur **Enregistrer la configuration**.

1. Cliquez sur **Système** > **Outils** > **Gestion du cache**.

1. Cliquez sur **Vider le cache du Magento**.

1. Suivez les étapes suivantes pour chaque extension, ce qui peut entraîner des problèmes avec les en-têtes Fastly :

   - Activez une extension à la fois, enregistrez la configuration et videz le cache Adobe Commerce.

   - Exécutez la variable [`curl` Commandes](#check-live-site-through-fastly) pour vérifier la variable [en-têtes de réponse](#check-cache-hit-and-miss-response-headers).

   Répétez cette procédure pour chaque extension. Si les en-têtes de réponse Fastly ne s’affichent plus, vous avez identifié l’extension qui entraîne des problèmes avec Fastly.

Une fois que vous avez identifié l’extension qui réinitialise les en-têtes Fastly, contactez le développeur de l’extension pour obtenir une aide supplémentaire. Nous ne pouvons pas fournir de correctifs ou de mises à jour pour que les extensions tierces fonctionnent avec une mise en cache rapide.

## Restauration rapide de la configuration

Si des mises à jour de fragments de code VCL personnalisés ou d’autres modifications de configuration rapides entraînent la rupture ou le renvoi d’erreurs d’une Adobe Commerce sur le site d’infrastructure cloud, utilisez l’API Fastly [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) pour restaurer une version antérieure de VCL. Vous ne pouvez pas restaurer la version VCL à partir de l’administrateur.

**Pour restaurer la version VCL**:

1. Pour obtenir la liste des versions VCL disponibles pour un service, exécutez la commande suivante :

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. Exécutez la commande suivante pour remplacer la version active de VCL par une version spécifiée.

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

Pour plus d’informations sur l’utilisation de l’API Fastly pour examiner et gérer VCL, voir [Gestion de VCL à l’aide de l’API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
