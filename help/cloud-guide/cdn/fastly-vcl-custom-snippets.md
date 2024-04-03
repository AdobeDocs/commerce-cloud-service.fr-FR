---
title: Prise en main des fragments de code VCL personnalisés
description: Découvrez comment utiliser des fragments de code de langue de contrôle en vernis pour personnaliser la configuration de service Fastly pour Adobe Commerce.
feature: Cloud, Configuration, Services
exl-id: df0f0906-8ffa-41a1-a31c-d36deb5a6a31
source-git-commit: 89c57a486545d6165e0407f913f4fa4cf6c95abe
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 0%

---

# Prise en main de VCL personnalisé

Prise en charge rapide d’une version personnalisée du langage de configuration de vernis (VCL) pour adapter la configuration de service Fastly à vos besoins.

Les fragments de code VCL personnalisés sont des blocs de logique VCL ajoutés à la version VCL active chargée sur votre site Adobe Commerce. Un extrait de code VCL personnalisé modifie la manière dont les services de mise en cache rapide répondent au trafic de demande. Par exemple, vous pouvez ajouter un extrait de code VCL personnalisé pour autoriser le trafic de requêtes provenant uniquement d’adresses IP client spécifiées. Vous pouvez également créer un fragment de code afin de bloquer le trafic provenant de sites web connus pour envoyer du courrier indésirable à vos sites Adobe Commerce.

Les fragments de code VCL personnalisés (générés, compilés et transmis à tous les caches rapides) sont chargés et activés sans temps d’arrêt du serveur.

>[!NOTE]
>
>Avant d’ajouter du code VCL personnalisé, des dictionnaires de périphérie et des listes de contrôle d’accès à votre configuration de module Fastly, vérifiez que le service de mise en cache Fastly fonctionne avec la configuration par défaut. Voir [Configuration des services Fastly](fastly-configuration.md).

Prise en charge rapide de deux types de fragments de code VCL personnalisés :

