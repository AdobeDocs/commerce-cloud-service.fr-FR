---
title: Configuration de plusieurs sites web ou magasins
description: Découvrez comment configurer plusieurs sites web ou magasins pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Configuration de plusieurs sites web ou magasins

Vous pouvez configurer Adobe Commerce pour qu’il y ait plusieurs sites Web ou magasins, tels qu’un magasin anglais, un magasin français et un magasin allemand. Voir [Présentation des sites web, des magasins et des vues de magasin](best-practices.md#store-views).

>[!WARNING]
>
>Les données du catalogue s’étendent au fur et à mesure que vous augmentez le nombre de sites web et de magasins. Selon l’architecture de votre projet, les magasins supplémentaires peuvent entraîner un processus d’indexation plus long et des temps de réponse plus lents pour les pages de catalogue non mises en cache. Adobe vous recommande de surveiller de près les performances du site.

Le processus de configuration de plusieurs magasins varie selon que vous choisissez d’utiliser des domaines uniques ou partagés.

Plusieurs magasins avec des domaines uniques :

```terminal
https://first.store.com/
https://second.store.com/
```

Plusieurs magasins avec le même domaine :

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Pour ajouter une vue de magasin à l’URL de base du site, il n’est pas nécessaire de créer plusieurs répertoires. Voir [Ajouter le code de magasin à l’URL de base](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) dans le _Guide de configuration_.

## Ajout de domaines

Les domaines personnalisés peuvent être ajoutés à Pro Staging et à tout environnement de production ; ils ne peuvent pas être ajoutés aux environnements d’intégration.

Le processus d’ajout d’un domaine dépend du type de compte Cloud :

- Pour l’évaluation et la production Pro

  Ajoutez le nouveau domaine à Fastly, voir [Gestion des domaines](../cdn/fastly-custom-cache-configuration.md#manage-domains)ou ouvrez un ticket d’assistance pour demander de l’aide. En outre, vous devez [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander l’ajout de nouveaux domaines à une grappe.

- Pour la production de démarrage uniquement

  Ajoutez le nouveau domaine à Fastly, voir [Gestion des domaines](../cdn/fastly-custom-cache-configuration.md#manage-domains), ou [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander de l’aide. En outre, vous devez ajouter le nouveau domaine au **Domaines** dans le [!DNL Cloud Console]: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Configuration de l’installation locale

Pour configurer votre installation locale afin d’utiliser plusieurs magasins, voir [Plusieurs sites web ou magasins][config-multiweb] dans le _Guide de configuration_.

Après avoir créé et testé l’installation locale pour utiliser plusieurs magasins, vous devez préparer votre environnement d’intégration :

1. **Configuration des itinéraires ou des emplacements**: spécifiez la manière dont les URL entrantes sont gérées par Adobe Commerce.

   - [Itinéraires de domaines distincts](#configure-routes-for-separate-domains)
   - [Emplacements des domaines partagés](#configure-locations-for-shared-domains)

1. **Configuration des sites web, des magasins et des vues de magasin**: configuration à l’aide de l’interface utilisateur d’administration d’Adobe Commerce
1. **Modification des variables**: spécifiez les valeurs de la variable `MAGE_RUN_TYPE` et `MAGE_RUN_CODE` dans la variable `magento-vars.php` fichier
1. **Déploiement et test des environnements**: déployez et testez le `integration` branche

>[!TIP]
>
>Vous pouvez utiliser un environnement local pour configurer plusieurs sites web ou magasins. Consultez les instructions de Cloud Docker pour [Configuration de plusieurs sites web ou magasins](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Mises à jour de configuration des environnements Pro

{{pro-self-service-warning}}

### Configuration d’itinéraires pour des domaines distincts

Les itinéraires définissent le traitement des URL entrantes. Plusieurs magasins avec des domaines uniques nécessitent de définir chaque domaine dans la variable `routes.yaml` fichier . La configuration des itinéraires dépend de la manière dont votre site doit fonctionner.

**Pour configurer des itinéraires dans un environnement d’intégration**:

1. Sur votre poste de travail local, ouvrez le `.magento/routes.yaml` dans un éditeur de texte.

1. Définissez le domaine et les sous-domaines. La variable `mymagento` la valeur en amont est la même valeur que la propriété name dans la propriété `.magento.app.yaml` fichier .

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Enregistrez vos modifications dans le `routes.yaml` fichier .

1. Passez à [Configuration des sites web, des magasins et des vues de magasin](#set-up-websites-stores-and-store-views).

### Configuration des emplacements pour les domaines partagés

Lorsque la configuration des itinéraires définit le mode de traitement des URL, la variable `web` dans la propriété `.magento.app.yaml` définit la manière dont votre application est exposée sur le web. Web _emplacements_ permettent une plus grande granularité pour les requêtes entrantes. Par exemple, si votre domaine est `store.com`, vous pouvez utiliser `/first` (site par défaut) et `/second` pour les demandes envoyées à deux magasins différents qui partagent un domaine.

**Pour configurer un nouvel emplacement web**:

1. Créez un alias pour la racine (`/`). Dans cet exemple, l’alias est `&app` à la ligne 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Création d’une passerelle pour le site web (`/website`) et référencez la racine à l’aide de l’alias de l’étape précédente.

   L’alias permet `website` pour accéder aux valeurs de l’emplacement racine. Dans cet exemple, le site web `passthru` est à la ligne 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**Pour configurer un emplacement avec un autre répertoire**:

1. Créez un alias pour la racine (`/`) et pour le paramètre statique (`/static`).

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Créez un sous-répertoire pour le site web sous le `pub` directory: `pub/<website>`

1. Copiez le `pub/index.php` dans le fichier `pub/<website>` et mettre à jour le répertoire `bootstrap` path (`/../../app/bootstrap.php`).

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Création d’une transmission pour la variable `index.php` fichier .

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Validez et envoyez les fichiers modifiés.

   - `pub/<website>/index.php` (Si ce fichier se trouve dans la variable `.gitignore`, la notification push peut nécessiter l’option force .)
   - `.magento.app.yaml`

### Configuration des sites web, des magasins et des vues de magasin

Dans le _Interface utilisateur d’administration_, configurez votre Adobe Commerce **Sites web**, **Magasins**, et **Vues du magasin**. Voir [Configuration de plusieurs sites web, magasins et vues de magasin dans l’administrateur](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) dans le _Guide de configuration_.

Il est important d’utiliser le même nom et le même code pour vos sites web, magasins et magasins des vues de votre administrateur lors de la configuration de votre installation locale. Vous avez besoin de ces valeurs lorsque vous mettez à jour la variable `magento-vars.php` fichier .

### Modification des variables

Au lieu de configurer un hôte virtuel NGINX, transmettez la variable `MAGE_RUN_CODE` et `MAGE_RUN_TYPE` en utilisant la variable `magento-vars.php` dans le répertoire racine du projet.

**Pour transmettre des variables à l’aide de la variable `magento-vars.php` fichier**:

1. Ouvrez le `magento-vars.php` dans un éditeur de texte.

   La variable [default `magento-vars.php` fichier](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) doit ressembler à ce qui suit :

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. Déplacer le commentaire `if` block afin qu’elle soit _after_ la valeur `function` et ne commente plus.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Remplacez les valeurs suivantes dans la variable `if (isHttpHost("example.com"))` block:
   - `example.com`: avec l’URL de base de votre _site web_
   - `default`: avec le CODE unique pour votre _site web_ ou _vue de magasin_
   - `store`—avec l’une des valeurs suivantes :
      - `website`—load la variable _site web_ sur le storefront
      - `store`—load a _vue de magasin_ sur le storefront

   Pour plusieurs sites utilisant des domaines uniques :

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   Pour plusieurs sites avec le même domaine, vous devez vérifier la variable _hôte_ et la variable _URI_:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Enregistrez vos modifications dans le `magento-vars.php` fichier .

### Déploiement et test sur le serveur d’intégration

Envoyez vos modifications à votre Adobe Commerce dans l’environnement d’intégration de l’infrastructure cloud et testez votre site.

1. Ajoutez, validez et poussez les modifications de code à la branche distante.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Attendez que le déploiement soit terminé.

1. Après le déploiement, ouvrez l’URL de votre magasin dans un navigateur web.

   Avec un domaine unique, utilisez le format suivant : `http://<magento-run-code>.<site-URL>`

   Par exemple, `http://french.master-name-projectID.us.magentosite.cloud/`

   Avec un domaine partagé, utilisez le format suivant : `http://<site-URL>/<magento-run-code>`

   Par exemple, `http://master-name-projectID.us.magentosite.cloud/french/`

1. Testez minutieusement votre site et fusionnez le code dans la variable `integration` branche pour un déploiement ultérieur.

## Déploiement vers l’évaluation et la production

Suivez le processus de déploiement pour [déploiement vers l’évaluation et la production](../deploy/staging-production.md). Pour les environnements Starter et Pro, vous utilisez le [!DNL Cloud Console] pour envoyer du code à l’ensemble des environnements.

Adobe recommande de réaliser des tests complets dans l’environnement d’évaluation avant de passer à l’environnement de production. Apportez des modifications au code dans l’environnement d’intégration et commencez le processus à déployer à nouveau dans tous les environnements.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
