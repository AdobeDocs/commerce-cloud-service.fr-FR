---
title: Déploiement basé sur des scénarios
description: Découvrez comment personnaliser Adobe Commerce sur les déploiements d’infrastructure cloud à l’aide de fichiers de configuration personnalisés.
feature: Cloud, Configuration, Deploy, Build
exl-id: df243068-c7a3-46dd-abe9-9e05198fa343
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Déploiement basé sur des scénarios

Avec `ece-tools` 2002.1.0 et versions ultérieures, vous pouvez utiliser la fonctionnalité de déploiement basée sur un scénario pour personnaliser le comportement de déploiement par défaut.
Cette fonctionnalité utilise **scénarios** et **étapes** dans la configuration :

- **Configuration du scénario** - Chaque crochet de déploiement est un *scénario*, qui est un fichier de configuration XML qui décrit la séquence et les paramètres de configuration pour terminer les tâches de déploiement. Vous configurez les scénarios dans la section `hooks` du fichier `.magento.app.yaml`.

- **Configuration des étapes** : chaque scénario utilise une séquence de *étapes* qui décrit par programmation les opérations requises pour terminer les tâches de déploiement. Vous configurez les étapes dans un fichier de configuration de scénario XML.

Adobe Commerce sur l’infrastructure cloud fournit un ensemble de [scénarios par défaut](https://github.com/magento/ece-tools/tree/2002.1/scenario) et [étapes par défaut](https://github.com/magento/ece-tools/tree/2002.1/src/Step) dans le package `ece-tools`. Vous pouvez personnaliser le comportement du déploiement en créant des fichiers de configuration XML personnalisés pour remplacer ou personnaliser la configuration par défaut. Vous pouvez également utiliser des scénarios et des étapes pour exécuter du code à partir de modules personnalisés.

## Ajout de scénarios à l’aide de hooks de création et de déploiement

Vous ajoutez les scénarios de création et de déploiement d’Adobe Commerce à la section `hooks` du fichier `.magento.app.yaml`. Chaque point d’extension spécifie les scénarios à exécuter lors de chaque phase. L’exemple suivant illustre la configuration du scénario par défaut.

> `magento.app.yaml` hooks

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!NOTE]
>
>Avec la version de `ece-tools` 2002.1.x, il existe un nouveau format [hooks configuration](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property.html). Le format hérité des versions `ece-tools` 2002.0.x est toujours pris en charge. Cependant, vous devez effectuer une mise à jour vers le nouveau format pour utiliser la fonctionnalité de déploiement basée sur un scénario.

## Étapes du scénario de révision

Dans la configuration du crochet, chaque scénario est un fichier XML qui contient les étapes d’exécution des tâches de création, de déploiement ou de post-déploiement. Par exemple, le fichier `scenario/transfer` comprend trois étapes : `compress-static-content`, `clear-init-directory` et `backup-data`

> `scenario/transfer.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="compress-static-content" type="Magento\MagentoCloud\Step\Build\CompressStaticContent" priority="100"/>
    <step name="clear-init-directory" type="Magento\MagentoCloud\Step\Build\ClearInitDirectory" priority="200"/>
    <step name="backup-data" type="Magento\MagentoCloud\Step\Build\BackupData" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="static-content" xsi:type="object" priority="100">Magento\MagentoCloud\Step\Build\BackupData\StaticContent</item>
                <item name="writable-dirs" xsi:type="object"  priority="200">Magento\MagentoCloud\Step\Build\BackupData\WritableDirectories</item>
            </argument>
        </arguments>
    </step>
</scenario>
```

## Étendre un scénario par défaut

L’exemple suivant étend le scénario de déploiement par défaut en ajoutant des fichiers de configuration de déploiement supplémentaires à la configuration du point d’extension.

```yaml
hooks:
  deploy: |
    php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/<vendor-name>/<module-name>/deploy.xml vendor/<vendor-name>/<module-name>/deploy2.xml
```

Lors du déploiement, les scénarios personnalisés fusionnent avec le scénario par défaut en fonction des règles suivantes :

