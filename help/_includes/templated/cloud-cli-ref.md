---
source-git-commit: c160be020d855983eaf7a06d04cee6e27819b2a0
workflow-type: tm+mt
source-wordcount: '21467'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce sur l’infrastructure cloud)

<!-- The template to render with above values -->
**Version**: 1.46.1

Cette référence contient 119 commandes disponibles via le `magento-cloud` outil de ligne de commande.
La liste initiale est générée automatiquement à l’aide de la fonction `magento-cloud list` sur Adobe Commerce sur l’infrastructure cloud.

>[!NOTE]
>
>Cette référence est générée à partir du code base de l’application. Pour modifier le contenu, vous pouvez mettre à jour le code source de l’implémentation de la commande correspondante dans le [codebase](https://github.com/magento/magento-cloud-cli) et envoyer vos modifications pour révision. Une autre méthode consiste à _Donnez-nous vos commentaires_ (trouvez le lien en haut à droite). Pour obtenir des instructions sur les contributions, voir [Contributions au code](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

Effacer le cache de l’interface de ligne de commande

```bash
magento-cloud cc
```

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `decode`

Décodez une chaîne codée telle que MAGENTO_CLOUD_VARIABLES .

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

La valeur de la variable à décoder

- Obligatoire

### `--property`, `-P`

La propriété à afficher dans la variable

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `docs`

Ouvrir la documentation en ligne

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Termes de recherche

- Valeur par défaut : `[]`

- Tableau

### `--browser`

Navigateur à utiliser pour ouvrir l’URL. Définissez 0 pour aucun.

- Requiert une valeur

### `--pipe`

Extrayez l’URL vers stdout.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `help`

Affiche une aide pour une commande

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Nom de la commande

- Valeur par défaut : `help`


### `--format`

Format de sortie (txt, json ou md)

- Valeur par défaut : `txt`
- Requiert une valeur

### `--raw`

Pour générer l’aide de la commande brute

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `list`

Commandes Listes

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

Commande à exécuter

- Obligatoire

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

### `--all`

Afficher toutes les commandes, y compris les commandes masquées

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `multi`

Exécution d’une commande sur plusieurs projets

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

Commande à exécuter

- Valeur par défaut : `[]`

- Obligatoire
- Tableau

### `--projects`, `-p`

Une liste d’ID de projet, séparés par des virgules et/ou un espace blanc

- Requiert une valeur

### `--continue`

Poursuivre l’exécution des commandes même en cas d’exception

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--sort`

Une propriété par laquelle trier la liste des options de projet

- Valeur par défaut : `title`
- Requiert une valeur

### `--reverse`

Inverser l’ordre des options du projet

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `web`

Ouvrez le projet dans l’interface utilisateur web.

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

Navigateur à utiliser pour ouvrir l’URL. Définissez 0 pour aucun.

- Requiert une valeur

### `--pipe`

Extrayez l’URL vers stdout.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `activity:cancel`

Annulation d’une activité

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

ID d’activité. La valeur par défaut est l’activité annulable la plus récente.


### `--type`, `-t`

Filtrer par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour le type, par exemple &#39;%var%&#39; pour sélectionner les activités liées aux variables.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`, `-x`

Exclure par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour exclure les types.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--all`, `-a`

Vérifier les activités récentes sur tous les environnements (lors de la sélection d’une activité par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `activity:get`

Affichage d’informations détaillées sur une seule activité

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

ID d’activité. La valeur par défaut est l’activité la plus récente.


### `--property`, `-P`

La propriété à afficher

- Requiert une valeur

### `--type`, `-t`

Filtrer par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour le type, par exemple &#39;%var%&#39; pour sélectionner les activités liées aux variables.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`, `-x`

Exclure par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour exclure les types.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--state`

Filtrer par état (lors de la sélection d’une activité par défaut) : en_cours, en attente, terminé ou annulé. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--result`

Filtrer par résultat (lors de la sélection d’une activité par défaut) : succès ou échec

- Requiert une valeur

### `--incomplete`, `-i`

N’incluez que les activités incomplètes (lors de la sélection d’une activité par défaut). Ceci est un raccourci pour \&lt;info>—state=in_progress,pending\&lt;/info>

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--all`, `-a`

Vérifier les activités récentes sur tous les environnements (lors de la sélection d’une activité par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `activity:list`

Obtention d’une liste des activités pour un environnement ou un projet

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Les activités de filtrage par type Valeurs peuvent être fractionnées par des virgules (par exemple &quot;a, b, c&quot;) et/ou un espace blanc. La première partie du nom de l&#39;activité peut être omise, par exemple &#39;cron&#39; peut sélectionner les activités &#39;environment.cron&#39;. Les caractères % ou * peuvent être utilisés comme caractères génériques, par exemple &#39;%var%&#39; pour sélectionner des activités liées à des variables.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`, `-x`

Exclure les activités par type. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. La première partie du nom de l&#39;activité peut être omise, par exemple &#39;cron&#39; peut exclure les activités &#39;environment.cron&#39;. Les caractères % ou * peuvent être utilisés comme caractère générique pour exclure les types.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--limit`

Limiter le nombre de résultats affichés

- Valeur par défaut : `10`
- Requiert une valeur

### `--start`

Seules les activités créées avant cette date seront répertoriées.

- Requiert une valeur

### `--state`

Filtrer les activités par état : en_cours, en attente, terminé ou annulé. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--result`

Filtrage des activités par résultat : succès ou échec

- Requiert une valeur

### `--incomplete`, `-i`

Ne répertorier que les activités incomplètes

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--all`, `-a`

Liste des activités dans tous les environnements

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : id*, created*, description*, progress*, state*, result*, completed, environment, type (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `activity:log`

Afficher le journal d’une activité

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

ID d’activité. La valeur par défaut est l’activité la plus récente.


### `--refresh`

Intervalle d’actualisation des activités (secondes). Définissez cette variable sur 0 pour désactiver l’actualisation.

- Valeur par défaut : `3`
- Requiert une valeur

### `--timestamps`, `-t`

Affichage d’un horodatage en regard de chaque message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--type`

Filtrer par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour le type, par exemple &#39;%var%&#39; pour sélectionner les activités liées aux variables.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`, `-x`

Exclure par type (lors de la sélection d’une activité par défaut). Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour exclure les types.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--state`

Filtrer par état (lors de la sélection d’une activité par défaut) : en_cours, en attente, terminé ou annulé. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--result`

Filtrer par résultat (lors de la sélection d’une activité par défaut) : succès ou échec

- Requiert une valeur

### `--incomplete`, `-i`

N’incluez que les activités incomplètes (lors de la sélection d’une activité par défaut). Ceci est un raccourci pour \&lt;info>—state=in_progress,pending\&lt;/info>

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--all`, `-a`

Vérifier les activités récentes sur tous les environnements (lors de la sélection d’une activité par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `app:config-get`

Affichage de la configuration d’une application

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`, `-P`

La propriété de configuration à afficher

- Requiert une valeur

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--identity-file`, `-i`

[Option obsolète, qui n’est plus utilisée]

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `app:list`

Liste des applications dans le projet

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--pipe`

Générer une liste de noms d’application uniquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : nom*, type*, disque, chemin, taille (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `auth:api-token-login`

Connexion à Magento Cloud à l’aide d’un jeton API

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `auth:browser-login`

Connexion à Magento Cloud via un navigateur

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Connectez-vous à nouveau, même si vous êtes déjà connecté.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--browser`

Navigateur à utiliser pour ouvrir l’URL. Définissez 0 pour aucun.

- Requiert une valeur

### `--pipe`

Extrayez l’URL vers stdout.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `auth:info`

Afficher les informations de votre compte

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

Propriété du compte à afficher


### `--no-auto-login`

Ignore la connexion automatique. Aucun résultat ne sera affiché s’il n’est pas connecté et le code de sortie sera 0, en supposant aucune autre erreur.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--property`, `-P`

Propriété du compte à afficher (syntaxe alternative)

- Requiert une valeur

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `auth:logout`

Déconnexion de Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Déconnexion de toutes les sessions locales

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--other`

Déconnexion à partir d’autres sessions locales

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `blackfire:setup`

Configuration de l’intégration de Blackfire.io pour le projet

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

ID du serveur

- Requiert une valeur

### `--server_token`

Jeton de serveur

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `certificate:add`

Ajout d’un certificat SSL au projet

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

Chemin d’accès au fichier de certificat

- Requiert une valeur

### `--key`

Le chemin d’accès au fichier de clé privée du certificat

- Requiert une valeur

### `--chain`

Chemin d’accès au fichier de chaîne de certificats

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `certificate:delete`

Suppression d’un certificat du projet

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

L’ID de certificat (ou le début de celui-ci)

- Obligatoire

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `certificate:get`

Affichage d’un certificat

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

L’ID de certificat (ou le début de celui-ci)

- Obligatoire

### `--property`, `-P`

La propriété de certificat à afficher

- Requiert une valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `certificate:list`

Liste des certificats de projet

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Filtrage par nom de domaine (recherche non sensible à la casse)

- Requiert une valeur

### `--exclude-domain`

Exclure des certificats, par nom de domaine (recherche non sensible à la casse)

- Requiert une valeur

### `--issuer`

Filtrage par émetteur

- Requiert une valeur

### `--only-auto`

Afficher uniquement les certificats configurés automatiquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-auto`

Afficher uniquement les certificats ajoutés manuellement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--ignore-expiry`

Afficher les certificats expirés et non expirés

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--only-expired`

Afficher uniquement les certificats expirés

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-expired`

Afficher uniquement les certificats non expirés (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--pipe-domains`

Ne renvoient qu’une liste de noms de domaine couverts par les certificats

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : créées, domaines, expires, id, émetteur. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `commit:get`

Afficher les détails de validation

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

La validation SHA. Cela peut également accepter les suffixes &quot;HEAD&quot; et caret (^) ou tilde (~) pour les validations parentes.

- Valeur par défaut : `HEAD`


### `--property`, `-P`

La propriété commit à afficher.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `commit:list`

Validation de liste

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

SHA de validation Git de départ. Cela peut également accepter les suffixes &quot;HEAD&quot; et caret (^) ou tilde (~) pour les validations parentes.


### `--limit`

Nombre de validations à afficher.

- Valeur par défaut : `10`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : auteur, date, sha, summary. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `db:dump`

Créer un vidage local de la base distante

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

Le schéma à vider. Omettez d’utiliser le schéma par défaut (généralement &quot;main&quot;).

- Requiert une valeur

### `--file`, `-f`

Un nom de fichier personnalisé pour la sauvegarde

- Requiert une valeur

### `--directory`, `-d`

Un répertoire personnalisé pour la vidage

- Requiert une valeur

### `--gzip`, `-z`

Compresser la vidure à l’aide de gzip

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--timestamp`, `-t`

Ajouter un horodatage au nom de fichier de vidage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--stdout`, `-o`

Sortie à STDOUT au lieu d’un fichier

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--table`

Tableau(s) à inclure

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-table`

Tableau(s) à exclure

- Valeur par défaut : `[]`
- Requiert une valeur

### `--schema-only`

vidage des schémas uniquement, sans données

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--charset`

Encodage du jeu de caractères pour le vidage

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `db:size`

Estimation de l’utilisation du disque d’une base de données

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`, `-B`

Afficher les tailles en octets.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--cleanup`, `-C`

Vérifiez si les tableaux peuvent être nettoyés et affichez-moi des recommandations (InnoDb uniquement).

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : max, percent_used, utilisé. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `db:sql`

Exécution SQL sur la base distante

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

Instruction SQL à exécuter


### `--raw`

Générer une sortie brute et non tabulaire

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--schema`

Le schéma à utiliser. Omettez d’utiliser le schéma par défaut (généralement &quot;main&quot;). Transmettez une chaîne vide pour ne pas utiliser de schéma.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `domain:add`

Ajouter un nouveau domaine au projet

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Nom de domaine

- Obligatoire

### `--cert`

Chemin d’accès au fichier de certificat pour ce domaine

- Requiert une valeur

### `--key`

Le chemin d’accès au fichier de clé privée pour le certificat fourni.

- Requiert une valeur

### `--chain`

Le chemin d’accès au fichier ou aux fichiers de la chaîne de certificat pour le certificat fourni

- Valeur par défaut : `[]`
- Requiert une valeur

### `--attach`

Domaine de production que celui-ci remplace dans les itinéraires de l’environnement. Requis pour les domaines d’environnement hors production.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `domain:delete`

Suppression d’un domaine du projet

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Nom de domaine

- Obligatoire

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `domain:get`

Affichage des informations détaillées d’un domaine

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

Nom de domaine


### `--property`, `-P`

Propriété de domaine à afficher

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `domain:list`

Obtention d’une liste de tous les domaines

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : name*, ssl*, created_at*, registered_name, replace_for, type, updated_at (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `domain:update`

Mettre à jour un domaine

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Nom de domaine

- Obligatoire

### `--cert`

Chemin d’accès au fichier de certificat pour ce domaine

- Requiert une valeur

### `--key`

Le chemin d’accès au fichier de clé privée pour le certificat fourni.

- Requiert une valeur

### `--chain`

Le chemin d’accès au fichier ou aux fichiers de la chaîne de certificat pour le certificat fourni

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:activate`

Activation d’un environnement

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Environnement(s) à activer

- Valeur par défaut : `[]`

- Tableau

### `--parent`

Définition d’un nouveau parent d’environnement avant activation

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:branch`

Branchement et environnement

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

ID (nom de branche) du nouvel environnement


### `parent`

Parent du nouvel environnement


### `--title`

Titre du nouvel environnement

- Requiert une valeur

### `--type`

Type du nouvel environnement

- Requiert une valeur

### `--no-clone-parent`

Ne pas cloner les données de l’environnement parent

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:checkout`

Vérification d’un environnement

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

L’identifiant de l’environnement à extraire. Par exemple : &quot;sprint2&quot;


### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:delete`

Suppression d’un ou de plusieurs environnements

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Environnements à supprimer. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`

- Tableau

### `--delete-branch`

Suppression des branches Git pour les environnements inactifs, sans confirmation

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-delete-branch`

Ne supprimez aucune branche(s) Git (environnements inactifs)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--type`

Supprimez tous les environnements d’un type (en les ajoutant à tous les autres environnements sélectionnés) Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a, b, c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--only-type`, `-t`

Seuls les environnements de suppression de valeurs d’un type spécifique peuvent être fractionnés par des virgules (par exemple &quot;a, b, c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude`

Environnement(s) à ne pas supprimer. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`

Les types d’environnement dont les valeurs ne doivent pas être supprimées peuvent être fractionnés par des virgules (par exemple &quot;a, b, c&quot;) et/ou un espace blanc.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--inactive`

Supprimer tous les environnements inactifs (en les ajoutant à tous les autres environnements sélectionnés)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--merged`

Supprimez tous les environnements fusionnés (en les ajoutant à tous les autres environnements sélectionnés).

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--allow-delete-parent`

Autoriser la suppression des environnements ayant des enfants

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:http-access`

Mise à jour des paramètres d’accès HTTP pour un environnement

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Restriction d’accès au format &quot;permission:address&quot;. Utilisez 0 pour effacer toutes les adresses.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--auth`

Informations d’identification HTTP Basic auth au format &quot;username:password&quot;. Utilisez 0 pour effacer toutes les informations d’identification.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--enabled`

Indique si le contrôle d’accès doit être activé : 1 à activer, 0 à désactiver

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:info`

Lecture ou définition des propriétés d’un environnement

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Nom de la propriété


### `value`

Définir une nouvelle valeur pour la propriété


### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:init`

Initialisation d’un environnement à partir d’un référentiel Git public

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

URL d’un référentiel Git

- Obligatoire

### `--profile`

Nom du profil

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:list`

Obtention d’une liste des environnements

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Ne pas afficher les environnements inactifs

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--pipe`

Générer une liste simple d’identifiants d’environnement.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--refresh`

Actualisation ou non de la liste.

- Valeur par défaut : `1`
- Requiert une valeur

### `--sort`

Propriété à trier par

- Valeur par défaut : `title`
- Requiert une valeur

### `--reverse`

Tri dans l’ordre inverse (décroissant)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--type`

Vous pouvez filtrer la liste par type d&#39;environnement. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : id*, titre*, statut*, type*, créé, nom_machine, mise à jour (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:logs`

Lecture des journaux d’un environnement

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

Le type de journal, par exemple &quot;access&quot; ou &quot;error&quot;


### `--lines`

Le nombre de lignes à afficher

- Valeur par défaut : `100`
- Requiert une valeur

### `--tail`

Quitter le journal en continu

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:merge`

Fusionner un environnement

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Environnement à fusionner


### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:pause`

Mettre en pause un environnement

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:push`

Push du code dans un environnement

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

Référence source : nom de branche ou hachage de validation

- Valeur par défaut : `HEAD`


### `--target`

Nom de la branche cible. La valeur par défaut est la branche actuelle.

- Requiert une valeur

### `--force`, `-f`

Autoriser des mises à jour non rapides

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--force-with-lease`

Autoriser les mises à jour à transfert rapide, si la branche de suivi à distance est à jour

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--set-upstream`, `-u`

Définissez l’environnement cible comme amont pour la branche source. Le projet cible sera également défini comme distant pour le référentiel local.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--activate`

Activez l’environnement avant d’effectuer des opérations

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--parent`

Définissez le nouveau parent d’environnement (utilisé uniquement avec —activate).

- Requiert une valeur

### `--type`

Définissez le type d’environnement (utilisé uniquement avec —activate )

- Requiert une valeur

### `--no-clone-parent`

Ne pas cloner les données de la branche parente (utilisé uniquement avec —activate)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:redeploy`

Redéployer un environnement

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:relationships`

Afficher les relations d’un environnement

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

L&#39;environnement


### `--property`, `-P`

La propriété de relation à afficher

- Requiert une valeur

### `--refresh`

Actualisation ou non des relations

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:resume`

Reprendre un environnement en pause

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:scp`

Copie de fichiers vers et depuis un environnement à l’aide de scp

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

Fichiers à copier. Utilisez le préfixe remote : pour définir des emplacements distants.

- Valeur par défaut : `[]`

- Tableau

### `--recursive`, `-r`

Copier récursivement des répertoires entiers

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:ssh`

SSH vers l’environnement actuel

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Commande à exécuter sur l’environnement.

- Valeur par défaut : `[]`

- Tableau

### `--pipe`

Ne sortez que l’URL SSH.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--all`

Sortez toutes les URL SSH (pour chaque application).

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:synchronize`

Synchroniser le code et/ou les données d’un environnement avec son parent

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

Que synchroniser : &quot;code&quot;, &quot;données&quot; ou les deux

- Valeur par défaut : `[]`

- Tableau

### `--rebase`

Synchroniser le code en rebasant au lieu de fusionner

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:url`

Obtention des URL publiques d’un environnement

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`, `-1`

Ne renvoie que l’URL de l’itinéraire principal

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--browser`

Navigateur à utiliser pour ouvrir l’URL. Définissez 0 pour aucun.

- Requiert une valeur

### `--pipe`

Extrayez l’URL vers stdout.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `environment:xdebug`

Ouvrir un tunnel vers Xdebug sur l’environnement

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Le port local

- Valeur par défaut : `9000`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:activity:get`

Affichage d’informations détaillées sur une seule activité d’intégration

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Identifiant d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `activity`

ID d’activité. La valeur par défaut est l’activité d’intégration la plus récente.


### `--property`, `-P`

La propriété à afficher

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

[Option obsolète, non utilisée]

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:activity:list`

Obtention d’une liste des activités pour une intégration

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Identifiant d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `--type`

Filtrez les activités par type. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--exclude-type`, `-x`

Exclure les activités par type. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs. Les caractères % ou * peuvent être utilisés comme caractère générique pour exclure les types.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--limit`

Limiter le nombre de résultats affichés

- Valeur par défaut : `10`
- Requiert une valeur

### `--start`

Seules les activités créées avant cette date seront répertoriées.

- Requiert une valeur

### `--state`

Filtrage des activités par état. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--result`

Filtrage des activités par résultat

- Requiert une valeur

### `--incomplete`, `-i`

Ne répertorier que les activités incomplètes

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : id*, created*, description*, type*, state*, result*, completed (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

[Option obsolète, non utilisée]

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:activity:log`

Afficher le journal d’une activité d’intégration

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

Identifiant d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `activity`

ID d’activité. La valeur par défaut est l’activité d’intégration la plus récente.


### `--timestamps`, `-t`

Affichage d’un horodatage en regard de chaque message

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

[Option obsolète, non utilisée]

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:add`

Ajout d’une intégration au projet

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

Le type d&#39;intégration (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerDuty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;split&#39;, &#39;sumological&#39;, &#39;syslog&#39;).

- Requiert une valeur

### `--base-url`

URL de base de l’installation du serveur

- Requiert une valeur

### `--bitbucket-url`

URL de base de l’installation du serveur Bitbucket

- Requiert une valeur

### `--username`

Nom d’utilisateur du serveur Bitbucket

- Requiert une valeur

### `--token`

Un jeton d’authentification ou d’accès pour l’intégration

- Requiert une valeur

### `--key`

Une clé de consommateur OAuth pour Bitbucket

- Requiert une valeur

### `--secret`

Un secret de consommateur OAuth pour Bitbucket

- Requiert une valeur

### `--license-key`

Clé de licence des journaux New Relic

- Requiert une valeur

### `--server-project`

Le projet (par exemple &#39;espace de noms/repo&#39;)

- Requiert une valeur

### `--repository`

Le référentiel à suivre (par exemple, &#39;propriétaire/référentiel&#39;)

- Requiert une valeur

### `--build-merge-requests`

GitLab : créer des requêtes de fusion en tant qu’environnements

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-pull-requests`

Créer chaque demande d’extraction en tant qu’environnement

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-draft-pull-requests`

Création de requêtes d’extraction de brouillons

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-pull-requests-post-merge`

Créer des requêtes d’extraction en fonction de leur état de post-fusion

- Valeur par défaut : `false`
- Requiert une valeur

### `--build-wip-merge-requests`

GitLab : création de requêtes de fusion en cours

- Valeur par défaut : `true`
- Requiert une valeur

### `--merge-requests-clone-parent-data`

GitLab : données de clone pour les requêtes de fusion

- Valeur par défaut : `true`
- Requiert une valeur

### `--pull-requests-clone-parent-data`

Cloner les données de l’environnement parent pour les demandes d’extraction

- Valeur par défaut : `true`
- Requiert une valeur

### `--resync-pull-requests`

Resynchroniser les données de l’environnement des demandes d’extraction sur chaque version

- Valeur par défaut : `false`
- Requiert une valeur

### `--fetch-branches`

Récupérer toutes les branches à partir de la distante (en tant qu’environnements inactifs)

- Valeur par défaut : `true`
- Requiert une valeur

### `--prune-branches`

Supprimer les branches qui n’existent pas sur la télécommande

- Valeur par défaut : `true`
- Requiert une valeur

### `--resources-init`

Les ressources à utiliser lors de l&#39;initialisation d&#39;un nouveau service (&#39;minimum&#39;, &#39;défaut&#39;, &#39;manuel&#39;, &#39;parent&#39;)

- Requiert une valeur

### `--url`

URL ou point d’entrée d’API pour l’intégration

- Requiert une valeur

### `--shared-key`

Webhook : clé secrète partagée JWS

- Requiert une valeur

### `--file`

Nom d’un fichier local qui contient le script à charger.

- Requiert une valeur

### `--events`

Liste des événements sur lesquels agir, par exemple environment.push

- Valeur par défaut : `*`
- Requiert une valeur

### `--states`

Liste des états sur lesquels agir, par exemple en attente, en cours, terminé

- Valeur par défaut : `complete`
- Requiert une valeur

### `--environments`

Les identifiants d’environnement à inclure

- Valeur par défaut : `*`
- Requiert une valeur

### `--excluded-environments`

Les identifiants d’environnement à exclure

- Valeur par défaut : `[]`
- Requiert une valeur

### `--from-address`

[Facultatif] Adresse de l’expéditeur personnalisée pour les e-mails d’alerte

- Requiert une valeur

### `--recipients`

Adresse électronique du ou des destinataires

- Valeur par défaut : `[]`
- Requiert une valeur

### `--channel`

Canal Slack

- Requiert une valeur

### `--routing-key`

Clé de routage PagerDuty

- Requiert une valeur

### `--category`

La catégorie Logique de sumo, utilisée pour le filtrage

- Requiert une valeur

### `--index`

Index Splunk

- Requiert une valeur

### `--sourcetype`

Type de source d’événement Splunk

- Requiert une valeur

### `--protocol`

Protocole de transport Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Valeur par défaut : `tls`
- Requiert une valeur

### `--syslog-host`

Relais/hôte collecteur Syslog

- Requiert une valeur

### `--syslog-port`

Port du relais/collecteur Syslog

- Requiert une valeur

### `--facility`

Fonctionnalité Syslog

- Valeur par défaut : `1`
- Requiert une valeur

### `--message-format`

Format du message Syslog (&#39;rfc3164&#39; ou &#39;rfc5424&#39;)

- Valeur par défaut : `rfc5424`
- Requiert une valeur

### `--auth-mode`

Mode d’authentification (&#39;prefix&#39; ou &#39;structured_data&#39;)

- Valeur par défaut : `prefix`
- Requiert une valeur

### `--auth-token`

Jeton d’authentification

- Requiert une valeur

### `--verify-tls`

Indique si la vérification de certificat HTTPS doit être activée (recommandé).

- Valeur par défaut : `true`
- Requiert une valeur

### `--header`

En-tête(s) HTTP à utiliser dans les requêtes de POST. Séparez les noms et les valeurs par deux points (:).

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:delete`

Suppression d’une intégration d’un projet

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

ID d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:get`

Affichage des détails d’une intégration

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Identifiant d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `--property`, `-P`

La propriété d’intégration à afficher

- Accepte une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:list`

Affichage d’une liste des intégrations de projet

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : id, summary, type. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:update`

Mettre à jour une intégration

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

ID de l’intégration à mettre à jour


### `--type`

Le type d&#39;intégration (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhook&#39;, &#39;health.email&#39;, &#39;health.pagerDuty&#39;, &#39;health.slack&#39;, &#39;health.webhook&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;split&#39;, &#39;sumological&#39;, &#39;syslog&#39;).

- Requiert une valeur

### `--base-url`

URL de base de l’installation du serveur

- Requiert une valeur

### `--bitbucket-url`

URL de base de l’installation du serveur Bitbucket

- Requiert une valeur

### `--username`

Nom d’utilisateur du serveur Bitbucket

- Requiert une valeur

### `--token`

Un jeton d’authentification ou d’accès pour l’intégration

- Requiert une valeur

### `--key`

Une clé de consommateur OAuth pour Bitbucket

- Requiert une valeur

### `--secret`

Un secret de consommateur OAuth pour Bitbucket

- Requiert une valeur

### `--license-key`

Clé de licence des journaux New Relic

- Requiert une valeur

### `--server-project`

Le projet (par exemple &#39;espace de noms/repo&#39;)

- Requiert une valeur

### `--repository`

Le référentiel à suivre (par exemple, &#39;propriétaire/référentiel&#39;)

- Requiert une valeur

### `--build-merge-requests`

GitLab : créer des requêtes de fusion en tant qu’environnements

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-pull-requests`

Créer chaque demande d’extraction en tant qu’environnement

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-draft-pull-requests`

Création de requêtes d’extraction de brouillons

- Valeur par défaut : `true`
- Requiert une valeur

### `--build-pull-requests-post-merge`

Créer des requêtes d’extraction en fonction de leur état de post-fusion

- Valeur par défaut : `false`
- Requiert une valeur

### `--build-wip-merge-requests`

GitLab : création de requêtes de fusion en cours

- Valeur par défaut : `true`
- Requiert une valeur

### `--merge-requests-clone-parent-data`

GitLab : données de clone pour les requêtes de fusion

- Valeur par défaut : `true`
- Requiert une valeur

### `--pull-requests-clone-parent-data`

Cloner les données de l’environnement parent pour les demandes d’extraction

- Valeur par défaut : `true`
- Requiert une valeur

### `--resync-pull-requests`

Resynchroniser les données de l’environnement des demandes d’extraction sur chaque version

- Valeur par défaut : `false`
- Requiert une valeur

### `--fetch-branches`

Récupérer toutes les branches à partir de la distante (en tant qu’environnements inactifs)

- Valeur par défaut : `true`
- Requiert une valeur

### `--prune-branches`

Supprimer les branches qui n’existent pas sur la télécommande

- Valeur par défaut : `true`
- Requiert une valeur

### `--resources-init`

Les ressources à utiliser lors de l&#39;initialisation d&#39;un nouveau service (&#39;minimum&#39;, &#39;défaut&#39;, &#39;manuel&#39;, &#39;parent&#39;)

- Requiert une valeur

### `--url`

URL ou point d’entrée d’API pour l’intégration

- Requiert une valeur

### `--shared-key`

Webhook : clé secrète partagée JWS

- Requiert une valeur

### `--file`

Nom d’un fichier local qui contient le script à charger.

- Requiert une valeur

### `--events`

Liste des événements sur lesquels agir, par exemple environment.push

- Valeur par défaut : `*`
- Requiert une valeur

### `--states`

Liste des états sur lesquels agir, par exemple en attente, en cours, terminé

- Valeur par défaut : `complete`
- Requiert une valeur

### `--environments`

Les identifiants d’environnement à inclure

- Valeur par défaut : `*`
- Requiert une valeur

### `--excluded-environments`

Les identifiants d’environnement à exclure

- Valeur par défaut : `[]`
- Requiert une valeur

### `--from-address`

[Facultatif] Adresse de l’expéditeur personnalisée pour les e-mails d’alerte

- Requiert une valeur

### `--recipients`

Adresse électronique du ou des destinataires

- Valeur par défaut : `[]`
- Requiert une valeur

### `--channel`

Canal Slack

- Requiert une valeur

### `--routing-key`

Clé de routage PagerDuty

- Requiert une valeur

### `--category`

La catégorie Logique de sumo, utilisée pour le filtrage

- Requiert une valeur

### `--index`

Index Splunk

- Requiert une valeur

### `--sourcetype`

Type de source d’événement Splunk

- Requiert une valeur

### `--protocol`

Protocole de transport Syslog (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Valeur par défaut : `tls`
- Requiert une valeur

### `--syslog-host`

Relais/hôte collecteur Syslog

- Requiert une valeur

### `--syslog-port`

Port du relais/collecteur Syslog

- Requiert une valeur

### `--facility`

Fonctionnalité Syslog

- Valeur par défaut : `1`
- Requiert une valeur

### `--message-format`

Format du message Syslog (&#39;rfc3164&#39; ou &#39;rfc5424&#39;)

- Valeur par défaut : `rfc5424`
- Requiert une valeur

### `--auth-mode`

Mode d’authentification (&#39;prefix&#39; ou &#39;structured_data&#39;)

- Valeur par défaut : `prefix`
- Requiert une valeur

### `--auth-token`

Jeton d’authentification

- Requiert une valeur

### `--verify-tls`

Indique si la vérification de certificat HTTPS doit être activée (recommandé).

- Valeur par défaut : `true`
- Requiert une valeur

### `--header`

En-tête(s) HTTP à utiliser dans les requêtes de POST. Séparez les noms et les valeurs par deux points (:).

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `integration:validate`

Validation d’une intégration existante

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

Identifiant d’intégration. Laissez vide pour effectuer une sélection dans une liste.


### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `local:build`

Créer localement le projet actuel

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Spécification des applications à créer

- Valeur par défaut : `[]`

- Tableau

### `--abslinks`, `-a`

Utiliser des liens absolus

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--source`, `-s`

Répertoire source. La valeur par défaut est la racine du projet actuel.

- Requiert une valeur

### `--destination`, `-d`

La destination, à laquelle la racine web de chaque application sera associée par un lien symbolique. Valeur par défaut : _www

- Requiert une valeur

### `--copy`, `-c`

Copiez dans un répertoire de build, au lieu de créer un lien symbolique à partir de la source

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--clone`

Utilisation de Git pour cloner l’HEAD actuel dans le répertoire de génération

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--run-deploy-hooks`

Exécuter le déploiement et/ou les hooks post_deploy

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-clean`

Ne pas supprimer les anciennes versions

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-archive`

Ne pas créer ni utiliser d’archive de version

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-backup`

Ne pas sauvegarder le build précédent

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-cache`

Désactiver la mise en cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-build-hooks`

N’exécutez pas les crochets après la génération

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-deps`

N’installez pas de dépendances de build localement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--working-copy`

Drush : utilisez git pour cloner un référentiel de chaque module Drupal plutôt que de simplement télécharger une version.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--concurrency`

Supprimer : définissez le nombre de projets simultanés qui seront traités simultanément.

- Valeur par défaut : `4`
- Requiert une valeur

### `--lock`

Drush : création ou mise à jour d&#39;un fichier de verrouillage (disponible uniquement avec Drush version 7+)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `local:dir`

Recherche de la racine de projet locale

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

Le sous-répertoire à trouver (&#39;local&#39;, &#39;web&#39; ou &#39;shared&#39;)


### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `metrics:all`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Afficher les mesures du processeur, du disque et de la mémoire pour un environnement

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Afficher les tailles en octets

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--range`, `-r`

Période. Les mesures seront chargées pendant cette durée jusqu’à l’heure de fin (—to). Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>5m\&lt;/comment>, maximum \&lt;comment>8h\&lt;/comment> ou plus (selon le projet), \ par défaut&lt;comment>10m\&lt;/comment>.

- Requiert une valeur

### `--interval`, `-i`

Intervalle de temps. La valeur par défaut est une division de la plage. Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Requiert une valeur

### `--to`

L&#39;heure de fin. La valeur par défaut est désormais définie.

- Requiert une valeur

### `--latest`, `-1`

Afficher uniquement le dernier point de données unique

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--service`, `-s`

Filtrer par nom de service ou d’application Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--type`

Filtrez par type de service (si —service n’est pas fourni). La version n’est pas requise. Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : timestamp*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used, tmp_inodes limit, tmp_inodes_percent, tmp_inodes_used, type (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `metrics:cpu`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BÊTA \&lt;/> Afficher l’utilisation du processeur dans un environnement

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

Période. Les mesures seront chargées pendant cette durée jusqu’à l’heure de fin (—to). Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>5m\&lt;/comment>, maximum \&lt;comment>8h\&lt;/comment> ou plus (selon le projet), \ par défaut&lt;comment>10m\&lt;/comment>.

- Requiert une valeur

### `--interval`, `-i`

Intervalle de temps. La valeur par défaut est une division de la plage. Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Requiert une valeur

### `--to`

L&#39;heure de fin. La valeur par défaut est désormais définie.

- Requiert une valeur

### `--latest`, `-1`

Afficher uniquement le dernier point de données unique

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--service`, `-s`

Filtrer par nom de service ou d’application Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--type`

Filtrez par type de service (si —service n’est pas fourni). La version n’est pas requise. Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : horodatage*, service*, utilisé*, limite*, pourcentage*, type (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `metrics:disk-usage`

Afficher l’utilisation du disque dans un environnement

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Afficher les tailles en octets

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--range`, `-r`

Période. Les mesures seront chargées pendant cette durée jusqu’à l’heure de fin (—to). Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>5m\&lt;/comment>, maximum \&lt;comment>8h\&lt;/comment> ou plus (selon le projet), \ par défaut&lt;comment>10m\&lt;/comment>.

- Requiert une valeur

### `--interval`, `-i`

Intervalle de temps. La valeur par défaut est une division de la plage. Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Requiert une valeur

### `--to`

L&#39;heure de fin. La valeur par défaut est désormais définie.

- Requiert une valeur

### `--latest`, `-1`

Afficher uniquement le dernier point de données unique

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--service`, `-s`

Filtrer par nom de service ou d’application Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--type`

Filtrez par type de service (si —service n’est pas fourni). La version n’est pas requise. Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--tmp`

Rapport sur l’utilisation temporaire du disque (affiche les colonnes : horodatage, service, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `metrics:memory`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Afficher l’utilisation de la mémoire dans un environnement

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Afficher les tailles en octets

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--range`, `-r`

Période. Les mesures seront chargées pendant cette durée jusqu’à l’heure de fin (—to). Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>5m\&lt;/comment>, maximum \&lt;comment>8h\&lt;/comment> ou plus (selon le projet), \ par défaut&lt;comment>10m\&lt;/comment>.

- Requiert une valeur

### `--interval`, `-i`

Intervalle de temps. La valeur par défaut est une division de la plage. Vous pouvez spécifier les unités : heures (h), minutes (m) ou secondes (s). Minimum \&lt;comment>1m\&lt;/comment>.

- Requiert une valeur

### `--to`

L&#39;heure de fin. La valeur par défaut est désormais définie.

- Requiert une valeur

### `--latest`, `-1`

Afficher uniquement le dernier point de données unique

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--service`, `-s`

Filtrer par nom de service ou d’application Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--type`

Filtrez par type de service (si —service n’est pas fourni). La version n’est pas requise. Les caractères % ou * peuvent être utilisés comme caractères génériques.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : horodatage*, service*, utilisé*, limite*, pourcentage*, type (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `mount:download`

Téléchargement de fichiers à partir d’un montage à l’aide de la synchronisation

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Téléchargement depuis toutes les montures

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--mount`, `-m`

Le montage (en tant que chemin relatif à l’application)

- Requiert une valeur

### `--target`

Répertoire vers lequel les fichiers seront téléchargés. Si —all est utilisé, le chemin de montage est ajouté

- Requiert une valeur

### `--source-path`

Utilisez le chemin source du montage (plutôt que le chemin de montage) comme sous-répertoire de la cible, lorsque —all est utilisé

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--delete`

Suppression des fichiers superflus dans le répertoire cible

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--exclude`

Fichier(s) à exclure du téléchargement (modèle)

- Valeur par défaut : `[]`
- Requiert une valeur

### `--include`

Fichier(s) à ne pas exclure (motif)

- Valeur par défaut : `[]`
- Requiert une valeur

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `mount:list`

Obtention d’une liste de montages

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Sortie des chemins de montage uniquement (une par ligne)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : définition, chemin. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `mount:size`

Vérification de l’utilisation des supports sur le disque

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Afficher les tailles en octets

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--refresh`

Actualisation du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : disponibles, max, montées, percent_used, tailles, utilisées. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `mount:upload`

Chargement de fichiers sur un montage à l’aide de la synchronisation

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

Un répertoire contenant les fichiers à charger

- Requiert une valeur

### `--mount`, `-m`

Le montage (en tant que chemin relatif à l’application)

- Requiert une valeur

### `--delete`

Suppression des fichiers superflus dans le montage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--exclude`

Fichier(s) à exclure du transfert (modèle)

- Valeur par défaut : `[]`
- Requiert une valeur

### `--include`

Fichier(s) à ne pas exclure (motif)

- Valeur par défaut : `[]`
- Requiert une valeur

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--instance`, `-I`

Un ID d’instance

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `operation:list`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Liste des opérations d’exécution dans un environnement

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Ne limitez pas la longueur de la commande à afficher. La limite par défaut est de 24 lignes.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : service*, nom*, début*, rôle, arrêt (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `operation:run`

\&lt;fg white=&quot;&quot; bg=&quot;red&quot;> BETA \&lt;/> Exécuter une opération sur l’environnement

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Nom de l’opération


### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--worker`

Nom du travailleur

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `project:clear-build-cache`

Effacer le cache de création d’un projet

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `project:get`

Clonage local d’un projet

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

ID de projet


### `directory`

Répertoire vers lequel effectuer le clonage. Par défaut, titre du projet


### `--environment`, `-e`

ID d’environnement à cloner. La valeur par défaut est le projet ou le premier environnement disponible.

- Requiert une valeur

### `--depth`

Créer un clone superficiel : limite le nombre de validations dans l&#39;historique

- Requiert une valeur

### `--build`

Création du projet après clonage

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `project:info`

Lecture ou définition des propriétés d’un projet

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Nom de la propriété


### `value`

Définir une nouvelle valeur pour la propriété


### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `project:list`

Obtention d’une liste de tous les projets actifs

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Permet de générer une liste simple d’ID de projet. Désactive la pagination.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--region`

Filtrage par région (correspondance exacte)

- Requiert une valeur

### `--title`

Filtrage par titre (recherche non sensible à la casse)

- Requiert une valeur

### `--my`

Afficher uniquement les projets que vous possédez

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--refresh`

Actualisation ou non de la liste

- Valeur par défaut : `1`
- Requiert une valeur

### `--sort`

Propriété à trier par

- Valeur par défaut : `title`
- Requiert une valeur

### `--reverse`

Tri dans l’ordre inverse (décroissant)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--page`

Numéro de page. Cela active la pagination, malgré la configuration ou —count. Ignoré si —pipe est spécifié.

- Requiert une valeur

### `--count`, `-c`

Nombre de projets à afficher par page. Utilisez 0 pour désactiver la pagination. Ignoré si —page est spécifié.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`

Colonnes à afficher. Colonnes disponibles : id*, titre*, région*, created_at, organization_id, organization_label, organization_name, status (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `project:set-remote`

Définition du projet distant pour le référentiel Git actuel

```bash
magento-cloud set-remote [<project>]
```


### `project`

ID de projet


### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `repo:cat`

Lecture d’un fichier dans le référentiel de projet

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

Chemin d’accès au fichier

- Obligatoire

### `--commit`, `-c`

La validation SHA. Cela peut également accepter les suffixes &quot;HEAD&quot; et caret (^) ou tilde (~) pour les validations parentes.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `repo:ls`

Liste des fichiers dans le référentiel du projet

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Chemin d’accès à un sous-répertoire


### `--directories`, `-d`

Afficher uniquement les répertoires

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--files`, `-f`

Afficher les fichiers uniquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--git-style`

Sortie de style similaire à &quot;git ls-tree&quot;

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--commit`, `-c`

La validation SHA. Cela peut également accepter les suffixes &quot;HEAD&quot; et caret (^) ou tilde (~) pour les validations parentes.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `repo:read`

Lecture d’un répertoire ou d’un fichier dans le référentiel de projet

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Chemin d’accès au répertoire ou au fichier


### `--commit`, `-c`

La validation SHA. Cela peut également accepter les suffixes &quot;HEAD&quot; et caret (^) ou tilde (~) pour les validations parentes.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `route:get`

Affichage d’informations détaillées sur un itinéraire

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

URL d’origine de l’itinéraire


### `--id`

Identifiant d’itinéraire à sélectionner

- Requiert une valeur

### `--primary`, `-1`

Sélectionner l’itinéraire principal

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--property`, `-P`

La propriété à afficher

- Requiert une valeur

### `--refresh`

Contournement du cache des itinéraires

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

[Option obsolète, qui n’est plus utilisée]

- Requiert une valeur

### `--identity-file`, `-i`

[Option obsolète, qui n’est plus utilisée]

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `route:list`

Répertorier toutes les routes d’un environnement

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

ID d’environnement


### `--refresh`

Contournement du cache des itinéraires

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : route*, type*, to*, url (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `self:install`

Installation ou mise à jour des fichiers de configuration de l’interface de ligne de commande

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

Type shell pour la saisie semi-automatique (bash ou zsh)

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `self:update`

Mise à jour de l’interface de ligne de commande vers la dernière version

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Mise à jour uniquement entre les versions mineures ou les versions de correctif

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--unstable`

Mise à jour vers une nouvelle version instable, le cas échéant

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--manifest`

Remplacement de l’emplacement du fichier manifeste

- Requiert une valeur

### `--current-version`

Remplacer la version actuelle

- Requiert une valeur

### `--timeout`

Délai d’expiration de la vérification de version

- Valeur par défaut : `30`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:list`

Répertorier les services du projet

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--pipe`

Générer une liste de noms de service uniquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : disque, nom, taille, type. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:mongo:dump`

Création d’un vidage d’archive binaire de données à partir de MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

La collection à vider

- Requiert une valeur

### `--gzip`, `-z`

Compresser la vidure à l’aide de gzip

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--stdout`, `-o`

Sortie à STDOUT au lieu d’un fichier

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:mongo:export`

Exporter des données depuis MongoDB

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

La collection à exporter

- Requiert une valeur

### `--jsonArray`

Exportation des données sous la forme d’un tableau JSON unique

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--type`

Type d’exportation, par exemple &quot;csv&quot;

- Requiert une valeur

### `--fields`, `-f`

Champs à exporter

- Valeur par défaut : `[]`
- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:mongo:restore`

Restauration d’un vidage d’archive binaire de données dans MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

La collection à restaurer

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:mongo:shell`

Utilisation du conteneur MongoDB

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Transmettre un fragment JavaScript au conteneur

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `service:redis-cli`

Accès à l’interface de ligne de commande Redis

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

Arguments à ajouter à la commande Redis


### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `snapshot:create`

Créer un instantané d’un environnement

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

L&#39;environnement


### `--live`

Sauvegarde en direct : n’arrêtez pas l’environnement. Si cette option est définie, l’environnement est exécuté et ouvert aux connexions pendant la sauvegarde. Cela réduit les temps d’arrêt, au risque de sauvegarder les données dans un état incohérent.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `snapshot:delete`

Suppression d’un instantané d’environnement

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Identifiant de l’instantané. Requis en mode non interactif.


### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `snapshot:get`

Affichage d’un instantané d’environnement

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Identifiant de l’instantané. La valeur par défaut est la plus récente.


### `--property`, `-P`

La propriété à afficher.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `snapshot:list`

Liste des instantanés disponibles d’un environnement

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `snapshot:restore`

Restauration d’un instantané d’environnement

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

Nom de l’instantané. La valeur par défaut est la plus récente.


### `--target`

Environnement vers lequel restaurer. Par défaut, l’environnement actuel de l’instantané

- Requiert une valeur

### `--branch-from`

Si —target n’existe pas encore, cela indique le parent du nouvel environnement.

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `source-operation:list`

Liste des opérations source sur un environnement

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Ne limitez pas la longueur de la commande à afficher. La limite par défaut est de 24 lignes.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : application, commande, opération. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `source-operation:run`

Exécution d’une opération source

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Nom de l’opération


### `--variable`

Variable à définir pendant l’opération, au format \&lt;info>type:name=value\&lt;/info>

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `ssh-cert:load`

Générer un certificat SSH

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Actualisez uniquement le certificat, si nécessaire (n’écrivez pas de configuration SSH)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--new`

Forcer l’actualisation du certificat

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--new-key`

[Obsolète] Utilisez plutôt —new

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `ssh-key:add`

Ajout d’une nouvelle clé SSH

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

Chemin d’accès à une clé publique SSH existante


### `--name`

Nom permettant d’identifier la clé

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `ssh-key:delete`

Supprimer une clé SSH

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

ID de la clé SSH à supprimer


### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `ssh-key:list`

Obtention d’une liste des clés SSH dans votre compte

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : id*, titre*, chemin*, empreinte digitale (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `subscription:info`

Lecture ou modification des propriétés d’abonnement

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

Nom de la propriété


### `value`

Définir une nouvelle valeur pour la propriété


### `--id`, `-s`

ID d’abonnement

- Requiert une valeur

### `--date-fmt`

Format de date (en tant que chaîne de format de date PHP)

- Valeur par défaut : `c`
- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `tunnel:close`

Fermer les tunnels SSH

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Fermer tous les tunnels

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `tunnel:info`

Affichage des informations de relation pour les tunnels SSH

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

La propriété de relation à afficher

- Requiert une valeur

### `--encode`, `-c`

Sortie sous forme de JSON encodé en base64

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `tunnel:list`

Liste des tunnels SSH

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`, `-a`

Afficher tous les tunnels

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : port*, projet*, environnement*, app*, relation*, url (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `tunnel:open`

Ouvrir les tunnels SSH aux relations d’une application

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Autoriser les hôtes distants à se connecter aux ports transférés locaux

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `tunnel:single`

Ouvrir un tunnel SSH unique vers une relation d’application

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Le port local

- Requiert une valeur

### `--gateway-ports`, `-g`

Autoriser les hôtes distants à se connecter aux ports transférés locaux

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--app`, `-A`

Nom de l’application distante

- Requiert une valeur

### `--relationship`, `-r`

Relation de service à utiliser

- Requiert une valeur

### `--identity-file`, `-i`

Une identité SSH (clé privée) à utiliser

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `user:add`

Ajout d’un utilisateur au projet

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Adresse électronique de l’utilisateur


### `--role`, `-r`

Rôle de projet de l’utilisateur (&#39;admin&#39; ou &#39;viewer&#39;) ou rôle de type d’environnement (par exemple &#39;staging:contributor&#39; ou &#39;production:viewer&#39;). Pour supprimer un utilisateur d’un type d’environnement, définissez le rôle sur &quot;aucun&quot;. Les caractères % ou * peuvent être utilisés comme caractères génériques pour le type d’environnement, par exemple &#39;%:viewer&#39; pour donner à l’utilisateur le rôle &quot;visualisateur&quot; sur tous les types. Le rôle peut être abrégé, par exemple &#39;production:v&#39;.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--force-invite`

Envoyer une invitation, même si une invitation a déjà été envoyée

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `user:delete`

Suppression d’un utilisateur du projet

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

Adresse électronique de l’utilisateur

- Obligatoire

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `user:get`

Affichage du ou des rôles d’un utilisateur

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

Adresse électronique de l’utilisateur


### `--level`, `-l`

Le niveau de rôle (&#39;projet&#39; ou &#39;environnement&#39;)

- Requiert une valeur

### `--pipe`

Extraire le rôle sur stdout (après avoir apporté des modifications)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--role`, `-r`

[Obsolète : utilisez user:update pour modifier le ou les rôles d’un utilisateur]

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `user:list`

Liste des utilisateurs de projet

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : email*, nom*, rôle*, id*, allow_at, updated_at (* = colonnes par défaut). Le caractère &quot;+&quot; peut être utilisé comme espace réservé pour les colonnes par défaut. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `user:update`

Mise à jour du ou des rôles utilisateur sur un projet

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Adresse électronique de l’utilisateur


### `--role`, `-r`

Rôle de projet de l’utilisateur (&#39;admin&#39; ou &#39;viewer&#39;) ou rôle de type d’environnement (par exemple &#39;staging:contributor&#39; ou &#39;production:viewer&#39;). Pour supprimer un utilisateur d’un type d’environnement, définissez le rôle sur &quot;aucun&quot;. Les caractères % ou * peuvent être utilisés comme caractères génériques pour le type d’environnement, par exemple &#39;%:viewer&#39; pour donner à l’utilisateur le rôle &quot;visualisateur&quot; sur tous les types. Le rôle peut être abrégé, par exemple &#39;production:v&#39;.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `variable:create`

Création d’une variable

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

Nom de variable


### `--update`, `-u`

Mettre à jour la variable si elle existe déjà

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--level`, `-l`

Le niveau auquel définir la variable (&#39;projet&#39; ou &#39;environnement&#39;)

- Requiert une valeur

### `--name`

Nom de variable

- Requiert une valeur

### `--value`

Valeur de la variable

- Requiert une valeur

### `--json`

Si la valeur de la variable est au format JSON

- Valeur par défaut : `false`
- Requiert une valeur

### `--sensitive`

Si la valeur de la variable est sensible

- Valeur par défaut : `false`
- Requiert une valeur

### `--prefix`

Préfixe du nom de variable qui peut déterminer son type, par exemple &#39;env&#39;. Uniquement applicable si le nom ne contient pas déjà de préfixe. (par exemple, &#39;none&#39; ou &#39;env:&#39;)

- Valeur par défaut : `none`
- Requiert une valeur

### `--enabled`

si la variable doit être activée dans l’environnement ;

- Valeur par défaut : `true`
- Requiert une valeur

### `--inheritable`

Si la variable est héritable par les environnements enfants

- Valeur par défaut : `true`
- Requiert une valeur

### `--visible-build`

Si la variable doit être visible au moment de la création.

- Requiert une valeur

### `--visible-runtime`

Si la variable doit être visible au moment de l’exécution

- Valeur par défaut : `true`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `variable:delete`

Suppression d’une variable

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Nom de variable

- Obligatoire

### `--level`, `-l`

Au niveau de la variable (&#39;projet&#39;, &#39;environnement&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `variable:get`

Affichage d’une variable

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

Nom de la variable


### `--property`, `-P`

Affichage d’une propriété de variable unique

- Requiert une valeur

### `--level`, `-l`

Au niveau de la variable (&#39;projet&#39;, &#39;environnement&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--pipe`

[Option obsolète] Générer la valeur de variable uniquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `variable:list`

Variables de liste

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`, `-l`

Au niveau de la variable (&#39;projet&#39;, &#39;environnement&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : is_enabled, niveau, nom, valeur. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `variable:update`

Mettre à jour une variable

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Nom de variable

- Obligatoire

### `--allow-no-change`

Retour réussi (zéro code de sortie) si aucune modification n’a été apportée

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--level`, `-l`

Au niveau de la variable (&#39;projet&#39;, &#39;environnement&#39;, &#39;p&#39; ou &#39;e&#39;)

- Requiert une valeur

### `--value`

Valeur de la variable

- Requiert une valeur

### `--json`

Si la valeur de la variable est au format JSON

- Valeur par défaut : `false`
- Requiert une valeur

### `--sensitive`

Si la valeur de la variable est sensible

- Valeur par défaut : `false`
- Requiert une valeur

### `--enabled`

si la variable doit être activée dans l’environnement ;

- Valeur par défaut : `true`
- Requiert une valeur

### `--inheritable`

Si la variable est héritable par les environnements enfants

- Valeur par défaut : `true`
- Requiert une valeur

### `--visible-build`

Si la variable doit être visible au moment de la création.

- Requiert une valeur

### `--visible-runtime`

Si la variable doit être visible au moment de l’exécution

- Valeur par défaut : `true`
- Requiert une valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--no-wait`, `-W`

N’attendez pas la fin de l’opération.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--wait`

Attente de la fin de l’opération (par défaut)

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur


## `worker:list`

Obtention d’une liste de tous les programmes de travail déployés

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Actualisation ou non du cache

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--pipe`

Générer une liste de noms de programmes de travail uniquement

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--project`, `-p`

ID ou URL du projet

- Requiert une valeur

### `--environment`, `-e`

Identifiant de l’environnement. Utilisez &quot;.&quot; pour sélectionner l’environnement par défaut du projet.

- Requiert une valeur

### `--format`

Format de sortie : tableau, csv, tsv ou brut

- Valeur par défaut : `table`
- Requiert une valeur

### `--columns`, `-c`

Colonnes à afficher. Colonnes disponibles : commandes, nom, type. Les caractères % ou * peuvent être utilisés comme caractères génériques. Les valeurs peuvent être fractionnées par des virgules (par exemple &quot;a,b,c&quot;) et/ou des espaces blancs.

- Valeur par défaut : `[]`
- Requiert une valeur

### `--no-header`

Ne pas générer l’en-tête du tableau

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--help`, `-h`

Afficher ce message d’aide

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--verbose`, `-v|-vv|-vvv`

Augmenter la verbalisation des messages

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--version`, `-V`

Afficher cette version de l’application

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--yes`, `-y`

Répondez &quot;oui&quot; aux questions de confirmation ; acceptez la valeur par défaut pour les autres questions ; désactivez l’interaction.

- Valeur par défaut : `false`
- N’accepte pas de valeur

### `--no-interaction`

Ne posez aucune question interactive ; acceptez les valeurs par défaut. Équivalent à l’utilisation de la variable d’environnement : \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Valeur par défaut : `false`
- N’accepte pas de valeur

