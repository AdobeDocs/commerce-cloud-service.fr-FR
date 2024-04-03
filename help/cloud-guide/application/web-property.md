---
title: Propriété Web
description: Voir des exemples de configuration de la propriété web dans la section [!DNL Commerce] fichier de configuration de l’application.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Propriété Web

La variable `web` définit la manière dont votre application est exposée sur le web (en HTTP), détermine la manière dont l’application web diffuse le contenu et contrôle la manière dont le conteneur d’applications répond aux requêtes entrantes en définissant des règles à chaque emplacement. _block_. Un bloc représente un chemin absolu menant à une barre oblique (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

Vous pouvez affiner votre `locations` configuration à l’aide des valeurs clés suivantes pour chaque `locations` block:

| Attribut | Description |
| :--- | :--- |
| `allow` | Servez les fichiers qui ne correspondent pas aux &quot;règles&quot;. Valeur par défaut = `true` |
| `expires` | Définissez le nombre de secondes pour mettre en cache le contenu dans le navigateur. Cette clé active la fonction `cache-control` et `expires` en-têtes pour le contenu statique. Si cette valeur n’est pas définie, la variable `expires` Les en-têtes de directive et résultants ne sont pas inclus lors de la diffusion de fichiers de contenu statiques. Un 1 négatif (`-1`) n’entraîne aucune mise en cache et est la valeur par défaut. Vous pouvez exprimer la valeur de temps avec les unités suivantes :  `ms` (millisecondes), `s` (secondes), `m` (minutes), `h` (heures), `d` (jours), `w` (semaines), `M` (mois, 30 j) ou `y` (years, 365d) |
| `headers` | Définissez des en-têtes personnalisés, tels que `X-Frame-Options`, pour le contenu statique fourni à partir de cet emplacement. |
| `index` | Répertorier les fichiers statiques à utiliser pour votre application, tels que le `index.html` fichier . Cette clé attend une collection. Cela ne fonctionne que si l’accès au fichier ou aux fichiers est &quot;autorisé&quot; par la fonction `allow` ou `rules` clé de cet emplacement. |
| `rules` | Spécifiez les remplacements d’un emplacement. Utilisez une expression régulière pour faire correspondre une requête. Si une requête entrante correspond à la règle, la gestion régulière de la requête est remplacée par les clés utilisées dans la règle. |
| `passthru` | Définissez l’URL utilisée au cas où un fichier statique ou PHP serait introuvable. En règle générale, cette URL est le contrôleur frontal de vos applications, telles que `/index.php` ou `/app.php`. |
| `root` | Définissez le chemin d’accès relatif à la racine de l’application exposée sur le Web. Le répertoire public (emplacement &quot;/&quot;) d’un projet Cloud est défini sur &quot;pub&quot; par défaut. |
| `scripts` | Autoriser le chargement des scripts à cet emplacement. Définissez la valeur sur `true` pour autoriser les scripts. |

La configuration par défaut permet ce qui suit :

- À partir de la racine (`/`), seul le Web et le média sont accessibles.
- Dans la `~/pub/static` et `~/pub/media` chemins, tout fichier est accessible

L’exemple suivant illustre la configuration par défaut dans la variable `.magento.app.yaml` pour un ensemble d’emplacements accessibles sur le Web associés à une entrée dans la variable  [`mounts` property](properties.md#mounts):

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
>Cet exemple illustre la configuration web par défaut d’un projet Cloud configuré pour prendre en charge un seul domaine. Pour un projet qui nécessite la prise en charge de plusieurs sites web ou magasins, la méthode `web` La configuration doit être configurée pour prendre en charge les domaines partagés. Voir [Configuration des emplacements pour les domaines partagés](../store/multiple-sites.md#configure-locations-for-shared-domains).
