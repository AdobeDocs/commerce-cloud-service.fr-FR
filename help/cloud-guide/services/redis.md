---
title: Configuration du service Redis
description: Découvrez comment configurer et optimiser Redis en tant que solution de cache d’arrière-plan pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: 38c29e3a2cee1658bb73922f0f56fdfa84af5a6f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Configuration du service Redis

[Redis](https://redis.io) est une solution de cache d’arrière-plan facultative qui remplace Zend_Cache_Backend_File du Zend Framework, que Adobe Commerce utilise par défaut.

Voir [Configuration de Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) dans le _Guide de configuration_.

{{service-instruction}}

**Pour activer Redis** :

1. Ajoutez le nom et le type requis au fichier `.magento/services.yaml`.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Pour fournir votre propre configuration Redis, ajoutez une clé `core_config` dans votre fichier `.magento/services.yaml` :

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configurez les relations dans le fichier `.magento.app.yaml`.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Vérifiez les relations de service](services-yaml.md#service-relationships).

{{service-change-tip}}

## Utilisation de l’interface de ligne de commande Redis

En supposant que votre relation Redis soit nommée `redis`, vous pouvez y accéder à l’aide de l’outil `redis-cli`.

1. Utilisez SSH pour vous connecter à l’environnement d’intégration avec Redis installé et configuré.

1. Ouvrez un tunnel SSH vers un hôte.

   ```bash
   redis-cli -h redis.internal
   ```

## Obtenir la version de Redis installée

Utilisez la commande suivante pour installer la version Redis sur un environnement d’intégration :

```bash
redis-cli -h redis.internal info | grep version
```

Exemple de réponse :

```
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis sur l’évaluation et la production Pro

Pour installer la version Redis sur un environnement d&#39;évaluation ou de production, utilisez la commande `redis-server` :

```bash
redis-server -v
```

```
Redis server v=7.0.5 ...
```

Utilisez la commande suivante pour installer la configuration Redis dans un environnement d’évaluation ou de production Pro :

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Exemple de réponse :

```json
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Résolution des problèmes liés aux redis

Pour obtenir de l’aide sur la résolution des problèmes liés aux Redis, reportez-vous aux articles suivants du support Adobe Commerce :

- [Redis issue delay Admin login ou checkout](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Mise en oeuvre du cache Redis étendu Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [Alertes gérées sur Adobe Commerce : alerte d’avertissement de mémoire de révision](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [ Alertes gérées sur Adobe Commerce : redit l’alerte critique de mémoire ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
