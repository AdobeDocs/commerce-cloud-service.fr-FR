---
source-git-commit: 74ce2b69c1d4f9412f9eac98dfea93cc08f737b6
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 0%

---
# Packages Cloud pour Adobe Commerce

<!-- The 'packages' variable contains the 'packages' node of the '_data/codebase/cloud/composer_lock.json' file
 -->

<!-- The 'packages-dev' variable contains the 'packages-dev' node of the '_data/codebase/cloud/composer_lock.json' file
 -->

<!-- The 'product' variable contains data of the 'magento/magento-cloud-metapackage' package
 -->

<!-- The edition variable contains `cloud` value from the _data/names.yml file
 -->

Adobe Commerce sur l’infrastructure cloud utilise le compositeur pour gérer les packages PHP.

La variable `composer.json` déclare la liste des modules, tandis que la variable `composer.lock` stocke une liste complète des packages (une version complète de chaque package et ses dépendances) utilisés pour créer une installation d’Adobe Commerce.

La documentation de référence suivante est générée à partir de la `composer.lock` et couvre les modules requis inclus dans Adobe Commerce sur l’infrastructure cloud 2.4.7.

## Dépendances

`magento/magento-cloud-metapackage 2.4.7` comporte les dépendances suivantes :

```config
fastly/magento2: ^1.2.34
magento/ece-tools: ^2002.1.0
magento/module-paypal-on-boarding: ~100.5.0
magento/product-enterprise-edition: >=2.4.7 <2.4.8
```

## Licences tierces

### Apache-2.0, LGPL-2.1 uniquement

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/elastic/elasticsearch-php.git">élasticsearch/élasticsearch</a>
    </td>
    <td>bibliothèque</td>
    <td>Client PHP pour Elasticsearch</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/opensearch-project/opensearch-php.git">opensearch-project/opensearch-php</a>
    </td>
    <td>bibliothèque</td>
    <td>Client PHP pour OpenSearch</td>
  </tr>
  </tbody>
</table>

### Apache-2.0

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/adobe/stock-api-libphp.git">astock/stock-api-libphp</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque d’API Adobe Stock</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/awslabs/aws-crt-php.git">aws/aws-crt-php</a>
    </td>
    <td>bibliothèque</td>
    <td>AWS Common Runtime pour PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/aws/aws-sdk-php.git">aws/aws-sdk-php</a>
    </td>
    <td>bibliothèque</td>
    <td>SDK AWS pour PHP - Utilisation de Amazon Web Services dans votre projet PHP</td>
  </tr>
  <tr>
    <td>
      paypal/module-braintree
    </td>
    <td>métapackage</td>
    <td>Magento Braintree</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/wikimedia/less.php.git">wikimedia/less.php</a>
    </td>
    <td>bibliothèque</td>
    <td>Port PHP du processeur LESS</td>
  </tr>
  </tbody>
</table>

### BSD-2-Clause

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/Bacon/BaconQrCode.git">bacon/bacon-qr-code</a>
    </td>
    <td>bibliothèque</td>
    <td>BaconQrCode est un générateur de code QR pour PHP.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/DASPRiD/Enum.git">dasprid/enum</a>
    </td>
    <td>bibliothèque</td>
    <td>Implémentation d’énumération PHP 7.1</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/webimpress/safe-writer.git">webimpress/safe-writer</a>
    </td>
    <td>bibliothèque</td>
    <td>Outil pour écrire des fichiers en toute sécurité, afin d’éviter les conditions de concurrence</td>
  </tr>
  </tbody>
</table>

