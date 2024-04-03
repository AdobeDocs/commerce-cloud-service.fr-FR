---
title: Déploiement vers l’évaluation et la production
description: Découvrez comment déployer votre Adobe Commerce sur le code d’infrastructure cloud dans les environnements d’évaluation et de production pour effectuer d’autres tests.
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# Déploiement vers l’évaluation et la production

Le processus de déploiement et de mise en production commence par le développement, se poursuit par l’évaluation et se termine par la mise en production. Adobe fournit une solution d’environnement de bout en bout pour garantir des configurations cohérentes. Chaque environnement prend en charge l’accès URL direct au storefront et l’accès Admin et SSH pour les commandes d’interface de ligne de commande.

Lorsque vous êtes prêt à déployer votre magasin, vous devez effectuer le déploiement et les tests dans l’environnement d’évaluation avant de procéder au déploiement vers Production. Cette section fournit des instructions et des informations détaillées sur le processus de création et de déploiement, la migration des données et du contenu et les tests.

>[!TIP]
>
>Adobe recommande de créer une [sauvegarde](../storage/snapshots.md) de l’environnement avant les déploiements.

Vous pouvez également activer [Suivi des déploiements avec New Relic](../monitor/track-deployments.md) pour surveiller les événements de déploiement et vous aider à analyser les performances entre les déploiements.

## Flux de déploiement de démarrage

Adobe recommande de créer une `staging` de la branche `master` pour prendre en charge au mieux le développement et le déploiement de votre plan de démarrage. Deux de vos quatre environnements actifs sont ensuite prêts : `master` pour la production et `staging` pour l’évaluation.

Pour plus d’informations sur le processus, voir [Démarrer le développement et le déploiement du workflow](../architecture/starter-develop-deploy-workflow.md).

## Flux de déploiement Pro

Pro est fourni avec un grand environnement d’intégration avec deux branches actives, une `master` branches Branche, Évaluation et Production. Lorsque vous créez votre projet, le code est prêt à se branche, à se développer et à effectuer des transmissions pour créer et déployer votre site. Bien que l’environnement d’intégration puisse comporter de nombreuses branches, l’évaluation et la production ne comportent qu’une seule branche pour chaque environnement.

Pour plus d’informations sur le processus, voir [Processus de développement et de déploiement Pro](../architecture/pro-develop-deploy-workflow.md).

## Déploiement du code vers l’évaluation

L’environnement d’évaluation fournit un environnement de quasi-production qui comprend une base de données, un serveur web et tous les services, y compris Fastly et New Relic. Vous pouvez entièrement effectuer des transmissions de type push, fusion et déploiement via le [[!DNL Cloud Console]](../project/overview.md) ou [Commandes de l’interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md) par le biais d’une application terminal.

### Déployez du code avec le [!DNL Cloud Console]

La variable [!DNL Cloud Console] fournit des fonctionnalités pour créer, gérer et déployer du code dans les environnements d’intégration, d’évaluation et de production pour les plans Starter et Pro.

**Pour les projets Pro, déployez la branche d’intégration vers l’évaluation.**:

