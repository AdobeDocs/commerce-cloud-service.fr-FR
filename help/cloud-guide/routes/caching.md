---
title: Mise en cache
description: Découvrez comment activer la mise en cache pour votre Adobe Commerce dans les environnements d’infrastructure cloud.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Mise en cache

Vous pouvez activer la mise en cache dans l’environnement de projet de votre infrastructure cloud. Si vous désactivez la mise en cache, Adobe Commerce diffuse directement les fichiers.

{{route-placeholder}}

## Configuration de la mise en cache

Activez la mise en cache de votre application en configurant les règles de mise en cache dans le `.magento/routes.yaml` comme suit :

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Mise en cache basée sur les itinéraires

Activez la mise en cache affinée en configurant les règles de mise en cache de plusieurs itinéraires séparément, comme le montre l’exemple suivant :

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

L’exemple précédent met en cache les itinéraires suivants :

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

Et les itinéraires suivants sont **not** mis en cache :

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>Les expressions régulières des itinéraires sont **not** pris en charge.

## Durée du cache

La durée du cache est déterminée par la variable `Cache-Control` valeur de l’en-tête de réponse. Si non `Cache-Control` L’en-tête se trouve dans la réponse, la variable `default_ttl` est utilisée.

## Clé de cache

Pour décider comment mettre en cache une réponse, Adobe Commerce crée une clé de cache qui dépend de plusieurs facteurs et stocke la réponse associée à cette clé. Lorsqu’une requête est fournie avec la même clé de cache, la réponse est réutilisée. Son objectif est similaire au HTTP [`Vary` header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Les paramètres `headers` et `cookies` Les clés permettent de modifier cette clé de cache.

La valeur par défaut de ces clés est la suivante :

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Attributs du cache

### `enabled`

Lorsque la variable est définie sur `true`, activez le cache pour cet itinéraire. Lorsque la variable est définie sur `false`, désactivez le cache de cet itinéraire.

### `headers`

Définit les valeurs dont doit dépendre la clé de cache.

Par exemple, si la variable `headers` clé est la suivante :

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Adobe Commerce met ensuite en cache une réponse différente pour chaque valeur de la variable `Accept` En-tête HTTP.

### `cookies`

La variable `cookies` key définit les valeurs dont la clé de cache doit dépendre.

Par exemple :

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

La clé de cache dépend de la valeur de la variable `value` dans la requête.

Il existe un cas particulier si la variable `cookies` La clé contient la variable `["*"]` . Cette valeur signifie que toute requête avec un cookie contourne le cache. Il s’agit de la valeur par défaut.

>[!NOTE]
>
>Vous ne pouvez pas utiliser de caractères génériques dans le nom du cookie. Utilisez un nom de cookie précis ou faites correspondre tous les cookies à un astérisque (`*`). Par exemple : `SESS*` ou `~SESS` sont actuellement **not** valeurs valides.

Les cookies comportent les restrictions suivantes :

- Vous pouvez définir le nombre maximal de **50 cookies** dans le système. Dans le cas contraire, l’application renvoie une `Unable to send the cookie. Maximum number of cookies would be exceeded` exception.
- La taille maximale du cookie est **4 096 octets**. Dans le cas contraire, l’application renvoie une `Unable to send the cookie. Size of '%name' is %size bytes` exception.

### `default_ttl`

Si la réponse n’a pas de `Cache-Control` en-tête, `default_ttl` est utilisée pour définir la durée du cache, en secondes. La valeur par défaut est `0`, ce qui signifie que rien n’est mis en cache.
