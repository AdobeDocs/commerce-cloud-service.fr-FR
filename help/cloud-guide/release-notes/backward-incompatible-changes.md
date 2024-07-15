---
title: Modifications incompatibles avec l’arrière
description: Découvrez la rétrocompatibilité lors de la mise à niveau de projets Cloud existants.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Modifications incompatibles avec l’arrière

Les modifications rétrocompatibles peuvent nécessiter l’ajustement de la configuration et des processus cloud pour les projets cloud existants lorsque vous effectuez une mise à niveau vers la dernière version du package `ece-tools` ou d’autres modules Cloud Tools Suite pour Commerce.

## Modifications apportées au package `ece-tools`

Certaines fonctionnalités précédemment incluses dans le package `ece-tools` sont désormais fournies dans des packages distincts. Ces packages sont des dépendances de compositeur pour `ece-tools`, qui sont installées et mises à jour automatiquement lors de l’installation ou de la mise à jour d’outils de texte.

La nouvelle architecture ne doit pas affecter vos processus d’installation ou de mise à jour. Cependant, il se peut que vous deviez modifier la syntaxe des commandes et les processus lorsque vous travaillez avec votre Adobe Commerce sur un projet d’infrastructure cloud. Pour plus d’informations, consultez les informations de modification incompatibles en amont suivantes et les [ notes de mise à jour de la suite d’outils cloud ](cloud-tools-suite.md).

### Modifications des exigences de version du service

Nous avons modifié la version PHP minimale requise de 7.0.x à 7.1.x pour les projets cloud qui utilisent `ece-tools` v2002.1.0 et versions ultérieures. Si votre configuration d&#39;environnement spécifie PHP 7.0, mettez à jour la [configuration php](../application/php-settings.md) dans le fichier `.magento.app.yaml`.

>[!WARNING]
>
>En raison de la modification de la configuration requise pour PHP, `ece-tools` 2002.1.0 prend uniquement en charge Adobe Commerce sur les projets d’infrastructure cloud exécutant Adobe Commerce 2.1.15 ou une version ultérieure. Si votre projet utilise une version antérieure, vous devez [mettre à niveau](../development/commerce-version.md) avant de procéder à la mise à jour vers `ece-tools` 2002.1.0.

### Modifications de la configuration d’environnement

Le tableau suivant fournit des informations sur les variables d’environnement et d’autres fichiers de configuration d’environnement qui ont été supprimés ou obsolètes dans `ece-tools` v2002.1.0.

| Élément | Remplacement |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` variable | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` variable | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` variable | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` variable | Aucun. Désormais, la version crée toujours un lien symbolique vers le répertoire de contenu statique `pub/static`. |
| `build_options.ini` fichier | Utilisez le fichier [`.magento.env.yaml`](../application/configure-app-yaml.md) pour configurer les variables d’environnement afin de gérer les actions de création et de déploiement dans tous vos environnements.<p>Si vous créez un environnement Cloud qui comprend le fichier `build_options.ini`, la version échoue. |

### Modifications des commandes de l’interface de ligne de commande

Le tableau suivant récapitule les modifications apportées aux commandes de l’interface de ligne de commande dans la version 2002.1.0 de CEE-Outils, qui peuvent nécessiter la mise à jour des commandes ou des scripts.

| Commande | Remplacement |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

Dans les versions antérieures d&#39;outils ECE, vous pouvez utiliser les commandes `m2-ece-build` et `m2-ece-deploy` pour configurer les hooks de déploiement dans le fichier `.magento.app.yaml`. Lorsque vous effectuez une mise à jour vers la version 2002.1.0, vérifiez la configuration `hooks` du fichier `.magento.app.yaml` pour connaître les commandes obsolètes et remplacez-les si nécessaire.

## Modifications des correctifs du cloud

- **Supprimer les correctifs téléchargés** - Le package `magento/magento-cloud-patches` regroupe tous les correctifs disponibles sur la page [téléchargements de logiciels](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) et les applique automatiquement lorsque vous effectuez un déploiement sur le cloud. Pour éviter les conflits de correctifs après la mise à niveau vers la version 2002.1.0 ou ultérieure de CEE-Tools, supprimez tous les correctifs fournis par Adobe que vous avez téléchargés et ajoutés manuellement à votre projet.

