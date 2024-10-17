---
source-git-commit: 63c86bab0f3feb5a3a641a7a785ea625338045f4
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---
# ece-tools

**Version** : 2002.2.0

Cette référence contient 34 commandes disponibles via l’outil de ligne de commande `ece-tools`.
La liste initiale est générée automatiquement à l’aide de la commande `ece-tools list` sur Adobe Commerce sur l’infrastructure cloud.

## Général

Cette référence est générée à partir du code base de l’application. Pour modifier le contenu, _Donnez-nous un commentaire_ (trouvez le lien en haut à droite). Pour obtenir des instructions sur les contributions, voir [Contributions au code](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

### Options globales

#### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie à l’aide de l’affichage de la commande de liste

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

#### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `_complete`

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

Commande interne permettant de fournir des suggestions d’achèvement du shell

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--shell`, `-s`

Le type de conteneur (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Requiert une valeur

#### `--input`, `-i`

Un tableau de jetons d’entrée (par exemple, &quot;C.C._WORDS&quot; ou &quot;argv&quot;)

- Valeur par défaut : `[]`
- Requiert une valeur

#### `--current`, `-c`

Index de la table &quot;input&quot; dans laquelle se trouve le curseur (par exemple, Throne_CWORD)

- Requiert une valeur

#### `--api-version`, `-a`

Version API du script d’achèvement

- Requiert une valeur

#### `--symfony`, `-S`

obsolète

- Requiert une valeur


## `build`

```bash
ece-tools build
```

Crée une application.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `completion`

```bash
ece-tools completion [--debug] [--] [<shell>]
```

Saut du script d’achèvement du shell

```
The completion command dumps the shell completion script required
to use shell autocompletion (currently, bash, fish, zsh completion are supported).

Static installation
-------------------

Dump the script to a global completion file and restart your shell:

    bin/ece-tools completion  | sudo tee /etc/bash_completion.d/ece-tools

Or dump the script to a local file and source it:

    bin/ece-tools completion  > completion.sh

    # source the file whenever you use the project
    source completion.sh

    # or add this line at the end of your "~/.bashrc" file:
    source /path/to/completion.sh

Dynamic installation
--------------------

Add this to the end of your shell configuration file (e.g. "~/.bashrc"):

    eval "$(/var/jenkins/workspace/gendocs-ece-tools-cli/bin/ece-tools completion )"
```

### Arguments

#### `shell`

Le type de shell (par exemple &quot;bash&quot;), la valeur de la variable d’environnement &quot;$SHELL&quot; sera utilisée si ce n’est pas le cas.

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--debug`

Suivi du journal de débogage de fin

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `db-dump`

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```

Crée des sauvegardes de la base de données.

### Arguments

#### `databases`

Bases de données pour la sauvegarde. Valeurs disponibles : [ ventes de devis principales]. Si la valeur de l’argument n’est pas spécifiée, les sauvegardes de la base de données sont créées à l’aide des informations d’identification stockées dans la variable d’environnement `MAGENTO_CLOUD_RELATIONSHIP` ou/et de la propriété `stage.deploy.DATABASE_CONFIGURATION` du fichier de configuration .magento.env.yaml.

- Valeur par défaut : `[]`
- Tableau

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--remove-definers`, `-d`

Suppression des définitions du vidage de base de données

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--dump-directory`, `-a`

Utiliser un autre répertoire pour enregistrer le fichier de sauvegarde

- Requiert une valeur


## `deploy`

```bash
ece-tools deploy
```

Déploie l’application.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `help`

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```

Afficher l’aide d’une commande

```
The help command displays help for a given command:

  bin/ece-tools help list

You can also output the help in other formats by using the --format option:

  bin/ece-tools help --format=xml list

To display the list of available commands, please use the list command.
```

### Arguments

#### `command_name`

Nom de la commande

- Valeur par défaut : `help`

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--format`

Format de sortie (txt, xml, json ou md)

- Valeur par défaut : `txt`
- Requiert une valeur

#### `--raw`

Pour générer l’aide de la commande brute

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `list`

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```

Commandes de liste

```
The list command lists all commands:

  bin/ece-tools list

You can also display the commands for a specific namespace:

  bin/ece-tools list test

You can also output the information in other formats by using the --format option:

  bin/ece-tools list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  bin/ece-tools list --raw
```

### Arguments

#### `namespace`

Nom de l’espace de noms

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--raw`

Pour générer la liste de commandes brute

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--format`

Format de sortie (txt, xml, json ou md)

- Valeur par défaut : `txt`
- Requiert une valeur

#### `--short`

Pour ignorer les arguments de description des commandes

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `patch`

```bash
ece-tools patch
```

Applique des correctifs personnalisés.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `post-deploy`

```bash
ece-tools post-deploy
```

Effectue les opérations après le déploiement.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `run`

```bash
ece-tools run <scenario>...
```

Exécuter le ou les scénarios.

### Arguments

#### `scenario`

Scénario(s)

- Valeur par défaut : `[]`
- Obligatoire

- Tableau

### Options

Pour les options globales, voir [Options globales](#global-options).


## `backup:list`

```bash
ece-tools backup:list
```

Affiche la liste des fichiers de sauvegarde.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `backup:restore`

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

Restaurez les fichiers de configuration importants. Exécutez backup:list pour afficher la liste des fichiers de sauvegarde.

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--force`, `-f`

Remplacer les fichiers existants lors de la restauration d’une sauvegarde

- Valeur par défaut : `false`
- N’accepte pas de valeur

#### `--file`

Un chemin de récupération de fichier spécifique

- Accepte une valeur


## `build:generate`

```bash
ece-tools build:generate
```

Génère tous les fichiers nécessaires pour l’étape de création.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `build:transfer`

```bash
ece-tools build:transfer
```

Transfère les fichiers générés dans le répertoire init.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cloud:config:create`

```bash
ece-tools cloud:config:create <configuration>
```

Crée un fichier `.magento.env.yaml` avec la configuration de variable de version, de déploiement et de post-déploiement spécifiée. Permet de remplacer tout fichier `.magento,.env.yaml` existant.

### Arguments

#### `configuration`

Configuration au format JSON

- Obligatoire

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cloud:config:update`

```bash
ece-tools cloud:config:update <configuration>
```

Met à jour le fichier `.magento.env.yaml` existant avec la configuration spécifiée. Crée un fichier `.magento.env.yaml` s’il n’existe pas.

### Arguments

#### `configuration`

Configuration au format JSON

- Obligatoire

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cloud:config:validate`

```bash
ece-tools cloud:config:validate
```

Valide le fichier de configuration `.magento.env.yaml`

### Options

Pour les options globales, voir [Options globales](#global-options).


## `config:dump`

```bash
ece-tools config:dumpdump
```

Configuration du saut pour le déploiement de contenu statique.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cron:disable`

```bash
ece-tools cron:disable
```

Désactivez tous les processus cron de Magento et arrête tous les processus en cours d’exécution.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cron:enable`

```bash
ece-tools cron:enable
```

Active les processus cron Magento.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cron:kill`

```bash
ece-tools cron:kill
```

Arrête tous les processus cron du Magento.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `cron:unlock`

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

Déverrouillez les tâches cron bloquées à l’état &quot;en cours d’exécution&quot;.

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--job-code`

Code de tâche cron à déverrouiller.

- Valeur par défaut : `[]`
- Accepte plusieurs valeurs


## `dev:generate:schema-error`

```bash
ece-tools dev:generate:schema-error
```

Génère le fichier dist/error-codes.md à partir du fichier schema.error.yaml.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `dev:git:update-composer`

```bash
ece-tools dev:git:update-composer
```

Met à jour le compositeur pour le déploiement à partir de Git.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `env:config:show`

```bash
ece-tools env:config:show [<variable>...]
```

Affichez les variables d’environnement de configuration de cloud codées.

### Arguments

#### `variable`

Variables d’environnement à afficher, options possibles : services, itinéraires, variables

- Valeur par défaut : `[]`
- Tableau

### Options

Pour les options globales, voir [Options globales](#global-options).


## `error:show`

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```

Affiche des informations sur les erreurs par identifiant d’erreur ou sur toutes les erreurs du dernier déploiement.

### Arguments

#### `error-code`

Code d’erreur, si la commande n’est pas transmise, affiche des informations sur toutes les erreurs du dernier déploiement.

### Options

Pour les options globales, voir [Options globales](#global-options).

#### `--json`, `-j`

Utilisé pour obtenir un résultat au format JSON

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `module:refresh`

```bash
ece-tools module:refresh
```

Actualise la configuration pour activer les modules nouvellement ajoutés.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `schema:generate`

```bash
ece-tools schema:generate
```

Génère le fichier de schéma *.dist.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:ideal-state`

```bash
ece-tools wizard:ideal-state
```

Vérifie l’état de configuration idéal.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:master-slave`

```bash
ece-tools wizard:master-slave
```

Vérifie la configuration maître-esclave.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:scd-on-build`

```bash
ece-tools wizard:scd-on-build
```

Vérifie le SCD lors de la configuration de la version.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:scd-on-demand`

```bash
ece-tools wizard:scd-on-demand
```

Vérifie la configuration SCD on Demand.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:scd-on-deploy`

```bash
ece-tools wizard:scd-on-deploy
```

Vérifie le SCD lors de la configuration du déploiement.

### Options

Pour les options globales, voir [Options globales](#global-options).


## `wizard:split-db-state`

```bash
ece-tools wizard:split-db-state
```

Vérifie la capacité à diviser DB et si DB a déjà été partagé ou non.

### Options

Pour les options globales, voir [Options globales](#global-options).
