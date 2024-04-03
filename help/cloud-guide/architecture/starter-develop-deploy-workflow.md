---
title: Workflow du projet de démarrage
description: Découvrez comment utiliser les workflows de développement et de déploiement de Starter.
feature: Cloud, Paas
exl-id: f334047a-1e0d-45c7-bf96-5c2964741951
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Workflow du projet de démarrage

Adobe Commerce sur l’infrastructure cloud comprend un seul référentiel Git avec une `master` branche pour l’environnement de production qui peut être branché afin de créer un environnement d’évaluation et plusieurs environnements d’intégration pour le travail de test et de développement. Vous pouvez avoir jusqu’à quatre environnements actifs, dont un `master` environnement de votre serveur de production. Voir [Architecture de démarrage](starter-architecture.md) pour une vue d’ensemble.

Pour vos environnements, suivez le [!UICONTROL Development > Staging > Production] pour développer et déployer votre site.

- **Environnement de production (site actif)**: fournit un environnement de production complet avec tous les services créés et déployés à partir du code sur la `master` branche.
- **Environnement d’évaluation**: fournit un environnement d’évaluation complet qui correspond à l’environnement de production avec tous les services créés et déployés à partir d’un `staging` branche que vous créez en clonant à partir de `master`.
- **Environnements d’intégration**: fournit jusqu’à deux environnements de développement actifs que vous créez à partir du `staging` branche. La variable `integration` ne prend pas en charge les services tiers tels que Fastly et New Relic.

Pour vos branches, vous pouvez suivre n’importe quelle méthodologie de développement. Par exemple, vous pouvez suivre une méthodologie Agile telle que le scrum pour créer des branches pour chaque sprint.

À partir de chaque sprint, vous pouvez créer des branches pour chaque article client. Toutes les histoires deviennent vérifiables. Vous pouvez constamment fusionner vers la branche sprint et valider cette branche de manière continue. Lorsque le sprint se termine, vous pouvez fusionner la branche du sprint en `master` pour déployer toutes les modifications sprint en production sans avoir à gérer un goulot d’étranglement des tests.

## Workflow de développement

Le développement et le déploiement sur les plans de démarrage commencent par votre projet initial. Vous créez votre projet avec le &quot;site vierge&quot;, qui est un référentiel de code de modèle d’infrastructure cloud Adobe Commerce avec un magasin entièrement préparé. Cela crée une `master` branche avec une copie du code de votre environnement de production.

Le workflow de développement comprend les éléments suivants :

