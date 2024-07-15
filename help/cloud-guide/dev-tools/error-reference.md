---
title: Messages d’erreur pour le package CEE-Outils
description: Consultez la liste des codes et messages d’erreur qui peuvent se produire pendant Adobe Commerce sur les processus de création, de déploiement et de post-déploiement de l’infrastructure cloud.
recommendations: noDisplay
role: Developer
exl-id: d8cc8d49-32da-43cf-a105-aa56b5334000
source-git-commit: 9dda6fe7f6a9d6064436820a3c8426ec982b5230
workflow-type: tm+mt
source-wordcount: '2763'
ht-degree: 4%

---

# Messages d’erreur pour les outils CEE

Cette référence de message d’erreur fournit des informations pour résoudre les erreurs qui peuvent se produire pendant Adobe Commerce lors des processus de création, de déploiement et de post-déploiement de l’infrastructure cloud.

Tous les messages d’erreur critiques et d’avertissement qui se produisent pendant le déploiement sont écrits dans les fichiers `var/log/cloud.log` et `/var/log/cloud.error.log`. Le fichier journal des erreurs du cloud contient uniquement des erreurs provenant du dernier déploiement. Un fichier vide indique un déploiement réussi sans erreur.

Dans le fichier `cloud.error.log`, chaque entrée est formatée en tant que chaîne JSON pour une analyse plus facile :

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Les messages d’erreur sont classés selon l’une des étapes de déploiement : création, déploiement et post-déploiement. Chaque section fournit une liste des erreurs associées avec les informations suivantes pour chaque erreur :

- **Code d’erreur** : identifiant attribué par Adobe Commerce au message d’erreur
- **Stage** : indique si l’erreur s’est produite pendant l’étape de création, de déploiement ou de post-déploiement
- **Étape** : indique l’étape dans le scénario de déploiement qui peut renvoyer l’erreur. Si la colonne _Étape_ est vide, l’erreur est une erreur générale qui peut être renvoyée par plusieurs étapes, ou lors d’opérations de prétraitement. Voir [Déploiement basé sur les scénarios](../deploy/scenario-based.md) pour plus d’informations sur les étapes de création, de déploiement et de post-déploiement.
- **Suggestion** : fournit des conseils pour dépanner et résoudre l’erreur.
- **Titre (description de l’erreur)** : description qui résume la cause de l’erreur
- **Type** : indique si l’erreur est une erreur critique ou un avertissement

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Erreurs critiques

Les erreurs critiques indiquent un problème avec Commerce sur la configuration du projet d’infrastructure cloud qui entraîne l’échec du déploiement, par exemple une configuration incorrecte, non prise en charge ou une configuration manquante pour les paramètres requis. Avant de pouvoir déployer, vous devez mettre à jour la configuration pour résoudre ces erreurs.

### Etape de création

