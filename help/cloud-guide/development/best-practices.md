---
title: Bonnes pratiques relatives à la mise à niveau de votre projet
description: Consultez la liste des bonnes pratiques pour mettre à niveau vos fichiers de projet.
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Bonnes pratiques relatives à la mise à niveau de votre projet

Suivez les bonnes pratiques relatives aux versions et au déploiement, et utilisez le workflow [Mises à niveau et correctifs](../development/commerce-version.md) pour mettre à niveau votre application. Suivez les instructions suivantes pour planifier votre mise à niveau et votre travail après la mise à niveau :

- **Sauvegardez votre projet** : avant de mettre à niveau Adobe Commerce et toutes les extensions tierces ou personnalisées, sauvegardez la base de données dans les environnements d’intégration, d’évaluation et de production. Voir [Sauvegarde de la base de données](../development/commerce-version.md#project-backup).

- **Vérifiez les problèmes de compatibilité**-

   - Assurez-vous que tous les thèmes personnalisés sont compatibles avec la nouvelle version d’Adobe Commerce.

   - Après la mise à niveau d’extensions tierces et personnalisées, utilisez la commande `magento-cloud local:build` pour valider les dépendances du compositeur avant le déploiement.

   - Consultez les notes de mise à jour et la documentation sur l’extension Adobe Commerce pour vous assurer que vous avez mis en oeuvre les solutions ou modifications de configuration requises pour résoudre les problèmes fonctionnels connus et les bogues liés à la mise à niveau de la version et des extensions d’Adobe Commerce.

   - Assurez-vous que les versions de service installées sont compatibles avec la nouvelle version d’Adobe Commerce et mettez à niveau les services si nécessaire. Voir [Services](../services/services-yaml.md).

   - Testez votre base de données pour résoudre les problèmes liés aux mises à jour de la version et des extensions d’Adobe Commerce.

   - Effectuez les mises à jour requises des paramètres spécifiques à l’environnement avant de procéder au déploiement dans l’environnement distant.

   - Assurez-vous que la version du service de recherche est compatible avec la version du client PHP. Voir [Configuration de l’Elasticsearch](../services/elasticsearch.md) ou [Configuration d’OpenSearch](../services/opensearch.md).

- **Vérifiez la connectivité de la base de données et le stockage disponible dans les environnements distants**-

   - Utilisez SSH pour vous connecter au serveur distant et vérifier la connexion à la base de données MySQL. Voir [Connexion à la base de données](../services/mysql.md#connect-to-the-database).

   - Vérifiez le stockage disponible dans l’environnement distant. Utilisez la commande `disk free` pour afficher et gérer l’espace disque disponible dans vos environnements cloud. Voir [Gestion de l’espace disque](../storage/manage-disk-space.md).

      - Vérifiez la taille de la base de données mise à niveau et assurez-vous que le fichier `services.yaml` a suffisamment d’espace disque alloué.

      - Libérez de l’espace disque : effacez le cache et nettoyez les répertoires `/log` et `/tmp` avant de procéder au déploiement.

- **Planifiez et effectuez une mise à niveau réussie sur les environnements locaux et d’intégration, avant le déploiement vers l’évaluation** - Après la mise à niveau, testez votre déploiement et résolvez les problèmes.

- **Fusionner le code vers l’évaluation, puis vers la production** - Testez et résolvez tous les problèmes dans l’environnement d’évaluation avant d’envoyer les modifications vers l’environnement de production.

- **Tâches de mise à niveau vers Post**-

   - Utilisez SSH pour vous connecter au serveur distant et vérifiez les éléments suivants :

      - Vérifiez l’état de l’indexeur et réindexez-le selon vos besoins. Voir [Gestion des indexeurs](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) dans le _Guide de configuration_.

      - Vérifiez les journaux `cron` et la table `cron_schedule` de la base de données Adobe Commerce pour vérifier l’état cron et réexécuter les tâches cron si nécessaire.
Voir [Journalisation](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) dans le _Guide de configuration_.

   - Effectuez les tests d’acceptation utilisateur après la mise à niveau UAT dans les environnements d’évaluation et de production et corrigez les problèmes liés aux mises à niveau d’extension tierces et personnalisées.
