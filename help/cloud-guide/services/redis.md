---
title: Configuration du service Redis
description: Découvrez comment configurer et optimiser Redis en tant que solution de cache d’arrière-plan pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Cache, Services
exl-id: d6971875-d302-495a-ad10-a81c507c2bc9
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Configuration du service Redis

[Redis](https://redis.io) est une solution de cache d’arrière-plan facultative qui remplace Zend_Cache_Backend_File de Zend Framework, que Adobe Commerce utilise par défaut.

Voir [Configuration de Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) dans le _Guide de configuration_.

{{service-instruction}}

**Pour activer Redis**:

1. Ajoutez le nom et le type requis au `.magento/services.yaml` fichier .

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Pour fournir votre propre configuration Redis, ajoutez une `core_config` clé dans votre `.magento/services.yaml` fichier :

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configurez les relations dans le `.magento.app.yaml` fichier .

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

1. [Vérification des relations de service](services-yaml.md#service-relationships).

{{service-change-tip}}

## Utilisation de l’interface de ligne de commande Redis

En supposant que votre relation Redis soit nommée `redis`, vous pouvez y accéder à l’aide de la fonction `redis-cli` outil.

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

```terminal
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis sur l’évaluation et la production Pro

Pour installer la version de Redis sur un environnement d’évaluation ou de production, utilisez le `redis-server` command :

```bash
redis-server -v
```

```terminal
Redis server v=7.0.5 ...
```

Utilisez la commande suivante pour installer la configuration Redis dans un environnement d’évaluation ou de production Pro :

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Exemple de réponse :

```terminal
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

- [Redis issue : délai de connexion de l’administrateur ou passage en caisse](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
- [Mise en oeuvre étendue du cache Redis dans Adobe Commerce 2.3.5+](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html)
- [MDVA-30102 : le cache de Redis devient plein](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/v1-0-6/mdva-30102-magento-patch-redis-cache-getting-full.html)
- [Alertes gérées sur Adobe Commerce : alerte d’avertissement de mémoire réduite](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
- [Alertes gérées sur Adobe Commerce : permet de réduire l’alerte critique de mémoire](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
- [Résolution des problèmes de Redis](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
