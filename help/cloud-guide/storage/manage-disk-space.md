---
title: Gestion de l’espace disque
description: Découvrez comment gérer l’espace disque à l’aide de l’interface de ligne de commande.
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 8b40397796ee865aefbf8a7948cc9a3aceb1d35c
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Gestion de l’espace disque

Vous trouverez la capacité de stockage totale de votre projet Cloud dans votre Adobe Commerce sur le contrat d’infrastructure cloud et sur votre [page de compte](https://accounts.magento.cloud/user). Chaque carte de projet de votre compte indique le nombre de _environnements_, la variable _stockage_ capacité en Go et nombre _utilisateurs_. Vous pouvez également utiliser la commande Cloud suivante :

```bash
magento-cloud subscription:info | grep storage
```

Exemple de réponse :

```terminal
| storage              | 51200
```

Lorsqu’un environnement de production ou d’évaluation Pro atteint ou dépasse 95 % de la capacité de stockage, l’outil de surveillance de l’infrastructure cloud déclenche une alerte de support vous informant d’une augmentation automatique de la capacité de stockage.

Exemple de notification :

>[!BEGINSHADEBOX]

_&quot;Notre surveillance a détecté que le stockage des fichiers sur votre grappe (projet-id-environment) est presque complet. L’utilisation du disque atteint actuellement des niveaux d’utilisation critiques avec moins d’1 GiB restant. Le volume de stockage partagé est actuellement mis à niveau de 60 GiB à 70 GiB pour que vos services restent opérationnels. Jetez un oeil à l’utilisation des fichiers de production et d’évaluation pour voir si vous pouvez libérer de l’espace.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>Il est recommandé de surveiller régulièrement votre capacité de stockage et de l’entretenir bien en dessous de 90 % afin d’éviter ces augmentations automatiques. Une fois allouée, l’augmentation de stockage pour l’évaluation et la production Pro ne peut pas être annulée.

## Vérification de l’environnement d’intégration

Vous pouvez vérifier l’utilisation de l’espace disque pour votre environnement d’intégration à l’aide de la variable `magento-cloud` Interface de ligne de commande.

**Pour vérifier l’utilisation approximative de l’espace disque**:

```bash
magento-cloud db:size
```

Exemple de réponse :

```terminal
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Toutes les montures partagent un disque. Vous pouvez vérifier l’utilisation de l’espace disque pour les montages à l’aide du `magento-cloud` Interface de ligne de commande.

**Pour vérifier l’utilisation approximative de l’espace disque pour les montages**:

```bash
magento-cloud mount:size
```

Exemple de réponse :

```terminal
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Vérifier les clusters dédiés

Pour les environnements d’évaluation et de production Pro, vous pouvez vérifier l’utilisation de l’espace disque dans chaque environnement à l’aide de la variable `disk free` , qui indique l’espace disque utilisé par le système de fichiers. Vous devez utiliser SSH pour vous connecter à un environnement distant.

```bash
df -h
```

La variable `-h` affiche le rapport dans un format lisible par l’utilisateur (Ko, Mo ou Go).

Dans l’exemple de réponse suivant, la variable `/mnt/shared` le montage affiche l’espace disque pour le média et `/data/mysql/` le montage affiche l’espace disque de la base de données :

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

Vous pouvez limiter la réponse en spécifiant un répertoire. Par exemple :

```bash
df -h var/
```

Exemple de réponse :

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Allouer de l’espace disque

Deux [fichiers de configuration](../environment/overview.md) contrôler l’allocation de l’espace disque dans les environnements cloud : `.magento.app.yaml` et le fichier `.magento/services.yaml` fichier . Chaque fichier contient le `disk` qui définit la valeur de taille du disque en Mo pour la configuration correspondante. Vous pouvez uniquement modifier l’allocation de l’espace disque sur les environnements Pro Integration et Starter.

>[!IMPORTANT]
>
>Pour les environnements de production et intermédiaires, vous devez [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour modifier l’allocation de l’espace disque. Une augmentation de la taille des environnements de production et d’évaluation peut uniquement survenir à certains intervalles. Par conséquent, selon l’utilisation actuelle de l’espace disque, la prise en charge peut recommander une augmentation de l’allocation de l’espace disque d’au moins 10 Go. Une fois allouée, l’augmentation de stockage pour l’évaluation et la production Pro ne peut pas être annulée. Le stockage ne peut pas être réalloué ni redistribué entre les ressources. Pour ajouter plus d’espace de stockage de fichiers, réduisez l’espace disque alloué à MySQL.

### Espace disque de l’application

La variable `.magento.app.yaml` contrôle le fichier [espace disque persistant](../application/properties.md#disk) disponible pour l’application.

**Pour augmenter l’espace disque de votre application**:

1. Dans votre environnement de développement local, ouvrez le `.magento.app.yaml` fichier de configuration.

1. Définissez une nouvelle valeur pour la variable `disk` (en Mo).

   ```yaml
   disk: <value-mb>
   ```

1. Enregistrez les modifications dans le fichier.

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   Les modifications prennent effet une fois que vous avez envoyé le fichier YAML mis à jour vers l’environnement distant.

### Espace disque du service

La variable `.magento/services.yaml` contrôle l’espace disque disponible pour chaque service, tel que MySQL et Redis.

**Pour augmenter l’espace disque d’un service**:

1. Dans votre environnement de développement local, ouvrez le `.magento/services.yaml` fichier de configuration.

1. Ajoutez ou recherchez un service dans le fichier . Voir [en savoir plus sur la configuration des services](../services/services-yaml.md).

1. Définissez une nouvelle valeur pour la propriété de disque (en Mo).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Enregistrez les modifications dans le fichier.

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   Les modifications prennent effet une fois que vous avez envoyé le fichier YAML mis à jour vers l’environnement distant.

## Surveillance de l’espace disque

Dans les environnements Pro Production, vous pouvez surveiller l’espace disque et d’autres indicateurs de performances à l’aide de la stratégie d’alerte Gestion des alertes pour Adobe Commerce pour New Relic. Pour plus d’informations, voir [Surveillance des performances à l’aide des alertes gérées](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Pour plus d’informations, voir [Bonnes pratiques pour résoudre les problèmes de performances de la base de données](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## Aucun espace à gauche

Le cache de génération peut s’agrandir au fil du temps. Si vous recevez un avertissement indiquant que la variable `No space left on device`, essayez d’effacer le cache de génération et de redéployer :

```bash
magento-cloud project:clear-build-cache
```
