---
title: Inclusions côté serveur
description: Découvrez comment utiliser les inclusions côté serveur avec Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Routes
exl-id: 34a38cb5-5f0e-49ac-9dba-bb581a06aeed
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Inclusions côté serveur

[Inclusions côté serveur](https://nginx.org/en/docs/http/ngx_http_ssi_module.html) (SSI) sont des directives dans les pages de HTML qui sont évaluées sur le serveur pendant le rendu des pages. SSI vous permet d’ajouter du contenu généré dynamiquement à une page de HTML existante sans diffuser la page entière.

Dans votre `.magento/routes.yaml`; par exemple :

```yaml
    "http://{default}/":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: false
            ssi:
                enabled: true
    "http://{default}/time.php":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: true
```

SSI vous permet d’inclure dans vos directives de réponse de HTML qui font que le serveur remplit des parties du HTML, en respectant les directives existantes. [configuration de mise en cache](caching.md).

L’exemple suivant montre comment insérer une commande de date dynamique en haut d’une page et une autre commande de date en bas, qui se met à jour toutes les 600 secondes :

Ajoutez ce qui suit à n’importe quelle page, par exemple `/index.php`:

```php?start_inline=1
echo date(DATE_RFC2822);
<!--#include virtual="time.php" -->
```

Ajoutez ce qui suit à `time.php`:

```php?start_inline=1
header("Cache-Control: max-age=600");
echo date(DATE_RFC2822);
```

Accédez à la page sur laquelle vous avez ajouté le contrôle. Actualisez la page plusieurs fois et notez que l’heure en haut de la page change, mais que l’heure en bas ne change que toutes les 600 secondes.
