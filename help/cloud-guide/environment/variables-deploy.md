---
title: Déploiement de variables
description: Consultez la liste des variables d’environnement qui contrôlent les actions dans Adobe Commerce lors de la phase de déploiement de l’infrastructure cloud.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Déploiement de variables

Les éléments suivants _deploy_ contrôlent les actions lors de la phase de déploiement et peuvent hériter et remplacer des valeurs de la fonction [Variables globales](variables-global.md). Insérez ces variables dans le `deploy` étape de la `.magento.env.yaml` fichier :

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Pour plus d’informations sur la personnalisation du processus de création et de déploiement :

- [Configuration du déploiement](configure-env-yaml.md)
- [Processus de déploiement](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Configurez la page Redis et la mise en cache par défaut. Lors de la définition de la variable `cm_cache_backend_redis` , vous devez spécifier la variable `server`, `port`, et `database` options.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

L’exemple suivant fusionne de nouvelles valeurs avec une configuration existante :

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

L’exemple suivant utilise la méthode [Fonction de préchargement Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) comme défini dans la variable _Guide de configuration_:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Pour utiliser une [REDIS_BACKEND](#redis_backend) (et pas uniquement à partir de la liste autorisée), définissez la variable `_custom_redis_backend` option à `true` pour activer la validation correcte, comme dans l’exemple suivant :

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Par défaut**—`true`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Active ou désactive le nettoyage [fichiers de contenu statique](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) générés pendant la phase de création ou de déploiement. Utiliser la valeur par défaut _true_ dans le développement en tant que bonne pratique.

- **`true`**: supprime tout le contenu statique existant avant de déployer le contenu statique mis à jour.
- **`false`**: le déploiement remplace uniquement les fichiers de contenu statique existants si le contenu généré contient une version plus récente.

Si vous modifiez du contenu statique par le biais d’un processus distinct, définissez la valeur sur _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

L’échec du nettoyage des fichiers d’affichage statiques avant le déploiement peut entraîner des problèmes si vous déployez des mises à jour vers des fichiers existants sans supprimer les versions précédentes. En raison de [secours de fichier statique](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) règles, les opérations de secours peuvent afficher un fichier incorrect si le répertoire contient plusieurs versions du même fichier.

## `CRON_CONSUMERS_RUNNER`

- **Par défaut**—`cron_run = false`, `max_messages = 1000`
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Utilisez cette variable d’environnement pour confirmer que les files d’attente de messages s’exécutent après un déploiement.

- `cron_run`: valeur booléenne qui active ou désactive la variable `consumers_runner` tâche cron (par défaut = `false`).
- `max_messages`—Un nombre spécifiant le nombre maximal de messages que chaque consommateur doit traiter avant de s’arrêter (par défaut = `1000`). Vous pouvez définir la valeur sur `0` pour empêcher le consommateur de s’arrêter.
- `consumers`: un tableau de chaînes spécifiant les consommateurs à exécuter. Un tableau vide s’exécute. _all_ consommateurs.

- `multiple_processes`-Un nombre spécifiant le nombre de processus à générer pour chaque consommateur. Pris en charge dans Commerce **2.4.4** ou supérieur.

>[!NOTE]
>
>Pour renvoyer une liste de files de messages `consumers`, exécutez le `./bin/magento queue:consumers:list` dans l’environnement distant.

Exemple de tableau qui exécute des `consumers` et la variable `multiple_processes` pour générer pour chaque consommateur :

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Exemple de tableau vide qui exécute tout `consumers`:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Par défaut, le processus de déploiement remplace tous les paramètres du `env.php` fichier . Voir [Gestion des files d’attente de messages](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) dans le _Guide de configuration de Commerce_ pour Adobe Commerce sur site.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Configuration de `consumers` traitez les messages de la file d’attente des messages en sélectionnant l’une des options suivantes :

- `false`—`Consumers` traitez les messages disponibles dans la file d’attente, fermez la connexion TCP, puis arrêtez-la. `Consumers` n’attendez pas que des messages supplémentaires entrent dans la file d’attente, même si le nombre de messages traités est inférieur à la valeur `max_messages` spécifiée dans la variable `CRON_CONSUMERS_RUNNER` Variable de déploiement.

- `true`—`Consumers` continuer à traiter les messages de la file d’attente des messages jusqu’à atteindre le nombre maximum de messages (`max_messages`) spécifié dans la variable `CRON_CONSUMERS_RUNNER` déploie la variable avant de fermer la connexion TCP et d’interrompre le processus client. Si la file d’attente se vide avant d’atteindre `max_messages`, le consommateur attend que d’autres messages arrivent.

>[!WARNING]
>
>Si vous utilisez des objets Worker pour exécuter `consumers` au lieu d’utiliser une tâche cron, définissez cette variable sur true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

>[!WARNING]
>
>Définissez la variable `CRYPT_KEY` au moyen de la variable [!DNL Cloud Console] au lieu de `.magento.env.yaml` pour éviter d’exposer la clé dans le référentiel de code source de votre environnement. Voir [Définition des variables d’environnement et de projet](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

Lorsque vous déplacez la base de données d’un environnement à un autre sans processus d’installation, vous avez besoin des informations cryptographiques correspondantes. Adobe Commerce utilise la valeur de clé de chiffrement définie dans la variable [!DNL Cloud Console] comme la propriété `crypt/key` dans la variable `env.php` fichier .

## `DATABASE_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Si vous avez défini une base de données dans la variable [propriété relations](../application/properties.md#relationships) de `.magento.app.yaml` , vous pouvez personnaliser les connexions de votre base de données pour le déploiement.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

L’exemple suivant fusionne de nouvelles valeurs avec une configuration existante :

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

Vous pouvez également configurer un préfixe de tableau.

>[!WARNING]
>
>Si vous n’utilisez pas l’option de fusion avec le préfixe de tableau, vous devez fournir les paramètres de connexion par défaut, sinon la validation du déploiement échoue.

L’exemple suivant utilise la méthode `ece_` préfixe de tableau avec les paramètres de connexion par défaut au lieu d’utiliser la variable `_merge` option :

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Exemple de sortie :

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Conserve la personnalisation [!DNL Elastic Suite] Paramètres du service entre les déploiements et l’utilise dans la section &quot;system/default/smile_élasticsuite_core_base_settings&quot; de la section principale [!DNL Elastic Suite] configuration. Si la variable [!DNL Elastic Suite] Le package de compositeur est installé, il est configuré automatiquement.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

L’exemple suivant fusionne une nouvelle valeur avec la configuration existante :

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Limites connues**:

- Remplacer le moteur de recherche par un autre type que `elasticsuite` provoque un échec de déploiement accompagné d’une erreur de validation appropriée.
- La suppression du service Elasticsearch entraîne un échec de déploiement accompagné d’une erreur de validation appropriée.

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation ou le dépannage de la variable [!DNL Elastic Suite] avec Adobe Commerce, voir la section [[!DNL Elastic Suite] documentation](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Active et désactive les Google Analytics lors du déploiement dans les environnements d’évaluation et d’intégration. Par défaut, le paramètre Google Analytics est défini sur true uniquement pour l’environnement de production. Définissez cette valeur sur `true` pour activer les Google Analytics dans les environnements d’évaluation et d’intégration.

- **`true`**: active les Google Analytics dans les environnements d’évaluation et d’intégration.
- **`false`**: désactive les Google Analytics dans les environnements d’évaluation et d’intégration.

Ajoutez la variable `ENABLE_GOOGLE_ANALYTICS` de la variable d’environnement `deploy` dans la `.magento.env.yaml` fichier :

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Le processus de déploiement active toujours les Google Analytics dans les environnements de production.

## `FORCE_UPDATE_URLS`

- **Par défaut**—`true`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Lors du déploiement dans les environnements Pro ou Starter Staging et Production, cette variable remplace les URL de base Adobe Commerce dans la base de données par les URL de projet spécifiées par la variable [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) Variable . Utilisez ce paramètre pour remplacer le comportement par défaut de la variable [UPDATE_URLS](#update_urls) Variable deploy, qui est ignorée lors du déploiement dans les environnements d’évaluation ou de production.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Par défaut**—`file`
- **Version**—Adobe Commerce 2.2.5 et versions ultérieures

Le fournisseur de verrouillage empêche le lancement de tâches cron en double et de groupes cron. Utilisez la variable `file` fournisseur de verrouillage dans l’environnement de production. Les environnements de démarrage et l’environnement d’intégration Pro n’utilisent pas la variable [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) , etc. `ece-tools` applique la variable `db` fournisseur de verrouillage automatiquement.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Voir [Configuration du verrouillage](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) dans le _Guide d’installation_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

>[!TIP]
>
>La variable `MYSQL_USE_SLAVE_CONNECTION` n’est prise en charge que sur Adobe Commerce dans les environnements de grappe d’infrastructure cloud Staging et Production Pro et n’est pas prise en charge dans les projets de démarrage.

Adobe Commerce peut lire plusieurs bases de données de manière asynchrone. Définissez sur . `true` pour utiliser automatiquement un _lecture seule_ connexion à la base de données pour recevoir du trafic en lecture seule sur un noeud non maître. Cette connexion améliore les performances grâce à l’équilibrage de charge, car un seul noeud traite le trafic lecture-écriture. Définissez sur . `false` pour supprimer tout tableau de connexion en lecture seule existant du `env.php` fichier .

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Lorsque la variable `MYSQL_USE_SLAVE_CONNECTION` est définie sur `true`, la variable `synchronous_replication` est défini sur `true` par défaut dans le `env.php` sur les environnements d’évaluation et de production Pro. Lorsque la variable `MYSQL_USE_SLAVE_CONNECTION` est défini sur `false`, la variable `synchronous_replication` n’est pas configuré.

## `QUEUE_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Utilisez cette variable d’environnement pour conserver les paramètres de service AMQP personnalisés entre les déploiements. Par exemple, si vous préférez utiliser un service de file d’attente de messages existant plutôt que de vous fier à l’infrastructure cloud pour le créer, utilisez la variable `QUEUE_CONFIGURATION` pour la connecter à votre site :

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

L’exemple suivant fusionne de nouvelles valeurs avec une configuration existante :

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Par défaut**—`Cm_Cache_Backend_Redis`
- **Version**—Adobe Commerce 2.3.0 et versions ultérieures

Spécifie la configuration du modèle principal pour le cache Redis.

Adobe Commerce version 2.3.0 et ultérieure comprend les modèles principaux suivants :

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

L’exemple de définition de `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Si vous spécifiez `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` comme modèle d’arrière-plan Redis à activer [Cache L2](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html), `ece-tools` génère automatiquement la configuration du cache. Voir un exemple [fichier de configuration](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) dans le _Guide de configuration d’Adobe Commerce_. Pour remplacer la configuration de cache générée, utilisez la méthode [CACHE_CONFIGURATION](#cache_configuration) Variable de déploiement.

## `REDIS_USE_SLAVE_CONNECTION`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.1.16 et versions ultérieures

>[!WARNING]
>
>Do _not_ Activez cette variable sur une [architecture mise à l’échelle](../architecture/scaled-architecture.md) projet. Cela entraîne des erreurs de connexion Redis. Les esclaves Redis sont toujours actifs mais ne sont pas utilisés pour les lectures Redis. Adobe recommande d’utiliser Adobe Commerce 2.3.5 ou version ultérieure, de mettre en oeuvre une nouvelle configuration de serveur principal Redis et de mettre en cache L2 pour Redis.

>[!TIP]
>
>La variable `REDIS_USE_SLAVE_CONNECTION` n’est prise en charge que sur Adobe Commerce dans les environnements de grappe d’infrastructure cloud Staging et Production Pro et n’est pas prise en charge dans les projets de démarrage.

Adobe Commerce peut lire plusieurs instances Redis de manière asynchrone. Définissez sur . `true` pour utiliser automatiquement un _lecture seule_ connexion à une instance Redis pour recevoir du trafic en lecture seule sur un noeud non maître. Cette connexion améliore les performances grâce à l’équilibrage de charge, car un seul noeud traite le trafic lecture-écriture. Définissez sur . `false` pour supprimer tout tableau de connexion en lecture seule existant du `env.php` fichier .

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Un service Redis doit être configuré dans la variable `.magento.app.yaml` et dans le fichier `services.yaml` fichier .

[CEE-Outils version 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) et plus tard utilise des paramètres plus tolérants aux erreurs. Si Adobe Commerce ne peut pas lire les données des Redis _esclave_ , puis il lit les données du Redis _master_ instance.

La connexion en lecture seule n’est pas disponible dans l’environnement d’intégration ou si vous utilisez le [`CACHE_CONFIGURATION` variable](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **Par défaut**—Not set
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Mappe un nom de ressource à une connexion à la base de données ; Ce paramétrage correspond au `resource` de la `env.php` fichier .

{{merge-options}}

L’exemple suivant fusionne de nouvelles valeurs avec une configuration existante :

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Par défaut**—`4`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Spécifie [gzip](https://www.gnu.org/software/gzip) niveau de compression (`0` to `9`) à utiliser lors de la compression de contenu statique ; `0` désactive la compression.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Par défaut**—`600`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Lorsque le temps nécessaire à la compression des ressources statiques dépasse la limite du délai d’expiration de compression, cela interrompt le processus de déploiement. Définissez la durée d’exécution maximale, en secondes, de la commande de compression de contenu statique.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Vous pouvez configurer plusieurs paramètres régionaux par thème. Cette personnalisation accélère le processus de déploiement en réduisant le nombre de fichiers de thème inutiles. Vous pouvez, par exemple, déployer le _magento/backend_ en anglais et un thème personnalisé dans d’autres langues.

L’exemple suivant déploie le `Magento/backend` thème avec trois paramètres régionaux :

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Vous pouvez également choisir de _not_ déployer un thème :

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Permet d’augmenter le temps d’exécution maximum prévu pour le déploiement de contenu statique.

Par défaut, Adobe Commerce définit l’exécution maximale prévue à 900 secondes, mais dans certains cas, il peut s’avérer nécessaire de consacrer plus de temps au déploiement de contenu statique pour un projet Cloud.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.4.2 et versions ultérieures

Lors de la phase de déploiement, définissez `SCD_NO_PARENT: true` de sorte que la génération du contenu statique pour les thèmes parents ne se produise pas pendant la phase de déploiement. Ce paramètre réduit le temps de déploiement et évite les temps d’arrêt du site qui peuvent se produire si la génération de contenu statique échoue pendant le déploiement. Voir [Déploiement de contenu statique](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Par défaut**—`quick`
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Permet de personnaliser les [stratégie de déploiement](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) pour le contenu statique. Voir [Déploiement de fichiers d’affichage statique](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Utiliser ces options _only_ si vous avez plusieurs paramètres régionaux :

- `standard`: déploie tous les fichiers d’affichage statique pour tous les modules.
- `quick`—(_default_) réduit le temps de déploiement.
- `compact`: conserve l’espace disque sur le serveur. Dans Adobe Commerce version 2.2.4 et antérieure, ce paramètre remplace la valeur de `scd_threads` avec la valeur de `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Par défaut**—Automatique
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définit le nombre de threads pour le déploiement de contenu statique. La valeur par défaut est définie en fonction du nombre de threads du processeur détecté et ne dépasse pas une valeur de 4. L’augmentation du nombre de threads accélère le déploiement de contenu statique ; la réduction du nombre de threads la ralentit. Vous pouvez définir la valeur de thread, par exemple :

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Pour réduire davantage le temps de déploiement, utilisez [Gestion des configurations](../store/store-settings.md) avec la propriété `scd-dump` pour déplacer le déploiement statique dans la phase de génération.

## `SEARCH_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Utilisez cette variable d’environnement pour conserver les paramètres de service de recherche personnalisés entre les déploiements. Par exemple :

Configuration Elasticsearch :

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: elasticsearch
     elasticsearch_server_hostname: http://elasticsearch.internal
     elasticsearch_server_port: '9200'
     elasticsearch_index_prefix: magento2
     elasticsearch_server_timeout: '15'
```

Configuration OpenSearch (pour Commerce 2.4.6 et versions ultérieures) :

```yaml
stage:
  deploy:
   SEARCH_CONFIGURATION:
     engine: opensearch
     opensearch_server_hostname: 'http://opensearch.internal'
     opensearch_server_port: '9200'
     opensearch_index_prefix: 'magento2'
     opensearch_server_timeout: '15'
```

{{merge-options}}

L’exemple suivant fusionne une nouvelle valeur avec la configuration existante :

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Configurez le stockage de la session Redis. Nécessite le `save`, `redis`, `host`, `port`, et `database` options de la variable de stockage de session. Par exemple :

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

L’exemple suivant fusionne une nouvelle valeur avec la configuration existante :

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Par défaut**— _Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définissez sur . `true` pour ignorer le déploiement du contenu statique pendant la phase de déploiement.

Lors de la phase de déploiement, définissez `SKIP_SCD: true` afin que la création de contenu statique ne se produise pas pendant la phase de déploiement. Ce paramètre réduit le temps de déploiement et évite les temps d’arrêt du site qui peuvent se produire si la génération de contenu statique échoue pendant le déploiement. Voir [Déploiement de contenu statique](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Par défaut**—`true`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Lors du déploiement, remplacez les URL de base Adobe Commerce dans la base de données par les URL de projet spécifiées par la variable [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) Variable . Cette configuration est utile pour le développement local, où les URL de base sont configurées pour votre environnement local. Lorsque vous effectuez un déploiement dans un environnement cloud, les URL sont mises à jour afin que vous puissiez accéder à votre storefront et à votre administrateur à l’aide des URL du projet.

Si vous devez mettre à jour les URL lors du déploiement dans les environnements Pro ou Starter Staging et Production, utilisez la variable [`FORCE_UPDATE_URLS`](#force_update_urls) Variable .

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Activez ou désactivez la variable [Symfony](https://symfony.com/doc/current/console/verbosity.html) niveau de détail du débogage pour `bin/magento` Commandes d’interface de ligne de commande exécutées lors de la phase de déploiement

>[!NOTE]
>
>Pour utiliser le paramètre VERBOSE_COMMANDS afin de contrôler le détail dans la sortie de commande pour les performances et les échecs `bin/magento` Commandes d’interface de ligne de commande, vous devez définir [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Sélectionnez le niveau de détail fourni dans les logs :

- `-v`= sortie normale
- `-vv`= sortie plus détaillée
- `-vvv` = sortie verbeuse idéale pour le débogage

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