- [Clonage et branche](#clone-and-branch) de la `master` pour créer `staging` et branches de développement
- [Développer le code](#develop-code) et installer des extensions localement dans une branche de développement, y compris [!DNL Composer] mises à jour
- [Configurer](#configure-store) paramètres de magasin et d’extension
- [Générer la configuration](#generate-configuration-management-files) fichiers de gestion
- [Code push](#push-code-and-test) et de la configuration à créer et déployer sur le `staging` et `production` environnements

![Workflow de développement et de déploiement](../../assets/starter/workflow.png)

Vous avez également quelques étapes facultatives pour vous aider à développer et tester votre code et vos données de magasin :

- [Installer des exemples de données](#optional-install-sample-data) à votre boutique
- [Extraire les données de l’entrepôt de production](#optional-pull-production-data) jusqu’aux environnements

Ce processus suppose que vous avez configuré votre [espace de travail du développeur local](../development/overview.md).

### Clonage et branche

Pour un nouveau projet de formule de démarrage, un `master` a été clonée à partir d’Adobe Commerce sur le référentiel Git de l’infrastructure cloud. Pour commencer à utiliser un embranchement et du code, clonez le `master` branche vers votre environnement local.

Le format de la commande de clonage Git est le suivant :

```bash
git fetch origin
```

```bash
git pull origin <environment-ID>
```

La première fois que vous commencez à travailler dans des branches pour votre projet de démarrage, créez un `staging` branche. Cette opération crée une branche de code correspondant à l’événement `master` qui se déploie sur un environnement d’évaluation pour tester la configuration et les modifications de code avant le déploiement sur l’environnement de production.

Créez ensuite des branches à partir de `staging` pour développer du code, ajouter des extensions et configurer des intégrations tierces. Chaque fois que vous développez du code personnalisé, ajoutez des extensions, intégrez à un service tiers, travaillez dans une branche de développement créée à partir de la fonction `staging` branche. Quatre environnements d’intégration actifs sont disponibles. Lorsque vous poussez une branche active, l’un de ces environnements d’intégration déploie automatiquement votre code à tester.

Le format de la commande de branche Git est le suivant :

```bash
git checkout <branch-name>
```

Format de l’interface de ligne de commande de Cloud `branch` est la commande suivante :

```bash
magento-cloud environment:branch <environment-name> <parent-environment-ID>
```

![Branche à partir du Principal](../../assets/starter/branching.png)

### Développer le code

En utilisant la branche de base d’Adobe Commerce sur le code d’infrastructure cloud, vous pouvez commencer à installer des extensions, développer du code personnalisé, ajouter des thèmes, etc.

Utilisez une stratégie d’embranchement avec votre travail de développement. L’utilisation d’une branche pour effectuer toutes vos tâches en même temps peut rendre les tests difficiles. Par exemple, vous pouvez suivre les méthodologies d’intégration continue et de sprint pour fonctionner :

- Ajouter quelques extensions et les configurer avec votre première branche
- Poussez ce code, testez-le et fusionnez-le dans Évaluation puis Production.
- Configurez entièrement vos services dans `services.yaml` et ajouter un thème
- Poussez ce code, testez-le et fusionnez-le dans Évaluation puis Production.
- Intégration à un service tiers
- Poussez ce code, testez-le et fusionnez-le dans Évaluation puis Production.

Jusqu’à ce que votre magasin soit entièrement créé, configuré et prêt à être lancé. Mais continuez à lire, il existe de nombreuses options pour votre configuration de magasin et de code.

>[!NOTE]
>
>N’effectuez pas encore de configuration dans votre poste de travail local.

![Code push local](../../assets/starter/push-code.png)

### Configurer le magasin

Lorsque vous êtes prêt à configurer votre magasin, envoyez tout votre code à la variable `integration` environnement. Configurez les paramètres du magasin à partir de l’administrateur pour l’environnement d’intégration, et non dans votre environnement local. Vous pouvez trouver l’URL en cliquant sur **Accès au site** dans le [!DNL Cloud Console]

Pour obtenir les meilleures informations sur les configurations, consultez la documentation d’Adobe Commerce et des extensions installées. Voici quelques liens et idées qui vous aident à démarrer :

- [Bonnes pratiques relatives à la configuration des magasins](../store/best-practices.md) pour connaître les bonnes pratiques spécifiques à cloud
- [Configuration de base](https://docs.magento.com/user-guide/configuration/configuration-basic.html) pour l’accès administrateur de magasin, le nom, les langues, les devises, la marque, les sites, les vues de magasin, etc.
- [Thème](https://docs.magento.com/user-guide/design/design-theme.html) pour votre apparence du site et des magasins, y compris les pages CSS et les mises en page
- [Configuration du système](https://docs.magento.com/user-guide/system/system.html) pour les rôles, outils, notifications et votre clé de chiffrement pour votre base de données
- Paramètres d’extension utilisant leur documentation

Au-delà des seuls paramètres de magasin, vous pouvez configurer davantage plusieurs sites et magasins, des services configurés, etc. Voir [Configuration de votre boutique](../store/overview.md).

### Génération des fichiers de gestion de configuration

Si vous connaissez Adobe Commerce, vous pouvez vous demander comment obtenir vos paramètres de configuration de votre base de données en développement vers les environnements d’évaluation et de production. Auparavant, vous deviez copier tous vos paramètres de configuration sur papier ou dans un fichier, puis les appliquer manuellement à d’autres environnements. Ou vous avez peut-être vidé votre base de données et transféré ces données vers un autre environnement.

Adobe Commerce sur l’infrastructure cloud fournit un ensemble de deux [Gestion des configurations](../store/store-settings.md) Commandes qui exportent les paramètres de configuration de votre environnement dans un fichier. Ces commandes ne sont disponibles que pour **Adobe Commerce sur l’infrastructure cloud 2.2 et versions ultérieures**.

- `php .vendor/bin/ece-tools config:dump`: exporte uniquement les paramètres de configuration que vous avez saisis ou modifiés à partir des paramètres par défaut dans un fichier de configuration. _Recommandé_.
- `php bin/magento app:config:dump`: exporte chaque paramètre de configuration, y compris modifié et par défaut, dans un fichier de configuration.

Le fichier généré est `app/etc/config.php`.

Générez le fichier dans l’environnement d’intégration dans lequel vous avez configuré Adobe Commerce. Suivez le processus de génération du fichier, d’ajout à votre branche et de déploiement.

**Remarques importantes** sur Configuration Management :

- Tout paramètre de configuration inclus dans le fichier généré à partir du `app:config:dump` est verrouillée de la modification ou de la lecture seule dans l’environnement déployé. C’est l’une des raisons pour lesquelles Adobe recommande d’utiliser le `.vendor/bin/ece-tools config:dump` .

  Par exemple, vous installez un module pour Fastly dans votre environnement de développement. Vous ne pouvez configurer ce module que dans l’environnement d’évaluation et de production. En utilisant la variable `.vendor/bin/ece-tools config:dump` permet de conserver ces champs par défaut modifiables lorsque vous déployez vos modifications de développement dans l’environnement d’évaluation et de production.

- Le fichier généré peut être long en fonction de la taille de votre déploiement. La variable `.vendor/bin/ece-tools config:dump` génère un fichier plus petit que celui généré par la commande `app:config:dump` .

Si vous utilisez Adobe Commerce version 2.2 ou ultérieure, les commandes de gestion de la configuration offrent une fonctionnalité supplémentaire pour protéger les données sensibles, telles que les informations d’identification sandbox pour un module PayPal. Pendant le processus d’exportation, toutes les valeurs contenant des données sensibles sont exportées dans un fichier de configuration distinct.`env.php` dans le `app/etc/` répertoire . Ce fichier reste dans votre environnement local et n’est pas copié lorsque vous poussez votre code vers une autre branche. Vous pouvez également créer des variables d’environnement avec des commandes d’interface de ligne de commande dans toutes les versions d’infrastructure cloud d’Adobe Commerce.

![Génération de variables d’environnement](../../assets/starter/env-variables.png)

Voir [Gestion des configurations](../store/store-settings.md).

### Code push et test

À ce stade, vous devez disposer d’une branche de code développée avec un fichier de configuration (`config.local.php` ou `config.php`) prêt à être testé.

Chaque fois que vous poussez du code depuis votre environnement local, une série de scripts de création et de déploiement s’exécute. Ces scripts génèrent un nouveau code et le déploient dans l’environnement distant. Par exemple, si vous poussez une branche de développement de votre environnement local vers la branche distante, un environnement correspondant met à jour les services, le code et le contenu statique.

Vous pouvez accéder directement à cet environnement à l’aide d’une URL de magasin, d’une URL d’administration et d’un SSH. Ces environnements incluent un serveur web, une base de données et des services configurés. Une fois prêt, vous pouvez commencer le déploiement et le test dans l’environnement d’évaluation.

Pour plus d’informations, voir [Workflow de déploiement](#deployment-workflow).

### Facultatif : installation de données d’exemple

Si vous avez besoin de données d’exemple lors du développement de votre magasin, vous pouvez installer des données d’exemple. Ces données simulent un magasin actif, y compris les clients, les produits et d’autres données. Ces exemples de données fonctionnent mieux avec une Adobe Commerce &quot;site vierge&quot; sur l’installation d’un modèle d’infrastructure cloud lors de la création de votre projet. Il est recommandé de supprimer les exemples de données avant la mise en ligne. Voir [Installer des exemples de données facultatifs](../test/sample-data.md).

![Installer des exemples de données facultatifs](../../assets/starter/sample-data.png)

### Facultatif : extraction des données de production

Ajoutez tous vos produits, catalogues, contenu du site, etc., directement à la variable `production` environnement. En ajoutant ces données à l’environnement de production, vous pouvez fournir à vos clients des prix, des coupons, des stocks mis à jour, des annonces de ventes, des informations sur les offres futures, etc. Ces données n’incluent pas les configurations d’extension que vous configurez dans votre branche de développement locale.

Lorsque vous développez des fonctionnalités, ajoutez des extensions et des thèmes de conception, il est utile d’avoir de vraies données à utiliser. À tout moment, vous pouvez [créer un vidage de base de données](../storage/database-dump.md) de l’environnement de production et placez-le dans vos environnements d’évaluation et d’intégration, si nécessaire.

Pour aider à exporter des données de production en tant que données de test à utiliser dans les environnements d’évaluation et d’intégration :

- [Exécution des utilitaires de support](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) Commandes d’interface de ligne de commande (recommandées) lors de l’exportation d’une sauvegarde protégée des données client et du stockage à l’aide de votre clé de chiffrement Adobe Commerce

- [Collecte de données](https://docs.magento.com/user-guide/system/support-data-collector.html) outil de génération et d&#39;export de données

Pour migrer ces données, voir [Migration et déploiement de fichiers et de données statiques](../deploy/staging-production.md#migrate-static-files).

![Extraction et assainissement des données de production](../../assets/starter/data-code-process.png)

>[!NOTE]
>
>Avant de transférer les données vers un autre environnement, vous devez envisager d’assainir vos données. Vous disposez de plusieurs options, dont [utilisation des utilitaires de support](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) ou développer un script pour analyser les données client.

>[!WARNING]
>
>Ne poussez pas une base de données d’un environnement d’intégration ou d’évaluation vers un environnement de production. Si vous le faites, les données de l’environnement d’intégration ou d’évaluation remplacent vos données de production en direct, notamment les ventes, les commandes, les nouveaux clients et les clients mis à jour, etc.

## Workflow de déploiement

Comme indiqué dans les informations d’architecture, Adobe Commerce sur l’infrastructure cloud est piloté par Git. Le déploiement d’Adobe Commerce sur l’infrastructure cloud fait partie de vos processus push Git pour les branches.

Lorsque vous poussez du code embranché de votre environnement local vers la branche distante, une série de scripts de création et de déploiement commencent.

Création de scripts :

- Le site de l’environnement cible continue de fonctionner pendant une génération

- Vérifier et exécuter Adobe Commerce sur les correctifs et correctifs de l’infrastructure cloud

- Compilation de votre code à l’aide d’un journal de création et de déploiement

- Recherchez Configuration Management si le déploiement de contenu statique survient au cours de cette phase.

- Créer ou utiliser une limace de code inchangé pour un processus plus rapide

- Configuration de tous les services et applications principaux

Déployer des scripts :

- Place votre site dans l’environnement cible en mode de maintenance

- Déploiement du contenu statique s’il n’est pas terminé pendant la génération

- Installation ou mise à jour d’Adobe Commerce sur l’infrastructure cloud

- Configuration du routage pour le trafic

Une fois l’opération terminée, votre boutique revient en ligne, en ligne, avec l’ensemble du code et des configurations mis à jour.

Voir [Processus de déploiement](../deploy/process.md).

### Push to Staging and test

Envoyez toujours votre code par itérations au `staging` environnement pour des tests complets. La première fois que vous utilisez cet environnement, vous devez configurer quelques services, dont [Fastly](/help/cloud-guide/cdn/fastly.md) et [New Relic](../monitor/new-relic-service.md). En outre, configurez les passerelles de paiement, l’expédition, les notifications et d’autres services essentiels avec sandbox ou testez les informations d’identification.

L’évaluation est un environnement de pré-production qui fournit tous les services et paramètres aussi proches que possible de la production. Testez minutieusement chaque service, vérifiez vos outils de test de performance, effectuez des tests UAT en tant qu’administrateur et en tant que client, jusqu’à ce que votre magasin soit prêt pour la production.

Voir [Déployer votre boutique](../deploy/staging-production.md).

### Push to Production

Lorsque vous appuyez sur la variable `master` branche, vous effectuez un envoi vers la balise `production` environnement. Complétez les activités de configuration et de test dans l’environnement de production comme vous l’avez fait dans l’environnement d’évaluation avec une différence importante. Dans l’environnement de production, utilisez les informations d’identification en direct pour la configuration et le test. Au moment du lancement de votre site, les clients peuvent effectuer des achats et les administrateurs peuvent gérer la boutique en ligne.

Voir [Déployer votre boutique](../deploy/staging-production.md).

### Lancement du site

Il existe une procédure claire pour passer en ligne avec votre site. Une fois ces étapes terminées, votre boutique peut immédiatement proposer des produits sur votre thème personnalisé à vendre.

Voir [Lancement du site](../launch/overview.md).

## Intégration continue

En suivant vos méthodologies d’embranchement et de développement, vous pouvez facilement développer de nouvelles fonctionnalités, configurer des modifications et ajouter des extensions pour développer et déployer en continu des mises à jour.

Tous les environnements d’infrastructure cloud prennent en charge l’intégration continue pour les mises à jour constantes. Ce workflow prend en charge les versions plusieurs fois par jour ou selon un calendrier défini en fonction des besoins de votre entreprise.

- Créer des branches de développement avec les fonctions et modifications futures

- Testez le code de votre `integration` environnement

- Déploiement et test dans `staging` environnement

- Déployez sur le `production` environnement
