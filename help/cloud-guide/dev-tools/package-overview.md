---
title: '[!DNL ECE-Tools] Package'
description: En savoir plus sur les [!DNL ECE-Tools] module et de la manière dont il permet de gérer et de déployer Adobe Commerce.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Module d’outils CEE

La variable [!DNL ECE-Tools] Le module est un ensemble de scripts et d’outils conçus pour gérer et déployer le [!DNL Commerce] application. La variable `ece-tools` package simplifie de nombreux processus, tels que la gestion des tâches cron, la vérification de la configuration du projet et l’application de correctifs et correctifs Adobes. Vous pouvez afficher et contribuer au [open source [!DNL ECE-Tools] référentiel de code sur GitHub][ece-repo].

{{ece-tools-package}}

La variable `ece-tools` est compatible avec Adobe Commerce (à partir de la version 2.1.4) et contient des scripts et Adobe Commerce sur les commandes d’infrastructure cloud conçues pour vous aider à gérer votre code et à créer et déployer automatiquement vos projets.

La liste suivante répertorie les `ece-tools` Commandes :

```bash
php ./vendor/bin/ece-tools list
```

## Créer et déployer

La variable `ece-tools` Le module contient des commandes permettant d’effectuer des opérations pour les étapes de création, de déploiement et de post-déploiement du lancement d’Adobe Commerce sur l’application d’infrastructure cloud. Par exemple, la variable `php ./vendor/bin/ece-tools build` lance le processus de création de l’application.

Par défaut, ces `ece-tools` Les commandes se trouvent dans la fonction [hooks, propriété](../application/hooks-property.md) de `.magento.app.yaml` fichier de configuration.

## Générateur de configuration Docker

La variable `ece-tools` comprend une dépendance pour la variable [magento/magento-cloud-docker] qui fournit des fonctionnalités et des fichiers de configuration pour les images Docker afin de lancer un environnement de développement Docker pour Adobe Commerce sur l’infrastructure cloud. Vous pouvez également exécuter Cloud Docker pour Commerce en tant que module autonome. Voir [Développement de Docker](../dev-tools/cloud-docker.md).

## Services, itinéraires et variables

Vous pouvez utiliser la variable `ece-tools` pour afficher des informations détaillées sur le codage Base64 [Variables cloud](../environment/variables-cloud.md) utilisé dans n’importe quel environnement cloud. La commande suivante affiche tous les services, itinéraires et variables.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Pour afficher un ensemble d’informations spécifique, utilisez le format suivant :

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services`: affiche les données de relation de la variable `MAGENTO_CLOUD_RELATIONSHIPS` Variable d’environnement, définie dans la variable `services.yaml` fichier .
- `routes`: affiche les itinéraires configurés pour le projet à l’aide de la variable `MAGENTO_CLOUD_ROUTES` Variable d’environnement.
- `variables`: affiche les variables configurées pour le projet à l’aide de la variable `MAGENTO_CLOUD_VARIABLES` Variable d’environnement.

Exemple de sortie pour le `services` option :

```terminal
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

Un ensemble de commandes de vérification est disponible pour vous aider à évaluer la configuration de votre projet. Voir [Assistant dynamique](../deploy/smart-wizards.md) dans le _Optimisation du déploiement_ pour une description détaillée de chaque commande de l&#39;assistant. La variable `wizard:ideal-state` s’exécute automatiquement pendant la phase de création. Pour vérifier l’état idéal de votre projet :

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Vous devez exécuter la variable `wizard:ideal-state` dans l’environnement cloud distant. La commande renvoie toujours le `The configured state is not ideal` lors de l’exécution dans l’environnement de développement local.

Exemple de sortie :

```terminal
Ideal state is configured
```

Voir [Notes de mise à jour de ece Tools](../release-notes/cloud-tools-suite.md).

## Correctifs d’Adobe et correctifs personnalisés

La variable `ece-tools` comprend une dépendance pour la variable [magento/magento-cloud-Correctifs] qui fournit des correctifs d’Adobe et des correctifs qui améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud et prennent en charge la livraison rapide de correctifs critiques. Le &quot;fournit également des correctifs personnalisés que vous ajoutez à votre projet d’infrastructure cloud Adobe Commerce. Voir [Appliquer les correctifs](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-Correctifs]: https://github.com/magento/magento-cloud-patches