### BSD-3-Clause

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/colinmollenhour/Cm_Cache_Backend_File.git">colinmollenhour/cache-backend-file</a>
    </td>
    <td>magento-module</td>
    <td>Le serveur principal Zend_Cache_Backend_File de stock présente des performances extrêmement médiocres pour le nettoyage par balises, ce qui le rend inutilisable à mesure que le nombre d’éléments mis en cache augmente. Ce serveur principal apporte de nombreuses modifications, ce qui se traduit par une amélioration considérable des performances, en particulier pour le nettoyage des balises.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/colinmollenhour/php-redis-session-abstract.git">colinmollenhour/php-redis-session-abstract</a>
    </td>
    <td>bibliothèque</td>
    <td>Un gestionnaire de session Redis avec verrouillage optimiste</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/fastly/fastly-magento2.git">fast/magento2</a>
    </td>
    <td>magento2-module</td>
    <td>Module CDN rapide pour Magento 2.4.x</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/firebase/php-jwt.git">firebase/php-jwt</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque simple pour coder et décoder les jetons Web JSON (JWT) en PHP. Doit être conforme à la spécification actuelle.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/google/recaptcha.git">google/recaptcha</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque cliente pour reCAPTCHA, un service gratuit qui protège les sites contre les spams et les abus.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-captcha.git">laminas/laminas-captcha</a>
    </td>
    <td>bibliothèque</td>
    <td>Générer et valider des CAPTCHA à l’aide de Figlets, d’images, de ReCaptcha, etc.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-code.git">laminas/laminas-code</a>
    </td>
    <td>bibliothèque</td>
    <td>Extensions de l’API de réflexion PHP, de l’analyse de code statique et de la génération de code</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-config.git">laminas/laminas-config</a>
    </td>
    <td>bibliothèque</td>
    <td>fournit une interface utilisateur basée sur une propriété d’objet imbriquée pour accéder à ces données de configuration dans le code de l’application.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-crypt.git">laminas/laminas-crypt</a>
    </td>
    <td>bibliothèque</td>
    <td>Outils de cryptographie forts et hachage de mot de passe</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-db.git">laminas/laminas-db</a>
    </td>
    <td>bibliothèque</td>
    <td>Couche d’abstraction de la base de données, abstraction SQL, abstraction de l’ensemble de résultats et implémentations de RowDataGateway et de TableDataGateway</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-di.git">laminas/laminas-di</a>
    </td>
    <td>bibliothèque</td>
    <td>Injection de dépendance automatisée pour les conteneurs PSR-11</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-escaper.git">plasas/laminas-escaper</a>
    </td>
    <td>bibliothèque</td>
    <td>HTML, attributs de HTML, JavaScript, CSS et URL sécurisés et échappés en toute sécurité</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-eventmanager.git">laminas/laminas-eventmanager</a>
    </td>
    <td>bibliothèque</td>
    <td>Déclencher et écouter les événements dans une application PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-feed.git">laminas/flux laminas</a>
    </td>
    <td>bibliothèque</td>
    <td>fournit des fonctionnalités pour créer et utiliser des flux RSS et Atom ;</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-file.git">laminas/laminas-file</a>
    </td>
    <td>bibliothèque</td>
    <td>Localisation des fichiers de classe PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-filter.git">laminas/laminas-filter</a>
    </td>
    <td>bibliothèque</td>
    <td>Filtrage et normalisation par programmation des données et des fichiers</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-http.git">laminas/laminas-http</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit une interface simple pour exécuter des requêtes HTTP (HyperText Transfer Protocol)</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-i18n.git">laminas/laminas-i18n</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournir des traductions pour votre application, filtrer et valider les valeurs internationalisées</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-json.git">laminas/laminas-json</a>
    </td>
    <td>bibliothèque</td>
    <td>fournit des méthodes pratiques pour sérialiser du code PHP natif en JSON et décoder le code JSON en code PHP natif ;</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-loader.git">laminas/laminas-loader</a>
    </td>
    <td>bibliothèque</td>
    <td>Chargement automatique et stratégies de chargement de module externe</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-mail.git">laminas/laminas-mail</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit une fonctionnalité générale pour composer et envoyer des messages électroniques en plusieurs parties compatibles avec MIME et du texte.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-math.git">laminas/laminas-math</a>
    </td>
    <td>bibliothèque</td>
    <td>Créer des nombres pseudo-aléatoires sécurisés au niveau cryptographique et gérer des entiers volumineux</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-mime.git">laminas/laminas-mime</a>
    </td>
    <td>bibliothèque</td>
    <td>Créer et analyser des messages MIME et des parties</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-modulemanager.git">laminas/laminas-modulemanager</a>
    </td>
    <td>bibliothèque</td>
    <td>Système applicatif modulaire pour les applications laminas-mvc</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-mvc.git">laminas/laminas-mvc</a>
    </td>
    <td>bibliothèque</td>
    <td>Couche MVC pilotée par les événements de Laminas, y compris les applications MVC, les contrôleurs et les modules externes</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-oauth.git">laminas/laminas-oauth</a>
    </td>
    <td>bibliothèque</td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-permissions-acl.git">laminas/laminas-permissions-acl</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit une mise en oeuvre légère et flexible de liste de contrôle d’accès (ACL) pour la gestion des privilèges</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-recaptcha.git">laminas/laminas-recaptcha</a>
    </td>
    <td>bibliothèque</td>
    <td>wrapper OOP pour le service Web ReCaptcha</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-router.git">laminas/laminas-router</a>
    </td>
    <td>bibliothèque</td>
    <td>Système de routage flexible pour les applications HTTP et console</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-server.git">laminas/laminas-server</a>
    </td>
    <td>bibliothèque</td>
    <td>Création de serveurs RPC basés sur une réflexion</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-servicemanager.git">laminas/laminas-servicemanager</a>
    </td>
    <td>bibliothèque</td>
    <td>Conteneur d’injection de dépendances piloté par les usines</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-session.git">laminas/laminas-session</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface orientée objet vers les sessions PHP et le stockage</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-soap.git">laminas/laminas-soap</a>
    </td>
    <td>bibliothèque</td>
    <td></td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-stdlib.git">laminas/laminas-stdlib</a>
    </td>
    <td>bibliothèque</td>
    <td>Extensions SPL, utilitaires de tableau, gestionnaires d’erreurs, etc.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-text.git">laminas/laminas-text</a>
    </td>
    <td>bibliothèque</td>
    <td>Création de FIGlets et de tableaux basés sur du texte</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-uri.git">laminas/laminas-uri</a>
    </td>
    <td>bibliothèque</td>
    <td>Composant qui facilite la manipulation et la validation des "URI" (Uniform Resource Identifiers)</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-validator.git">laminas/laminas-validator</a>
    </td>
    <td>bibliothèque</td>
    <td>Classes de validation pour un large éventail de domaines et possibilité de regrouper des validateurs afin de créer des critères de validation complexes</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/laminas/laminas-view.git">laminas/vues laminaires</a>
    </td>
    <td>bibliothèque</td>
    <td>Calque d’affichage flexible prenant en charge et fournissant plusieurs calques d’affichage, assistants, etc.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/nikic/PHP-Parser.git">nikic/php-parser</a>
    </td>
    <td>bibliothèque</td>
    <td>Un analyseur PHP écrit en PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/tedious/JShrink.git">tedivm/jshrink</a>
    </td>
    <td>bibliothèque</td>
    <td>Minificateur JavaScript intégré à PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/tubalmartin/YUI-CSS-compressor-PHP-port.git">tubalMartin/cssmin</a>
    </td>
    <td>bibliothèque</td>
    <td>Un port PHP du compresseur CSS YUI</td>
  </tr>
  </tbody>
