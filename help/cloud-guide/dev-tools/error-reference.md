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

Tous les messages d’erreur critiques et d’avertissement qui surviennent lors du déploiement sont écrits dans les `var/log/cloud.log` et `/var/log/cloud.error.log` fichiers . Le fichier journal des erreurs du cloud contient uniquement des erreurs provenant du dernier déploiement. Un fichier vide indique un déploiement réussi sans erreur.

Dans le `cloud.error.log` chaque entrée est formatée sous la forme d’une chaîne JSON pour une analyse plus facile :

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Les messages d’erreur sont classés selon l’une des étapes de déploiement : création, déploiement et post-déploiement. Chaque section fournit une liste des erreurs associées avec les informations suivantes pour chaque erreur :

- **Code d’erreur**: identifiant attribué par Adobe Commerce pour le message d’erreur
- **Évaluation**: indique si l’erreur s’est produite pendant l’étape de création, de déploiement ou de post-déploiement
- **Étape**: indique l’étape du scénario de déploiement qui peut renvoyer l’erreur. Si la variable _Étape_ n’est pas renseignée, l’erreur est une erreur générale qui peut être renvoyée par plusieurs étapes ou lors d’opérations de prétraitement. Voir [Déploiement basé sur des scénarios](../deploy/scenario-based.md) pour plus d’informations sur les étapes de création, de déploiement et de post-déploiement.
- **Suggestion**: fournit des conseils pour dépanner et résoudre l’erreur ;
- **Titre (description de l’erreur)**: description qui résume la cause de l’erreur.
- **Type**: indique si l’erreur est une erreur critique ou un avertissement

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Erreurs critiques

Les erreurs critiques indiquent un problème avec Commerce sur la configuration du projet d’infrastructure cloud qui entraîne l’échec du déploiement, par exemple une configuration incorrecte, non prise en charge ou une configuration manquante pour les paramètres requis. Avant de pouvoir déployer, vous devez mettre à jour la configuration pour résoudre ces erreurs.

### Etape de création