| Code d’erreur | Etape de création | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 2 |  | Impossible d’écrire dans le fichier `./app/etc/env.php` | Le script de déploiement ne peut pas apporter les modifications requises au fichier `/app/etc/env.php`. Vérifiez les autorisations de votre système de fichiers. |
| 3 |  | La configuration n&#39;est pas définie dans le fichier `schema.yaml` | La configuration n’est pas définie dans le fichier `./vendor/magento/ece-tools/config/schema.yaml`. Vérifiez que le nom de la variable de configuration est correct et défini. |
| 4 |  | Échec de l&#39;analyse du fichier `.magento.env.yaml` | Le format de fichier `./.magento.env.yaml` n’est pas valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 5 |  | Impossible de lire le fichier `.magento.env.yaml` | Impossible de lire le fichier `./.magento.env.yaml`. Vérifiez les autorisations de fichier. |
| 6 |  | Impossible de lire le fichier `.schema.yaml` | Impossible de lire le fichier `./vendor/magento/ece-tools/config/magento.env.yaml`. Vérifiez les autorisations de fichier et redéployez (`magento-cloud environment:redeploy`). |
| 7 | refresh-modules | Impossible d’écrire dans le fichier `./app/etc/config.php` | Le script de déploiement ne peut pas apporter les modifications requises au fichier `/app/etc/config.php`. Vérifiez les autorisations de votre système de fichiers. |
| 8 | validate-config | Impossible de lire le fichier `composer.json` | Impossible de lire le fichier `./composer.json`. Vérifiez les autorisations de fichier. |
| 9 | validate-config | La section de chargement automatique requise du fichier `composer.json` est manquante. | La section `autoload` requise est absente du fichier `composer.json`. Comparez la section Chargement automatique au fichier `composer.json` dans le modèle cloud et ajoutez la configuration manquante. |
| 10 | validate-config | Le fichier `.magento.env.yaml` contient une option qui n’est pas déclarée dans le schéma, ou une option configurée avec une valeur ou une étape non valide | Le fichier `./.magento.env.yaml` contient une configuration non valide. Consultez le journal des erreurs pour obtenir des informations détaillées. |
| 11 | refresh-modules | Échec de la commande : `/bin/magento module:enable --all` | Essayez d’exécuter `composer update` localement. Ensuite, validez et envoyez le fichier `composer.lock` mis à jour. Consultez également le `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 12 | apply-Correctifs | Échec de l’application du correctif |  |
| 13 | set-report-dir-imbrication-level | Impossible d&#39;écrire dans le fichier `/pub/errors/local.xml` |  |
| 14 | copy-sample-data | Échec de la copie des fichiers de données d’exemple |  |
| 15 | compile-di | Échec de la commande : `/bin/magento setup:di:compile` | Pour plus d’informations, consultez le `cloud.log` . Ajoutez `VERBOSE_COMMANDS: '-vvv'` dans `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 16 | dump-autoload | Échec de la commande : `composer dump-autoload` | La commande `composer dump-autoload` a échoué. Pour plus d’informations, consultez le `cloud.log` . |
| 17 | run-baler | Échec de la commande d’exécution `Baler` pour le regroupement JavaScript | Vérifiez la variable d’environnement `SCD_USE_BALER` pour vérifier que le module Baler est configuré et activé pour le regroupement JS. Si vous n’avez pas besoin du module Baler, définissez `SCD_USE_BALER: false`. |
| 18 | compress-static-content | Utilitaire requis introuvable (timeout, bash) |  |
| 19 | deploy-static-content | La commande `/bin/magento setup:static-content:deploy` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 20 | compress-static-content | Échec de la compression de contenu statique | Pour plus d’informations, consultez le `cloud.log` . |
| 21 | backup-data: static-content | Échec de la copie du contenu statique dans le répertoire `init` | Pour plus d’informations, consultez le `cloud.log` . |
| 22 | backup-data: write-able-dirs | Échec de la copie de certains répertoires modifiables dans le répertoire `init` | Échec de la copie des répertoires modifiables dans le dossier `./init`. Vérifiez les autorisations de votre système de fichiers. |
| 23 |  | Impossible de créer un objet journal |  |
| 24 | backup-data: static-content | Échec du nettoyage du répertoire `./init/pub/static/` | Échec du nettoyage du dossier `./init/pub/static`. Vérifiez les autorisations de votre système de fichiers. |
| 25 |  | Impossible de trouver le package du compositeur | Si vous avez installé la version de l’application Adobe Commerce directement à partir du référentiel GitHub, vérifiez que la variable d’environnement `DEPLOYED_MAGENTO_VERSION_FROM_GIT` est configurée. |
| 26 | validate-config | Supprimez la configuration du module Braintree Magento qui n’est plus prise en charge dans Adobe Commerce et les versions 2.4 et ultérieures de Magento Open Source. | La prise en charge du module de Braintree n’est plus incluse dans Magento 2.4.0 et versions ultérieures. Supprimez la variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL de la section des variables du fichier `.magento.app.yaml`. Pour l’aide au paiement des Braintree, utilisez plutôt une extension officielle du Commerce Marketplace. |

### Déploiement de l’étape

