---
title: Propriété Web
description: Voir des exemples sur la configuration de la propriété web dans le fichier de configuration de l'application  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Propriété Web

La propriété `web` définit la manière dont votre application est exposée sur le web (en HTTP), détermine la manière dont l’application web diffuse du contenu et contrôle la manière dont le conteneur d’applications répond aux requêtes entrantes en définissant des règles à chaque emplacement _block_. Un bloc représente un chemin absolu menant avec une barre oblique (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

Vous pouvez affiner votre configuration `locations` à l’aide des valeurs clés suivantes pour chaque bloc `locations` :

| Attribut | Description |
| :--- | :--- |
| `allow` | Servez les fichiers qui ne correspondent pas aux &quot;règles&quot;. Valeur par défaut = `true` |
| `expires` | Définissez le nombre de secondes pour mettre en cache le contenu dans le navigateur. Cette clé active les en-têtes `cache-control` et `expires` pour le contenu statique. Si cette valeur n’est pas définie, la directive `expires` et les en-têtes résultants ne sont pas inclus lors de la diffusion de fichiers de contenu statique. Une valeur négative de 1 (`-1`) n’entraîne aucune mise en cache et est la valeur par défaut. Vous pouvez exprimer une valeur de temps avec les unités suivantes : `ms` (millisecondes), `s` (secondes), `m` (minutes), `h` (heures), `d` (jours), `w` (semaines), `M` (mois, 30j), ou `y` (années, 365j) |
| `headers` | Définissez des en-têtes personnalisés, tels que `X-Frame-Options`, pour le contenu statique diffusé à partir de cet emplacement. |
| `index` | Répertorier les fichiers statiques à utiliser pour votre application, tels que le fichier `index.html`. Cette clé attend une collection. Cela ne fonctionne que si l’accès au fichier ou aux fichiers est &quot;autorisé&quot; par la clé `allow` ou `rules` de cet emplacement. |
| `rules` | Spécifiez les remplacements d’un emplacement. Utilisez une expression régulière pour faire correspondre une requête. Si une requête entrante correspond à la règle, la gestion régulière de la requête est remplacée par les clés utilisées dans la règle. |
| `passthru` | Définissez l’URL utilisée au cas où un fichier statique ou PHP serait introuvable. En règle générale, cette URL est le contrôleur frontal de vos applications, par exemple `/index.php` ou `/app.php`. |
| `root` | Définissez le chemin d’accès relatif à la racine de l’application exposée sur le Web. Le répertoire public (emplacement &quot;/&quot;) d’un projet Cloud est défini sur &quot;pub&quot; par défaut. |
| `scripts` | Autoriser le chargement des scripts à cet emplacement. Définissez la valeur sur `true` pour autoriser les scripts. |

La configuration par défaut permet ce qui suit :

- À partir du chemin d’accès racine (`/`), seuls les médias et le web sont accessibles.
- À partir des chemins `~/pub/static` et `~/pub/media`, tout fichier est accessible

L’exemple suivant montre la configuration par défaut dans le fichier `.magento.app.yaml` pour un ensemble d’emplacements accessibles sur le Web associés à une entrée dans la propriété [`mounts`](properties.md#mounts) :

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>Cet exemple illustre la configuration web par défaut d’un projet Cloud configuré pour prendre en charge un seul domaine. Pour un projet qui nécessite la prise en charge de plusieurs sites web ou magasins, la configuration `web` doit être configurée pour prendre en charge les domaines partagés. Voir [Configuration d’emplacements pour les domaines partagés](../store/multiple-sites.md#configure-locations-for-shared-domains).