| Code d’erreur | Etape de création | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 2 |  | Impossible d’écrire dans le `./app/etc/env.php` fichier | Le script de déploiement ne peut pas apporter les modifications requises au `/app/etc/env.php` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 3 |  | La configuration n’est pas définie dans la variable `schema.yaml` fichier | La configuration n’est pas définie dans la variable `./vendor/magento/ece-tools/config/schema.yaml` fichier . Vérifiez que le nom de la variable de configuration est correct et défini. |
| 4 |  | Échec de l’analyse de la variable `.magento.env.yaml` fichier | La variable `./.magento.env.yaml` format de fichier non valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 5 |  | Impossible de lire le `.magento.env.yaml` fichier | Impossible de lire le `./.magento.env.yaml` fichier . Vérifiez les autorisations de fichier. |
| 6 |  | Impossible de lire le `.schema.yaml` fichier | Impossible de lire le `./vendor/magento/ece-tools/config/magento.env.yaml` fichier . Vérifiez les autorisations de fichier et redéployez (`magento-cloud environment:redeploy`). |
| 7 | refresh-modules | Impossible d’écrire dans le `./app/etc/config.php` fichier | Le script de déploiement ne peut pas apporter les modifications requises au `/app/etc/config.php` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 8 | validate-config | Impossible de lire le `composer.json` fichier | Impossible de lire le `./composer.json` fichier . Vérifiez les autorisations de fichier. |
| 9 | validate-config | La variable `composer.json` fichier manquant : section de chargement automatique requise | Obligatoire `autoload` est absente de la section `composer.json` fichier . Comparez la section Chargement automatique à la section `composer.json` dans le modèle Cloud et ajoutez la configuration manquante. |
| 10 | validate-config | La variable `.magento.env.yaml` Le fichier contient une option qui n’est pas déclarée dans le schéma, ou une option configurée avec une valeur ou une étape non valide | La variable `./.magento.env.yaml` contient une configuration non valide. Consultez le journal des erreurs pour obtenir des informations détaillées. |
| 11 | refresh-modules | La commande a échoué : `/bin/magento module:enable --all` | Essayer d’exécuter `composer update` localement. Ensuite, validez et envoyez la mise à jour `composer.lock` fichier . Vérifiez également la variable `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 12 | apply-Correctifs | Échec de l’application du correctif |  |
| 13 | set-report-dir-imbrication-level | Impossible d’écrire dans le fichier `/pub/errors/local.xml` |  |
| 14 | copy-sample-data | Échec de la copie des fichiers de données d’exemple |  |
| 15 | compile-di | La commande a échoué : `/bin/magento setup:di:compile` | Vérifiez les `cloud.log` pour plus d’informations. Ajouter `VERBOSE_COMMANDS: '-vvv'` into `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 16 | dump-autoload | La commande a échoué : `composer dump-autoload` | La variable `composer dump-autoload` échec de la commande . Vérifiez les `cloud.log` pour plus d’informations. |
| 17 | run-baler | Commande à exécuter `Baler` Échec du regroupement pour Javascript | Vérifiez les `SCD_USE_BALER` pour vérifier que le module Baler est configuré et activé pour le regroupement JS. Si vous n’avez pas besoin du module Baler, définissez `SCD_USE_BALER: false`. |
| 18 | compress-static-content | Utilitaire requis introuvable (timeout, bash) |  |
| 19 | deploy-static-content | Commande `/bin/magento setup:static-content:deploy` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 20 | compress-static-content | Échec de la compression de contenu statique | Vérifiez les `cloud.log` pour plus d’informations. |
| 21 | backup-data: static-content | Échec de la copie du contenu statique dans la variable `init` directory | Vérifiez les `cloud.log` pour plus d’informations. |
| 22 | backup-data: write-able-dirs | Échec de la copie de certains répertoires modifiables dans le `init` directory | Échec de la copie des répertoires modifiables dans le `./init` dossier. Vérifiez les autorisations de votre système de fichiers. |
| 23 |  | Impossible de créer un objet journal |  |
| 24 | backup-data: static-content | Echec du nettoyage de la variable `./init/pub/static/` directory | Échec du nettoyage `./init/pub/static` dossier. Vérifiez les autorisations de votre système de fichiers. |
| 25 |  | Impossible de trouver le package du compositeur | Si vous avez installé la version de l’application Adobe Commerce directement à partir du référentiel GitHub, vérifiez que la variable `DEPLOYED_MAGENTO_VERSION_FROM_GIT` La variable d’environnement est configurée. |
| 26 | validate-config | Supprimez la configuration du module Braintree Magento qui n’est plus prise en charge dans Adobe Commerce et les versions 2.4 et ultérieures de Magento Open Source. | La prise en charge du module de Braintree n’est plus incluse dans Magento 2.4.0 et versions ultérieures. Supprimez la variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL de la section variables de la variable `.magento.app.yaml` fichier . Pour l’aide au paiement des Braintree, utilisez plutôt une extension officielle du Commerce Marketplace. |

### Déploiement de l’étape

