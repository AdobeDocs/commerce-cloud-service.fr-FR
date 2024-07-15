---
title: VCL personnalisée pour les requêtes de blocage
description: Bloquez les requêtes entrantes par adresse IP à l’aide d’une liste de contrôle d’accès Edge (ACL) avec un extrait de code VCL personnalisé.
feature: Cloud, Configuration, Security
exl-id: 1f637612-3858-49d0-91f7-9b8823933cc9
source-git-commit: 0e9ace747cc56808108781e42b97c86756089818
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# VCL personnalisée pour les requêtes de blocage

Vous pouvez utiliser le module CDN Fastly pour Magento 2 pour créer une liste de contrôle d’accès Edge avec une liste d’adresses IP que vous souhaitez bloquer. Vous pouvez ensuite utiliser cette liste avec un extrait de code VCL pour bloquer les requêtes entrantes. Le code vérifie l’adresse IP de la requête entrante. S’il correspond à une adresse IP incluse dans la liste ACL, bloque Fastly la demande d’accès à votre site et renvoie un `403 Forbidden error`. Toutes les autres adresses IP clientes sont autorisées.

**Conditions préalables :**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste des adresses IP du client à bloquer

## Création d’une liste de contrôle d’accès Edge pour le blocage des adresses IP du client

Vous créez une liste de contrôle d’accès Edge pour définir la liste des adresses IP à bloquer. Après avoir créé la liste de contrôle d’accès, vous pouvez l’utiliser dans un extrait de code VCL personnalisé pour gérer l’accès à votre site d’évaluation ou de production.

Gérez l’accès pour les sites d’évaluation et de production en créant la liste de contrôle d’accès Edge avec le même nom dans les deux environnements. Le code du fragment de code VCL s’applique aux deux environnements.

1. Connectez-vous à l’administrateur.
1. Accédez à **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système** > **Cache de page complet** > **Configuration rapide**.
1. Développez la section **Edge ACL** .
1. Cliquez sur **Ajouter ACL** pour créer une liste. Pour cet exemple, nommez la liste &quot;liste bloquée&quot;.
1. Saisissez les valeurs des adresses IP dans la liste. Toutes les adresses IP du client ajoutées à cette liste sont bloquées et ne peuvent pas accéder au site.
1. Si nécessaire, cochez la case **Negated** .

Vous référencez l’ACL Edge par nom dans votre code de fragment de code VCL.

## Création de la VCL personnalisée pour la liste bloquée

>[!NOTE]
>
>Cet exemple montre aux utilisateurs avancés comment créer un extrait de code VCL pour configurer des règles de blocage personnalisées à charger vers le service Fastly. Vous pouvez configurer une liste bloquée ou une liste autorisée en fonction du pays à partir de l’administrateur Adobe Commerce à l’aide de la fonction [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) disponible dans le module Fastly CDN for Magento 2.

Après avoir défini l’ACL Edge, vous pouvez l’utiliser pour créer le fragment de code VCL afin de bloquer l’accès aux adresses IP spécifiées dans l’ACL. Vous pouvez utiliser le même extrait de code VCL dans les environnements d’évaluation et de production, mais vous devez le charger séparément dans chaque environnement.

Le code de fragment de code VCL personnalisé suivant (format JSON) indique la logique permettant de bloquer les requêtes entrantes avec une adresse IP du client correspondant à une adresse dans la liste de contrôle d’accès de la liste bloquée.

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

Avant de créer un fragment de code basé sur cet exemple, vérifiez les valeurs pour déterminer si vous devez apporter des modifications :

- `name` : nom du fragment de code VCL. Pour cet exemple, nous avons utilisé le nom `blocklist`.

- `priority` : détermine le moment où le fragment de code VCL s’exécute. La priorité est `5` pour s’exécuter immédiatement et vérifier si une requête d’administrateur provient d’une adresse IP autorisée. L’extrait de code s’exécute avant que l’un des fragments de code VCL par défaut du Magento (`magentomodule_*`) n’ait une priorité de 50. Définissez la priorité de chaque fragment de code personnalisé sur une valeur supérieure ou inférieure à 50 selon le moment où vous souhaitez que votre fragment de code s’exécute. Les fragments de code dont les numéros de priorité sont plus bas s’exécutent en premier.

