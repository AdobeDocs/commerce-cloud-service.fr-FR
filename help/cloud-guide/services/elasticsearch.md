---
title: Configuration du service Elasticsearch
description: Découvrez comment activer le service Elasticsearch pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Search, Services
exl-id: ac559cbb-342a-4756-ade5-49eba4827965
source-git-commit: c39332d352f6dcb6f92c312a6ef1b74319d37aa3
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Configuration du service Elasticsearch

[Elasticsearch](https://www.elastic.co) est un produit open source qui vous permet de récupérer des données de n’importe quelle source, n’importe quel format, de les rechercher et de les visualiser en temps réel.

{{elasticsearch-support}}

Pour Adobe Commerce version 2.4.4 et ultérieure, voir [Configuration du service OpenSearch](opensearch.md).

- Elasticsearch effectue des recherches rapides et avancées sur les produits du catalogue de produits.
- Les analyseurs Elasticsearch prennent en charge plusieurs langues
- Prend en charge les mots vides et les synonymes
- L’indexation n’affecte pas les clients tant que l’opération de réindexation n’est pas terminée.

>[!TIP]
>
>Adobe recommande de toujours configurer Elasticsearch pour votre projet d’infrastructure cloud Adobe Commerce, même si vous envisagez de configurer un outil de recherche tiers pour votre application Adobe Commerce. La configuration de Elasticsearch fournit une option de secours en cas d’échec de l’outil de recherche tiers.

{{service-instruction}}

**Pour activer Elasticsearch** :

1. Pour les projets de démarrage, ajoutez le service `elasticsearch` au fichier `.magento/services.yaml` avec la version Elasticsearch et allouez de l’espace disque en Mo.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   Pour les projets Pro, vous devez envoyer un ticket d’assistance Adobe Commerce pour modifier la version Elasticsearch dans les environnements d’évaluation et de production.

1. Définissez la propriété `relationships` dans le fichier `.magento.app.yaml`.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   Pour plus d&#39;informations sur la façon dont ces modifications affectent vos environnements, voir [Services](services-yaml.md).

1. Une fois le processus de déploiement terminé, utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Réindexez l’index de recherche catalogue.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Nettoyez le cache.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## Compatibilité des logiciels Elasticsearch

Lorsque vous installez ou mettez à niveau votre Adobe Commerce sur le projet d’infrastructure cloud, vérifiez toujours la compatibilité entre la version de service Elasticsearch et le client [PHP Elasticsearch](https://github.com/elastic/elasticsearch-php) pour Adobe Commerce.

- **Première configuration** - Confirmez que la version Elasticsearch spécifiée dans le fichier `services.yaml` est compatible avec le client PHP Elasticsearch configuré pour Adobe Commerce.

- **Mise à niveau du projet** - Vérifiez que le client PHP Elasticsearch dans la nouvelle version de l’application est compatible avec la version du service Elasticsearch installée sur l’infrastructure cloud.

La prise en charge de la version du service et de la compatibilité pour Adobe Commerce sur l’infrastructure cloud est déterminée par les versions déployées sur l’infrastructure cloud et diffère parfois des versions prises en charge par les déploiements sur site d’Adobe Commerce. Voir [Versions de service](services-yaml.md#service-versions).

**Pour vérifier la compatibilité des logiciels Elasticsearch** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Affichez les détails de l’Elasticsearch pour l’environnement actif.

   ```bash
   magento-cloud relationships --property=elasticsearch
   ```

1. Vous pouvez également utiliser SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Vérifiez la version du package du compositeur pour `elasticsearch/elasticsearch`.

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   Dans la réponse, vérifiez la version installée dans la propriété `versions`.

   ```
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v7.17.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org/licenses/Apache-2.0.html#licenseText
   license  : GNU Lesser General Public License v2.1 only (LGPL-2.1-only) (OSI approved) https://spdx.org/licenses/LGPL-2.1-only.html#licenseText
   homepage :
   source   : [git] git@github.com:elastic/elasticsearch-php.git f1b8918f411b837ce5f6325e829a73518fd50367
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/f1b8918f411b837ce5f6325e829a73518fd50367 f1b8918f411b837ce5f6325e829a73518fd50367
   path     : ~/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   Vous trouverez également la version du client PHP Elasticsearch dans le fichier `composer.lock` du répertoire racine de l’environnement.

1. Dans la ligne de commande, récupérez les détails de connexion au service Elasticsearch.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   Dans la réponse, recherchez l’adresse IP du point de terminaison du service Elasticsearch :

   ```
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. Récupérez le service Elasticsearch installé `version:number` à partir du point d’entrée de service.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```json
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Vérifiez la compatibilité des versions entre le service Elasticsearch et le client PHP.

   Si les versions sont incompatibles, effectuez l’une des mises à jour suivantes sur la configuration de votre environnement :

   - Remplacez le client PHP Elasticsearch par une version compatible avec la version du service Elasticsearch.

     ```bash
     composer require "elasticsearch/elasticsearch:~<version>"
     ```

   - Remplacez la version du service Elasticsearch du fichier `services.yaml` par une version compatible avec le client PHP Elasticsearch.

     {{pro-update-service}}

## Redémarrer le service Elasticsearch

Si vous devez redémarrer le service [Elasticsearch](https://www.elastic.co), vous devez contacter le support Adobe Commerce.

## Configuration de recherche supplémentaire

- Par défaut, la configuration de recherche des environnements Cloud se régénère chaque fois que vous déployez. Vous pouvez utiliser la variable de déploiement `SEARCH_CONFIGURATION` pour conserver les paramètres de recherche personnalisés entre les déploiements. Voir [Déploiement de variables](../environment/variables-deploy.md#search_configuration).

- Après avoir configuré le service Elasticsearch pour votre projet, utilisez l’interface utilisateur d’administration pour tester la connexion Elasticsearch et personnaliser les paramètres Elasticsearch pour Adobe Commerce.

### Ajout de modules externes pour Elasticsearch

Vous pouvez éventuellement ajouter des modules externes pour Elasticsearch en ajoutant la section `configuration:plugins` au service Elasticsearch dans le fichier `.magento/services.yaml`. Par exemple, le code suivant active les modules complémentaires Analyse de l’ICU et Analyse phonétique.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Si vous utilisez le module externe tiers d’Elastic Suite, vous devez [mettre à jour le `ece-tools` package](../dev-tools/update-package.md) vers la version 2002.0.19 ou ultérieure.
Lors de la configuration d’Elastic Suite, ajoutez les paramètres de configuration à la variable de déploiement `ELASTICSUITE_CONFIGURATION`. Cette configuration enregistre les paramètres pour tous les déploiements.

### Suppression de modules externes pour Elasticsearch

La suppression des entrées du module externe de `elasticsearch:` dans `.magento/services.yaml` ne les désinstalle pas ou ne les désactive pas comme prévu. Vous devez réindexer vos données Elasticsearch. Ce comportement est intentionnel afin d’empêcher toute perte ou corruption de données qui dépend de ces modules externes.

**Pour supprimer les modules externes d’Elasticsearch** :

1. Supprimez les entrées de module externe Elasticsearch de votre fichier `.magento/services.yaml`.
1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Validez les modifications `.magento/services.yaml` apportées à votre référentiel Cloud.
1. Réindexez l’index de recherche catalogue.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Nettoyez le cache.

   ```bash
   bin/magento cache:clean
   ```

>[!TIP]
>
>Pour plus d’informations sur l’utilisation ou le dépannage du module externe d’Elastic Suite avec Adobe Commerce, consultez la [documentation d’Elastic Suite](https://github.com/Smile-SA/elasticsuite).

## Dépannage

Pour obtenir de l’aide sur la résolution des problèmes des Elasticsearch, reportez-vous aux articles suivants du support Adobe Commerce :

- [Elasticsearch 5 est configuré, mais la page de recherche ne se charge pas avec &quot;Field data is disabled...&quot; erreur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html)
- [La pagination du catalogue ne fonctionne pas lorsque Elasticsearch 6.x est utilisé](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/catalog-pagination-doesn-t-work-when-elasticsearch-6.x-is-used.html)
- [Elasticsearch dans l’outil de dépannage Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-in-magento-troubleshooter.html)
- [ {Elasticsearch Index Status is `yellow` or `red`](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-index-status-is-yellow-or-red.html)
