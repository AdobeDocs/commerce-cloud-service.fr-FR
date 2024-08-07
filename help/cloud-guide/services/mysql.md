---
title: Configuration du service MySQL
description: Découvrez comment gérer le service MySQL pour le stockage de données persistant avec Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
source-git-commit: 9be8d1e062ab3dba86bc4d9c9ee8b8ece33d5b75
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# Configuration du service MySQL

Le service `mysql` fournit un stockage de données persistant basé sur les versions 10.2 à 10.4 de [MariaDB](https://mariadb.com/), prenant en charge le moteur de stockage [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) et les fonctionnalités réimplémentées de MySQL 5.6 et 5.7.

La réindexation sur MariaDB 10.4 prend plus de temps que les autres versions de MariaDB ou de MySQL. Voir [Indexers](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) dans le guide _Bonnes pratiques de performances_ .

>[!WARNING]
>
>Soyez prudent lors de la mise à niveau de MariaDB de la version 10.1 vers la version 10.2. MariaDB 10.1 est la dernière version qui prend en charge _XtraDB_ en tant que moteur de stockage. MariaDB 10.2 utilise _InnoDB_ pour le moteur de stockage. Après la mise à niveau de la version 10.1 vers la version 10.2, vous ne pouvez pas annuler la modification. Adobe Commerce prend en charge les deux moteurs de stockage. Cependant, vous devez vérifier les extensions et les autres systèmes utilisés par votre projet pour vous assurer qu’ils sont compatibles avec MariaDB 10.2. Voir [Modifications incompatibles entre 10.1 et 10.2](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**Pour activer MySQL** :

1. Ajoutez le nom, le type et la valeur de disque requis (en Mo) au fichier `.magento/services.yaml`.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >Des erreurs MySQL, telles que `PDO Exception: MySQL server has gone away`, peuvent se produire en raison d’un espace disque insuffisant. Vérifiez que vous avez alloué suffisamment d’espace disque au service dans le fichier [`.magento/services.yaml`](services-yaml.md#disk).

1. Configurez les relations dans le fichier `.magento.app.yaml`.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [Vérifiez les relations de service](services-yaml.md#service-relationships).

{{service-change-tip}}

## Configuration de la base de données MySQL

Lors de la configuration de la base de données MySQL, vous disposez des options suivantes :

- **`schemas`** : un schéma définit une base de données. Le schéma par défaut est la base de données `main`.
- **`endpoints`** : chaque point de terminaison représente des informations d’identification avec des privilèges spécifiques. Le point de terminaison par défaut est `mysql`, qui a `admin` accès à la base de données `main`.
- **`properties`** : les propriétés sont utilisées pour définir des configurations de base de données supplémentaires.

Voici un exemple de configuration de base dans le fichier `.magento/services.yaml` :

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

`properties` dans l’exemple ci-dessus modifie les paramètres par défaut `optimizer` comme [ recommandé dans le guide des bonnes pratiques de performances](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers).

**Options de configuration MariaDB** :

| Options | Description | Valeur par défaut |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | Jeu de caractères par défaut. | utf8mb4 |
| `default_collation` | Classement par défaut. | utf8mb4_unicode_ci |
| `max_allowed_packet` | Taille maximale des paquets, en Mo. Plage `1` à `100`. | 16 |
| `optimizer_switch` | Définissez des valeurs pour l’optimiseur de requête. Voir la [documentation MariaDB](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Sélectionnez les statistiques utilisées par l&#39;optimiseur. Plage `1` à `5`. Voir la [documentation MariaDB](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 pour 10.4 et versions ultérieures |

### Configuration de plusieurs utilisateurs de la base de données

Vous pouvez éventuellement configurer plusieurs utilisateurs avec différentes autorisations pour accéder à la base de données `main`.

Par défaut, un point d’entrée nommé `mysql` a un accès administrateur à la base de données. Pour configurer plusieurs utilisateurs de la base de données, vous devez définir plusieurs points de terminaison dans le fichier `services.yaml` et déclarer les relations dans le fichier `.magento.app.yaml`. Pour les environnements d’évaluation et de production Pro, [Envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander à l’utilisateur supplémentaire.

Utilisez un tableau imbriqué pour définir les points de terminaison d’un accès utilisateur spécifique. Chaque point de terminaison peut désigner l’accès à un ou plusieurs schémas (bases de données) et différents niveaux d’autorisation pour chacun d’eux.

Les niveaux d’autorisation valides sont les suivants :

- `ro` : seules les requêtes SELECT sont autorisées.
- `rw` : les requêtes SELECT et les requêtes INSERT, UPDATE et DELETE sont autorisées.
- `admin` : toutes les requêtes sont autorisées, y compris les requêtes DDL (CREATE TABLE, DROP TABLE, etc.).

Par exemple :

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

Dans l’exemple précédent, le point d’entrée `admin` fournit un accès de niveau administrateur à la base de données `main`, le point d’entrée `reporter` fournit un accès en lecture seule et le point d’entrée `importer` fournit un accès en lecture-écriture, ce qui signifie :

- L’utilisateur `admin` contrôle entièrement la base de données.
- L’utilisateur `reporter` dispose uniquement de privilèges SELECT .
- L’utilisateur `importer` dispose des privilèges SELECT, INSERT, UPDATE et DELETE.

Ajoutez les points de terminaison définis dans l’exemple ci-dessus à la propriété `relationships` du fichier `.magento.app.yaml`. Par exemple :

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>Si vous configurez un utilisateur MySQL, vous ne pouvez pas utiliser le mécanisme de contrôle d’accès [`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) pour les procédures et vues stockées.

## Connexion à la base de données

Pour accéder directement à la base de données MariaDB, vous devez utiliser un SSH afin de vous connecter à l’environnement cloud distant et vous connecter à la base de données.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Récupérez les informations d’identification de connexion MySQL des propriétés `database` et `type` dans la variable [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) .

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Dans la réponse, recherchez les informations MySQL. Par exemple :

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Connexion à la base de données.

   - Pour commencer, utilisez la commande suivante :

     ```bash
     mysql -h database.internal -u <username>
     ```

   - Pour Pro, utilisez la commande suivante avec le nom d’hôte, le numéro de port, le nom d’utilisateur et le mot de passe récupérés de la variable `$MAGENTO_CLOUD_RELATIONSHIPS`.

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>Vous pouvez utiliser la commande `magento-cloud db:sql` pour vous connecter à la base distante et exécuter des commandes SQL.

## Connexion à la base de données secondaire

>[!IMPORTANT]
>
>Cette fonctionnalité est disponible uniquement sur les grappes de production et d’évaluation Pro.

Parfois, vous devez vous connecter à la base de données secondaire pour améliorer les performances de la base de données ou résoudre les problèmes de verrouillage de la base de données. Si cette configuration est requise, utilisez `"port" : 3304` pour établir la connexion. Voir la rubrique [ Meilleures pratiques pour configurer la connexion esclave MySQL](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) dans le guide _Bonnes pratiques d’implémentation_ .

## Dépannage

Pour obtenir de l’aide sur la résolution des problèmes MySQL, reportez-vous aux articles suivants du support Adobe Commerce :

- [Vérification de requêtes lentes et processus MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [Créer un vidage de base de données sur Cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [Dépannage de l’outil de migration de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Mise à niveau d’Adobe Commerce : compacte vers les tables dynamiques 2.2.x, 2.3.x vers 2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
