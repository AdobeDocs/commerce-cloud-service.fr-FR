---
title: Propriétés
description: Utilisez la liste de propriétés comme référence lors de la configuration du [!DNL Commerce] application pour génération et déploiement sur l’infrastructure cloud.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Propriétés pour la configuration de l’application

Le `.magento.app.yaml` Le fichier utilise des propriétés pour gérer la prise en charge de l’environnement pour le [!DNL Commerce] application.

| Nom | Description | Par défaut | Obligatoire |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Personnaliser les rôles utilisateur | — | Non |
| [`crons`](crons-property.md) | Mise à jour des spécifications et planification des tâches cron | — | Non |
| [`dependencies`](#dependencies) | Activer les dépendances supplémentaires | `php:composer/composer: '2.2.4'` | Non |
| [`disk`](#disk) | Définition de la taille du disque persistant | `5120` | Oui |
| [`firewall`](firewall-property.md) | (Démarrage uniquement) Contrôle du trafic sortant | — | Non |
| [`hooks`](hooks-property.md) | Personnalisation des commandes shell pour les phases de création, de déploiement et de post-déploiement | — | Non |
| [`mounts`](#mounts) | Définir les chemins | Chemins :<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Non |
| [`name`](#name) | Définition du nom de l’application | `mymagento` | Oui |
| [`relationships`](#relationships) | Services de carte | Services :<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Non |
| [`runtime`](#runtime) | La propriété d’exécution inclut les extensions requises par le [!DNL Commerce] application. | Extensions :<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Oui |
| [`type`](#type-and-build) | Définir l’image du conteneur de base | `php:8.3` | Oui |
| [`variables`](variables-property.md) | Application d’une variable d’environnement à une version de Commerce spécifique | — | Non |
| [`web`](web-property.md) | Gestion des requêtes externes | — | Oui |
| [`workers`](workers-property.md) | Gestion des requêtes externes | — | Oui, si vous n’utilisez pas la propriété web |

{style="table-layout:auto"}

## `name`

Le `name` indique le nom de l’application utilisé dans [`routes.yaml`](../routes/routes-yaml.md) pour définir le HTTP en amont (par défaut, `mymagento:http`). Par exemple, si la valeur de `name` est `app`, vous devez utiliser `app:http` dans le champ en amont.

>[!WARNING]
>
>Ne modifiez pas le nom de l’application après son déploiement. Cela entraîne une perte de données.

## `type` et `build`

Le `type`  et `build` les propriétés fournissent des informations sur l’image du conteneur de base pour créer et exécuter le projet.

Les pris en charge `type` Le langage est PHP. Spécifiez la version PHP comme suit :

```yaml
type: php:<version>
```

Le `build` détermine ce qui se passe par défaut lors de la création du projet. Le `flavor` spécifie un ensemble par défaut de tâches de génération à exécuter. L’exemple suivant illustre la configuration par défaut pour . `type` et `build` de `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.3
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.7.2'
```

### Installation et utilisation du compositeur 2

Le `build: flavor:` La propriété n’est pas utilisée pour le compositeur 2.x. Vous devez donc installer manuellement le compositeur pendant la phase de création. Pour installer et utiliser le compositeur 2.x dans vos projets Starter et Pro, vous devez apporter trois modifications à votre `.magento.app.yaml` configuration :

1. Supprimer `composer` comme `build: flavor:` et ajouter `none`. Cette modification empêche Cloud d’utiliser la version 1.x par défaut du compositeur pour exécuter les tâches de création.
1. Ajouter `composer/composer: '^2.0'` as a `php` dépendance pour l’installation du compositeur 2.x.
1. Ajouter le `composer` créer des tâches dans un `build` pour exécuter les tâches de génération à l’aide du compositeur 2.x.

Utilisez les fragments de configuration suivants dans les vôtres `.magento.app.yaml` configuration :

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Voir [Packages requis](../development/overview.md#required-packages) pour plus d’informations sur le compositeur.

## `dependencies`

Spécifiez les dépendances dont votre application peut avoir besoin pendant le processus de création.

Adobe Commerce prend en charge les dépendances dans les langues suivantes :

- PHP
- Ruby
- Node.js

Ces dépendances sont indépendantes des dépendances éventuelles de votre application et sont disponibles dans le `PATH`, pendant le processus de création et dans l’environnement d’exécution de votre application.

Vous pouvez spécifier ces dépendances comme suit :

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Utilisez pour modifier la configuration PHP au moment de l&#39;exécution, par exemple pour activer les extensions. Les extensions suivantes sont requises :

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Voir [Paramètres PHP](php-settings.md) pour plus d’informations sur l’activation des extensions.

## `disk`

Définit la taille du disque persistant de l’application en Mo.

```yaml
disk: 5120
```

La taille de disque minimale recommandée est de 256 Mo. Si l’erreur s’affiche `UserError: Error building the project: Disk size may not be smaller than 128MB`, augmentez la taille à 256 Mo.

>[!NOTE]
>
>Pour les environnements d’évaluation et de production Pro, vous devez : [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour mettre à jour `mounts` et `disk` configuration pour votre application. Lorsque vous soumettez le ticket, indiquez les modifications de configuration requises et incluez une version mise à jour de votre `.magento.app.yaml` fichier .

## `relationships`

Définit le mapping de service dans l&#39;application.

La relation `name` est disponible pour l’application dans `MAGENTO_CLOUD_RELATIONSHIPS` variable d’environnement. Le `<service-name>:<endpoint-name>` La relation est mappée aux valeurs de nom et de type définies dans `.magento/services.yaml` fichier .

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Voici un exemple de relations par défaut :

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Voir [Services tertiaires](../services/services-yaml.md) pour obtenir une liste complète des types de services et des points d’entrée actuellement pris en charge.

## `mounts`

Objet dont les clés sont des chemins d’accès relatifs à la racine de l’application. Le montage est une zone accessible en écriture sur le disque pour les fichiers. Voici une liste par défaut des montages configurés dans le `magento.app.yaml` fichier utilisant `volume_id[/subpath]` syntaxe :

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

Le format d’ajout de votre montage à cette liste est le suivant :

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`: partage un volume entre vos applications au sein d’un environnement.
- `disk`: définit la taille disponible pour le volume partagé.

>[!NOTE]
>
>Pour les environnements d’évaluation et de production Pro, vous devez : [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour mettre à jour `mounts` et `disk` configuration pour votre application. Lorsque vous soumettez le ticket, indiquez les modifications de configuration requises et incluez une version mise à jour de votre `.magento.app.yaml` fichier .

Vous pouvez rendre le montage web accessible en l’ajoutant au [`web`](web-property.md) bloc d’emplacements.

>[!WARNING]
>
>Une fois que votre site contient des données, ne modifiez pas les `subpath` partie du nom du montage. Cette valeur est l’identifiant unique de l’ `files` zone. Si vous modifiez ce nom, vous perdrez toutes les données du site stockées à l’ancien emplacement.

## `access`

Le `access` La propriété indique un niveau minimum de rôle d’utilisateur qui est autorisé à accéder aux environnements SSH. Les rôles utilisateur disponibles sont les suivants :

- `admin`: peut modifier les paramètres et exécuter des actions dans l&#39;environnement ; a _contributeur_ et _visionneuse_ droits.
- `contributor`: peut envoyer du code vers cet environnement et se brancher à partir de l’environnement ; a _visionneuse_ droits.
- `viewer`: peut uniquement afficher l’environnement.

Le rôle utilisateur par défaut est . `contributor`, qui restreint l’accès SSH des utilisateurs avec uniquement _visionneuse_ droits. Vous pouvez remplacer le rôle utilisateur par . `viewer` pour autoriser l’accès SSH aux utilisateurs avec uniquement _visionneuse_ droits :

```yaml
access:
    ssh: viewer
```