- [Fragments de code réguliers](https://docs.fastly.com/en/guides/about-vcl-snippets): les fragments de code VCL standard personnalisés sont codés pour des versions VCL spécifiques. Vous pouvez créer, modifier et déployer des fragments de code VCL standard à partir de l’API Admin ou Fastly.

- [Extraits dynamiques](https://docs.fastly.com/en/guides/using-dynamic-vcl-snippets): fragments de code VCL créés à l’aide de l’API Fastly. Vous pouvez modifier et déployer des fragments de code dynamiques sans avoir à mettre à jour la version Fastly VCL de votre service.

Nous vous recommandons d’utiliser des fragments de code VCL personnalisés avec des dictionnaires Edge et des listes de contrôle d’accès (ACL) pour stocker les données utilisées dans votre code personnalisé.

- [**Dictionnaire Edge**](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries): stocke les données en tant que paires clé-valeur dans un conteneur de dictionnaire pouvant être référencé à partir de fragments de code VCL personnalisés.

- [**ACL Edge**](https://docs.fastly.com/guides/access-control-lists/about-acls): stocke les données d’adresse IP du client qui définissent la liste de contrôle d’accès pour les règles de blocage ou d’autorisation implémentées à l’aide de fragments de code VCL personnalisés.

Le dictionnaire et les données ACL sont déployés sur les noeuds Fastly Edge accessibles sur toutes les régions du réseau. En outre, les données peuvent être mises à jour dynamiquement sur le réseau sans que vous ayez à redéployer le code VCL pour votre environnement d’évaluation ou de production.

>[!NOTE]
>
>Vous ne pouvez ajouter des fragments de code VCL personnalisés qu’à un environnement d’évaluation ou de production si vous disposez des éléments suivants : [services Fastly configurés](fastly-configuration.md) pour cet environnement.

## Tutoriel

Ce tutoriel et ces exemples montrent l’utilisation de fragments de code VCL personnalisés standard avec les dictionnaires Edge et les listes de contrôle d’accès Edge pour personnaliser la configuration de service Fastly pour Adobe Commerce. Pour plus d’informations, voir la documentation Fastly :

- [Guide de Fastly VCL](https://docs.fastly.com/guides/vcl/guide-to-vcl): informations sur l’implémentation de la marque Fastly Varnish, les extensions Fastly VCL et les ressources pour en savoir plus sur le vernis et VCL.
- [Référence VCL très rapide](https://docs.fastly.com/guides/vcl/): référence de programmation détaillée pour développer et résoudre les problèmes liés aux fragments de code VCL personnalisés et Fastly.

Vous pouvez créer et gérer des fragments de code VCL personnalisés à partir de l’administrateur Adobe Commerce ou à l’aide de l’API Fastly :

- [Administrateur Adobe Commerce](#manage-custom-vcl-from-admin): nous vous recommandons d’utiliser l’administrateur Adobe Commerce pour gérer les fragments de code VCL personnalisés, car il automatise le processus de validation, de chargement et d’application des modifications VCL à la configuration de service Fastly. En outre, vous pouvez afficher et modifier les fragments de code VCL personnalisés ajoutés à la configuration de service Fastly à partir de l’administrateur.

- [API Fastly](#manage-vcl-using-the-api): si vous ne pouvez pas accéder à l’administrateur, utilisez l’API Fastly pour gérer les fragments de code VCL personnalisés. Par exemple, utilisez l’API pour résoudre les problèmes de configuration du service Fastly lorsque le site est hors service ou pour ajouter un extrait de code VCL personnalisé. En outre, certaines opérations ne peuvent être effectuées qu’à l’aide de l’API. Par exemple, vous devez utiliser l’API pour réactiver une ancienne version de VCL ou pour afficher tous les fragments de code VCL inclus dans une version de VCL spécifiée. Voir [Référence rapide de l’API pour les fragments de code VCL](#api-quick-reference-for-vcl-snippets).

### Exemple de code de fragment de code VCL

L’exemple suivant illustre le fragment de code VCL personnalisé (format JSON) qui filtre le trafic par adresse IP du client :

```json
{
  "service_id": "FASTLY_SERVICE_ID",
  "version": "{Editable Version #}",
  "name": "apply_acl",
  "priority": "100",
  "dynamic": "1",
  "type": "hit",
  "content": "if ((client.ip ~ {ACLNAME}) && !req.http.Fastly-FF){ error 403; }"
}
```

>[!WARNING]
>
>Dans cet exemple, le code VCL est formaté en tant que charge utile JSON pouvant être enregistrée dans un fichier et envoyée dans une requête API Fastly. Pour éviter les erreurs de validation JSON lors de l’envoi du fragment de code au format JSON pour une requête API, utilisez une barre oblique inverse pour échapper les caractères spéciaux dans le code. Voir [Utilisation de fragments de code VCL dynamiques](https://docs.fastly.com/vcl/vcl-snippets/) dans la documentation Fastly VCL . Si vous envoyez le fragment de code VCL depuis l’administrateur, vous n’avez pas à ajouter d’échappement aux caractères spéciaux.

La logique VCL dans la variable `content` exécute les actions suivantes :

- Vérifie l’adresse IP entrante, `client.ip` sur chaque requête

- Blocage de toute requête avec une adresse IP incluse dans la variable *ACLNAME* liste de contrôle d’accès Edge, renvoi d’une `403 Forbidden` error

Le tableau suivant fournit des détails sur les données clés des fragments de code VCL personnalisés. Pour une référence plus détaillée, voir la section [Fragments de code VCL](https://docs.fastly.com/api/config#api-section-snippet) dans la documentation Fastly.

| Valeur | Description |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `API_KEY` | Clé API pour accéder à votre compte Fastly. Voir [Obtention des informations d’identification](fastly-configuration.md). |
| `active` | État actif du fragment de code ou de la version. Renvoie `true` ou `false`. Si la valeur est true, le fragment de code ou la version est en cours d’utilisation. Cloner un extrait de code actif à l’aide de son numéro de version. |
| `content` | Fragment de code VCL à exécuter. Fastly ne prend pas en charge toutes les fonctionnalités de langage VCL. Elle fournit également des extensions Fastly avec des fonctionnalités personnalisées. Pour plus d’informations sur les fonctionnalités prises en charge, voir [Référence de programmation VCL très rapide](https://docs.fastly.com/vcl/reference/). |
| `dynamic` | État dynamique d’un fragment de code. Renvoie `false` pour [fragments de code standard](https://docs.fastly.com/en/guides/about-vcl-snippets) inclus dans le VCL versionné pour la configuration de service Fastly. Renvoie `true` pour un [fragment de code dynamique](https://docs.fastly.com/vcl/vcl-snippets/using-dynamic-vcl-snippets/) qui peut être modifié et déployé sans nécessiter de nouvelle version de VCL. |
| `number` | Numéro de version VCL où le fragment de code est inclus. Utilisation rapide *Modification de la version #* dans leurs exemples de valeurs. Si vous ajoutez des fragments de code personnalisés à partir de l’API, incluez le numéro de version dans la requête API. Si vous ajoutez un VCL personnalisé à partir de l’administrateur, la version est fournie pour vous. |
| `priority` | Valeur numérique de `1` to `100` qui spécifie quand le code de fragment de code VCL personnalisé s’exécute. Les fragments de code avec des valeurs de priorité inférieure s’exécutent en premier. Si elle n’est pas spécifiée, la variable `priority` valeur par défaut : `100`.<p>Tout fragment de code VCL personnalisé avec une valeur de priorité de `5` s’exécute immédiatement, ce qui est préférable pour le code VCL qui implémente le routage des demandes (bloquer et listes autorisées et redirections). Priorité `100` est préférable pour remplacer le code de fragment de code VCL par défaut.<p>Tous [fragments de code VCL par défaut](fastly-configuration.md#upload-vcl-snippets) inclus dans le module Magento-Fastly ont `priority=50`.<ul><li>Attribuez une priorité élevée comme `100` pour exécuter du code VCL personnalisé après toutes les autres fonctions VCL et remplacer le code VCL par défaut.</li></ul> |
| `service_id` | Identifiant de service Fastly pour un environnement d’évaluation ou de production spécifique. Cet identifiant est attribué lorsque votre projet est ajouté à Adobe Commerce sur l’infrastructure cloud [Compte de service Fastly](fastly.md#fastly-service-account-and-credentials). |
| `type` | Indique l’emplacement d’insertion du fragment de code généré, tel que `init` (sous-routines ci-dessus) et `recv` (dans des sous-routines). Pour plus d’informations, voir [Fragments de code VCL](https://docs.fastly.com/api/config#api-section-snippet) référence. |

## Gestion des VCL personnalisés à partir d’Admin

Vous pouvez [ajout de fragments de code VCL personnalisés](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) de la *Configuration rapide* > *Fragments de code VCL personnalisés* dans la section Admin.

![Gestion des fragments de code VCL personnalisés](../../assets/cdn/fastly-edit-snippets.png)

La variable *Fragments de code VCL personnalisés* La vue affiche uniquement les fragments de code qui ont été ajoutés par l’intermédiaire de l’administrateur. Si des fragments de code sont ajoutés à l’aide de l’API Fastly, utilisez l’API pour [gérer les](#manage-vcl-using-the-api).

Les exemples suivants montrent comment créer et gérer des fragments de code VCL personnalisés à partir de l’administrateur et utiliser des modules Edge Fastly et des dictionnaires Edge :

- [Rétablir les requêtes vers le serveur principal CMS](fastly-vcl-wordpress.md)
- [Blocage du courrier indésirable](fastly-vcl-badreferer.md)
- [Blocage du courrier indésirable](fastly-vcl-badreferer.md)
- [VCL personnalisée pour la liste autorisée IP](fastly-vcl-allowlist.md)
- [VCL personnalisée pour la liste bloquée IP](fastly-vcl-blocking.md)
- [Contournement rapide du cache](fastly-vcl-bypass-to-origin.md)

## Gestion de VCL à l’aide de l’API

La présentation suivante vous explique comment créer des fichiers de fragments de code VCL standard et les ajouter à votre configuration de service Fastly à l’aide de l’API Fastly. Vous pouvez créer et gérer des fragments de code à partir du *terminal* application. Vous n’avez pas besoin d’une connexion SSH dans un environnement spécifique.

**Conditions préalables :**

- Configurez votre environnement Adobe Commerce sur l’infrastructure cloud pour les services Fastly. Voir [Configuration rapide](fastly-configuration.md).

- [Obtention des informations d’identification d’API rapides](fastly-configuration.md) pour authentifier les requêtes sur l’API Fastly. Assurez-vous d’obtenir les informations d’identification pour l’environnement approprié : Évaluation ou Production.

- Enregistrez les informations d’identification du service Fastly en tant que variables d’environnement bash que vous pouvez utiliser dans les commandes cURL :

  ```bash
  export FASTLY_SERVICE_ID=<Service-ID>
  ```

  ```bash
  export FASTLY_API_TOKEN=<API-Token>
  ```

  Les variables d’environnement exportées ne sont disponibles que dans la session bash actuelle et sont perdues lorsque vous fermez le terminal. Vous pouvez redéfinir des variables en exportant une nouvelle valeur. Pour afficher la liste des variables exportées liées à Fastly :

  ```bash
  export | grep FASTLY
  ```

## Ajout de fragments de code VCL

Ce tutoriel décrit les étapes de base pour ajouter des fragments de code personnalisés à l’aide de l’API Fastly.

>[!NOTE]
>
>Pour savoir comment gérer des fragments de code VCL personnalisés à partir de l’administrateur Adobe Commerce, voir [Gestion de VCL à partir de l’administrateur Adobe Commerce](#manage-custom-vcl-from-admin).


**Conditions préalables**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

### Étape 1 : Localisation de la version VCL active

Utilisation de l’API Fastly [obtenir la version](https://docs.fastly.com/api/config#version_dfde9093f4eb0aa2497bbfd1d9415987) pour obtenir le numéro de version VCL actif :

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
```

Dans la réponse JSON, notez le numéro de version VCL actif renvoyé dans la variable `number` clé, par exemple `"number": 99`. Vous avez besoin du numéro de version lorsque vous clonez le VCL en vue de le modifier.

```json
{
  "testing": false,
  "locked": true,
  "number": 99,
  "active": true,
  "service_id": "872zhjyxhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Enregistrez le numéro de version actif dans une variable d’environnement bash afin de l’utiliser dans les demandes d’API suivantes :

```bash
export FASTLY_VERSION_ACTIVE=<Version>
```

### Étape 2 : cloner la version VCL active et tous les fragments de code

Avant de pouvoir ajouter ou modifier des fragments de code VCL personnalisés, vous devez créer une copie de la version VCL active pour modification. Utilisation de l’API Fastly [clone](https://docs.fastly.com/api/config#version_7f4937d0663a27fbb765820d4c76c709) operation :

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION_ACTIVE/clone -X PUT
```

Dans la réponse JSON, le numéro de version est incrémenté et la variable *active* la valeur clé est `false`. Vous pouvez modifier localement la nouvelle version inactive du VCL.

```json
{
  "testing": false,
  "locked": false,
  "number": 100,
  "active": false,
  "service_id": "vW2bLFWhhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Enregistrez le nouveau numéro de version dans une variable d&#39;environnement de base afin de l&#39;utiliser dans les commandes suivantes :

```bash
export FASTLY_EDIT_VERSION=<Version>
```

### Étape 3 : création d’un fragment de code VCL personnalisé

Créez et enregistrez votre code VCL personnalisé dans un fichier JSON avec le contenu et le format suivants :

```json
{
  "name": "<name>",
  "dynamic": "0",
  "type": "<type>",
  "priority": "100",
  "content": "<code all in one line>"
}
```

Les valeurs incluent :

- `name`—Nom du fragment de code VCL.

- `dynamic`: indique s’il s’agit d’une [extrait de code normal](https://docs.fastly.com/en/guides/about-vcl-snippets) ou [fragment de code dynamique](https://docs.fastly.com/guides/vcl-snippets/using-dynamic-vcl-snippets).

- `type`: spécifie l’emplacement d’insertion du fragment de code généré, tel que `init` (sous-routines ci-dessus) et `recv` (dans des sous-routines). Voir [Valeurs d’objet Fragment de code VCL à un stade précoce](https://docs.fastly.com/api/config#snippet) pour plus d’informations sur ces valeurs.

- `priority`—Une valeur de `1` to `100` qui détermine le moment où le code du fragment de code VCL personnalisé s’exécute. Les fragments de code VCL personnalisés avec des valeurs inférieures s’exécutent en premier.

  Tout le code VCL par défaut du module VCL Fastly comporte une `priority` de `50`. Si vous souhaitez qu’une action se produise en dernier ou pour remplacer le code VCL par défaut, utilisez un nombre plus élevé, tel que `100`. Pour exécuter immédiatement le code de fragment de code VCL personnalisé, définissez la priorité sur une valeur inférieure, telle que `5`.

- `content`: fragment de code VCL à exécuter sur une ligne, sans saut de ligne. Voir [Exemple de fragment de code VCL personnalisé](#example-vcl-snippet-code).

### Étape 4 : Ajout d’un extrait de code VCL à la configuration Fastly

Utilisation de l’API Fastly [créer un fragment de code](https://docs.fastly.com/api/config#snippet_41e0e11c662d4d56adada215e707f30d) pour ajouter le fragment de code VCL personnalisé à la version VCL.

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/snippet -H 'Content-Type: application/json' -X POST --data @<filename.json>
```

La variable `<filename.json>` est le nom du fichier que vous avez préparé à l’étape précédente. Répétez cette commande pour chaque extrait de code VCL.

Si vous recevez un `500 Internal Server Error` à partir du service Fastly, vérifiez la syntaxe du fichier JSON pour vous assurer que vous téléchargez un fichier valide.

### Étape 5 : validation et activation des fragments de code VCL personnalisés

Après avoir ajouté un extrait de code VCL personnalisé, insère rapidement le fragment de code dans la version VCL que vous modifiez. Pour appliquer des modifications, procédez comme suit pour valider le code du fragment de code VCL et activer la version VCL.

1. Utilisation de l’API Fastly [valider la version VCL](https://docs.fastly.com/api/config#version_97f8cf7bfd5dc2e5ea1933d94dc5a9a6) pour vérifier le code VCL mis à jour.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/validate
   ```

   Si l’API Fastly renvoie une erreur, corrigez le problème et validez à nouveau la version mise à jour de VCL.

1. Utilisation de l’API Fastly [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) pour activer la nouvelle version de VCL.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/activate -X PUT
   ```

## Référence rapide de l’API pour les fragments de code VCL

Ces exemples de requête d’API utilisent des variables d’environnement exportées pour fournir les informations d’identification à authentifier rapidement. Pour plus d’informations sur ces commandes, voir [Référence rapide à l’API](https://docs.fastly.com/api/config#vcl).

>[!NOTE]
>
>Utilisez ces commandes pour gérer les fragments de code que vous avez ajoutés à l’aide de l’API Fastly. Si vous avez ajouté des fragments de code à partir de l’administrateur, reportez-vous à la section [Gestion des fragments de code VCL à l’aide de l’option Admin](#manage-vcl-using-the-api).

- **Obtention du numéro de version VCL actif**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
  ```

- **Répertorier tous les fragments de code VCL normaux associés à un service**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet
  ```

- **Vérification d’un fragment de code individuel**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name>
  ```

  La variable `<snippet_name>` est le nom d’un fragment de code, tel que `my_regular_snippet`.

- **Mise à jour d’un fragment de code**

  Modifiez la variable [fichier JSON préparé](#step-3-create-a-custom-vcl-snippet) et envoyez la demande suivante :

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -H 'Content-Type: application/json' -X PUT --data @<filename.json>
  ```

- **Suppression d’un fragment de code VCL individuel**

  Obtenez une liste de fragments de code et utilisez les éléments suivants : `curl` avec le nom du fragment de code à supprimer :

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -X DELETE
  ```

- **Remplacer les valeurs dans [code VCL Fastly par défaut](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets)**

  Créez un fragment de code avec des valeurs mises à jour et attribuez une priorité à `100`.
