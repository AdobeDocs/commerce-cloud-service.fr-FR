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

Le processus de déploiement commence lorsque vous effectuez une fusion, une notification push ou une synchronisation de votre environnement, ou lorsque vous déclenchez un [redéploiement manuel](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). Le processus de déploiement prend du temps, mais il existe des moyens d’optimiser le déploiement qui dépendent du développement et du test ou de l’utilisation d’un site actif. Plus particulièrement, vous pouvez contrôler le [déploiement de contenu statique](static-content.md).

Le processus de déploiement comprend trois phases distinctes : création, déploiement et post-déploiement. Chaque phase effectue des actions spécifiques avec des ressources limitées :

## ![Phase de création](../../assets/status-build.png) phase de création

La phase _build_ assemble les conteneurs pour les services définis dans les fichiers de configuration, installe les dépendances basées sur le fichier `composer.lock` et exécute les hooks de version définis dans le fichier `.magento.app.yaml`. Sans possibilité de se connecter à un service ou d&#39;accéder à la base de données, la phase de création dépend des ressources limitées à l&#39;environnement.

## ![Phase de déploiement](../../assets/status-deploy.png) Phase de déploiement

La phase _deploy_ place un blocage temporaire sur les requêtes entrantes et passe le site en [mode de maintenance](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). La phase de déploiement utilise les nouveaux conteneurs et, après le montage du système de fichiers, ouvre les connexions réseau, active les services définis dans la section `relationships` du fichier `.magento.app.yaml` et exécute les hooks de déploiement définis dans le fichier `.magento.app.yaml`. Tout est _lecture seule_, à l’exception des répertoires définis dans le fichier `.magento.app.yaml`. Par défaut, la propriété [`mounts`](../application/properties.md#mounts) comprend les répertoires suivants :

- `app/etc` : contient les fichiers de configuration `env.php` et `config.php`
- `pub/media` : contient toutes les données multimédias, telles que les produits ou les catégories
- `pub/static` : contient des fichiers statiques générés
- `var` : contient des fichiers temporaires créés lors de l’exécution

Tous les autres répertoires disposent d’autorisations en lecture seule. Le nouveau site devient actif à la fin de la phase de déploiement lorsqu’il passe hors du mode de maintenance et libère l’attente temporaire sur les requêtes entrantes.

Lors de la phase de déploiement, les copies des fichiers de configuration de déploiement `app/etc/config.php` et `app/etc/env.php` sont enregistrées avec l’extension BAK. Pour en savoir plus sur la restauration de ces fichiers, voir [Paramètres du magasin](../store/store-settings.md#restore-configuration-files) .

## ![Phase de déploiement Post](../../assets/status-post-deploy.png) Phase de déploiement Post

La phase _post-déploiement_ exécute les hooks de post-déploiement définis dans le fichier `.magento.app.yaml`. L’exécution d’une action sur cette phase peut affecter les performances du site. Vous pouvez toutefois utiliser la variable d’environnement [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) pour remplir le cache.

## ![Vérifier l’état](../../assets/status-verify.png) Vérifiez les configurations

Vous pouvez tester la configuration optimale pour l’état de votre projet en exécutant les [assistants intelligents](smart-wizards.md).

>[!NOTE]
>
>Avec `ece-tools` 2002.1.0 et versions ultérieures, vous pouvez utiliser la fonctionnalité de déploiement basée sur des scénarios pour personnaliser les processus de création, de déploiement et de post-déploiement pour votre projet d’infrastructure cloud Adobe Commerce. Voir [Déploiement basé sur les scénarios](scenario-based.md).