- Les scénarios sont hiérarchisés en fonction de leur séquence dans la définition du point d’extension, le dernier scénario répertorié ayant la priorité la plus élevée.

  Dans cet exemple, les scénarios ont la priorité suivante :

   1. `vendor/vendor-name/module-name/deploy2.xml`
   1. `vendor/vendor-name/module-name/deploy.xml`
   1. `scenario/deploy.xml` (scénario par défaut ou de ligne de base)

- Les étapes du scénario de priorité la plus élevée remplacent les étapes portant le même nom dans les autres scénarios. De nouvelles étapes sont ajoutées à la configuration. Les mêmes règles s’appliquent à plus de deux scénarios dont chaque scénario est hiérarchisé de droite à gauche, par exemple (C → B → A).

### Suppression des étapes par défaut

Vous supprimez les étapes des scénarios par défaut à l’aide du paramètre `skip` .

Par exemple, pour ignorer les étapes `enable-maintenance-mode` et `set-production-mode` dans le scénario de déploiement par défaut, créez un fichier de configuration qui comprend la configuration suivante.

> `vendor/vendor-name/module-name/deploy-custom-mode-config.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="enable-maintenance-mode" skip="true" />
    <step name="set-production-mode"  skip="true" />
</scenario>
```

Pour utiliser le fichier de configuration personnalisé, mettez à jour le fichier `.magento.app.yaml` par défaut.

> `.magento.app.yaml` avec scénario de déploiement personnalisé

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-custom-mode-config.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

### Remplacer les étapes par défaut

Les scénarios personnalisés peuvent remplacer les étapes par défaut pour fournir une implémentation personnalisée. Pour ce faire, utilisez le nom de l’étape par défaut comme nom de l’étape personnalisée.

Par exemple, dans le [scénario de déploiement par défaut], l’étape `enable-maintenance-mode` exécute le [ script PHP EnableMaintenanceMode par défaut].

```xml
<step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="300"/>
```

Pour remplacer cette étape, créez un fichier de configuration de scénario personnalisé afin d’exécuter un script différent lors de l’exécution de l’étape `enable-maintenance-mode`.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="VendorName\VendorModule\Step\CustomEnableMaintenanceMode" priority="300"/>
</scenario>
```

### Modification de la priorité des étapes

Les scénarios personnalisés peuvent modifier la priorité des étapes par défaut. L’étape suivante change la priorité de l’étape `enable-maintenance-mode` de `300` à `10` afin que l’étape s’exécute plus tôt dans le scénario de déploiement.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="10"/>
</scenario>
```

Dans cet exemple, l’étape `enable-maintenance-mode` se déplace au début du scénario, car elle a une priorité inférieure à toutes les autres étapes du scénario de déploiement par défaut.

### Exemple : extension du scénario de déploiement

L’exemple suivant personnalise le [scénario de déploiement par défaut] avec les modifications suivantes :

- Remplace l’étape `remove-deploy-failed-flag` par une étape personnalisée.
- Ignore le sous-projet `clean-redis-cache` lors de l’étape de pré-déploiement
- Ignore l’étape `unlock-cron-jobs`
- Ignore l’étape `validate-config` pour désactiver les validateurs critiques
- Ajoute une nouvelle étape de prédéploiement.

> `vendor/vendor-name/module-name/deploy-extended.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <!-- Replace "remove-deploy-failed-flag" step with custom step -->
    <step name="remove-deploy-failed-flag" type="Vendor\ModuleName\Step\Deploy\RemoveDeployFailedFlag" priority="100"/>

    <!-- Skip "clean-redis-cache" sub-step in pre-deploy step -->
    <step name="pre-deploy" type="Magento\MagentoCloud\Step\Deploy\PreDeploy" priority="200">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="clean-redis-cache" xsi:type="object" skip="true"/>
            </argument>
        </arguments>
    </step>

    <!-- Skip step "unlock-cron-jobs" -->
    <step name="unlock-cron-jobs" skip="true"/>

    <!-- Skip critical validators -->
    <step name="validate-config" type="Magento\MagentoCloud\Step\ValidateConfiguration" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="validators" xsi:type="array">
                <item name="critical" xsi:type="array">
                    <item name="database-configuration" xsi:type="object" skip="true"/>
                    <item name="search-configuration" xsi:type="object" skip="true"/>
                </item>
            </argument>
        </arguments>
    </step>

    <!-- Add new step into the beginning of the deploy scenario -->
    <step name="new-pre-deploy-step" type="Vendor\ModuleName\Step\Deploy\PreDeploy" priority="10"/>
</scenario>
```