| Code d’erreur | Étape de déploiement | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 101 | pré-déploiement : cache | Configuration de cache incorrecte (port ou hôte manquant) | Paramètres requis manquants pour la configuration du cache `server` ou `port`. Vérifiez les `cloud.log` pour plus d’informations. |
| 102 |  | Impossible d’écrire dans le `./app/etc/env.php` fichier | Le script de déploiement ne peut pas apporter les modifications requises au `/app/etc/env.php` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 103 |  | La configuration n’est pas définie dans la variable `schema.yaml` fichier | La configuration n’est pas définie dans la variable `./vendor/magento/ece-tools/config/schema.yaml` fichier . Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 104 |  | Échec de l’analyse de la variable `.magento.env.yaml` fichier | La configuration n’est pas définie dans la variable `./vendor/magento/ece-tools/config/schema.yaml` fichier . Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 105 |  | Impossible de lire le `.magento.env.yaml` fichier | Impossible de lire le `./.magento.env.yaml` fichier . Vérifiez les autorisations de fichier. |
| 106 |  | Impossible de lire le `.schema.yaml` fichier |  |
| 107 | pre-deploy: clean-redis-cache | Échec du nettoyage du cache Redis | Échec du nettoyage du cache Redis. Vérifiez que la configuration du cache Redis est correcte et que le service Redis est disponible. Voir [Configurer le service Redis](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/redis.html). |
| 108 | pré-déploiement : set-production-mode | Commande `/bin/magento maintenance:enable` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 109 | validate-config | Configuration de base de données incorrecte | Vérifiez que la variable `DATABASE_CONFIGURATION` La variable d’environnement est correctement configurée. |
| 110 | validate-config | Configuration de session incorrecte | Vérifiez que la variable `SESSION_CONFIGURATION` La variable d’environnement est correctement configurée. La configuration doit contenir au moins les `save` . |
| 111 | validate-config | Configuration de recherche incorrecte | Vérifiez que la variable `SEARCH_CONFIGURATION` La variable d’environnement est correctement configurée. La configuration doit contenir au moins les `engine` . |
| 112 | validate-config | Configuration de ressource incorrecte | Vérifiez que la variable `RESOURCE_CONFIGURATION` La variable d’environnement est correctement configurée. La configuration doit contenir au moins `connection` . |
| 113 | validate-config:élasticsuite-integrity | ElasticSuite est installé, mais le service Elasticsearch n’est pas disponible | Vérifiez que la variable `SEARCH_CONFIGURATION` La variable d’environnement est configurée correctement et vérifiez que le service Elasticsearch est disponible. |
| 114 | validate-config:élasticsuite-integrity | ElasticSuite est installé, mais un autre moteur de recherche est utilisé | ElasticSuite est installé, mais un autre moteur de recherche est configuré. Mettez à jour le `SEARCH_CONFIGURATION` pour activer Elasticsearch et vérifier la configuration du service Elasticsearch dans la variable `services.yaml` fichier . |
| 115 |  | Échec de l’exécution des requêtes de base de données |  |
| 116 | install-update: setup | Commande `/bin/magento setup:install` failed | Vérifiez les `cloud.log` et `install_upgrade.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 117 | install-update: config-import | Commande `app:config:import` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 118 |  | Utilitaire requis introuvable (timeout, bash) |  |
| 119 | install-update: deploy-static-content | Commande `/bin/magento setup:static-content:deploy` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 120 | compress-static-content | Échec de la compression de contenu statique | Vérifiez les `cloud.log` pour plus d’informations. |
| 121 | deploy-static-content:generate | Impossible de mettre à jour la version déployée | Impossible de mettre à jour la variable `./pub/static/deployed_version.txt` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 122 | clean-static-content | Échec du nettoyage des fichiers de contenu statique |  |
| 123 | install-update: split-db | Commande `/bin/magento setup:db-schema:split` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 124 | clean-view-preprocessed | Echec du nettoyage de la variable `var/view_preprocessed` folder | Impossible de nettoyer le `./var/view_preprocessed` dossier. Vérifiez les autorisations de votre système de fichiers. |
| 125 | install-update: reset-password | Échec de la mise à jour du `/var/credentials_email.txt` fichier | Échec de la mise à jour du `/var/credentials_email.txt` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 126 | install-update: update | Commande `/bin/magento setup:upgrade` failed | Vérifiez les `cloud.log` et `install_upgrade.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 127 | clean-cache | Commande `/bin/magento cache:flush` failed | Vérifiez les `cloud.log` pour plus d’informations. Pour une sortie de commande plus détaillée, ajoutez le `VERBOSE_COMMANDS: '-vvv'` à l’option `.magento.env.yaml` fichier . |
| 128 | disable-maintenance-mode | Commande `/bin/magento maintenance:disable` failed | Vérifiez les `cloud.log` pour plus d’informations. Ajouter `VERBOSE_COMMANDS: '-vvv'` into `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 129 | install-update: reset-password | Impossible de lire le modèle de réinitialisation de mot de passe |  |
| 130 | install-update: cache_type | La commande a échoué : `php ./bin/magento cache:enable` | Commande `php ./bin/magento cache:enable` s’exécute uniquement lorsque Adobe Commerce a été installé, mais `./app/etc/env.php` était absent ou vide au début du déploiement. Vérifiez les `cloud.log` pour plus d’informations. Ajouter `VERBOSE_COMMANDS: '-vvv'` into `.magento.env.yaml` pour une sortie de commande plus détaillée. |
| 131 | install-update | La variable `crypt/key`  La valeur de clé n’existe pas dans la variable `./app/etc/env.php` ou le fichier `CRYPT_KEY` variable d’environnement cloud | Cette erreur se produit si la variable `./app/etc/env.php` n’est pas présent au début du déploiement d’Adobe Commerce ou si la variable `crypt/key` n’est pas définie. Si vous avez migré la base de données à partir d’un autre environnement, récupérez la valeur de la clé crypt de cet environnement. Ajoutez ensuite la valeur à la variable [CRYPT_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#crypt_key) variable d’environnement cloud dans votre environnement actuel. Voir [Clé de chiffrement Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/overview.html#gather-credentials). Si vous avez accidentellement supprimé le `./app/etc/env.php` , utilisez la commande suivante pour la restaurer à partir des fichiers de sauvegarde créés à partir d’un déploiement précédent : `./vendor/bin/ece-tools backup:restore` Commande de l’interface de ligne de commande .&quot; |
| 132 |  | Impossible de se connecter au service Elasticsearch | Recherchez des informations d’identification d’Elasticsearch valides et vérifiez que le service est en cours d’exécution. |
| 137 |  | Connexion impossible au service OpenSearch | Recherchez des informations d’identification OpenSearch valides et vérifiez que le service est en cours d’exécution. |
| 133 | validate-config | Supprimez la configuration du module Braintree Magento qui n’est plus prise en charge dans Adobe Commerce ou les versions 2.4 et ultérieures de Magento Open Source. | La prise en charge du module Braintree n’est plus incluse dans Adobe Commerce ou Magento Open Source 2.4.0 et versions ultérieures. Supprimez la variable CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL de la section variables de la variable `.magento.app.yaml` fichier . Pour la prise en charge des Braintree, utilisez plutôt une extension de paiement Braintree officielle du Commerce Marketplace . |
| 134 | validate-config | Adobe Commerce et Magento Open Source 2.4.0 nécessitent l’installation du service Elasticsearch | Installation du service Elasticsearch |
| 138 | validate-config | Adobe Commerce et Magento Open Source 2.4.4 nécessitent l’installation d’OpenSearch ou du service Elasticsearch | Installation du service OpenSearch |
| 135 | validate-config | Le moteur de recherche doit être défini sur Elasticsearch pour Adobe Commerce et Magento Open Source >= 2.4.0 | Vérifiez la variable SEARCH_CONFIGURATION pour la variable `engine` . S’il est configuré, supprimez l’option ou définissez la valeur sur &quot;élasticsearch&quot;. |
| 136 | validate-config | La base de données partagée a été supprimée à partir d’Adobe Commerce et de Magento Open Source 2.5.0. | Si vous utilisez une base de données partagée, vous devez restaurer ou migrer vers une base de données unique ou utiliser une autre approche. |
| 139 | validate-config | Moteur de recherche incorrect | Cette version d’Adobe Commerce ou de Magento Open Source ne prend pas en charge OpenSearch. Vous devez utiliser les versions 2.3.7-p3, 2.4.3-p2 ou ultérieures. |

### Etape post-déploiement

| Code d’erreur | Étape post-déploiement | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 201 | is-deploy-failed | Échec du déploiement de l’étape |  |
| 202 |  | La variable `./app/etc/env.php` Le fichier n’est pas modifiable | Le script de déploiement ne peut pas apporter les modifications requises au `/app/etc/env.php` fichier . Vérifiez les autorisations de votre système de fichiers. |
| 203 |  | La configuration n’est pas définie dans la variable `schema.yaml` fichier | La configuration n’est pas définie dans la variable `./vendor/magento/ece-tools/config/schema.yaml` fichier . Vérifiez que le nom de la variable de configuration est correct et qu’il est défini. |
| 204 |  | Échec de l’analyse de la variable `.magento.env.yaml` fichier | La variable `./.magento.env.yaml` format de fichier non valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 205 |  | Impossible de lire le `.magento.env.yaml` fichier | Vérifiez les autorisations de fichier. |
| 206 |  | Impossible de lire le `.schema.yaml` fichier |  |
| 207 | chauffage | Échec du préchargement de certaines pages de mise à niveau |  |
| 208 | time-to-firs-byte | Échec du test du temps jusqu’au premier octet (TTF) |  |
| 227 | clean-cache | Commande `/bin/magento cache:flush` failed | Vérifiez les `cloud.log` pour plus d’informations. Ajouter `VERBOSE_COMMANDS: '-vvv'` into `.magento.env.yaml` pour une sortie de commande plus détaillée. |

### Général

| Code d’erreur | Étape générale | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 243 |  | La configuration n’est pas définie dans la variable `schema.yaml` fichier | Vérifiez que le nom de la variable de configuration est correct et qu’il a été défini. |
| 244 |  | Échec de l’analyse de la variable `.magento.env.yaml` fichier | La variable `./.magento.env.yaml` format de fichier non valide. Utilisez un analyseur YAML pour vérifier la syntaxe et corriger les erreurs. |
| 245 |  | Impossible de lire le `.magento.env.yaml` fichier | Impossible de lire le `./.magento.env.yaml` fichier . Vérifiez les autorisations de fichier. |
| 246 |  | Impossible de lire le `.schema.yaml` fichier |  |
| 247 |  | Impossible de générer un module pour l’événement | Vérifiez les `cloud.log` pour plus d’informations. |
| 248 |  | Impossible d’activer un module pour l’événement | Vérifiez les `cloud.log` pour plus d’informations. |
| 249 |  | Échec de la génération du module AdobeCommerceWebhookPlugins | Vérifiez les `cloud.log` pour plus d’informations. |
| 250 |  | Échec de l’activation du module AdobeCommerceWebhookPlugins | Vérifiez les `cloud.log` pour plus d’informations. |

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
| 2006 | validate-config | L’utilisateur administrateur n’a pas été créé, car l’email administrateur n’a pas été défini. | Après l’installation, vous pouvez créer manuellement un utilisateur administrateur : utilisez ssh pour vous connecter à votre environnement. Ensuite, exécutez le `bin/magento admin:user:create` . |
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
| 2020 | install-update | L’installation d’Adobe Commerce est terminée, mais la variable `app/etc/env.php` le fichier de configuration était manquant ou vide. | Les données requises seront restaurées à partir des configurations d’environnement et du fichier .magento.env.yaml . |
| 2021 | install-update:db-connection | Pour les bases de données partagées utilisant des connexions personnalisées |  |
| 2022 | install-update:db-connection | Vous avez modifié la configuration de la base de données, qui n’est pas compatible avec la connexion esclave. |  |
| 2023 | install-update:split-db | L&#39;activation d&#39;une base de données partagée sera ignorée. |  |
| 2024 | install-update:split-db | La configuration de la variable SPLIT_DB est manquante pour les types de connexions partagés. |  |
| 2025 | install-update:split-db | Connexion esclave non définie. |  |
| 2026 | pre-deploy:restore-write-dirs | Échec de la restauration de certaines données générées pendant la phase de création dans les répertoires montés | Vérifiez les `cloud.log` pour plus d’informations. |
| 2027 | validate-config:mage-mode-variable | Valeur de mode pour la variable d’environnement MAGE_MODE non prise en charge | Supprimez la variable d’environnement MAGE_MODE ou remplacez sa valeur par &quot;production&quot;. Adobe Commerce sur l’infrastructure cloud prend uniquement en charge le mode &quot;production&quot;. |
| 2028 | remote-storage | Le stockage à distance n’a pas pu être activé. | Vérifiez les informations d’identification du stockage distant. |
| 2030 | validate-config | Les services Elasticsearch et OpenSearch sont tous deux installés sur la couche d’infrastructure. Adobe Commerce et Magento Open Source 2.4.4 et versions ultérieures utilisent OpenSearch par défaut. | Envisagez de supprimer l’Elasticsearch ou le service OpenSearch de la couche d’infrastructure afin d’optimiser l’utilisation des ressources. |

### Etape post-déploiement

| Code d’erreur | Étape post-déploiement | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 3001 | validate-config | La journalisation du débogage est activée dans Adobe Commerce | Pour économiser de l’espace disque, n’activez pas la journalisation de débogage pour vos environnements de production. |
| 3002 | chauffage | Impossible de récupérer les URL de magasin |  |
| 3003 | chauffage | Impossible de récupérer l’URL du magasin |  |
| 3004 | sauvegarde | Impossible de créer les fichiers de sauvegarde |  |

### Général

| Code d’erreur | Étape générale | Description de l’erreur (titre) | Action suggérée |
| - | - | - | - |
| 4001 |  | Impossible d’obtenir le nombre de processeurs du système : |  |
