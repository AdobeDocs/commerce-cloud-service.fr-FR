---
title: Configuration de l’environnement
description: Découvrez comment configurer des actions de création et de déploiement sur toutes les Commerce dans les environnements d’infrastructure cloud, y compris Pro Staging et Production, à l’aide de variables d’environnement.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Configuration des variables d’environnement pour le déploiement

Le fichier `.magento.env.yaml` utilise des variables d’environnement pour centraliser la gestion des actions de création et de déploiement dans tous vos environnements, y compris Pro Staging et Production. Pour configurer des actions uniques dans chaque environnement, vous devez modifier ce fichier dans chaque environnement.

>[!TIP]
>
>Les fichiers YAML sont sensibles à la casse et n’autorisent pas les onglets. Veillez à utiliser une mise en retrait cohérente dans tout le fichier `.magento.env.yaml` ou votre configuration risque de ne pas fonctionner comme prévu. Les exemples de la documentation et de l’exemple de fichier utilisent la mise en retrait _deux-espaces_. Utilisez la commande [ece-tools validate](#validate-configuration-file) pour vérifier votre configuration.

## Structure du fichier

Le fichier `.magento.env.yaml` contient deux sections : `stage` et `log`. La section `stage` contrôle les actions qui se produisent pendant les phases du [processus de déploiement cloud](../deploy/process.md).

- `stage` : utilisez la section intermédiaire pour définir certaines actions pour les étapes de déploiement suivantes :
   - `global` : contrôle les actions dans les phases de création, de déploiement et de post-déploiement. Vous pouvez remplacer ces paramètres dans les sections de création, de déploiement et de post-déploiement .
   - `build` : contrôle les actions uniquement pendant la phase de création. Si vous ne spécifiez aucun paramètre dans cette section, la phase de création utilise les paramètres de la section globale.
   - `deploy` : contrôle les actions uniquement pendant la phase de déploiement. Si vous ne spécifiez aucun paramètre dans cette section, la phase de déploiement utilise les paramètres de la section globale.
   - `post-deploy` : contrôle les actions _après le déploiement de votre application et_ après _que le conteneur commence à accepter les connexions._
- `log` : utilisez la section de journal pour configurer les [notifications](set-up-notifications.md), y compris les types de notifications et le niveau de détail.
   - `slack` : configurez un message à envoyer à un robot de Slack.
   - `email` : configurez un email à envoyer à un ou plusieurs destinataires de messagerie.
   - [gestionnaires de journaux](log-handlers.md) : configurez les messages d’application logicielle et matérielle envoyés à un serveur de journalisation distant.

### Variables d’environnement

Le package `ece-tools` définit des valeurs dans le fichier `env.php` en fonction des valeurs des [variables cloud](variables-cloud.md), des variables définies dans le fichier [!DNL Cloud Console] et du fichier de configuration `.magento.env.yaml`. Les variables d’environnement du fichier `.magento.env.yaml` personnalisent l’environnement cloud en remplaçant votre configuration Commerce existante. Si une valeur par défaut est `Not Set`, le package `ece-tools` effectue l’action **NO** et utilise la valeur par défaut [!DNL Commerce] ou la valeur de la configuration MAGENTO_CLOUD_RELATIONSHIPS. Si la valeur par défaut est définie, le package `ece-tools` agit pour définir cette valeur par défaut.

Les rubriques suivantes contiennent des définitions détaillées, par exemple si une valeur par défaut est définie ou non, de toutes les variables que vous pouvez utiliser dans le fichier `.magento.env.yaml` :

- [Global](variables-global.md) : les variables contrôlent les actions dans chaque phase : création, déploiement et post-déploiement
- [Build](variables-build.md) : les variables contrôlent les actions de création
- [Deploy](variables-deploy.md) : les variables contrôlent les actions de déploiement
- [Post-déploiement](variables-post-deploy.md) : les variables contrôlent les actions après le déploiement

### Création d’un fichier de configuration à partir de l’interface de ligne de commande

Vous pouvez générer un fichier de configuration `.magento.env.yaml` pour un environnement cloud à l’aide des commandes `ece-tools` suivantes.

>Crée un fichier de configuration

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Mise à jour des valeurs dans le fichier de configuration

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Les deux commandes nécessitent un seul argument : un tableau au format JSON qui spécifie une valeur pour au moins une variable de création, de déploiement ou de post-déploiement. Par exemple, la commande suivante définit des valeurs pour les variables `SCD_THREADS` et `CLEAN_STATIC_FILES` :

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

Et crée un fichier `.magento.env.yaml` avec les paramètres suivants :

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

Vous pouvez utiliser la commande `cloud:config:update` pour mettre à jour le nouveau fichier. Par exemple, la commande suivante modifie la valeur `SCD_THREADS` et ajoute la configuration `SCD_COMPRESSION_TIMEOUT` :

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

Utilisez la commande `ece-tools` suivante pour valider le fichier de configuration `.magento.env.yaml` avant de pousser les modifications vers l’environnement cloud distant.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

L’exemple de réponse suivant fournit une liste d’éléments à corriger :

```
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## constantes PHP

Vous pouvez utiliser des constantes PHP dans des définitions de fichier `.magento.env.yaml` au lieu de valeurs codées en dur. L’exemple suivant définit le `driver_options` à l’aide d’une constante PHP :

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
>L’analyse constante ne fonctionne pas lors de l’utilisation d’une version de package `symfony/yaml` antérieure à 3.2.

## Gestion des erreurs

Lorsqu’un échec se produit en raison d’une valeur inattendue dans le fichier de configuration `.magento.env.yaml`, vous recevez un message d’erreur. Par exemple, le message d’erreur suivant présente une liste de modifications suggérées pour chaque élément avec une valeur inattendue, fournissant parfois des options valides :

```
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