| Code d’erreur | Étape de déploiement | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 101 | pré-déploiement : cache | Configuration de cache incorrecte (port ou hôte manquant) | Les paramètres requis `server` ou `port` sont absents de la configuration du cache. Pour plus d’informations, consultez le `cloud.log` . |
| 102 |  | Impossible d’écrire dans le fichier `./app/etc/env.php` | Le script de déploiement ne peut pas apporter les modifications requises au fichier `/app/etc/env.php`. Vérifiez les autorisations de votre système de fichiers. |
| 103 |  | La configuration n&#39;est pas définie dans le fichier `schema.yaml` | La configuration n’est pas définie dans le fichier `./vendor/magento/ece-tools/config/schema.yaml`. Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 104 |  | Échec de l&#39;analyse du fichier `.magento.env.yaml` | La configuration n’est pas définie dans le fichier `./vendor/magento/ece-tools/config/schema.yaml`. Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 105 |  | Impossible de lire le fichier `.magento.env.yaml` | Impossible de lire le fichier `./.magento.env.yaml`. Vérifiez les autorisations de fichier. |
| 106 |  | Impossible de lire le fichier `.schema.yaml` |  |
| 107 | pre-deploy: clean-redis-cache | Échec du nettoyage du cache Redis | Échec du nettoyage du cache Redis. Vérifiez que la configuration du cache Redis est correcte et que le service Redis est disponible. Voir [Configuration du service Redis](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/redis.html). |
| 108 | pré-déploiement : set-production-mode | La commande `/bin/magento maintenance:enable` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 109 | validate-config | Configuration de base de données incorrecte | Vérifiez que la variable d&#39;environnement `DATABASE_CONFIGURATION` est correctement configurée. |
| 110 | validate-config | Configuration de session incorrecte | Vérifiez que la variable d&#39;environnement `SESSION_CONFIGURATION` est correctement configurée. La configuration doit contenir au moins le paramètre `save` . |
| 111 | validate-config | Configuration de recherche incorrecte | Vérifiez que la variable d&#39;environnement `SEARCH_CONFIGURATION` est correctement configurée. La configuration doit contenir au moins le paramètre `engine` . |
| 112 | validate-config | Configuration de ressource incorrecte | Vérifiez que la variable d&#39;environnement `RESOURCE_CONFIGURATION` est correctement configurée. La configuration doit contenir au moins `connection` paramètre. |
| 113 | validate-config:élasticsuite-integrity | ElasticSuite est installé, mais le service Elasticsearch n’est pas disponible | Vérifiez que la variable d&#39;environnement `SEARCH_CONFIGURATION` est correctement configurée et que le service Elasticsearch est disponible. |
| 114 | validate-config:élasticsuite-integrity | ElasticSuite est installé, mais un autre moteur de recherche est utilisé | ElasticSuite est installé, mais un autre moteur de recherche est configuré. Mettez à jour la variable d’environnement `SEARCH_CONFIGURATION` pour activer Elasticsearch et vérifiez la configuration du service Elasticsearch dans le fichier `services.yaml`. |
| 115 |  | Échec de l’exécution des requêtes de base de données |  |
| 116 | install-update: setup | La commande `/bin/magento setup:install` a échoué | Pour plus d’informations, consultez les sections `cloud.log` et `install_upgrade.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 117 | install-update: config-import | La commande `app:config:import` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 118 |  | Utilitaire requis introuvable (timeout, bash) |  |
| 119 | install-update: deploy-static-content | La commande `/bin/magento setup:static-content:deploy` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 120 | compress-static-content | Échec de la compression de contenu statique | Pour plus d’informations, consultez le `cloud.log` . |
| 121 | deploy-static-content:generate | Impossible de mettre à jour la version déployée | Impossible de mettre à jour le fichier `./pub/static/deployed_version.txt`. Vérifiez les autorisations de votre système de fichiers. |
| 122 | clean-static-content | Échec du nettoyage des fichiers de contenu statique |  |
| 123 | install-update: split-db | La commande `/bin/magento setup:db-schema:split` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 124 | clean-view-preprocessed | Échec du nettoyage du dossier `var/view_preprocessed` | Impossible de nettoyer le dossier `./var/view_preprocessed`. Vérifiez les autorisations de votre système de fichiers. |
| 125 | install-update: reset-password | Échec de la mise à jour du fichier `/var/credentials_email.txt` | Échec de la mise à jour du fichier `/var/credentials_email.txt`. Vérifiez les autorisations de votre système de fichiers. |
| 126 | install-update: update | La commande `/bin/magento setup:upgrade` a échoué | Pour plus d’informations, consultez les sections `cloud.log` et `install_upgrade.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 127 | clean-cache | La commande `/bin/magento cache:flush` a échoué | Pour plus d’informations, consultez le `cloud.log` . Pour une sortie de commande plus détaillée, ajoutez l’option `VERBOSE_COMMANDS: '-vvv'` au fichier `.magento.env.yaml`. |
| 128 | disable-maintenance-mode | La commande `/bin/magento maintenance:disable` a échoué | Pour plus d’informations, consultez le `cloud.log` . Ajoutez `VERBOSE_COMMANDS: '-vvv'` dans `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 129 | install-update: reset-password | Impossible de lire le modèle de réinitialisation de mot de passe |  |
| 130 | install-update: cache_type | Échec de la commande : `php ./bin/magento cache:enable` | La commande `php ./bin/magento cache:enable` s’exécute uniquement lorsque Adobe Commerce a été installé, mais le fichier `./app/etc/env.php` était absent ou vide au début du déploiement. Pour plus d’informations, consultez le `cloud.log` . Ajoutez `VERBOSE_COMMANDS: '-vvv'` dans `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 131 | install-update | La valeur de clé `crypt/key` n’existe pas dans le fichier `./app/etc/env.php` ou la variable d’environnement cloud `CRYPT_KEY` | Cette erreur se produit si le fichier `./app/etc/env.php` n’est pas présent au début du déploiement d’Adobe Commerce ou si la valeur `crypt/key` n’est pas définie. Si vous avez migré la base de données à partir d’un autre environnement, récupérez la valeur de la clé crypt de cet environnement. Ajoutez ensuite la valeur à la variable d’environnement cloud [CRYPT_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#crypt_key) dans votre environnement actuel. Voir [Clé de chiffrement Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/overview.html#gather-credentials). Si vous avez accidentellement supprimé le fichier `./app/etc/env.php`, utilisez la commande suivante pour le restaurer à partir des fichiers de sauvegarde créés à partir d’un déploiement précédent : `./vendor/bin/ece-tools backup:restore` Commande d’interface de ligne de commande .&quot; |
| 132 |  | Impossible de se connecter au service Elasticsearch | Recherchez des informations d’identification d’Elasticsearch valides et vérifiez que le service est en cours d’exécution. |
| 137 |  | Connexion impossible au service OpenSearch | Recherchez des informations d’identification OpenSearch valides et vérifiez que le service est en cours d’exécution. |
| 133 | validate-config | Supprimez la configuration du module Braintree Magento qui n’est plus prise en charge dans Adobe Commerce ou les versions 2.4 et ultérieures de Magento Open Source. | La prise en charge du module Braintree n’est plus incluse dans Adobe Commerce ou Magento Open Source 2.4.0 et versions ultérieures. Supprimez la variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL de la section des variables du fichier `.magento.app.yaml`. Pour la prise en charge des Braintree, utilisez plutôt une extension de paiement Braintree officielle du Commerce Marketplace . |
| 134 | validate-config | Adobe Commerce et Magento Open Source 2.4.0 nécessitent l’installation du service Elasticsearch | Installation du service Elasticsearch |
| 138 | validate-config | Adobe Commerce et Magento Open Source 2.4.4 nécessitent l’installation d’OpenSearch ou du service Elasticsearch | Installation du service OpenSearch |
| 135 | validate-config | Le moteur de recherche doit être défini sur Elasticsearch pour Adobe Commerce et Magento Open Source >= 2.4.0 | Vérifiez la variable SEARCH_CONFIGURATION pour l’option `engine`. S’il est configuré, supprimez l’option ou définissez la valeur sur &quot;élasticsearch&quot;. |
| 136 | validate-config | La base de données partagée a été supprimée à partir d’Adobe Commerce et de Magento Open Source 2.5.0. | Si vous utilisez une base de données partagée, vous devez restaurer ou migrer vers une base de données unique ou utiliser une autre approche. |
| 139 | validate-config | Moteur de recherche incorrect | Cette version d’Adobe Commerce ou de Magento Open Source ne prend pas en charge OpenSearch. Vous devez utiliser les versions 2.3.7-p3, 2.4.3-p2 ou ultérieures. |

### Étape de déploiement de Post

| Code d’erreur | Étape de déploiement de Post | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 201 | is-deploy-failed | Échec du déploiement de l’étape |  |
| 202 |  | Le fichier `./app/etc/env.php` ne peut pas être écrit. | Le script de déploiement ne peut pas apporter les modifications requises au fichier `/app/etc/env.php`. Vérifiez les autorisations de votre système de fichiers. |
| 203 |  | La configuration n&#39;est pas définie dans le fichier `schema.yaml` | La configuration n’est pas définie dans le fichier `./vendor/magento/ece-tools/config/schema.yaml`. Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 204 |  | Échec de l&#39;analyse du fichier `.magento.env.yaml` | Le format de fichier `./.magento.env.yaml` n’est pas valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 205 |  | Impossible de lire le fichier `.magento.env.yaml` | Vérifiez les autorisations de fichier. |
| 206 |  | Impossible de lire le fichier `.schema.yaml` |  |
| 207 | chauffage | Échec du préchargement de certaines pages de mise à niveau |  |
| 208 | time-to-firs-byte | Échec du test du temps jusqu’au premier octet (TTF) |  |
| 227 | clean-cache | La commande `/bin/magento cache:flush` a échoué | Pour plus d’informations, consultez le `cloud.log` . Ajoutez `VERBOSE_COMMANDS: '-vvv'` dans `.magento.env.yaml` pour une sortie de commande plus détaillée. |

### Général

| Code d’erreur | Étape générale | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 243 |  | La configuration n&#39;est pas définie dans le fichier `schema.yaml` | Vérifiez que le nom de la variable de configuration est correct et qu’il a été défini. |
| 244 |  | Échec de l&#39;analyse du fichier `.magento.env.yaml` | Le format de fichier `./.magento.env.yaml` n’est pas valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 245 |  | Impossible de lire le fichier `.magento.env.yaml` | Impossible de lire le fichier `./.magento.env.yaml`. Vérifiez les autorisations de fichier. |
| 246 |  | Impossible de lire le fichier `.schema.yaml` |  |
| 247 |  | Impossible de générer un module pour l’événement | Pour plus d’informations, consultez le `cloud.log` . |
| 248 |  | Impossible d’activer un module pour l’événement | Pour plus d’informations, consultez le `cloud.log` . |
| 249 |  | Échec de la génération du module AdobeCommerceWebhookPlugins | Pour plus d’informations, consultez le `cloud.log` . |
| 250 |  | Échec de l’activation du module AdobeCommerceWebhookPlugins | Pour plus d’informations, consultez le `cloud.log` . |

## Erreurs d’avertissement

Les erreurs d’avertissement indiquent un problème de configuration de projet d’infrastructure cloud de Commerce, tel que des paramètres de configuration incorrects, obsolètes, non pris en charge ou manquants pour les fonctionnalités facultatives qui peuvent affecter le fonctionnement du site. Bien qu’un avertissement ne provoque pas d’échec du déploiement, vous devez consulter les messages d’avertissement et mettre à jour la configuration pour les résoudre.

### Etape de création

| Code d’erreur | Etape de création | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 1001 | validate-config | Le fichier app/etc/config.php n’existe pas |  |
| 1002 | validate-config | Le .Le fichier /build_options.ini n’est plus pris en charge |  |
| 1003 | validate-config | La section modules est absente du fichier de configuration partagé |  |
| 1004 | validate-config | La configuration n’est pas compatible avec cette version de Magento |  |
| 1005 | validate-config | Options SCD ignorées |  |
| 1006 | validate-config | L’état configuré n’est pas idéal. |  |
| 1007 | run-baler | Le regroupement JS du baler ne peut pas être utilisé |  |

### Déploiement de l’étape

| Code d’erreur | Étape de déploiement | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 2001 | pre-deploy:cache | Le cache est configuré pour un service Redis qui n’est pas disponible. La configuration sera ignorée. |  |
| 2002 | validate-config | L’état configuré n’est pas idéal. |  |
| 2003 | validate-config | La valeur de niveau d’imbrication de répertoire pour le rapport d’erreurs n’a pas été configurée |  |
| 2004 | validate-config | Configuration non valide dans .fichier /pub/errors/local.xml . |  |
| 2005 | validate-config | Les données d’administration sont uniquement utilisées pour créer un utilisateur administrateur lors de l’installation initiale. Toute modification apportée aux données d’administration est ignorée pendant le processus de mise à niveau. | Après l’installation initiale, vous pouvez supprimer les données d’administration de la configuration. |
| 2006 | validate-config | L’utilisateur administrateur n’a pas été créé, car l’email administrateur n’a pas été défini. | Après l’installation, vous pouvez créer manuellement un utilisateur administrateur : utilisez ssh pour vous connecter à votre environnement. Exécutez ensuite la commande `bin/magento admin:user:create`. |
| 2007 | validate-config | Mettre à jour la version php vers la version recommandée |  |
| 2008 | validate-config | La prise en charge de Solr a été abandonnée dans Adobe Commerce et Magento Open Source 2.1. |  |
| 2009 | validate-config | Solr n’est plus pris en charge par Adobe Commerce et Magento Open Source 2.2 ou version ultérieure. |  |
| 2010 | validate-config | Le service Elasticsearch est installé sur la couche d’infrastructure, mais il n’est pas utilisé comme moteur de recherche. | Envisagez de supprimer le service Elasticsearch de la couche d’infrastructure afin d’optimiser l’utilisation des ressources. |
| 2011 | validate-config | La version de service Elasticsearch sur la couche d’infrastructure n’est pas compatible avec la version actuelle du module élasticsearch/élasticsearch, utilisé par votre application Adobe Commerce. |  |
| 2012 | validate-config | La configuration actuelle n’est pas compatible avec cette version d’Adobe Commerce |  |
| 2013 | validate-config | Options SCD ignorées car le processus de déploiement ne s’est pas exécuté lors de la phase de création. |  |
| 2014 | validate-config | La configuration contient des variables ou des valeurs obsolètes. |  |
| 2015 | validate-config | La configuration de l’environnement n’est pas valide |  |
| 2016 | validate-config | La configuration de type JSON ne peut pas être décodée |  |
| 2017 | validate-config | La configuration actuelle n’est pas compatible avec cette version d’Adobe Commerce |  |
| 2018 | validate-config | Certains services ont réussi la fin de vie |  |
| 2019 | validate-config | L’option de configuration de recherche MySQL est obsolète. | Utilisez Elasticsearch à la place. |
| 2029 | validate-config | La base de données partagée a été abandonnée dans Adobe Commerce et Magento Open Source 2.4.2 et sera supprimée dans la version 2.5. | Si vous utilisez une base de données partagée, vous devez commencer à planifier la restauration ou la migration vers une base de données unique ou utiliser une autre approche. |
| 2020 | install-update | L’installation d’Adobe Commerce s’est terminée, mais le fichier de configuration `app/etc/env.php` était manquant ou vide. | Les données requises seront restaurées à partir des configurations d’environnement et du fichier .magento.env.yaml . |
| 2021 | install-update:db-connection | Pour les bases de données partagées utilisant des connexions personnalisées |  |
| 2022 | install-update:db-connection | Vous avez modifié la configuration de la base de données, qui n’est pas compatible avec la connexion esclave. |  |
| 2023 | install-update:split-db | L&#39;activation d&#39;une base de données partagée sera ignorée. |  |
| 2024 | install-update:split-db | La configuration de la variable SPLIT_DB est manquante pour les types de connexions partagés. |  |
| 2025 | install-update:split-db | Connexion esclave non définie. |  |
| 2026 | pre-deploy:restore-write-dirs | Échec de la restauration de certaines données générées pendant la phase de création dans les répertoires montés | Pour plus d’informations, consultez le `cloud.log` . |
| 2027 | validate-config:mage-mode-variable | Valeur de mode pour la variable d’environnement MAGE_MODE non prise en charge | Supprimez la variable d’environnement MAGE_MODE ou remplacez sa valeur par &quot;production&quot;. Adobe Commerce sur l’infrastructure cloud prend uniquement en charge le mode &quot;production&quot;. |
| 2028 | remote-storage | Le stockage à distance n’a pas pu être activé. | Vérifiez les informations d’identification du stockage distant. |
| 2030 | validate-config | Les services Elasticsearch et OpenSearch sont tous deux installés sur la couche d’infrastructure. Adobe Commerce et Magento Open Source 2.4.4 et versions ultérieures utilisent OpenSearch par défaut. | Envisagez de supprimer l’Elasticsearch ou le service OpenSearch de la couche d’infrastructure afin d’optimiser l’utilisation des ressources. |

### Étape de déploiement de Post

| Code d’erreur | Étape de déploiement de Post | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 3001 | validate-config | La journalisation du débogage est activée dans Adobe Commerce | Pour économiser de l’espace disque, n’activez pas la journalisation de débogage pour vos environnements de production. |
| 3002 | chauffage | Impossible de récupérer les URL de magasin |  |
| 3003 | chauffage | Impossible de récupérer l’URL du magasin |  |
| 3004 | sauvegarde | Impossible de créer les fichiers de sauvegarde |  |

### Général

| Code d’erreur | Étape générale | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 4001 |  | Impossible d’obtenir le nombre de processeurs du système : |  |
