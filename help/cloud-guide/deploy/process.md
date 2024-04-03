---
title: Processus de déploiement
description: Découvrez comment fonctionne le déploiement pour Adobe Commerce sur les projets d’infrastructure cloud.
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Processus de déploiement

Le processus de déploiement commence lorsque vous effectuez une fusion, une notification push ou une synchronisation de votre environnement, ou lorsque vous déclenchez un événement [redéploiement manuel](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). Le processus de déploiement prend du temps, mais il existe des moyens d’optimiser le déploiement qui dépendent du développement et du test ou de l’utilisation d’un site actif. En particulier, vous pouvez contrôler la variable [déploiement de contenu statique](static-content.md).

Le processus de déploiement comprend trois phases distinctes : création, déploiement et post-déploiement. Chaque phase effectue des actions spécifiques avec des ressources limitées :

## ![Phase de création](../../assets/status-build.png) Phase de création

La variable _build_ assemble les conteneurs pour les services définis dans les fichiers de configuration, installe les dépendances basées sur la variable `composer.lock` et exécute les hooks de génération définis dans la variable `.magento.app.yaml` fichier . Sans possibilité de se connecter à un service ou d&#39;accéder à la base de données, la phase de création dépend des ressources limitées à l&#39;environnement.

## ![Phase de déploiement](../../assets/status-deploy.png) Phase de déploiement

La variable _deploy_ place un blocage temporaire sur les requêtes entrantes et passe le site à [mode de maintenance](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). La phase de déploiement utilise les nouveaux conteneurs et, après le montage du système de fichiers, ouvre les connexions réseau, active les services définis dans la variable `relationships` de la `.magento.app.yaml` et exécute les hooks de déploiement définis dans la variable `.magento.app.yaml` fichier . Tout est parfait _lecture seule_, à l’exception des répertoires définis dans la variable `.magento.app.yaml` fichier . Par défaut, la variable [`mounts` property](../application/properties.md#mounts) inclut les répertoires suivants :

- `app/etc`: contient la variable `env.php` et `config.php` fichiers de configuration
- `pub/media`: contient toutes les données multimédias, telles que les produits ou les catégories.
- `pub/static`: contient des fichiers statiques générés.
- `var`—contient des fichiers temporaires créés lors de l’exécution

Tous les autres répertoires disposent d’autorisations en lecture seule. Le nouveau site devient actif à la fin de la phase de déploiement lorsqu’il passe hors du mode de maintenance et libère l’attente temporaire sur les requêtes entrantes.

Lors de la phase de déploiement, les copies de la variable `app/etc/config.php` et `app/etc/env.php` les fichiers de configuration de déploiement sont enregistrés avec l’extension BAK. Voir [Paramètres de magasin](../store/store-settings.md#restore-configuration-files) pour découvrir comment restaurer ces fichiers.

## ![Phase de post-déploiement](../../assets/status-post-deploy.png) Phase de post-déploiement

La variable _post-déploiement_ exécute la phase d’exécution des hooks de post-déploiement définis dans la variable `.magento.app.yaml` fichier . L’exécution d’une action sur cette phase peut avoir une incidence sur les performances du site. Vous pouvez toutefois utiliser la variable [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) pour renseigner le cache.

## ![Vérification de l’état](../../assets/status-verify.png) Vérification des configurations

Vous pouvez tester la configuration optimale pour l’état de votre projet en exécutant l’événement [Assistant dynamique](smart-wizards.md).

>[!NOTE]
>
>Avec `ece-tools` 2002.1.0 et versions ultérieures, vous pouvez utiliser la fonctionnalité de déploiement basée sur des scénarios pour personnaliser les processus de création, de déploiement et de post-déploiement pour votre projet d’infrastructure cloud Adobe Commerce. Voir [Déploiement basé sur des scénarios](scenario-based.md).
