---
title: Créer des variables
description: Consultez la liste des variables d’environnement qui contrôlent les actions dans Adobe Commerce lors de la phase de création de l’infrastructure cloud.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Créer des variables

Les variables _build_ suivantes contrôlent les actions pendant la phase de génération et peuvent hériter et remplacer des valeurs des [variables globales](variables-global.md). Insérez ces variables à l’étape `build` du fichier `.magento.env.yaml` :

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Pour plus d’informations sur la personnalisation du processus de création et de déploiement :

- [Configuration du déploiement](configure-env-yaml.md)
- [Processus de déploiement](../deploy/process.md)

Les variables suivantes ont été supprimées dans la version v2.2 :

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Par défaut**—`1`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définissez le niveau d’imbrication de répertoires pour enregistrer les fichiers de rapport d’erreur afin d’éviter de remplir le répertoire de rapports avec des dizaines de milliers de fichiers, ce qui peut rendre difficile la gestion et la révision des données. Ce paramètre est défini par défaut sur `1`. En règle générale, vous n’avez pas besoin de modifier la valeur par défaut, sauf si vous rencontrez des problèmes pour gérer les fichiers de rapport d’erreur dans le répertoire `<magento_root>/var/report/`.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Spécifiez une liste de correctifs de qualité Adobe Commerce à appliquer lors du déploiement.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

L’exemple suivant indique trois correctifs à appliquer lors du déploiement.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Voir [Appliquer les correctifs](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

- **Par défaut**—`6`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Spécifie le niveau de compression [gzip](https://www.gnu.org/software/gzip) (`0` à `9`) à utiliser lors de la compression du contenu statique ; `0` désactive la compression.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Par défaut**—`600`
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Lorsque le temps nécessaire à la compression des ressources statiques dépasse la limite du délai d’expiration de compression, cela interrompt le processus de déploiement. Définissez la durée d’exécution maximale, en secondes, de la commande de compression de contenu statique.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Par défaut**—`false`
- **Version**—Adobe Commerce 2.4.2 et versions ultérieures

Définissez cette variable sur `true` pour empêcher la génération de contenu statique pour les thèmes parents pendant la phase de création.

Définissez `SCD_NO_PARENT: false` pendant la phase de génération de sorte que la génération du contenu statique pour les thèmes parents n’affecte pas le déploiement du site ou n’entraîne pas de temps d’arrêt inutile du site. Voir [Déploiement de contenu statique](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Vous pouvez configurer plusieurs paramètres régionaux par thème. Cette personnalisation permet d’accélérer le processus de création en réduisant le nombre de fichiers de thème inutiles. Par exemple, vous pouvez créer le thème _magento/backend_ en anglais et un thème personnalisé dans d’autres langues.

L’exemple suivant crée le thème `Magento/backend` avec trois paramètres régionaux :

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

L’exemple suivant crée trois thèmes avec trois paramètres régionaux :

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Vous pouvez également choisir de _ne pas_ déployer un thème :

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Permet d’augmenter le temps d’exécution maximum prévu pour le déploiement de contenu statique.

Par défaut, Adobe Commerce sur l’infrastructure cloud définit l’exécution maximale prévue à 900 secondes, mais dans certains scénarios, vous devrez peut-être plus de temps pour terminer le déploiement de contenu statique pour un projet Cloud.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Par défaut**—`quick`
- **Version**—Adobe Commerce 2.2.0 et versions ultérieures

Personnalisez la [stratégie de déploiement](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) pour le contenu statique. Voir [Déploiement de fichiers d’affichage statique](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Utilisez ces options _only_ si vous avez plusieurs paramètres régionaux :

- `standard` : déploie tous les fichiers d’affichage statique pour tous les modules.
- `quick`—(_default_) minimise le temps de déploiement.
- `compact` : conserve l’espace disque sur le serveur. Dans Adobe Commerce version 2.2.4 et antérieure, ce paramètre remplace la valeur de `scd_threads` par une valeur de `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Default**—Automatique
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définit le nombre de threads pour le déploiement de contenu statique. La valeur par défaut est définie en fonction du nombre de threads du processeur détecté et ne dépasse pas une valeur de 4. L’augmentation du nombre de threads accélère le déploiement de contenu statique ; la réduction du nombre de threads la ralentit. Vous pouvez définir la valeur de thread, par exemple :

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Pour réduire davantage le temps de déploiement, utilisez [Configuration Management](../store/store-settings.md) avec la commande `scd-dump` pour passer au déploiement statique dans la phase de création.

## `SCD_USE_BALER`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.3.0 et versions ultérieures

[Baler](https://github.com/magento/baler) analyse le code JavaScript généré et crée un lot JavaScript optimisé. Le déploiement du lot optimisé sur votre site peut réduire le nombre de requêtes réseau lors du chargement de votre site et améliorer les temps de chargement des pages.

Définissez cette variable sur `true` pour exécuter Baler après l’exécution du déploiement de contenu statique.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Étant donné que Baler est dans une version alpha, il n’est pas recommandé de l’utiliser dans les environnements de production.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Par défaut**— _Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définissez cette variable sur `true` pour ignorer la commande `composer dump-autoload` lors de l’installation de Cloud Docker. Cette variable ne s’applique qu’aux conteneurs Cloud Docker avec des systèmes de fichiers modifiables. Dans ce cas, ignorer la commande empêche les erreurs d’autres commandes d’accéder au code du répertoire `generated` supprimé.

Lorsqu’Adobe Commerce exécute `composer dump-autoload`, il crée des fichiers de chargement automatique avec des liens vers des classes générées dans le dossier `generated`, ce qui n’est pas un problème dans les environnements de production avec des systèmes de fichiers en lecture seule. Toutefois, pour les installations de Cloud Docker avec des systèmes de fichiers modifiables (créés uniquement à des fins de test et de développement à l’aide de `./vendor/bin/ece-docker build:compose --with-test`), vous pouvez exécuter la commande `bin/magento -n setup:upgrade` sans l’option `--keep-generated`, ce qui supprime le répertoire `generated`. Si le répertoire est supprimé, la commande `composer dump-autoload` échoue, car le chargement automatique contient des liens vers des fichiers du répertoire supprimé.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Par défaut**— _Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Définissez cette variable sur `true` pour ignorer le déploiement de contenu statique pendant la phase de création.

Si vous déployez déjà du contenu statique pendant la phase de création avec [Configuration Management](../store/store-settings.md), vous pouvez ignorer le déploiement de contenu statique pour un test de création rapide.

Lors de la phase de création, définissez `SKIP_SCD: false` de sorte que la génération de contenu statique se produise pendant la phase de création, lorsque le processus n’a aucune incidence sur le déploiement du site ou provoque des temps d’arrêt inutiles du site. Voir [Déploiement de contenu statique](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Par défaut**—_Non défini_
- **Version**—Adobe Commerce 2.1.4 et versions ultérieures

Activez ou désactivez le niveau de détail de débogage [Symfony](https://symfony.com/doc/current/console/verbosity.html) pour les commandes d’interface de ligne de commande `bin/magento` exécutées pendant la phase de déploiement.

>[!NOTE]
>
>Pour utiliser VERBOSE_COMMANDS afin de contrôler les détails de la sortie de commande pour les commandes CLI `bin/magento` réussies et échouées, vous devez définir [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Sélectionnez le niveau de détail fourni dans les logs :

- `-v`= sortie normale
- `-vv`= sortie plus détaillée
- `-vvv` = sortie verbeuse idéale pour le débogage

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