- `type` : spécifie le type de fragment de code VCL qui détermine l’emplacement du fragment de code VCL généré. Dans cet exemple, nous utilisons `recv`, qui insère le code VCL dans la sous-routine `vcl_recv`, sous la VCL standard et au-dessus de tous les objets. Pour obtenir la liste des types de fragments de code, reportez-vous à la [référence rapide de fragments de code VCL](https://docs.fastly.com/api/config#api-section-snippet) .

- `content` : extrait de code VCL à exécuter, qui vérifie l’adresse IP du client. Si l’adresse IP se trouve dans l’ACL Edge, elle est bloquée et une erreur `403 Forbidden` s’affiche pour l’ensemble du site web. Toutes les autres adresses IP clientes sont autorisées.

Après avoir examiné et mis à jour le code de votre environnement, utilisez l’une des méthodes suivantes pour ajouter le fragment de code VCL personnalisé à votre configuration de service Fastly :

- [Ajoutez le fragment de code VCL personnalisé à partir de l’Admin](#add-the-custom-vcl-snippet). Cette méthode est recommandée si vous pouvez accéder à l’administrateur. (Nécessite [Fastly version 1.2.58](fastly-configuration.md#upgrade-fastly-module) ou ultérieure.)

- Enregistrez l’exemple de code JSON dans un fichier (par exemple, `blocklist.json`) et [téléchargez-le à l’aide de l’API Fastly](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Utilisez cette méthode si vous ne pouvez pas accéder à l’administrateur.

## Ajout du fragment de code VCL personnalisé

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

1. Cliquez sur **Créer un fragment de code personnalisé**.

1. Ajoutez les valeurs du fragment de code VCL :

   - **Nom** — `blocklist`

   - **Type** — `recv`

   - **Priorité** — `5`

   - Ajoutez le contenu du fragment de code **VCL** :

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Cliquez sur **Créer** pour générer le fichier de fragment de code VCL avec le modèle de nom `type_priority_name.vcl`, par exemple `recv_5_blocklist.vcl`.

1. Après le rechargement de la page, cliquez sur **Télécharger VCL vers Fastly** dans la section *Configuration Fastly* pour ajouter le fichier à la configuration de service Fastly.

1. Après les chargements, actualisez le cache en fonction de la notification dans la partie supérieure de la page.

Valide rapidement la version mise à jour du code VCL pendant le processus de chargement. Si la validation échoue, modifiez le fragment de code VCL personnalisé pour résoudre le problème. Ensuite, chargez à nouveau le VCL.

## Exemples VCL supplémentaires pour le blocage des requêtes

Les exemples suivants montrent comment bloquer des requêtes à l’aide d’instructions de condition intégrées au lieu d’une liste ACL.

>[!WARNING]
>
>Dans ces exemples, le code VCL est formaté en tant que charge utile JSON pouvant être enregistrée dans un fichier et envoyée dans une requête d’API Fastly. Vous pouvez envoyer le fragment de code [VCL à partir de l’Admin](#add-the-custom-vcl-snippet) ou sous la forme d’une chaîne JSON à l’aide de l’API Fastly. Pour empêcher la validation lorsque vous utilisez l’API Fastly avec une chaîne JSON, vous devez utiliser une barre oblique inverse pour échapper les caractères spéciaux.

Voir [Utilisation de fragments de code VCL dynamiques](https://docs.fastly.com/vcl/vcl-snippets/) dans la documentation Fastly VCL.

### Exemple de code VCL : bloc par code de pays

Cet exemple utilise le code de pays ISO 3166-1 à deux caractères pour le pays associé à l’adresse IP.

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>Au lieu d’utiliser un extrait de code VCL personnalisé, vous pouvez utiliser la fonction Fastly [Blocking](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) dans Adobe Commerce sur l’administrateur d’infrastructure cloud pour configurer le blocage par code de pays ou une liste de codes de pays.

### Exemple de code VCL : bloc par en-tête de requête HTTP User-Agent

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
