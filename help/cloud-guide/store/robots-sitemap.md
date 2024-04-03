---
title: Ajout de robots de carte de site et de moteur de recherche
description: Découvrez comment ajouter des robots de carte de site et de moteur de recherche à Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Ajout de robots de carte de site et de moteur de recherche

Une tentative de génération et d’écriture de la variable `sitemap.xml` dans le répertoire racine, l’erreur suivante se produit :

```terminal
Please make sure that "/" is writable by the web-server.
```

Avec Adobe Commerce sur l’infrastructure cloud, vous ne pouvez écrire que dans des répertoires spécifiques, tels que `var`, `pub/media`, `pub/static`, ou `app/etc`. Lorsque vous générez la variable `sitemap.xml` à l’aide du panneau d’administration, vous devez spécifier la variable `/media/` chemin.

Il n’est pas nécessaire de générer une `robots.txt` car il génère la variable `robots.txt` contenu à la demande et le stocke dans la base de données. Vous pouvez afficher le contenu dans votre navigateur à l’aide de la fonction `<domain.your.project>/robots.txt` ou `<domain.your.project>/robots` lien.

Pour ce faire, la version 2002.0.12 et ultérieure des outils ECE doit être mise à jour. `.magento.app.yaml` fichier . Consultez un exemple de ces règles dans la section [référentiel magento-cloud](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**Pour générer un `sitemap.xml` dans les versions 2.2 et ultérieures**:

1. Accédez à l’administrateur.
1. Sur le _Marketing_ , cliquez sur **Carte du site** dans le _SEO &amp; Search_ .
1. Dans le _Carte du site_ afficher, cliquez sur **Ajouter un plan de site**.
1. Dans le _Nouvelle carte du site_ saisissez les valeurs suivantes :

   - **Nom du fichier**:`sitemap.xml`
   - **Chemin**:`/media/`

1. Cliquez sur **Enregistrer et générer**. La nouvelle carte du site devient disponible dans la _Carte du site_ grid.
1. Cliquez sur le chemin dans la _Lien vers Google_ colonne .

**Pour ajouter du contenu au `robots.txt` fichier**:

1. Accédez à l’administrateur.
1. Sur le _Contenu_ , cliquez sur **Configuration** dans le _Conception_ .
1. Dans le _Configuration de conception_ afficher, cliquez sur **Modifier** pour le site web dans la variable _Action_ colonne .
1. Dans le _Site web principal_ afficher, cliquez sur **Robots des moteurs de recherche**.
1. Mettez à jour le **Modifier l’instruction personnalisée de robots.txt** champ .
1. Cliquez sur **Enregistrer la configuration**.
1. Vérifiez les `<domain.your.project>/robots.txt` fichier ou `<domain.your.project>/robots` URL dans votre navigateur.

>[!NOTE]
>
>Si la variable `<domain.your.project>/robots.txt` génère un fichier `404 error`, [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour supprimer la redirection de `/robots.txt` to `/media/robots.txt`.

## Réécriture à l’aide d’un fragment de code VCL Fastly

Si vous avez des domaines différents et que vous avez besoin de mappages de site distincts, vous pouvez créer un VCL pour acheminer vers le plan de site approprié. Générez la variable `sitemap.xml` dans le panneau d’administration, comme décrit ci-dessus, puis créez un fragment de code VCL Fastly personnalisé pour gérer la redirection. Voir [Fragments de code VCL personnalisés](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> Vous pouvez charger des fragments de code VCL personnalisés à partir de l’interface utilisateur d’administration ou à l’aide de l’API Fastly. Voir [Exemples et tutoriels de fragments de code VCL personnalisés](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Utiliser un extrait de code VCL Fastly pour la redirection

Créer un fragment de code VCL personnalisé pour réécrire le chemin d’accès `sitemap.xml` to `/media/sitemap.xml` en utilisant la variable `type` et `content` paires clé-valeur.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

L’exemple suivant montre comment réécrire le chemin pour `robots.txt` et `sitemap.xml` to `/media/robots.txt` et `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**Pour utiliser un fragment de code VCL Fastly pour une redirection de domaine spécifique**:

Créez un `pub/media/domain_robots.txt` où le domaine est `domain.com`et utilisez le fragment de code VCL suivant :

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

Itinéraires des fragments de code VCL `http://domain.com/robots.txt` et présente la variable `pub/media/domain_robots.txt` fichier .

Pour configurer une redirection pour `robots.txt` et `sitemap.xml` dans un fragment de code unique, créez `pub/media/domain_robots.txt` et `pub/media/domain_sitemap.xml` fichiers, où le domaine est `domain.com` et utilisez le fragment de code VCL suivant :

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

Dans le `sitemap` admin config, vous devez spécifier l’emplacement du fichier à l’aide de `pub/media/` plutôt que `/`.

### Configuration de l’indexation par moteur de recherche

Pour activer `robots.txt` personnalisations, vous devez activer la fonction **L’indexation par les moteurs de recherche est activée pour`<environment-name>`** dans les paramètres du projet.

![Utilisez la variable [!DNL Cloud Console] pour gérer les environnements](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Si vous utilisez PWA Studio et ne parvenez pas à accéder à la variable `robots.txt` fichier, ajouter `robots.txt` à la fonction [Liste autorisée de prénom](https://github.com/magento/magento2-upward-connector#front-name-allowlist) at **Magasins** > Configuration > **Général** > **Web** > Configuration du PWA UPWARD.
