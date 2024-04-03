---
title: Variables de post-déploiement
description: Consultez la liste des variables d’environnement qui contrôlent les actions dans Adobe Commerce lors de la phase de post-déploiement de l’infrastructure cloud.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: 8b02757591c4e8f607e936de4eda74d76953d9b7
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variables de post-déploiement

Les éléments suivants _post-déploiement_ contrôlent les actions lors de la phase de post-déploiement et peuvent hériter et remplacer des valeurs de la variable [Variables globales](variables-global.md). Insérez ces variables dans le `post-deploy` étape de la `.magento.env.yaml` fichier :

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

Pour plus d’informations sur la personnalisation du processus de création et de déploiement :

- [Configuration du déploiement](configure-env-yaml.md)
- [Processus de déploiement](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **Par défaut**— `[]` (un tableau vide)
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Configurer _Time To First Byte_ (TTF) Test de pages spécifiées pour tester les performances de votre site. Spécifiez une référence de chemin absolu, ou URL avec protocole et hôte, pour chaque page qui nécessite le test.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

Une fois que vous avez spécifié les pages à tester et validé les modifications, la variable _Time To First Byte_ test s’exécute pendant la phase de post-déploiement et publie des résultats pour chaque chemin d’accès au journal cloud :

```terminal
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

Pour les chemins de redirection, le journal indique le chemin de la cible de redirection au lieu de celui configuré dans la variable d’environnement. Si vous spécifiez un chemin non valide, le journal affiche un message d’avertissement.

## `WARM_UP_CONCURRENCY`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Spécifiez la limite des demandes simultanées à envoyer lors des opérations de réchauffement du cache afin de réduire la charge du serveur. Cette valeur limite le nombre de connexions parallèles et est utile pour les configurations d’environnement où la variable `WARM_UP_PAGES` La variable post-deploy spécifie plusieurs pages pour le préchargement du cache.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Par défaut**— `index.php`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Personnaliser la liste des pages utilisées pour précharger le cache dans le `post_deploy` scène. Vous devez configurer le crochet de post-déploiement. Voir [section hooks](../application/hooks-property.md) de `.magento.app.yaml` fichier .

- **une seule page**: spécifiez une seule page à ajouter au cache. Vous n’avez pas à indiquer l’URL de base par défaut. L’exemple suivant met en cache la variable `BASE_URL/index.php` page :

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **plusieurs domaines**: répertorie plusieurs URL. L’exemple suivant met en cache des pages provenant de deux domaines :

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **plusieurs pages**: utilisez le format suivant pour mettre en cache plusieurs pages en fonction d’un modèle d’expression régulière spécifique :

  ```terminal
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: variantes possibles `category`, `cms-page`, `product`, `store-page`
   - `pattern|url|product_sku`: utilisez un `regexp` modèle ou correspondance exacte `url` pour filtrer les URL ou utilisez un astérisque (\*) pour toutes les pages. Utilisez le SKU du produit pour la variable `product` type d&#39;entité
   - `store_id|store_code`: utilisez l’identifiant ou le code du magasin ou un astérisque (\*) pour tous les magasins. Vous pouvez transmettre plusieurs identifiants ou codes de magasin séparés par `|`

  L’exemple suivant met en cache des `category` et `cms-page` types d’entités selon les critères suivants :
   - toutes les pages de catégorie pour le magasin avec ID `1`
   - toutes les pages de catégorie pour les magasins avec du code ; `store1` et `store2`
   - page de catégorie `cars` pour le magasin avec du code `store_en`
   - page cms `contact` pour tous les magasins
   - page cms `contact` pour les magasins avec ID `1` et `2`
   - toute page de catégorie contenant `car_` et se termine par `html` pour le magasin avec ID 2
   - toute page de catégorie contenant `tires_` pour le magasin avec du code `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  L’exemple suivant met en cache la variable `product` type d’entité selon les critères suivants :
   - tous les produits pour tous les magasins (par programmation limitée à 100 par magasin afin d’éviter des problèmes de performances) ;
   - tous les produits pour la boutique `store1`
   - produits avec `sku1` pour tous les magasins
   - produits avec `sku1` pour les magasins avec code `store1` et `store2`
   - produits avec `sku1`, `sku2` et `sku3` pour les magasins avec code `store1` et `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  L’exemple suivant met en cache la variable `store-page` type d’entité selon les critères suivants :
   - page `/contact-us` pour tous les magasins
   - page `/contact-us` pour le magasin avec ID `1`
   - page `/contact-us` pour les magasins avec code `code1` et `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