Pour utiliser ce script dans votre projet, ajoutez la configuration suivante au fichier `.magento.app.yaml` de votre projet d’infrastructure cloud Adobe Commerce :

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-extended.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!TIP]
>
>Vous pouvez passer en revue les [scénarios par défaut](https://github.com/magento/ece-tools/tree/2002.1/scenario) et la [ configuration d’étape par défaut](https://github.com/magento/ece-tools/tree/2002.1/src/Step) dans le référentiel GitHub `ece-tools` afin de déterminer les scénarios et les étapes à personnaliser pour les tâches de création, de déploiement et de post-déploiement de votre projet.

## Ajouter un module personnalisé pour étendre `ece-tools`

Le package `ece-tools` fournit des interfaces API par défaut qui respectent les normes de version sémantique. Toutes les interfaces API sont marquées d’une annotation **@api**. Vous pouvez remplacer l’implémentation de l’API par défaut par la vôtre en créant un module personnalisé et en modifiant le code par défaut selon vos besoins.

Pour utiliser le module personnalisé avec Adobe Commerce sur l’infrastructure cloud, vous devez enregistrer votre module dans la liste des extensions pour le module `ece-tools`. Le processus d’enregistrement est similaire au processus que vous utilisez pour enregistrer les modules dans Adobe Commerce.

**Pour enregistrer un module avec le `ece-tools` package** :

1. Créez ou étendez le fichier `registration.php` à la racine de votre module.

   ```php?start_inline=1
   \Magento\MagentoCloud\ExtensionRegistrar::register('module-name', __DIR__);
   ```

1. Mettez à jour la section `autoload` de votre fichier de configuration de module afin d’inclure le fichier `registration.php` pour charger automatiquement les fichiers de module dans `composer.json`.

   ```json
   {
     "name": "vendor/ece-tools-extend",
     "description": "Extension for ece-tools",
     "type": "magento2-component",
     "version": "1.0.0",
     "license": "OSL-3.0",
     "autoload": {
       "files": [ "registration.php" ],
       "psr-4": {
         "Vendor\\EceToolExtend\\": "src/"
       }
     }
   }
   ```

1. Ajoutez le fichier `config/services.xml` à votre module. Cette configuration est fusionnée sur `config/services.xml` à partir du package `ece-tools`.

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <container xmlns="http://symfony.com/schema/dic/services"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://symfony.com/schema/dic/services https://symfony.com/schema/dic/services/services-1.0.xsd">
       <services>
           <defaults autowire="true" autoconfigure="true" public="true"/>
   
           <prototype namespace="Vendor\EceToolExtend\" resource="../src/*" exclude="../src/{Test}"/>
   
           <!-- Use your own implementation of EnvironmentDataInterface -->
           <service id="Magento\MagentoCloud\Config\EnvironmentDataInterface" alias="Vendor\EceToolExtend\Config\CustomEnvironmentData" />
       </services>
   </container>
   ```

Pour en savoir plus sur l’injection de dépendance, voir [Symfony Dependency Injection](https://symfony.com/doc/current/components/dependency_injection.html).

<!-- link definitions -->

[scénario de déploiement par défaut]: https://github.com/magento/ece-tools/blob/develop/scenario/deploy.xml
[Script PHP EnableMaintenanceMode]: https://github.com/magento/ece-tools/blob/develop/src/Step/EnableMaintenanceMode.php