- **Mise à jour de la commande appliquer les correctifs** - Nous avons déplacé la commande pour appliquer des correctifs du répertoire `vendor/bin/ece-tools` vers le répertoire `vendor/bin/ece-patches`. Si vous utilisez cette commande pour appliquer des correctifs manuellement, utilisez le nouveau chemin.

  > Application manuelle de correctifs

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Modifications apportées à Cloud Docker

- **La version minimale de PHP requise est désormais PHP 7.1**. Si votre hôte Cloud Docker pour Commerce exécute une version antérieure, effectuez une mise à niveau vers PHP v7.1 ou une version ultérieure.

- **Modifications de la commande Cloud Docker for Commerce**-

   - **Mise à jour de Cloud Docker pour les commandes Commerce pour les opérations de création Docker** - Nous avons déplacé les commandes Cloud Docker pour Commerce du répertoire `vendor/bin/ece-tools` vers le répertoire `vendor/bin/ece-docker`. Mettez à jour les scripts et les commandes pour utiliser le nouveau chemin d’accès.

     Après la mise à niveau vers `ece-tools` 2002.1.0, utilisez la commande suivante pour afficher les commandes `ece-docker` disponibles.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Mise à jour des commandes cloud docker-composer** - Nous avons renommé le chemin d’accès au fichier de commande de `./bin/docker` à `./bin/magento-docker`. Mettez à jour les scripts et les commandes pour utiliser le nouveau chemin d’accès.

   - **Le conteneur Cron n’est plus inclus dans la configuration Docker par défaut**-Maintenant, vous devez ajouter l’option `--with-cron` à la commande `ece-docker build:compose` pour inclure le conteneur Cron dans la configuration de l’environnement Docker. Voir [Gestion des tâches cron](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) dans le guide _Cloud Docker for Commerce_.

     Les scripts qui ont généré précédemment des conteneurs avec des tâches cron sont désormais dépourvus du conteneur cron.

   - **En utilisant des conteneurs temporaires** - Dans les versions précédentes, les conteneurs créés par les opérations de commande `bin/magento-docker` n’ont pas été supprimés, vous pouvez donc les utiliser pour d’autres opérations. Désormais, les commandes `magento-docker` suppriment tous les conteneurs qu’elles créent une fois la commande terminée.

     Si vous souhaitez conserver un conteneur créé par une opération docker-composer, utilisez la commande `docker-compose run` au lieu de la commande `bin/magento-docker`.

   - **Exécution des hooks de post-déploiement** - La commande `cloud-deploy` n’exécute plus les hooks de post-déploiement. Utilisez la nouvelle commande `cloud-post-deploy` pour exécuter les hooks de post-déploiement après le déploiement. Mettez à jour vos scripts pour ajouter la commande permettant d’exécuter les hooks de post-déploiement.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Si vous utilisez directement les commandes `docker-compose`, exécutez la commande `docker-compose run deploy cloud-post-deploy` après la commande deploy.

- **Actualisation de la base de données** : le conteneur de la base de données est désormais stocké dans le `magento-db` volume Docker persistant. Lorsque vous actualisez l’environnement Docker, la base de données n’est plus supprimée automatiquement. Si nécessaire, utilisez l’une des commandes suivantes pour la supprimer manuellement.

   - Supprimez le conteneur `magento-db` :

     ```bash
     docker volume rm magento-db
     ```

   - Supprimez tous les volumes associés lors de l’arrêt des conteneurs Docker :

     ```bash
     docker-compose down -v
     ```

- **Remplacer les paramètres de synchronisation des fichiers d’archive et de sauvegarde** : les fichiers d’archive et de sauvegarde avec les extensions suivantes ne sont plus synchronisés lors de l’utilisation de docker-sync ou de mutagen : SQL, GZ, ZIP et BZ2. Vous pouvez remplacer la synchronisation des fichiers par défaut pour ces types de fichiers en renommant le fichier pour qu’il se termine par une extension différente. Par exemple : `synchronize-me.zip-backup`
