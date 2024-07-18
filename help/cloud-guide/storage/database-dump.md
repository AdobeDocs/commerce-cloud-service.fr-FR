---
title: Sauvegarde de la base
description: Découvrez comment utiliser les outils ECE pour créer une sauvegarde de la base de données pour un projet d’infrastructure cloud Adobe Commerce.
feature: Cloud, Iaas, Storage
exl-id: 8a96effe-a587-4edf-b0c7-e73ca8d3b56c
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Sauvegarde de la base

Vous pouvez créer une copie de votre base de données à l’aide de la commande `ece-tools db-dump` sans capturer toutes les données d’environnement des services et des montages. Par défaut, cette commande crée des sauvegardes dans le répertoire `/app/var/dump-main` pour toutes les connexions de base de données spécifiées dans la configuration de l’environnement. L’opération de vidage DB bascule l’application vers le mode de maintenance, arrête les processus de file d’attente des consommateurs et désactive les tâches cron avant que la vidage ne commence.

Tenez compte des instructions suivantes pour le vidage DB :

- Pour les environnements de production, Adobe recommande d’effectuer des opérations de vidage de la base de données aux heures creuses afin de minimiser les interruptions de service qui se produisent lorsque le site est en mode de maintenance.
- Si une erreur se produit lors de l’opération de vidage, la commande supprime le fichier de vidage pour économiser l’espace disque. Consultez les journaux pour plus de détails (`var/log/cloud.log`).
- Pour les environnements de production, cette commande est vidée uniquement de _un_ des trois noeuds haute disponibilité. Par conséquent, les données de production écrites sur un autre noeud pendant le vidage peuvent ne pas être copiées. La commande génère un fichier `var/dbdump.lock` pour empêcher l’exécution de la commande sur plusieurs noeuds.
- Pour une sauvegarde de tous les services d’environnement, Adobe recommande de créer une [sauvegarde](snapshots.md).

Vous pouvez choisir de sauvegarder plusieurs bases de données en ajoutant les noms de la base à la commande . L’exemple suivant sauvegarde deux bases de données : `main` et `sales` :

```bash
php vendor/bin/ece-tools db-dump main sales
```

Utilisez la commande `php vendor/bin/ece-tools db-dump --help` pour plus d’options :

- `--dump-directory=<dir>` : choisissez un répertoire cible pour le vidage de la base de données.
- `--remove-definers` : suppression des instructions DEFINER du vidage de base de données

**Pour créer un vidage de base de données dans l’environnement d’évaluation ou de production** :

1. [Utilisez SSH pour vous connecter ou créer un tunnel pour vous connecter à l’environnement distant ](../development/secure-connections.md) qui contient la base de données à copier.

1. Listez les relations de l&#39;environnement et notez les informations de connexion à la base de données.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Créez une sauvegarde de la base. Pour choisir un répertoire cible pour le vidage DB, utilisez l’option `--dump-directory`.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Exemple de réponse :

   ```
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. La commande `db-dump` crée un fichier d’archive `dump-<timestamp>.sql.gz` dans le répertoire du projet distant.

>[!TIP]
>
>Si vous souhaitez transmettre ces données à un environnement spécifique, reportez-vous à la section [Migration de données et de fichiers statiques](../deploy/staging-production.md#migrate-static-files).
