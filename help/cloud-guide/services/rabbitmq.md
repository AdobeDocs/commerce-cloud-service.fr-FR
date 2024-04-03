---
title: Configuration du service RabbitMQ
description: Découvrez comment activer le service RabbitMQ pour gérer les files d’attente de messages pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Configuration [!DNL RabbitMQ] service

La variable [Message Queue Framework (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) est un système d’Adobe Commerce qui permet à un [module](https://glossary.magento.com/module) pour publier des messages dans les files d’attente. Il définit également les consommateurs qui reçoivent les messages de manière asynchrone.

Le MQF utilise [RabbitMQ](https://www.rabbitmq.com/) en tant que courtier de messagerie, qui fournit une plateforme évolutive pour l’envoi et la réception de messages. Il comprend également un mécanisme de stockage des messages non diffusés. [!DNL RabbitMQ] est basé sur la spécification AMQP 0.9.1 du protocole Advanced Message Queuing Protocol (AMQP).

>[!WARNING]
>
>Si vous préférez utiliser un service AMQP existant, comme [!DNL RabbitMQ], au lieu de vous fier à Adobe Commerce sur l’infrastructure cloud pour la créer, utilisez la variable [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) pour la connecter à votre site.

{{service-instruction}}

**Pour activer RabbitMQ**:

1. Ajoutez le nom, le type et la valeur de disque requis (en Mo) au `.magento/services.yaml` avec la version de RabbitMQ installée.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configurez les relations dans le `.magento.app.yaml` fichier .

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Vérification des relations de service](services-yaml.md#service-relationships).

{{service-change-tip}}

## Connexion à RabbitMQ pour le débogage

À des fins de débogage, il est utile de se connecter directement à une instance de service de l’une des manières suivantes :

- Connexion à votre environnement de développement local
- Connexion à partir de l’application
- Connexion à partir de votre application PHP

### Connexion à votre environnement de développement local

1. Connectez-vous au `magento-cloud` Interface en ligne de commande et projet :

   ```bash
   magento-cloud login
   ```

1. Extrayez l’environnement sur lequel RabbitMQ est installé et configuré.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Utilisez SSH pour vous connecter à l’environnement cloud :

   ```bash
   magento-cloud ssh
   ```

1. Récupérez les informations de connexion et les informations de connexion de RabbitMQ à partir de la [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variable :

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Dans la réponse, recherchez les informations RabbitMQ, par exemple :

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Activez le transfert de port local vers RabbitMQ.

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Exemple d’accès à l’interface web de gestion RabbitMQ à l’adresse `http://localhost:15672` est :

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Pendant que la session est ouverte, vous pouvez démarrer un client RabbitMQ de votre choix à partir de votre poste de travail local, configuré pour vous connecter au `localhost:<portnumber>` à l’aide du numéro de port, du nom d’utilisateur et du mot de passe de la variable MAGENTO_CLOUD_RELATIONSHIPS.

### Connexion à partir de l’application

Pour vous connecter à RabbitMQ exécuté dans une application, installez un client, tel que [amqp-utils](https://github.com/dougbarth/amqp-utils), comme dépendance de projet dans votre `.magento.app.yaml` fichier .

Par exemple,

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Lorsque vous vous connectez à votre conteneur PHP, vous saisissez les `amqp-` pour gérer vos files d’attente.

### Connexion à partir de votre application PHP

Pour vous connecter à RabbitMQ à l’aide de votre application PHP, ajoutez un protocole PHP. [bibliothèque](https://glossary.magento.com/library) à votre arborescence source.
