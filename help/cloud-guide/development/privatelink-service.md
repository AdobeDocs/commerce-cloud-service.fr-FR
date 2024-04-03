---
title: Service PrivateLink
description: Découvrez comment utiliser le service PrivateLink pour établir une connexion sécurisée entre un cloud privé et une plateforme cloud Adobe Commerce dans la même région.
feature: Cloud, Iaas, Security
exl-id: b25548b8-312b-4a74-b242-f4e2ac6cf945
source-git-commit: 5b52157c6c623bb4c765a2d545919df79d81f1da
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Service PrivateLink

Adobe Commerce sur l’infrastructure cloud prend en charge l’intégration à [AWS PrivateLink](https://aws.amazon.com/privatelink/) ou [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/) service. Vous pouvez utiliser PrivateLink pour établir une communication privée sécurisée entre Adobe Commerce dans les environnements d’infrastructure cloud avec des services et des applications hébergés sur des systèmes externes. L’application Adobe Commerce et les systèmes externes doivent être accessibles via les points d’entrée Virtual Private Cloud (VPC) configurés sur la même plateforme cloud (AWS ou Azure) dans la même région de cloud.

>[!TIP]
>
>PrivateLink est idéal pour sécuriser les connexions pour les intégrations non HTTP(S), telles que les transferts de base de données ou de fichiers. Si vous prévoyez d’intégrer votre application aux API Adobe Commerce, découvrez comment créer une [Adobe API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _Maillage d’API pour Adobe Developer App Builder_.

## Fonctionnalités et support

L’intégration du service PrivateLink pour Adobe Commerce sur les projets d’infrastructure cloud comprend les fonctionnalités et la prise en charge suivantes :

- Connexion sécurisée entre un client de cloud virtuel privé (VPC) et le VPC d’Adobe sur la même plateforme cloud (AWS ou Azure) dans la même région du cloud.
- Prise en charge de la communication unidirectionnelle ou bidirectionnelle entre les services de point de terminaison disponibles sur les VPC Adobe et clients.
- Activation du service :

   - Ouvrez les ports requis dans Adobe Commerce dans l’environnement d’infrastructure cloud.
   - Établir la connexion initiale entre les VPC client et Adobe
   - Résolution des problèmes de connexion pendant l’activation

## Limites

- La prise en charge de PrivateLink est disponible uniquement dans les environnements de production et d’évaluation Pro. Elle n’est pas disponible sur les environnements locaux ou d’intégration, ni sur les projets de démarrage.
- Vous ne pouvez pas établir de connexions SSH à l’aide de PrivateLink. Voir [Activation des clés SSH](secure-connections.md).
- La prise en charge d’Adobe Commerce ne couvre pas la résolution des problèmes liés à AWS PrivateLink au-delà de l’activation initiale.
- Les clients sont responsables des coûts associés à la gestion de leur propre VPC.
- Vous ne pouvez pas utiliser le protocole HTTPS (port 443) pour vous connecter à Adobe Commerce sur l’infrastructure cloud via Azure Private Link en raison de [Fermeture à l&#39;origine](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html). Cette limitation ne s’applique pas à AWS PrivateLink.
- PrivateDNS n’est pas disponible.

## Types de connexion PrivateLink

Deux types de connexion PrivateLink sont disponibles (illustrés dans le diagramme de réseau suivant) pour établir une communication sécurisée entre votre magasin et les systèmes externes hébergés en dehors de l’environnement cloud.

![Diagramme réseau PrivateLink](../../assets/privatelink-architecture-diagram.png)

Choisissez l’un des types de connexions PrivateLink les mieux adaptés à votre Adobe Commerce dans les environnements d’infrastructure cloud :

- **Lien privé unidirectionnel**-Sélectionnez cette configuration pour récupérer les données en toute sécurité à partir d’un Adobe Commerce sur le magasin d’infrastructures cloud.
- **Lien privé bidirectionnel**-Sélectionnez cette configuration pour établir des connexions sécurisées vers et depuis des systèmes en dehors d’Adobe Commerce sur l’environnement d’infrastructure cloud. L’option bidirectionnelle requiert deux connexions :

   - Une connexion entre le VPC client et le VPC Adobe
   - Connexion entre le VPC d’Adobe et le VPC client

>[!TIP]
>
>Contactez votre administrateur réseau ou votre fournisseur de plateforme Cloud pour obtenir de l’aide sur la sélection du type de connexion PrivateLink ou sur la configuration et l’administration VPC. Voir la documentation de Cloud Platform PrivateLink : [AWS PrivateLink](https://aws.amazon.com/privatelink/) ou [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/).

## Demander l’activation de PrivateLink

>[!WARNING]
>
>L’activation de PrivateLink peut prendre jusqu’à _cinq_ jours ouvrés. Fournir des informations incomplètes ou inexactes peut retarder le processus.

### Conditions préalables

![check](../../assets/fix.svg) Un compte Cloud (AWS ou Azure) dans la même région que l’instance Adobe Commerce sur l’infrastructure cloud.

![check](../../assets/fix.svg) Un VPC dans l’environnement client qui héberge les services à connecter via PrivateLink. Pour obtenir de l’aide sur la configuration de VPC, consultez la documentation d’AWS ou d’Azure ou contactez votre administrateur réseau.

![check](../../assets/fix.svg) Pour les connexions PrivateLink bidirectionnelles, vous devez créer la configuration du service de point d’entrée pour votre application ou service, et créer un point d’entrée dans votre environnement VPC avant de demander l’activation de PrivateLink. Voir [Configuration des connexions PrivateLink bidirectionnelles](#set-up-for-bidirectional-privatelink-connections).

Rassemblez les données suivantes requises pour l’activation de PrivateLink :

- **Numéro de compte de Customer Cloud** (AWS ou Azure) : doit se trouver dans la même région que l’instance Adobe Commerce sur l’infrastructure cloud
- **Région du cloud**: indiquez la région du cloud où le compte est hébergé à des fins de vérification.
- **Services et ports de communication**: Adobe doit ouvrir les ports pour permettre la communication de service entre VPC, par exemple le port SQL 3306, le port SFTP 2222.
- **Identifiant de projet**: indiquez l’identifiant de projet Adobe Commerce sur l’infrastructure cloud Pro. Vous pouvez obtenir l’ID de projet et d’autres informations sur le projet à l’aide des éléments suivants : [Interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md) command : `magento-cloud project:info`
- **Type de connexion**: spécification unidirectionnelle ou bidirectionnelle pour le type de connexion
- **Service Endpoint**—Pour les connexions PrivateLink bidirectionnelles, fournissez l’URL DNS pour le service de point d’entrée VPC auquel l’Adobe doit se connecter, par exemple : `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **Accès au service Endpoint accordé**: pour vous connecter à un service externe, autorisez le service endpoint à accéder au principal de compte AWS suivant : `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Si l’accès au service de point de terminaison n’est pas fourni, la connexion PrivateLink bidirectionnelle au service dans votre VPC est **not** ajouté, ce qui retarde la configuration.

#### Autres prérequis spécifiques à l’activation de lien privé Azure

- Indiquez l’ID de grappe ; à l’aide de SSH, connectez-vous à la télécommande et utilisez la commande : `cat /etc/platform_cluster`
- Pour qu’un service externe se connecte à votre grappe Adobe Commerce Pro, vous avez besoin des éléments suivants :

   - Liste des ports de votre grappe Pro à exposer au nouveau point d’entrée privé externe
   - Liste des ID d’abonnement Azure pour les connexions Point de terminaison privé

- Pour connecter votre grappe Adobe Commerce Pro à un service externe, vous avez besoin des éléments suivants :

   - Liste des identifiants des ressources pour les services cibles. Les identifiants du service de lien privé externe ressemblent à ce qui suit :

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Workflow d’activation

Le workflow suivant décrit le processus d’activation de l’intégration de PrivateLink à Adobe Commerce sur l’infrastructure cloud.

1. **Client** envoie un ticket d’assistance demandant l’activation de PrivateLink avec l’objet `PrivateLink support for <company>`. Inclure la variable [données requises pour l’activation](#prerequisites) dans le ticket. Adobe utilise le ticket d’assistance pour coordonner la communication pendant le processus d’activation.

1. **Adobe** permet l’accès au compte client au service de point de terminaison dans le VPC Adobe.

   - Mettez à jour la configuration du service de point de terminaison Adobe pour accepter les demandes initiées à partir du compte AWS ou Azure du client.
   - Mettez à jour le ticket de support pour fournir le nom du service auquel le point d’entrée VPC d’Adobe doit se connecter, par exemple `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Client** ajoute le service Adobe endpoint à leur compte Cloud (AWS ou Azure), ce qui déclenche une demande de connexion à Adobe. Pour obtenir des instructions, consultez la documentation de la plateforme Cloud :

   - Pour AWS, voir [Acceptation et rejet des requêtes de connexion des points d’entrée de l’interface].
   - Pour Azure, voir [Gestion des requêtes de connexion].

1. **Adobe** approuve la demande de connexion.

1. Après la validation de la demande de connexion, **le client** [vérifie la connexion](#test-vpc-endpoint-service-connection) entre leur VPC et l’Adobe VPC.

1. Autres étapes pour activer les connexions bidirectionnelles :

   - **Adobe** fournit l’entité de compte d’Adobe (utilisateur root pour le compte AWS ou Azure) et demande l’accès au service de point de terminaison VPC client.
   - **Client** permet l’accès des Adobes au service de point de terminaison dans le VPC client. Cela suppose que l’entité de compte d’Adobe a accès à `arn:aws:iam::402592597372:root`, comme décrit précédemment dans la section **Accès au service Endpoint accordé** condition préalable.

      - Mettez à jour la configuration du service de point de terminaison client pour accepter les demandes initiées à partir du compte Adobe. Pour obtenir des instructions, consultez la documentation de la plateforme Cloud :

         - Pour AWS, voir [Ajout et suppression d’autorisations pour votre service de point de fin].
         - Pour Azure, voir [Gestion d’une connexion de point de terminaison privé]

      - Fournissez un Adobe avec le nom du service de point de terminaison pour le VPC client.

   - **Adobe** ajoute le service de point d’entrée client au compte de plateforme Adobe (AWS ou Azure), ce qui déclenche une demande de connexion au VPC client.
   - **Client** approuve la demande de connexion de l’Adobe pour terminer la configuration.
   - **Client** [vérifie la connexion](#test-vpc-endpoint-service-connection) de l’Adobe VPC.

## Test de la connexion au service de point d’entrée VPC

Vous pouvez utiliser l’application Telnet pour tester la connexion au service de point d’entrée VPC.

**Test de la connexion au service VPC endpoint**:

1. Dans le répertoire racine du projet, **passage en caisse** l’environnement d’évaluation ou de production configuré pour accéder au service de point d’entrée PrivateLink.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Exécutez la commande CURL suivante :

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Exemple :

   ```terminal
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Exemple de réponse réussie :

   ```terminal
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Exemple de réponse en échec :

   ```terminal
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Vérifiez que le service écoute sur VM.

   ```bash
   netstat -na | grep <port>
   ```

1. Vérifiez le flux des packages.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Vérifiez les paramètres internes suivants pour vous assurer que la configuration est valide :

   - Paramètres des services de point de fin et de point de fin
   - Paramètres NLB (Network Load Balancer)
   - Les groupes cibles de la NLB et vérifier qu&#39;ils sont en bonne santé
   - URL du point d’entrée netcat/curl de chaque VM (répertoriée ci-dessus)

   Consultez les articles suivants pour obtenir de l’aide sur la résolution des problèmes de connexion :

   - [AWS : résolution des problèmes de connexion au service de point d’entrée]
   - [Amazon : résolution des problèmes de connectivité Azure Private Link]

   Si vous ne parvenez pas à résoudre les erreurs, mettez à jour le ticket de support Adobe Commerce pour demander de l’aide pour établir la connexion.

## Modification de la configuration de PrivateLink

[Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour modifier une configuration PrivateLink existante. Par exemple, vous pouvez demander des modifications comme suit :

- Supprimez la connexion PrivateLink d’Adobe Commerce dans l’environnement de production ou d’évaluation de l’infrastructure cloud Pro.
- Modifiez le numéro de compte de la plateforme Customer Cloud pour accéder au service de point de terminaison Adobe.
- Ajoutez ou supprimez des connexions PrivateLink du VPC d’Adobe à d’autres services de point de terminaison disponibles dans l’environnement VPC client.

## Configuration des connexions PrivateLink bidirectionnelles

Le VPC client doit disposer des ressources suivantes disponibles pour prendre en charge les connexions PrivateLink bidirectionnelles :

- Un équilibreur de charge réseau (NLB)
- Une configuration de service de point de terminaison qui permet d’accéder à une application ou à un service à partir du client VPC
- Un [point d’entrée de l’interface] (AWS) ou [point d’entrée privé] (Azure) qui permet à Adobe de se connecter aux services de point de terminaison hébergés dans votre VPC

Si ces ressources ne sont pas disponibles dans le VPC client, vous devez vous connecter à votre compte de plateforme Cloud pour ajouter la configuration.

- Console Amazon VPC - `https://console.aws.amazon.com/vpc/`
- Portail Azure `https://portal.azure.com`

Consultez la documentation de votre plateforme Cloud pour obtenir des instructions sur la configuration de PrivateLink :

- **Documentation d’AWS PrivateLink**
   - [Création d’un équilibreur de charge réseau]
   - [Création d’une configuration de service de point de fin]
   - [Création d’un point d’entrée d’interface]
   - [Cycle de vie du point d’entrée de l’interface]

- **Documentation Azure PrivateLink**
   - [Création d’un équilibreur de charge]
   - [Workflow Azure Private Link]

<!--Link definitions-->

[Acceptation et rejet des requêtes de connexion des points d’entrée de l’interface]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Ajout et suppression d’autorisations pour votre service de point de fin]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon : résolution des problèmes de connectivité Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS : résolution des problèmes de connexion au service de point d’entrée]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Workflow Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Création d’un équilibreur de charge]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Création d’un équilibreur de charge réseau]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Création d’une configuration de service de point de fin]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Création d’un point d’entrée d’interface]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[point d’entrée de l’interface]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Gestion d’une connexion de point de terminaison privé]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Gestion des requêtes de connexion]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[point d’entrée privé]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
