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

L’exemple suivant montre comment gérer les règles de redirection sur votre Adobe Commerce pour les projets d’infrastructure cloud à l’aide du fichier de configuration `routes.yaml`. Si les méthodes de redirection abordées dans cette rubrique ne fonctionnent pas pour vous, vous pouvez utiliser des en-têtes de mise en cache pour faire la même chose.

{{route-placeholder}}

## Mises à jour des environnements Pro

{{pro-self-service-warning}}

>[!WARNING]
>
>Pour Adobe Commerce sur les projets d’infrastructure cloud, la configuration de nombreuses redirections et réécritures non regex dans le fichier `routes.yaml` peut entraîner des problèmes de performances. Si votre fichier `routes.yaml` fait 32 Ko ou plus, déchargez vos redirections non regex et réécrivez en mode Fastly. Voir [Décharger les redirections non regex vers Fastly au lieu de Nginx (itinéraires)](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) dans le _Centre d’aide Adobe Commerce_.

## Redirections tout-itinéraire

À l’aide de redirections d’itinéraire, vous pouvez définir des itinéraires simples à l’aide du fichier `routes.yaml`. Par exemple, vous pouvez rediriger d’un domaine d’application vers un sous-domaine `www` comme suit :

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Redirections d’itinéraire partiel

Dans le fichier `.magento/routes.yaml`, vous pouvez ajouter des règles de redirection partielles aux itinéraires existants en fonction de la correspondance de modèles :

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Les redirections partielles fonctionnent avec n’importe quel type d’itinéraire, y compris les itinéraires desservis directement par l’application.

Deux clés sont disponibles sous `redirects` :

- **expires** : facultatif. Cette option spécifie le temps nécessaire pour mettre en cache la redirection dans le navigateur. Parmi les exemples de valeurs valides, citons `3600s`, `1d`, `2w`, `3m`.

- **paths** : une ou plusieurs paires clé-valeur qui spécifient la configuration pour les règles de redirection à itinéraire partiel.

  Pour chaque règle de redirection, la clé est une expression permettant de filtrer les chemins de requête pour la redirection. La valeur est un objet qui spécifie la destination cible pour la redirection et les options pour le traitement de la redirection.

  L’objet value possède les propriétés suivantes :

  | Propriété | Description |
  | ---------- | ----------- |
  | `to` | Obligatoire, un chemin absolu partiel, une URL avec protocole et hôte, ou un modèle qui spécifie la destination cible de la règle de redirection. |
  | `regexp` | Facultatif, la valeur par défaut est `false`. Indique si la clé de chemin doit être interprétée comme une expression régulière PCRE. |
  | `prefix` | Indique si la redirection s’applique à la fois au chemin et à tous ses enfants, ou simplement au chemin lui-même. Par défaut : `true`. Cette valeur n’est pas prise en charge si `regexp` est `true`. |
  | `append_suffix` | Détermine si le suffixe est transféré avec la redirection. Par défaut : `true`. Cette valeur n’est pas prise en charge si la clé `regexp` est `true` ou* si la clé `prefix` est `false`. |
  | `code` | Indique le code d’état HTTP. Les codes d’état valides sont [`301` (Déplacé définitivement)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8) et [`308`](https://www.rfc-editor.org/rfc/rfc7238). Par défaut : `302`. |
  | `expires` | Facultatif, indique le temps nécessaire pour mettre en cache la redirection dans le navigateur. La valeur par défaut est `expires` définie directement sous la clé `redirects`, mais à ce niveau, vous pouvez affiner l’expiration du cache pour les redirections partielles individuelles. |

## Exemples de redirections à itinéraire partiel

Les exemples suivants montrent comment spécifier des redirections à itinéraire partiel dans le fichier `routes.yaml` à l’aide de diverses options de configuration `paths`.

### Correspondance de modèle d’expression régulière

Utilisez le format suivant pour configurer les demandes de redirection basées sur une expression régulière.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Cette configuration filtre les chemins de requête par rapport à une expression régulière et redirige les requêtes correspondantes vers `https://example.com`. Par exemple, une requête vers `https://example.com/regexp/a/b/c/match` redirige vers `https://example.com/a/b/c`.

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

- Redirige les requêtes qui correspondent au modèle `/from` vers le chemin `http://{default}/to`.

- Redirige les demandes qui correspondent au modèle `/from/another/path` vers `https://{default}/to/another/path`.

- Si vous définissez la propriété `prefix` sur `false`, les requêtes correspondant au modèle `/from` déclenchent une redirection, mais les requêtes correspondant au modèle `/from/another/path` ne le font pas.

### Correspondance de motifs de suffixe

Utilisez le format suivant pour configurer les requêtes de redirection qui ajoutent le suffixe de chemin de la requête à la destination cible :

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Cette configuration fonctionne comme suit :

- Redirige les requêtes qui correspondent au modèle `/from/path/suffix` vers le chemin `https://{default}/to`.

- Si vous définissez la propriété `append_suffix` sur `true`, les demandes qui correspondent à `/from/path/suffix` redirigent vers le chemin `https://{default}/to/path/suffix`.

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

- Les redirections du premier chemin d’accès (`/from`) sont mises en cache pendant une journée.

- Les redirections du deuxième chemin d’accès (`/here`) sont mises en cache pendant deux semaines.