1. [Connexion](https://accounts.magento.cloud) à votre projet.
1. Sélectionnez la variable `integration` branche.
1. Sélectionnez la variable **Fusion** pour effectuer un déploiement vers l’évaluation.

   ![Fusion](../../assets/button-merge.png){width="150"}

1. Compléter tout [test](../test/staging-and-production.md) dans l’environnement d’évaluation.
1. Lorsque l’évaluation est prête, sélectionnez la variable **Fusion** pour effectuer un déploiement vers Production.

**Pour commencer, déployez la branche de développement vers l’évaluation.**:

1. [Connexion](https://accounts.magento.cloud) à votre projet.
1. Sélectionnez la branche de code préparée.
1. Sélectionnez la variable **Fusion** pour effectuer un déploiement vers l’évaluation.

   ![Fusion](../../assets/button-merge.png){width="150"}

1. Compléter tout [test](../test/staging-and-production.md) dans l’environnement d’évaluation.
1. Lorsque l’évaluation est prête, sélectionnez la variable **Fusion** option de déploiement en production (`master`).

### Déploiement du code avec la ligne de commande

L’interface de ligne de commande de Cloud fournit des commandes pour déployer le code. Vous avez besoin d’un accès SSH et Git à votre projet.

#### Étape 1 : déploiement et test de l’environnement d’intégration

1. Après vous être connecté au projet, vérifiez l’environnement d’intégration :

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchronisez votre environnement d’intégration local avec l’environnement distant :

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Créez un instantané de l’environnement en tant que sauvegarde :

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Mettez à jour le code dans votre branche locale si nécessaire.

1. Ajoutez, validez et envoyez les modifications à l’environnement.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Effectuez les tests du site.

#### Étape 2 : fusionner les modifications dans l’évaluation et le déploiement

1. Consultez l’environnement d’évaluation :

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchronisez votre environnement d’évaluation local avec l’environnement distant :

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Créez un instantané de l’environnement en tant que sauvegarde :

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Fusionnez l’environnement d’intégration à l’environnement d’évaluation pour déployer :

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Effectuez les tests du site.

#### Étape 3 : déploiement en production

1. Extrayez, synchronisez et créez un instantané de votre environnement de production local.

1. Fusionnez l’environnement d’évaluation en production pour déployer :

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Effectuez les tests du site.

## Migration de fichiers statiques

[Fichiers statiques](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) sont stockées dans `mounts`. Il existe deux méthodes pour migrer des fichiers d’un emplacement de montage source, tel que votre environnement local, vers un emplacement de montage de destination. Les deux méthodes utilisent la méthode `rsync` , mais Adobe recommande d’utiliser la variable `magento-cloud` Interface en ligne de commande pour déplacer des fichiers entre l’environnement local et distant. Et Adobe recommande d’utiliser la variable `rsync` lors du déplacement de fichiers d’une source distante vers un autre emplacement distant.

### Migration de fichiers à l’aide de l’interface en ligne de commande

Vous pouvez utiliser la variable `mount:upload` et `mount:download` Commandes d’interface de ligne de commande pour migrer des fichiers entre l’environnement local et distant. Les deux commandes utilisent la méthode `rsync` , mais les commandes de l’interface de ligne de commande fournissent des options et des invites adaptées à Adobe Commerce dans l’environnement d’infrastructure cloud. Par exemple, si vous utilisez la commande simple sans option, l’interface de ligne de commande vous invite à sélectionner le montage ou le montage à télécharger ou à télécharger.

```bash
magento-cloud mount:download
```

Exemple de réponse :

```terminal
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**Pour charger des fichiers à partir d’un fichier local `pub/media/` dossier vers le dossier distant `pub/media/` dossier de l’environnement actuel**:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Exemple de réponse :

```terminal
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Utilisez la variable `--help` pour l’ `mount:upload` et `mount:download` pour afficher d’autres options. Par exemple, il existe une `--delete` pour supprimer les fichiers superflus lors de la migration.

### Migration des fichiers à l’aide de rsync

Vous pouvez également utiliser la variable `rsync` pour migrer des fichiers.

```bash
rsync -azvP <source> <destination>
```

Cette commande utilise les options suivantes :

- `a`-archive
- `z`-compresse les fichiers lors de la migration
- `v`-verbose
- `P`-progression partielle

Voir [rsync](https://linux.die.net/man/1/rsync) aide.

>[!NOTE]
>
>Pour transférer directement des médias d’environnements distants à distants, vous devez activer le transfert de l’agent SSH, voir [Conseils sur GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**Pour migrer directement des fichiers statiques d’environnements distants vers distants (approche rapide)**:

1. Utilisez SSH pour vous connecter à l’environnement source. N’utilisez pas la variable `magento-cloud` Interface de ligne de commande. En utilisant la variable `-A` est importante, car elle permet le transfert de la connexion de l’agent d’authentification.

   >[!TIP]
   >
   >Pour rechercher la variable **Accès SSH** dans votre [!DNL Cloud Console], sélectionnez l’environnement et cliquez sur **Accès au site**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Utilisez la variable `rsync` pour copier la commande `pub/media` de votre environnement source vers un autre environnement distant.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Connectez-vous à un autre environnement distant pour vérifier que les fichiers ont bien été migrés.

## Migration de la base de données

>[!WARNING]
>
>Les opérations d’import et d’export de base de données peuvent prendre du temps, ce qui peut avoir une incidence sur les performances et la disponibilité du site. Planifiez les opérations d’importation et d’exportation aux heures creuses afin d’éviter des performances ralenties ou des pannes sur les sites de production.

>[!BEGINSHADEBOX]

**Condition préalable requise :** Un vidage de base de données (voir l’étape 3) doit inclure les déclencheurs de base de données. Pour les jeter, vérifiez que vous disposez de la variable [Privilège TRIGGER](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger).

>[!IMPORTANT]
>
>La base de données de l’environnement d’intégration est strictement destinée aux tests de développement et peut inclure des données que vous ne souhaitez pas migrer vers les environnements d’évaluation et de production.

Pour les déploiements d’intégration continue, Adobe **ne recommande pas** migration des données de l’intégration vers l’évaluation et la production. Vous pouvez transmettre des données de test ou remplacer des données importantes. Toutes les configurations essentielles sont transmises à l’aide de la variable [fichier de configuration](../store/store-settings.md) et `setup:upgrade` pendant la création et le déploiement.

>[!ENDSHADEBOX]

Adobe **recommande** migration des données de la production vers l’évaluation afin de tester entièrement votre site et de le stocker dans un environnement de quasi-production avec tous les services et paramètres.

>[!NOTE]
>
>Pour transférer directement des médias d’environnements distants à distants, vous devez activer le transfert de l’agent SSH, voir [Conseils sur GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Sauvegarde de la base

Il est recommandé de créer une sauvegarde de la base de données. La procédure suivante utilise les conseils de [Sauvegarde de la base](../storage/database-dump.md).

**Pour vider la base**:

1. [Utilisez SSH pour vous connecter à l’environnement distant](../development/secure-connections.md#use-an-ssh-command) qui contient la base de données à copier.

1. Listez les relations de l&#39;environnement et notez les informations de connexion à la base de données.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   Pour les environnements d’évaluation et de production Pro, le nom de la base de données figure dans la variable `MAGENTO_CLOUD_RELATIONSHIPS` (généralement identique au nom et au nom d’utilisateur de l’application).

1. Créez une sauvegarde de la base. Pour choisir un répertoire cible pour le vidage DB, utilisez la méthode `--dump-directory` .

   Pour les environnements de démarrage et les environnements d’intégration Pro, utilisez `main` comme nom de la base de données :

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Options de vidage :
   - `--dump-directory=<dir>`: choisissez un répertoire cible pour le vidage de la base de données.
   - `--remove-definers`—Supprimer les instructions DEFINER du vidage de base de données

1. Bien que la méthode CEE-Outils soit préférée, une autre méthode consiste à créer un fichier de vidage de base de données à l’aide de MySQL natif au format GZIP.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Si vous avez configuré l’authentification à deux facteurs sur l’environnement cible, il est préférable d’exclure les tables 2FA associées afin d’éviter de le reconfigurer après la migration de la base de données :

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Type `logout` pour arrêter la connexion SSH.

### Déposer et recréer la base de données

Lors de l&#39;import de données, vous devez déposer et créer une base de données.

**Déposer et recréer la base de données**:

1. Créer une [tunnel SSH](../development/secure-connections.md#ssh-tunneling) à l’environnement distant.

1. Connexion au service de base de données.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. À l’emplacement `MariaDB [main]>` , déposez la base de données.

   Pour l’intégration de Starter et Pro :

   ```shell
   drop database main;
   ```

   Pour la production :

   ```shell
   drop database <cluster-id>;
   ```

   Pour l’évaluation :

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Recréez la base de données.

   Pour l’intégration de Starter et Pro :

   ```shell
   create database main;
   ```

   Importation pour production :

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Importation pour l’évaluation :

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```
