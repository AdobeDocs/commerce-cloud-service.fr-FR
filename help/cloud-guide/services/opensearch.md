---
title: Configuration du service OpenSearch
description: Découvrez comment activer le service OpenSearch pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Search, Services
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Configuration du service OpenSearch

Le service [OpenSearch](https://www.opensearch.org) est un branchement open source de 7.10.2 Elasticsearch, suite aux modifications de licence de l’Elasticsearch. Voir le [projet OpenSource](https://github.com/opensearch-project) dans GitHub.

{{elasticsearch-support}}

OpenSearch vous permet d’extraire des données de n’importe quelle source, n’importe quel format, de les rechercher et de les visualiser en temps réel.

- Recherches rapides et avancées sur les produits du catalogue de produits
- Les analyseurs OpenSearch prennent en charge plusieurs langues
- Prend en charge les mots vides et les synonymes
- L’indexation n’affecte pas les clients tant que l’opération de réindexation n’est pas terminée.

{{service-instruction}}

>[!TIP]
>
>Adobe recommande de toujours configurer OpenSearch pour votre projet d’infrastructure cloud Adobe Commerce, même si vous envisagez de configurer un outil de recherche tiers pour votre application Adobe Commerce. La configuration d’OpenSearch fournit une option de secours en cas d’échec de l’outil de recherche tiers.

**Pour activer OpenSearch** :

1. Pour les environnements d’intégration Starter et Pro, ajoutez le service `opensearch` au fichier `.magento/services.yaml` avec la version appropriée et allouez de l’espace disque en Mo. Dans ce cas, la version 2 est appropriée. La version mineure n’est pas requise, car l’infrastructure cloud utilise la dernière version d’OpenSearch.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   Pour les projets Pro, vous devez [envoyer un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour modifier la version OpenSearch dans les environnements d’évaluation et de production.

1. Définissez ou vérifiez la propriété `relationships` dans le fichier `.magento.app.yaml`.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   Pour plus d&#39;informations sur la façon dont ces modifications affectent vos environnements, voir [Configuration des services](services-yaml.md).

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

## Compatibilité des logiciels OpenSearch

Lorsque vous installez ou mettez à niveau votre Adobe Commerce sur le projet d’infrastructure cloud, vérifiez toujours la compatibilité entre la version du service OpenSearch et le client [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php) pour Adobe Commerce.

- **Première configuration** - Confirmez que la version OpenSearch spécifiée dans le fichier `services.yaml` est compatible avec le client PHP OpenSearch configuré pour Adobe Commerce.

- **Mise à niveau du projet** - Vérifiez que le client PHP OpenSearch de la nouvelle version de l’application est compatible avec la version du service OpenSearch installée sur l’infrastructure cloud.

La prise en charge de la version du service et de la compatibilité est déterminée par les versions testées et déployées sur l’infrastructure cloud et diffère parfois des versions prises en charge par les déploiements sur site d’Adobe Commerce. Pour obtenir la liste des versions prises en charge, reportez-vous à la section [Configuration système requise](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) du _Guide d’installation_.

**Pour vérifier la compatibilité des logiciels OpenSearch** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Affichez les détails OpenSearch pour l’environnement actif.

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. Vous pouvez également utiliser SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Récupérez les détails de connexion du service OpenSearch.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   Dans la réponse, recherchez l’adresse IP et le port du point d’entrée du service OpenSearch :

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. Récupérez le service OpenSearch `version:number` installé à partir du point de terminaison du service.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## Redémarrer le service OpenSearch

Si vous devez redémarrer le service OpenSearch, vous devez contacter le support Adobe Commerce.

## Configuration de recherche supplémentaire

- Par défaut, la configuration de recherche des environnements Cloud se régénère chaque fois que vous déployez. Vous pouvez utiliser la variable de déploiement `SEARCH_CONFIGURATION` pour conserver les paramètres de recherche personnalisés entre les déploiements. Voir [Déploiement de variables](../environment/variables-deploy.md#search_configuration).

- Après avoir configuré le service OpenSearch pour votre projet, utilisez l’interface utilisateur d’administration pour tester la connexion OpenSearch et personnaliser les paramètres OpenSearch pour Adobe Commerce.

### Ajout de modules externes pour OpenSearch

Vous pouvez éventuellement ajouter des modules externes pour OpenSearch en ajoutant la section `configuration:plugins` au service OpenSearch dans le fichier `.magento/services.yaml`. Par exemple, le code suivant active les modules complémentaires Analyse de l’ICU et Analyse phonétique.

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Pour plus d’informations sur les modules externes, voir le [projet OpenSearch](https://github.com/opensearch-project) .

### Suppression de modules externes pour OpenSearch

La suppression des entrées du module externe de la section `opensearch:` du fichier `.magento/services.yaml` ne désinstalle pas **ni ne désactive le service.** Pour désactiver complètement le service, vous devez réindexer vos données OpenSearch après avoir supprimé les modules externes de votre fichier `.magento/services.yaml`. Cette conception empêche la perte ou la corruption possible des données qui dépendent de ces modules externes.

**Pour supprimer les modules externes OpenSearch** :

1. Supprimez les entrées du module externe OpenSearch de votre fichier `.magento/services.yaml`.
1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Validez les modifications `.magento/services.yaml` apportées à votre référentiel cloud.
1. Réindexez l’index de recherche catalogue.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Nettoyez le cache.

   ```bash
   bin/magento cache:clean
   ```