</table>

### BSD-3-Clause-Modification

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/colinmollenhour/Cm_Cache_Backend_Redis.git">colinmollenhour/cache-backend-redis</a>
    </td>
    <td>magento-module</td>
    <td>Serveur principal Zend_Cache utilisant Redis avec prise en charge complète des balises.</td>
  </tr>
  </tbody>
</table>

### ISC

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/paragonie/sodium_compat.git">paragonie/sodium_compat</a>
    </td>
    <td>bibliothèque</td>
    <td>Mise en oeuvre Pure PHP de libsoude ; utilise l’extension PHP si elle existe</td>
  </tr>
  </tbody>
</table>

### LGPL-2.1-ou-version ultérieure

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/ezyang/htmlpurifier.git">ezyang/htmlpurifier</a>
    </td>
    <td>bibliothèque</td>
    <td>Filtre de HTML conforme aux normes écrit en PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-amqplib/php-amqplib.git">php-amqplib/php-amqplib</a>
    </td>
    <td>bibliothèque</td>
    <td>Anciennement videlalvaro/php-amqplib.  Cette bibliothèque est une implémentation PHP pure du protocole AMQP. Il a été testé contre RabbitMQ.</td>
  </tr>
  </tbody>
</table>

### MIT

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/braintree/braintree_php.git">braintree/braintree_php</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque cliente PHP Braintree</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/brick/math.git">brique/maths</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque arithmétique de précision arbitraire</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/brick/varexporter.git">brique/varporter</a>
    </td>
    <td>bibliothèque</td>
    <td>Une alternative puissante à var_export(), qui peut exporter des fermetures et des objets sans __set_state()</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/CarbonPHP/carbon-doctrine-types.git">carbonphp/carbone-doctrine-types</a>
    </td>
    <td>bibliothèque</td>
    <td>Des types d'utilisation du carbone dans la doctrine</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ChristianRiesen/base32.git">chrétien-riesen/base32</a>
    </td>
    <td>bibliothèque</td>
    <td>Codeur/décodeur Base32 selon la norme RFC 4648</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/colinmollenhour/credis.git">colinmollenhour/credis</a>
    </td>
    <td>bibliothèque</td>
    <td>Credis est une interface légère pour la banque de valeurs clés Redis qui enveloppe la bibliothèque phpredis lorsqu’elle est disponible pour de meilleures performances.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/ca-bundle.git">compositeur/ca-bundle</a>
    </td>
    <td>bibliothèque</td>
    <td>Permet de trouver un chemin d’accès au lot d’autorité de certification du système et inclut un secours au lot d’autorité de certification Mozilla.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/class-map-generator.git">compositeur/classe-map-generator</a>
    </td>
    <td>bibliothèque</td>
    <td>Utilitaires pour analyser le code PHP et générer des mappages de classe.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/composer.git">compositeur/compositeur</a>
    </td>
    <td>bibliothèque</td>
    <td>Le compositeur vous aide à déclarer, gérer et installer les dépendances des projets PHP. Cela vous garantit d’avoir la pile appropriée partout.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/metadata-minifier.git">compositeur/métadonnée-minifier</a>
    </td>
    <td>bibliothèque</td>
    <td>Petite bibliothèque utilitaire qui gère la minification et l’extension des métadonnées.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/pcre.git">compositeur/opérateur</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque d’encapsulage PCRE qui offre des remplacements preg_* sécurisés par type.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/semver.git">compositeur/semver</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque Semover qui propose des utilitaires, une analyse et une validation des contraintes de version.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/spdx-licenses.git">compositeur/spdx-licences</a>
    </td>
    <td>bibliothèque</td>
    <td>Liste des licences SPDX et bibliothèque de validation.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/composer/xdebug-handler.git">compositeur/xdebug-handler</a>
    </td>
    <td>bibliothèque</td>
    <td>Redémarre un processus sans Xdebug.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/endroid/qr-code.git">endroid/qr-code</a>
    </td>
    <td>bibliothèque</td>
    <td>Endroid QR Code</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ezimuel/guzzlestreams.git">ezimuel/guzzlestreams</a>
    </td>
    <td>bibliothèque</td>
    <td>Branchement de guzzle/flux (abandonné) à utiliser avec élasticsearch-php</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ezimuel/ringphp.git">ezimuel/ringphp</a>
    </td>
    <td>bibliothèque</td>
    <td>Branchement de guzzle/RingPHP (abandonné) à utiliser avec élasticsearch-php</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/FriendsOfPHP/proxy-manager-lts.git">friendsofphp/proxy-manager-lts</a>
    </td>
    <td>bibliothèque</td>
    <td>Ajout de la prise en charge d’un plus large éventail de versions PHP pour ocramius/proxy-manager</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/bzikarsky/gelf-php.git">graylog2/gelf-php</a>
    </td>
    <td>bibliothèque</td>
    <td>Une mise en oeuvre php pour envoyer des messages de journal à un serveur principal compatible avec GELF comme Graylog2.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/guzzle/guzzle.git">guzzlehttp/guzzle</a>
    </td>
    <td>bibliothèque</td>
    <td>Guzzle est une bibliothèque cliente HTTP PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/guzzle/promises.git">guzzlehttp/promesses</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque de promesses de guzzle</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/guzzle/psr7.git">guzzlehttp/psr7</a>
    </td>
    <td>bibliothèque</td>
    <td>Mise en oeuvre de messages PSR-7 qui fournit également des méthodes d’utilitaire courantes</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/illuminate/collections.git">illumination/collections</a>
    </td>
    <td>bibliothèque</td>
    <td>Le package Illuminer les collections .</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/illuminate/config.git">illuminate/config</a>
    </td>
    <td>bibliothèque</td>
    <td>Le package de configuration Illuminée.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/illuminate/contracts.git">illumination/contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>Le kit Illuminate Contrats.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/illuminate/macroable.git">illuminate/macroable</a>
    </td>
    <td>bibliothèque</td>
    <td>Le module Illuminer les macros.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/justinrainbow/json-schema.git">justinrainbow/json-schema</a>
    </td>
    <td>bibliothèque</td>
    <td>Une bibliothèque pour valider un schéma json.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/thephpleague/flysystem.git">ligue/système de vol</a>
    </td>
    <td>bibliothèque</td>
    <td>Extraction de stockage de fichiers pour PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/thephpleague/flysystem-aws-s3-v3.git">league/flysystem-aws-s3-v3</a>
    </td>
    <td>bibliothèque</td>
    <td>Adaptateur de système de fichiers AWS S3 pour Flysystem.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/thephpleague/mime-type-detection.git">league/mime-type-détection</a>
    </td>
    <td>bibliothèque</td>
    <td>Détection de type MIME pour Flysystem</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Seldaek/monolog.git">monolog/monolog</a>
    </td>
    <td>bibliothèque</td>
    <td>Envoie vos journaux à des fichiers, des sockets, des boîtes de réception, des bases de données et divers services Web.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/jmespath/jmespath.php.git">mtdowling/jmespath.php</a>
    </td>
    <td>bibliothèque</td>
    <td>Spécifier de manière déclarative comment extraire des éléments d’un document JSON</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/briannesbitt/Carbon.git">nesbot/carbone</a>
    </td>
    <td>bibliothèque</td>
    <td>Extension d’API pour DateTime qui prend en charge 281 langues différentes.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/paragonie/constant_time_encoding.git">paragonie/constant_time_encoding</a>
    </td>
    <td>bibliothèque</td>
    <td>Mises en oeuvre en temps constant du codage RFC 4648 (Base-64, Base-32, Base-16)</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/paragonie/random_compat.git">paragonie/random_compat</a>
    </td>
    <td>bibliothèque</td>
    <td>polyfill PHP 5.x pour random_bytes() et random_int() de PHP 7</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/MyIntervals/emogrifier.git">pelago/emogrifier</a>
    </td>
    <td>bibliothèque</td>
    <td>Convertit les styles CSS en attributs de style intégrés dans votre code de HTML.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/PhpGt/CssXPath.git">phpgt/cssxpath</a>
    </td>
    <td>bibliothèque</td>
    <td>Convertissez des sélecteurs CSS en requêtes XPath.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/PhpGt/Dom.git">phpgt/dom</a>
    </td>
    <td>bibliothèque</td>
    <td>API DOM moderne.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/PhpGt/PropFunc.git">phpgt/propfunc</a>
    </td>
    <td>bibliothèque</td>
    <td>Fonctions d’accès aux propriétés et de modification.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/phpseclib/mcrypt_compat.git">phpseclib/mcrypt_compat</a>
    </td>
    <td>bibliothèque</td>
    <td>polyfill PHP 5.x-8.x pour l’extension mcrypt</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/phpseclib/phpseclib.git">phpseclib/phpseclib</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque de communications sécurisée PHP : implémentations Pure-PHP de RSA, AES, SSH2, SFTP, X.509, etc.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/clock.git">psr/horloge</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface courante pour lire l'horloge.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/container.git">psr/container</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface de conteneur commune (gestion de fichiers PSR-11 PHP)</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/event-dispatcher.git">psr/event-dispatcher</a>
    </td>
    <td>bibliothèque</td>
    <td>Interfaces standard pour la gestion des événements.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/http-client.git">psr/http-client</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface courante pour les clients HTTP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/http-factory.git">psr/http-factory</a>
    </td>
    <td>bibliothèque</td>
    <td>Interfaces courantes des usines de messages HTTP PSR-7</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/http-message.git">psr/http-message</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface courante pour les messages HTTP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/log.git">psr/log</a>
    </td>
    <td>bibliothèque</td>
    <td>Interface commune pour les bibliothèques de journalisation</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/php-fig/simple-cache.git">psr/simple-cache</a>
    </td>
    <td>bibliothèque</td>
    <td>Interfaces communes pour la mise en cache simple</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ralouphie/getallheaders.git">ralouphie/getallheaders</a>
    </td>
    <td>bibliothèque</td>
    <td>polyfill pour getallheaders.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ramsey/collection.git">ramsey/collection</a>
    </td>
    <td>bibliothèque</td>
    <td>Bibliothèque PHP pour représenter et manipuler des collections.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/ramsey/uuid.git">ramsey/uuid</a>
    </td>
    <td>bibliothèque</td>
    <td>Une bibliothèque PHP pour générer et utiliser des identifiants universellement uniques (UUID).</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/reactphp/promise.git">response/promesse</a>
    </td>
    <td>bibliothèque</td>
    <td>Mise en oeuvre légère de CommonJS Promises/A pour PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/MyIntervals/PHP-CSS-Parser.git">sabberworm/php-css-parser</a>
    </td>
    <td>bibliothèque</td>
    <td>Analyseur des fichiers CSS écrits en PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Seldaek/jsonlint.git">seld/jsonlint</a>
    </td>
    <td>bibliothèque</td>
    <td>Liste JSON</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Seldaek/phar-utils.git">seld/phar-utils</a>
    </td>
    <td>bibliothèque</td>
    <td>Utilitaires de format de fichier PHAR, pour les appels PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Seldaek/signal-handler.git">seld/signal-handler</a>
    </td>
    <td>bibliothèque</td>
    <td>Gestionnaire de signaux unix simple qui échoue silencieusement lorsque les signaux ne sont pas pris en charge pour faciliter le développement sur plusieurs plateformes</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Spomky-Labs/aes-key-wrap.git">spomky-labs/aes-key-wrap</a>
    </td>
    <td>bibliothèque</td>
    <td>AES Key Wrap pour PHP.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Spomky-Labs/otphp.git">spomky-labs/otphp</a>
    </td>
    <td>bibliothèque</td>
    <td>Une bibliothèque PHP pour générer des mots de passe uniques conformément à la norme RFC 4226 (algorithme HOTP) et à la norme RFC 6238 (algorithme TOTP), compatible avec l’authentificateur Google.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/Spomky-Labs/pki-framework.git">spomky-labs/pki-framework</a>
    </td>
    <td>bibliothèque</td>
    <td>Un framework PHP pour la gestion des infrastructures de clé publique. Il comprend des certificats de clé publique X.509, des certificats d’attribut, des demandes de certification et la validation du chemin de certification.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/config.git">symfony/config</a>
    </td>
    <td>bibliothèque</td>
    <td>Permet de rechercher, charger, combiner, remplir automatiquement et valider les valeurs de configuration de tout type.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/console.git">symfony/console</a>
    </td>
    <td>bibliothèque</td>
    <td>Facilite la création d’interfaces de ligne de commande jolies et vérifiables.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/css-selector.git">symfony/css-selector</a>
    </td>
    <td>bibliothèque</td>
    <td>Convertit les sélecteurs CSS en expressions XPath</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/dependency-injection.git">symfony/dependency-injection</a>
    </td>
    <td>bibliothèque</td>
    <td>Permet de normaliser et de centraliser la manière dont les objets sont construits dans votre application.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/deprecation-contracts.git">symfony/deprecation-contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>Fonction et convention génériques pour déclencher des avis d’obsolescence</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/error-handler.git">symfony/error-handler</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des outils pour gérer les erreurs et faciliter le débogage du code PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/event-dispatcher.git">symfony/event-dispatcher</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des outils qui permettent aux composants de l’application de communiquer les uns avec les autres en distribuant les événements et en les écoutant.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/event-dispatcher-contracts.git">symfony/event-dispatcher-contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>abstractions génériques liées à la distribution d’un événement</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/filesystem.git">symfony/filessystem</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des utilitaires de base pour le système de fichiers</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/finder.git">symfony/finder</a>
    </td>
    <td>bibliothèque</td>
    <td>Recherche de fichiers et de répertoires via une interface utilisateur intuitive</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/http-client.git">symfony/http-client</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des méthodes puissantes pour récupérer des ressources HTTP de manière synchrone ou asynchrone</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/http-client-contracts.git">symfony/http-client-contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>abstractions génériques liées aux clients HTTP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/http-foundation.git">symfony/http-foundation</a>
    </td>
    <td>bibliothèque</td>
    <td>Définit une couche orientée objet pour la spécification HTTP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/http-kernel.git">symfony/http-kernel</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit un processus structuré pour convertir une requête en réponse</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/intl.git">symfony/intl</a>
    </td>
    <td>bibliothèque</td>
    <td>Permet d’accéder aux données de localisation de la bibliothèque ICU.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-ctype.git">symfony/polyfill-ctype</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill pour les fonctions ctype</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-intl-grapheme.git">symfony/polyfill-intl-grapheme</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill pour les fonctions grapheme_* d’intl</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-intl-idn.git">symfony/polyfill-intl-idn</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill pour les fonctions idn_to_ascii et idn_to_utf8 d’intl</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-intl-normalizer.git">symfony/polyfill-intl-normalizer</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill pour la classe Normalizer d’intl et les fonctions associées</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-mbstring.git">symfony/polyfill-mbstring</a>
    </td>
    <td>bibliothèque</td>
    <td>Polyfill Symfony pour l’extension Mbstring</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-php72.git">symfony/polyfill-php72</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill renvoyant certaines fonctionnalités PHP 7.2+ pour réduire les versions de PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-php73.git">symfony/polyfill-php73</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill renvoyant certaines fonctionnalités PHP 7.3+ pour réduire les versions de PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-php80.git">symfony/polyfill-php80</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill renvoyant certaines fonctionnalités PHP 8.0+ pour des versions PHP plus basses</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-php81.git">symfony/polyfill-php81</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill renvoyant certaines fonctionnalités PHP 8.1+ pour réduire les versions de PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/polyfill-php83.git">symfony/polyfill-php83</a>
    </td>
    <td>bibliothèque</td>
    <td>Symfony polyfill renvoyant certaines fonctionnalités PHP 8.3+ pour réduire les versions de PHP</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/process.git">symfony/process</a>
    </td>
    <td>bibliothèque</td>
    <td>Exécute les commandes dans les sous-processus.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/proxy-manager-bridge.git">symfony/proxy-manager-bridge</a>
    </td>
    <td>symfony-bridge</td>
    <td>Fournit l’intégration de ProxyManager avec divers composants Symfony</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/serializer.git">symfony/serializer</a>
    </td>
    <td>bibliothèque</td>
    <td>Gère la sérialisation et la désérialisation des structures de données, y compris les graphiques d’objets, en structures de tableau ou dans d’autres formats tels que XML et JSON.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/service-contracts.git">symfony/service-contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>abstractions génériques liées aux services d’écriture</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/string.git">symfony/string</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit une API orientée objet pour les chaînes et traite les octets, les points de code UTF-8 et les groupes de graphèmes de manière unifiée.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/translation.git">symfony/translation</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des outils pour internationaliser votre application</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/translation-contracts.git">symfony/translation-contrats</a>
    </td>
    <td>bibliothèque</td>
    <td>abstractions génériques liées à la traduction</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/var-dumper.git">symfony/var-dumper</a>
    </td>
    <td>bibliothèque</td>
    <td>Fournit des mécanismes permettant de parcourir n’importe quelle variable PHP arbitraire.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/var-exporter.git">symfony/var-exporter</a>
    </td>
    <td>bibliothèque</td>
    <td>Permet d’exporter toute structure de données PHP sérialisable en code PHP standard.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/symfony/yaml.git">symfony/yaml</a>
    </td>
    <td>bibliothèque</td>
    <td>Chargement et vidage de fichiers YAML</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/web-token/jwt-framework.git">web-token/jwt-framework</a>
    </td>
    <td>symfony-bundle</td>
    <td>Bibliothèque de signature et de chiffrement d’objet JSON pour PHP et Symfony Bundle.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/webmozarts/assert.git">webmozart/assert</a>
    </td>
    <td>bibliothèque</td>
    <td>Assertions pour valider l’entrée/la sortie de la méthode avec de bons messages d’erreur.</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/webonyx/graphql-php.git">webonyx/graphql-php</a>
    </td>
    <td>bibliothèque</td>
    <td>Un port PHP de l’implémentation de référence GraphQL</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/zordius/lightncandy.git">zordius/lightncandy</a>
    </td>
    <td>bibliothèque</td>
    <td>Une implémentation PHP extrêmement rapide des Guidons ( http://handlebarsjs.com/ ) et de la moustache ( http://mustache.github.io/ ).</td>
  </tr>
  </tbody>
</table>

### OSL-3.0, AFL-3.0

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      paypal/module-braintree-customer-balance
    </td>
    <td>magento2-module</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>
      paypal/module-braintree-cadeau-card-account
    </td>
    <td>magento2-module</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>
      paypal/module-braintree-cadeau-wrapping
    </td>
    <td>magento2-module</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>
      paypal/module-braintree-graph-ql
    </td>
    <td>magento2-module</td>
    <td>N/A</td>
  </tr>
  </tbody>
</table>

### OSL-3.0

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

### PHP

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      <a href="https://github.com/2tvenom/CBOREncode.git">2tvenom/cborencode</a>
    </td>
    <td>bibliothèque</td>
    <td>Codeur CBOR pour PHP</td>
  </tr>
  </tbody>
</table>

### Propriétaire

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>

### propriétaire

<table>
  <thead>
    <tr>
      <th>Nom</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td>
      paypal/module-braintree-core
    </td>
    <td>magento2-module</td>
    <td>Branchement du module Braintree Magento 2.2.0 par Gene Commerce pour PayPal.</td>
  </tr>
  </tbody>
</table>
