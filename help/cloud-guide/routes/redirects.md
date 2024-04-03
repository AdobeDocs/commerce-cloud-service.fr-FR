---
title: Redirections
description: Découvrez comment gérer les règles de redirection pour votre projet Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Routes
exl-id: 7089a790-6341-4443-990a-df42091f0680
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Redirections

La gestion des règles de redirection est une exigence courante dans les applications web, notamment lorsque vous ne souhaitez pas perdre les liens entrants qui ont été modifiés ou supprimés au fil du temps.

Les éléments suivants montrent comment gérer les règles de redirection sur votre Adobe Commerce dans les projets d’infrastructure cloud à l’aide de la variable `routes.yaml` fichier de configuration. Si les méthodes de redirection abordées dans cette rubrique ne fonctionnent pas pour vous, vous pouvez utiliser des en-têtes de mise en cache pour faire la même chose.

{{route-placeholder}}

## Mises à jour des environnements Pro

{{pro-self-service-warning}}

>[!WARNING]
>
>Pour Adobe Commerce sur les projets d’infrastructure cloud, la configuration de nombreuses redirections et réécritures non regex dans le `routes.yaml` peut entraîner des problèmes de performances. Si votre `routes.yaml` de 32 Ko ou plus, déchargez vos redirections non regex et réécrivez en mode Fastly. Voir [Décharger les redirections non regex vers Fastly au lieu de Nginx (itinéraires)](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) dans le _Centre d’aide Adobe Commerce_.

## Redirections tout-itinéraire

À l’aide de redirections d’itinéraire, vous pouvez définir des itinéraires simples à l’aide de la variable `routes.yaml` fichier . Par exemple, vous pouvez rediriger d’un domaine d’application vers un `www` sous-domaine comme suit :

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Redirections d’itinéraire partiel

Dans le `.magento/routes.yaml` vous pouvez ajouter des règles de redirection partielle à des itinéraires existants en fonction de la correspondance de modèles :

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Les redirections partielles fonctionnent avec n’importe quel type d’itinéraire, y compris les itinéraires desservis directement par l’application.

Deux clés sont disponibles sous `redirects`:

- **expires**: Facultatif, indique le temps nécessaire pour mettre en cache la redirection dans le navigateur. Exemples de valeurs valides : `3600s`, `1d`, `2w`, `3m`.

- **paths**: une ou plusieurs paires clé-valeur qui spécifient la configuration pour les règles de redirection à itinéraire partiel.

  Pour chaque règle de redirection, la clé est une expression permettant de filtrer les chemins de requête pour la redirection. La valeur est un objet qui spécifie la destination cible pour la redirection et les options pour le traitement de la redirection.

  L’objet value possède les propriétés suivantes :

  | Propriété | Description |
  | ---------- | ----------- |
  | `to` | Obligatoire, un chemin absolu partiel, une URL avec protocole et hôte, ou un modèle qui spécifie la destination cible de la règle de redirection. |
  | `regexp` | Facultatif, la valeur par défaut est `false`. Indique si la clé de chemin doit être interprétée comme une expression régulière PCRE. |
  | `prefix` | Indique si la redirection s’applique à la fois au chemin et à tous ses enfants, ou simplement au chemin lui-même. La valeur par défaut est `true`. Cette valeur n’est pas prise en charge si `regexp` is `true`. |
  | `append_suffix` | Détermine si le suffixe est transféré avec la redirection. La valeur par défaut est `true`. Cette valeur n’est pas prise en charge si la variable `regexp` key is `true` ou* si la variable `prefix` key is `false`. |
  | `code` | Indique le code d’état HTTP. Les codes d’état valides sont [`301` (Déplacé définitivement)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8), et [`308`](https://www.rfc-editor.org/rfc/rfc7238). La valeur par défaut est `302`. |
  | `expires` | Facultatif, indique le temps nécessaire pour mettre en cache la redirection dans le navigateur. La valeur par défaut est `expires` valeur définie directement sous `redirects` mais à ce niveau, vous pouvez affiner l’expiration du cache pour les redirections partielles individuelles. |

## Exemples de redirections à itinéraire partiel

Les exemples suivants montrent comment spécifier des redirections à itinéraire partiel dans la variable `routes.yaml` en utilisant divers `paths` options de configuration.

### Correspondance de modèle d’expression régulière

Utilisez le format suivant pour configurer les demandes de redirection basées sur une expression régulière.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Cette configuration filtre les chemins de requête par rapport à une expression régulière et redirige les requêtes correspondantes vers `https://example.com`. Par exemple, une requête pour `https://example.com/regexp/a/b/c/match` redirige vers `https://example.com/a/b/c`.

### Correspondance du modèle de préfixe

Utilisez le format suivant pour configurer les demandes de redirection pour les chemins commençant par un modèle de préfixe spécifié.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Cette configuration fonctionne comme suit :

- Redirige les demandes qui correspondent au modèle. `/from` vers le chemin `http://{default}/to`.

- Redirige les demandes qui correspondent au modèle. `/from/another/path` to `https://{default}/to/another/path`.

- Si vous modifiez la variable `prefix` de `false`, les demandes qui correspondent à la variable `/from` déclenche une redirection, mais les requêtes qui correspondent à la variable `/from/another/path` n’en a pas.

### Correspondance de motifs de suffixe

Utilisez le format suivant pour configurer les requêtes de redirection qui ajoutent le suffixe de chemin de la requête à la destination cible :

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Cette configuration fonctionne comme suit :

- Redirige les demandes qui correspondent au modèle. `/from/path/suffix` vers le chemin `https://{default}/to`.

- Si vous modifiez la variable `append_suffix` de `true`, puis les requêtes qui correspondent `/from/path/suffix`  rediriger vers le chemin `https://{default}/to/path/suffix`.

### Configuration du cache spécifique au chemin d’accès

Utilisez le format suivant pour personnaliser l’heure de mise en cache d’une redirection à partir d’un chemin spécifique :

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
    paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Cette configuration fonctionne comme suit :

- Redirections à partir du premier chemin (`/from`) sont mis en cache pendant un jour.

- Redirections à partir du deuxième chemin (`/here`) sont mises en cache pendant deux semaines.
