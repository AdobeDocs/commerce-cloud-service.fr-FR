---
title: Configuration des services
description: Découvrez comment configurer les services utilisés par Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Configuration des services

La variable `services.yaml` définit les services pris en charge et utilisés par Adobe Commerce sur l’infrastructure cloud, tels que MySQL, Redis et Elasticsearch ou OpenSearch. Vous n’avez pas besoin de vous abonner à des prestataires externes. Ce fichier se trouve dans la variable `.magento` répertoire de votre projet.

Le script de déploiement utilise les fichiers de configuration dans la variable `.magento` pour configurer l’environnement avec les services configurés. Un service devient disponible pour votre application s’il est inclus dans la variable [`relationships`](../application/properties.md#relationships) de la propriété `.magento.app.yaml` fichier . La variable `services.yaml` contient le fichier _type_ et _disque_ valeurs. Le type de service définit le service _name_ et _version_.

La modification de la configuration d’un service entraîne un déploiement à configurer l’environnement avec les services mis à jour, ce qui affecte les environnements suivants :

- Tous les environnements de démarrage, y compris Production `master`
- Environnements d’intégration Pro

{{pro-update-service}}

## Services par défaut et pris en charge

L’infrastructure cloud prend en charge et déploie les services suivants :

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

Vous pouvez afficher les versions par défaut et les valeurs du disque dans la version actuelle, [default `services.yaml` fichier](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). L’exemple suivant illustre la variable `mysql`, `redis`, `opensearch` ou `elasticsearch`, et `rabbitmq` services définis dans la variable `services.yaml` fichier de configuration :

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## Valeurs de service

Vous devez fournir l’ID de service et la configuration du type de service. `type: <name>:<version>`. Si le service utilise le stockage permanent, vous devez fournir une valeur de disque.

Utilisez le format suivant :

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

La variable `service-id` identifie le service dans le projet. Vous ne pouvez utiliser que des caractères alphanumériques minuscules : `a` to `z` et `0` to `9`, par exemple `redis`.

Ceci _service-id_ est utilisée dans la variable [`relationships`](../application/properties.md#relationships) de la propriété `.magento.app.yaml` fichier de configuration :

```yaml
relationships:
    redis: "<name>:redis"
```

Vous pouvez nommer plusieurs instances de chaque type de service. Par exemple, vous pouvez utiliser plusieurs instances Redis : une pour la session et une pour le cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

Changement du nom d’un service dans le `services.yaml` fichier **supprime définitivement** les éléments suivants :

- Le service existant avant de créer un service avec le nouveau nom que vous indiquez.
- Toutes les données existantes pour le service sont supprimées. Adobe recommande vivement que vous [sauvegarde de votre environnement de démarrage](../storage/snapshots.md) avant de modifier le nom d’un service existant.

### `type`

La variable `type` spécifie le nom et la version du service. Par exemple :

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

La variable `disk` value indique la taille du stockage du disque persistant (en Mo) à allouer au service. Les services qui utilisent le stockage persistant, comme MySQL, doivent fournir une valeur de disque. Les services qui utilisent de la mémoire plutôt que du stockage persistant, comme Redis, ne nécessitent pas de valeur de disque.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Le volume de stockage par défaut actuel par projet est de 5 Go, soit 512 0 Mo. Vous pouvez répartir ce montant entre votre application et chacun de ses services.

## Relations avec les services

Dans Adobe Commerce sur les projets d’infrastructure cloud, le service [relations](../application/properties.md#relationships) configuré dans la variable `.magento.app.yaml` détermine les services disponibles pour votre application.

Vous pouvez récupérer les données de configuration pour toutes les relations de service à partir de la variable [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) Variable d’environnement. Les données de configuration incluent le nom, le type et la version du service, ainsi que les détails de connexion requis, tels que le numéro de port et les informations de connexion.

**Vérification des relations dans l’environnement local**:

1. Dans votre environnement local, affichez les relations pour l’environnement actif.

   ```bash
   magento-cloud relationships
   ```

1. Confirmez le `service` et `type` de la réponse. La réponse fournit des informations de connexion, telles que l’adresse IP et le numéro de port.

   >Exemple de réponse abrégé

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**Vérification des relations dans les environnements distants**:

1. Utilisez SSH pour vous connecter à l’environnement distant.

1. Répertorier les données de configuration des relations pour tous les services configurés dans l’environnement.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou, utilisez ce qui suit : `ece-tools` pour visualiser les relations :

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Confirmez le `service` et `type` de la réponse. La réponse fournit des informations de connexion, telles que l’adresse IP et le numéro de port, ainsi que tout nom d’utilisateur et mot de passe requis.

## Versions de service

La prise en charge de la version du service et de la compatibilité pour Adobe Commerce sur l’infrastructure cloud est déterminée par les versions déployées et testées sur l’infrastructure cloud et diffère parfois des versions prises en charge par les déploiements sur site d’Adobe Commerce. Voir [Configuration requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) dans le _Installation_ Guide pour une liste des dépendances de logiciels tiers que Adobe a testées avec des versions Adobe Commerce et Magento Open Source spécifiques.

### Vérifications EOL du logiciel

Au cours du processus de déploiement, la variable `ece-tools` Le package vérifie les versions de service installées par rapport aux dates de fin de vie (EOL) de chaque service.

- Si une version de service se trouve dans les trois mois suivant la date de fin de vie, une notification s’affiche dans le journal de déploiement.
- Si la date de fin de vie se situe dans le passé, une notification d’avertissement s’affiche.

Pour maintenir la sécurité du magasin, mettez à jour les versions logicielles installées avant qu’elles n’atteignent EOL. Vous pouvez consulter les dates de fin de vie dans la variable [ece-tools&#39; `eol.yaml` fichier](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### Migration vers OpenSearch

{{elasticsearch-support}}

Pour les versions 2.4.4 et ultérieures d’Adobe Commerce, voir [Configuration du service OpenSearch](opensearch.md).

## Modification de la version du service

Vous pouvez mettre à niveau la version de service installée pour des raisons de compatibilité avec la version d’Adobe Commerce déployée dans votre environnement cloud.

Vous ne pouvez pas directement mettre à niveau la version du service pour un service installé. Vous pouvez toutefois créer un service avec la version requise. Voir [Version du service de rétrogradation](#downgrade-version).

### Mettre à niveau la version du service installé

Vous pouvez mettre à niveau la version du service installé en mettant à jour la configuration du service dans le `services.yaml` fichier .

1. Modifiez la variable [`type`](#type) pour le service dans la variable `.magento/services.yaml` fichier :

   > Définition du service d’origine

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Définition de service mise à jour

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Version de rétrogradation

Vous ne pouvez pas directement mettre à niveau un service installé. Vous disposez de deux options :

1. Renommez un service existant avec la nouvelle version, ce qui supprime le service et les données existants et en ajoute un nouveau.

1. Créez un service et enregistrez les données du service existant.

Lorsque vous modifiez la version du service, vous devez mettre à jour la configuration du service dans le `services.yaml` et de mettre à jour les relations dans la variable `.magento.app.yaml` fichier .

**Pour rétrograder une version de service en renommant un service existant**:

1. Renommez le service existant dans la fonction `.magento/services.yaml` et modifiez la version.

   >[!WARNING]
   >
   >Le fait de renommer un service existant le remplace et supprime toutes les données. Si vous devez conserver les données, créez un service au lieu de renommer celui existant.

   Par exemple, pour rétrograder la version de MariaDB pour le _mysql_ de la version 10.4 à la version 10.3, modifiez la _service-id_ et _type_ configuration.

   > Original `services.yaml` définition

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Nouveau `services.yaml` définition

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Mettez à jour les relations dans le `.magento.app.yaml` fichier .

   > Original `.magento.app.yaml` configuration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Mis à jour `.magento.app.yaml` configuration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Ajoutez, validez et poussez vos modifications de code.

**Pour rétrograder un service en créant un service**:

1. Ajoutez une définition de service à la fonction `services.yaml` pour votre projet avec la spécification de version dégradée. Voir _mysql2_ dans l’exemple suivant :

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Modifiez la configuration des relations dans le `.magento.app.yaml` pour utiliser le nouveau service.

   > Original `.magento.app.yaml` configuration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Nouveau `.magento.app.yaml` configuration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Ajoutez, validez et poussez vos modifications de code.
