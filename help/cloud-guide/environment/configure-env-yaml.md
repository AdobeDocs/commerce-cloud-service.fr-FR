---
title: Configuration de l’environnement
description: Découvrez comment configurer des actions de création et de déploiement sur l’ensemble des environnements de commerce sur l’infrastructure cloud, y compris Pro Staging et Production, à l’aide de variables d’environnement.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Configuration des variables d’environnement pour le déploiement

La variable `.magento.env.yaml` Le fichier utilise des variables d’environnement pour centraliser la gestion des actions de création et de déploiement dans tous vos environnements, y compris Pro Staging et Production. Pour configurer des actions uniques dans chaque environnement, vous devez modifier ce fichier dans chaque environnement.

>[!TIP]
>
>Les fichiers YAML sont sensibles à la casse et n’autorisent pas les onglets. Veillez à utiliser une mise en retrait cohérente dans l’ensemble des `.magento.env.yaml` ou votre configuration peut ne pas fonctionner comme prévu. Les exemples de la documentation et du fichier d’exemple utilisent _deux espaces_ retrait. Utilisez la variable [commande de validation d’outils-pièce](#validate-configuration-file) pour vérifier votre configuration.

## Structure du fichier

La variable `.magento.env.yaml` contient deux sections : `stage` et `log`. La variable `stage` contrôle les actions qui se produisent pendant les phases de la fonction [Processus de déploiement dans le cloud](../deploy/process.md).

- `stage`: utilisez la section d’étape pour définir certaines actions pour les étapes de déploiement suivantes :
   - `global`: contrôle les actions dans les phases de création, de déploiement et de post-déploiement. Vous pouvez remplacer ces paramètres dans les sections de création, de déploiement et de post-déploiement .
   - `build`: contrôle les actions uniquement lors de la phase de création. Si vous ne spécifiez aucun paramètre dans cette section, la phase de création utilise les paramètres de la section globale.
   - `deploy`: contrôle les actions uniquement pendant la phase de déploiement. Si vous ne spécifiez aucun paramètre dans cette section, la phase de déploiement utilise les paramètres de la section globale.
   - `post-deploy`—Actions de contrôle _after_ déploiement de votre application et _after_ le conteneur commence à accepter les connexions.
- `log`: utilisez la section de journal pour configurer [notifications](set-up-notifications.md), y compris les types de notification et le niveau de détail.
   - `slack`: configurez un message à envoyer à un robot de Slack.
   - `email`: configurez un email à envoyer à un ou plusieurs destinataires.
   - [gestionnaires de logs](log-handlers.md): configurez les messages d’application logicielle et matérielle envoyés à un serveur de journalisation distant.

### Variables d’environnement

La variable `ece-tools` définit les valeurs dans la variable `env.php` fichier en fonction des valeurs de [Variables cloud](variables-cloud.md), variables définies dans la variable [!DNL Cloud Console], et la variable `.magento.env.yaml` fichier de configuration. Les variables d’environnement dans la variable `.magento.env.yaml` personnalisez l’environnement cloud en remplaçant votre configuration Commerce existante. Si une valeur par défaut est `Not Set`, puis la variable `ece-tools` prises de package **NON** et utilise la variable [!DNL Commerce] valeur par défaut ou issue de la configuration MAGENTO_CLOUD_RELATIONSHIPS. Si la valeur par défaut est définie, la variable `ece-tools` Le package agit pour définir cette valeur par défaut.

Les rubriques suivantes contiennent des définitions détaillées, par exemple si une valeur par défaut est définie ou non, de toutes les variables que vous pouvez utiliser dans la variable `.magento.env.yaml` fichier :

- [Global](variables-global.md)—les variables contrôlent les actions dans chaque phase : création, déploiement et post-déploiement
- [Build](variables-build.md)—les variables contrôlent les actions de création
- [Déployer](variables-deploy.md)—variables contrôle les actions de déploiement
- [Post-déploiement](variables-post-deploy.md)—les variables contrôlent les actions après déploiement

### Création d’un fichier de configuration à partir de l’interface de ligne de commande

Vous pouvez générer une `.magento.env.yaml` fichier de configuration pour un environnement cloud à l’aide des éléments suivants `ece-tools` des commandes.

>Crée un fichier de configuration

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Mise à jour des valeurs dans le fichier de configuration

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Les deux commandes nécessitent un seul argument : un tableau au format JSON qui spécifie une valeur pour au moins une variable de création, de déploiement ou de post-déploiement. Par exemple, la commande suivante définit les valeurs de la variable `SCD_THREADS` et `CLEAN_STATIC_FILES` variables :

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

Et crée une `.magento.env.yaml` avec les paramètres suivants :

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

Vous pouvez utiliser la variable `cloud:config:update` pour mettre à jour le nouveau fichier. Par exemple, la commande suivante modifie la fonction `SCD_THREADS` et ajoute la valeur `SCD_COMPRESSION_TIMEOUT` configuration :

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

Le fichier mis à jour contient la configuration suivante :

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### Validation du fichier de configuration

Utilisez ce qui suit : `ece-tools` pour valider la commande `.magento.env.yaml` fichier de configuration avant d’envoyer les modifications à l’environnement cloud distant.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

L’exemple de réponse suivant fournit une liste d’éléments à corriger :

```terminal
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## constantes PHP

Vous pouvez utiliser des constantes PHP dans `.magento.env.yaml` Définitions de fichier au lieu de valeurs codées en dur. L’exemple suivant définit la variable `driver_options` en utilisant une constante PHP :

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>L’analyse constante ne fonctionne pas lors de l’utilisation d’une `symfony/yaml` version de package antérieure à 3.2.

## Gestion des erreurs

Lorsqu’un échec survient en raison d’une valeur inattendue dans la variable `.magento.env.yaml` fichier de configuration, vous recevez un message d’erreur. Par exemple, le message d’erreur suivant présente une liste de modifications suggérées pour chaque élément avec une valeur inattendue, fournissant parfois des options valides :

```terminal
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

Apportez les corrections, validez et poussez les modifications. Si vous ne recevez pas de message d’erreur, les modifications apportées à votre fichier de configuration sont validées.

## Optimisation de la gestion des configurations

Si vous avez activé Configuration Management après avoir vidé les configurations, vous devez déplacer les variables SCD_* de l’étape de déploiement vers l’étape de création. Voir [Stratégies de déploiement de contenu statique](../deploy/static-content.md).

>Avant Configuration Management :

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

>Après avoir activé Configuration Management, déplacez les variables SCD_* à l’étape de création :

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```
