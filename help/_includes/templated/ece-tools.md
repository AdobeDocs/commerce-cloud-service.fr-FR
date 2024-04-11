---
source-git-commit: 78e19b0cb274caf3799882d1f5d8242225c936ad
workflow-type: tm+mt
source-wordcount: '4098'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**Version**: 2002.1.18

Cette référence contient 34 commandes disponibles via le `ece-tools` outil de ligne de commande.
La liste initiale est générée automatiquement à l’aide de la fonction `ece-tools list` sur Adobe Commerce sur l’infrastructure cloud.

>[!NOTE]
>
>Cette référence est générée à partir du code base de l’application. Pour modifier le contenu, vous pouvez mettre à jour le code source de l’implémentation de la commande correspondante dans le [codebase](https://github.com/magento/magento-cloud-cli) et envoyer vos modifications pour révision. Une autre méthode consiste à _Donnez-nous vos commentaires_ (trouvez le lien en haut à droite). Pour obtenir des instructions sur les contributions, voir [Contributions au code](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `_complete`

Commande interne permettant de fournir des suggestions d’achèvement du shell

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`, `-s`

Le type de conteneur (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Requiert une valeur

### `--input`, `-i`

Un tableau de jetons d’entrée (par exemple, &quot;C.C._WORDS&quot; ou &quot;argv&quot;)

- Valeur par défaut : `[]`
- Requiert une valeur

### `--current`, `-c`

Index de la table &quot;input&quot; dans laquelle se trouve le curseur (par exemple, Throne_CWORD)

- Requiert une valeur

### `--api-version`, `-a`

Version API du script d’achèvement

- Requiert une valeur

### `--symfony`, `-S`

obsolète

- Requiert une valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `build`

Crée une application.

```bash
ece-tools build
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `completion`

Saut du script d’achèvement du shell

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

Le type de shell (par exemple &quot;bash&quot;), la valeur de la variable d’environnement &quot;$SHELL&quot; sera utilisée si ce n’est pas le cas.


### `--debug`

Suivi du journal de débogage de fin

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `db-dump`

Crée des sauvegardes de la base de données.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Bases de données pour la sauvegarde. Valeurs disponibles : [principales ventes de devis]. Si la valeur de l’argument n’est pas spécifiée, les sauvegardes de la base de données sont créées à l’aide des informations d’identification stockées dans la variable `MAGENTO_CLOUD_RELATIONSHIP` variable d’environnement ou et `stage.deploy.DATABASE_CONFIGURATION` du fichier de configuration .magento.env.yaml.

- Valeur par défaut : `[]`

- Tableau

### `--remove-definers`, `-d`

Suppression des définitions du vidage de base de données

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--dump-directory`, `-a`

Utiliser un autre répertoire pour enregistrer le fichier de sauvegarde

- Requiert une valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `deploy`

Déploie l’application.

```bash
ece-tools deploy
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `help`

Afficher l’aide d’une commande

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Nom de la commande

- Valeur par défaut : `help`


### `--format`

Format de sortie (txt, xml, json ou md)

- Valeur par défaut : `txt`
- Requiert une valeur

### `--raw`

Pour générer l’aide de la commande brute

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `list`

Commandes de liste

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```


### `namespace`

Nom de l’espace de noms


### `--raw`

Pour générer la liste de commandes brute

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie (txt, xml, json ou md)

- Valeur par défaut : `txt`
- Requiert une valeur

### `--short`

Pour ignorer les arguments de description des commandes

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `patch`

Applique des correctifs personnalisés.

```bash
ece-tools patch
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `post-deploy`

Effectue les opérations après le déploiement.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `run`

Exécuter le ou les scénarios.

```bash
ece-tools run <scenario>...
```


### `scenario`

Scénario(s)

- Valeur par défaut : `[]`

- Obligatoire
- Tableau

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `backup:list`

Affiche la liste des fichiers de sauvegarde.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `backup:restore`

Restaurez les fichiers de configuration importants. Exécutez backup:list pour afficher la liste des fichiers de sauvegarde.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Remplacer les fichiers existants lors de la restauration d’une sauvegarde

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--file`

Un chemin de récupération de fichier spécifique

- Accepte une valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `build:generate`

Génère tous les fichiers nécessaires pour l’étape de création.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `build:transfer`

Transfère les fichiers générés dans le répertoire init.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cloud:config:create`

Crée une `.magento.env.yaml` avec la configuration de variable de version, de déploiement et de post-déploiement spécifiée. Remplace toutes les `.magento,.env.yaml` fichier .

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Configuration au format JSON

- Obligatoire

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cloud:config:update`

Met à jour le `.magento.env.yaml` avec la configuration spécifiée. Crée `.magento.env.yaml` s’il n’existe pas.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Configuration au format JSON

- Obligatoire

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cloud:config:validate`

Validations `.magento.env.yaml` fichier de configuration

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `config:dump`

Configuration du saut pour le déploiement de contenu statique.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cron:disable`

Désactivez tous les processus cron de Magento et arrête tous les processus en cours d’exécution.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cron:enable`

Active les processus cron Magento.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cron:kill`

Arrête tous les processus cron du Magento.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `cron:unlock`

Déverrouillez les tâches cron bloquées à l’état &quot;en cours d’exécution&quot;.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Code de tâche cron à déverrouiller.

- Valeur par défaut : `[]`
- Accepte plusieurs valeurs

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `dev:generate:schema-error`

Génère le fichier dist/error-codes.md à partir du fichier schema.error.yaml.

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `dev:git:update-composer`

Met à jour le compositeur pour le déploiement à partir de Git.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `env:config:show`

Affichez les variables d’environnement de configuration de cloud codées.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Variables d’environnement à afficher, options possibles : services, itinéraires, variables

- Valeur par défaut : `[]`

- Tableau

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `error:show`

Affiche des informations sur les erreurs par identifiant d’erreur ou sur toutes les erreurs du dernier déploiement.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Code d’erreur, si la commande n’est pas transmise, affiche des informations sur toutes les erreurs du dernier déploiement.


### `--json`, `-j`

Utilisé pour obtenir un résultat au format JSON

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `module:refresh`

Actualise la configuration pour activer les modules nouvellement ajoutés.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `schema:generate`

Génère le fichier de schéma *.dist.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:ideal-state`

Vérifie l’état de configuration idéal.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:master-slave`

Vérifie la configuration maître-esclave.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:scd-on-build`

Vérifie le SCD lors de la configuration de la version.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:scd-on-demand`

Vérifie la configuration SCD on Demand.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:scd-on-deploy`

Vérifie le SCD lors de la configuration du déploiement.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `wizard:split-db-state`

Vérifie la capacité à diviser DB et si DB a déjà été partagé ou non.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Afficher l’aide pour la commande donnée. Lorsqu’aucune commande n’est fournie, l’aide d’affichage pour le \&lt;info>list\&lt;/info> command

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--quiet`, `-q`

Ne sortez aucun message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages : 1 pour une sortie normale, 2 pour une sortie plus détaillée et 3 pour le débogage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ansi`

Forcer (ou désactiver —no-ansi) la sortie ANSI

- N’accepte pas de valeur

### `--no-ansi`

Négociez l’option &quot;—ansi&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`, `-n`

Ne posez aucune question interactive

- Valeur par défaut : `false`
- N’accepte pas de valeur

