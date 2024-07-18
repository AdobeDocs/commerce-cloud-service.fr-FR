---
title: Module '[!DNL ECE-Tools]'
description: Découvrez le package  [!DNL ECE-Tools] et comment il permet de gérer et déployer Adobe Commerce.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Module d’outils CEE

Le package [!DNL ECE-Tools] est un ensemble de scripts et d’outils conçus pour gérer et déployer l’application [!DNL Commerce]. Le package `ece-tools` simplifie de nombreux processus, tels que la gestion des tâches cron, la vérification de la configuration du projet et l’application de correctifs et correctifs Adobes. Vous pouvez afficher et contribuer au référentiel de code [open-source [!DNL ECE-Tools] sur GitHub][ece-repo].

{{ece-tools-package}}

Le package `ece-tools` est compatible avec Adobe Commerce (à partir de la version 2.1.4) et contient des scripts et des commandes d’infrastructure de cloud Adobe Commerce conçus pour aider à gérer votre code et à créer et déployer automatiquement vos projets.

La liste suivante répertorie les commandes `ece-tools` disponibles :

```bash
php ./vendor/bin/ece-tools list
```

## Créer et déployer

Le package `ece-tools` contient des commandes permettant d’effectuer des opérations pour les étapes de création, de déploiement et de post-déploiement du lancement de votre Adobe Commerce sur l’application d’infrastructure cloud. Par exemple, la commande `php ./vendor/bin/ece-tools build` commence le processus de création de l’application.

Par défaut, ces commandes `ece-tools` se trouvent dans la propriété [hooks](../application/hooks-property.md) du fichier de configuration `.magento.app.yaml`.

## Générateur de configuration Docker

Le package `ece-tools` comprend une dépendance pour le package [magento/magento-cloud-docker], qui fournit des fonctionnalités et des fichiers de configuration pour que les images Docker lancent un environnement de développement Docker pour Adobe Commerce sur l’infrastructure cloud. Vous pouvez également exécuter Cloud Docker pour Commerce en tant que module autonome. Voir [Développement de Docker](../dev-tools/cloud-docker.md).

## Services, itinéraires et variables

Vous pouvez utiliser le package `ece-tools` pour afficher des informations détaillées sur les [variables cloud](../environment/variables-cloud.md) codées en Base64 utilisées dans n’importe quel environnement cloud. La commande suivante affiche tous les services, itinéraires et variables.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Pour afficher un ensemble d’informations spécifique, utilisez le format suivant :

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services` : affiche les données de relation de la variable d’environnement `MAGENTO_CLOUD_RELATIONSHIPS`, définies dans le fichier `services.yaml`.
- `routes` : affiche les itinéraires configurés pour le projet à l’aide de la variable d’environnement `MAGENTO_CLOUD_ROUTES`.
- `variables` : affiche les variables configurées pour le projet à l’aide de la variable d’environnement `MAGENTO_CLOUD_VARIABLES`.

Exemple de sortie pour l’option `services` :

```
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Vérification de la configuration de l’environnement

Un ensemble de commandes de vérification est disponible pour vous aider à évaluer la configuration de votre projet. Voir [Smart Wizards](../deploy/smart-wizards.md) dans la section _Optimize deployment_ pour une description détaillée de chaque commande de l’assistant. La commande `wizard:ideal-state` s’exécute automatiquement pendant la phase de génération. Pour vérifier l’état idéal de votre projet :

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Vous devez exécuter la commande `wizard:ideal-state` dans l’environnement cloud distant. La commande renvoie toujours l’erreur `The configured state is not ideal` lors de l’exécution dans l’environnement de développement local.

Exemple de sortie :

```
Ideal state is configured
```

Voir les [notes de mise à jour pour les outils de la pièce](../release-notes/cloud-tools-suite.md).

## Correctifs d’Adobe et correctifs personnalisés

Le package `ece-tools` comprend une dépendance pour le package [magento/magento-cloud-patches], qui fournit des correctifs et correctifs d’Adobe qui améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud et prennent en charge la livraison rapide de correctifs critiques. Le &quot;fournit également des correctifs personnalisés que vous ajoutez à votre projet d’infrastructure cloud Adobe Commerce. Voir [Appliquer les correctifs](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-Correctifs]: https://github.com/magento/magento-cloud-patches
