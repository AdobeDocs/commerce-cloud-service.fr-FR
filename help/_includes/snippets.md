---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---
# Fragments de code cloud

## Avertissement Elasticsearch {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 et versions ultérieures ne sont pas pris en charge pour Adobe Commerce sur l’infrastructure cloud. Les versions 2.3.7-p3, 2.4.3-p2 et 2.4.4 et ultérieures d’Adobe Commerce prennent en charge le service OpenSearch. Les installations sur site continuent de prendre en charge les Elasticsearch.

## Intégration améliorée {#enhanced-integration-envs}

>[!NOTE]
>
>Les projets configurés avant le 5 juin 2020 comportaient plusieurs environnements d’intégration plus petits. Si vous avez besoin d’un environnement d’intégration plus grand pour le test et le développement, demandez une mise à niveau vers les environnements d’intégration améliorée. Pour plus d’informations, reportez-vous à l’article [Demande d’environnement d’intégration](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) du _Centre d’aide Adobe Commerce_.

## Options de fusion {#merge-options}

Par défaut, le processus de déploiement remplace tous les paramètres du fichier `env.php`. Cependant, vous pouvez choisir de fusionner une ou plusieurs valeurs pour une configuration de service sans remplacer toutes les valeurs.

Définissez l’option `_merge` sur l’une des options suivantes :

- `true`—**Fusionner** les valeurs de service configurées avec les valeurs de variable d’environnement.
- `false`—**Remplacer** les valeurs de service configurées par les valeurs de variable d’environnement.

## Référentiel privé {#private-repository}

>[!NOTE]
>
>Adobe recommande vivement d’utiliser un référentiel privé pour votre projet d’infrastructure cloud Adobe Commerce afin de protéger les informations propriétaires ou les travaux de développement, tels que les extensions et les configurations sensibles.

## Avertissement Pro Self Service {#pro-self-service-warning}

>[!WARNING]
>
>Certains **projets Pro** ont besoin d’un ticket de support pour mettre à jour la configuration de l’itinéraire dans le fichier `routes.yaml` et la configuration cron dans le fichier `.magento.app.yaml`. Adobe recommande de mettre à jour et de tester les fichiers de configuration YAML dans un environnement d’intégration, puis de déployer les modifications dans l’environnement d’évaluation. Si vos modifications ne sont pas appliquées aux sites d’évaluation après le redéploiement et qu’il n’y a aucun message d’erreur associé dans le journal, alors vous **devez** [ envoyer un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) qui décrit les tentatives de modifications de configuration. Incluez tous les fichiers de configuration YAML mis à jour dans le ticket.

## Prise en charge des services Pro {#pro-update-service}

>[!TIP]
>Pour les projets Pro, vous devez [envoyer un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour installer ou mettre à jour [services](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) dans les environnements `Staging` et `Production` uniquement.
>
>Indiquez les modifications de service nécessaires, incluez vos fichiers `.magento.app.yaml` et `services.yaml` mis à jour et indiquez la version PHP dans le ticket. Pour les modifications en libre-service apportées à la version PHP, aux extensions ou aux paramètres d’environnement, voir [Paramètres PHP](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) dans la _configuration de l’application_.
>
>Pour les modifications apportées à un environnement de production _live_ (**Pro uniquement**), vous devez fournir un préavis d’au moins 48 heures afin de permettre à l’équipe d’infrastructure Cloud de disposer de suffisamment de temps pour mobiliser des ressources et réaliser une mise à niveau sécurisée.

## Sauvegardes Pro {#pro-backups}

>[!TIP]
>
>Dans les environnements d’évaluation et de production Pro, vous devez [envoyer un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour récupérer une sauvegarde spécifique notant la date, l’heure et le fuseau horaire dans le ticket.
>
>Adobe ne restaure **pas** les environnements d’une sauvegarde automatique. Pour obtenir de l’aide sur le choix d’une méthode pour restaurer un instantané d’évaluation ou de production, reportez-vous à la section [Restaurer un instantané de base de données depuis l’évaluation ou la production](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) .

## Redéployer l’avertissement {#redeploy-warning}

>[!WARNING]
>
>Le processus de déploiement commence lorsque vous effectuez une fusion, une notification push ou une synchronisation de votre environnement, ou lorsque vous déclenchez un redéploiement manuel, pendant lequel l’application [!DNL Commerce] est en mode de maintenance. Pour un environnement de production, Adobe recommande d’effectuer ce travail aux heures creuses afin d’éviter les interruptions de service.

## Espace réservé de la route {#route-placeholder}

>[!NOTE]
>
>Les exemples de configuration d’itinéraire suivants utilisent des modèles d’itinéraire avec des espaces réservés. L’espace réservé `{default}` représente le domaine par défaut configuré pour votre site. Si votre projet comporte plusieurs domaines, utilisez l’espace réservé `{all}` pour configurer le routage pour le domaine par défaut et tous les alias. Voir [Configuration des itinéraires](/help/cloud-guide/routes/routes-yaml.md).

## minutage SCD {#scd-timing-warning}

>[!WARNING]
>
>Si vous rencontrez des problèmes avec des fichiers de contenu statiques dans votre application après le déploiement, tels que l’absence de fichiers de thème personnalisés, augmentez le temps d’exécution maximum prévu à 900 secondes ou plus.

## Déploiement basé sur des scénarios {#scenarios}

>[!NOTE]
>
>Avec [!DNL ECE-Tools] 2002.1.0 et versions ultérieures, vous pouvez utiliser la fonctionnalité de déploiement basée sur des scénarios pour personnaliser les processus de création, de déploiement et de post-déploiement pour votre projet d’infrastructure cloud Adobe Commerce. Voir [Déploiement basé sur les scénarios](/help/cloud-guide/deploy/scenario-based.md).

## Instruction du service {#service-instruction}

Suivez les instructions suivantes pour la configuration du service dans les environnements Pro Integration et les environnements Starter, y compris la branche `master`.

>[!NOTE]
>
>[Envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour modifier la configuration du service dans les environnements de production et d’évaluation.

## Changement de service {#service-change-tip}

>[!TIP]
>
>Après la configuration initiale du service, vous pouvez modifier la version logicielle d&#39;un service installé en mettant à jour les fichiers de configuration `services.yaml` et `.magento.app.yaml`. Voir [Modification de la version de service](/help/cloud-guide/services/services-yaml.md#change-service-version) pour obtenir des conseils sur la mise à niveau ou la mise à niveau d’un service.

## Astuce de déploiement {#stuck-deployment-tip}

>[!TIP]
>
>Pour obtenir de l’aide sur les déploiements bloqués, utilisez l’[outil de dépannage du déploiement Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) dans le _Centre d’aide de Commerce_.

## Mise à jour vers les outils ECE {#ece-tools-package}

>[!NOTE]
>
>Si vous utilisez une version d’Adobe Commerce sur l’infrastructure cloud qui ne contient pas le package `ece-tools`, vous devez effectuer une [mise à niveau unique](/help/cloud-guide/dev-tools/install-package.md) vers votre projet cloud pour supprimer les packages obsolètes. Si vous utilisez actuellement le package `ece-tools` et que vous devez le mettre à jour, reportez-vous à la section [Mise à jour du package EC-Tools](/help/cloud-guide/dev-tools/update-package.md).

## Conseil de mise à niveau {#upgrade-tip}

>[!TIP]
>
>Avant de commencer une mise à niveau ou un processus de correction, créez une branche active à partir de l’environnement d’intégration et extrayez la nouvelle branche vers votre poste de travail local. Le fait de dédier une branche à la mise à niveau ou au processus de correctif permet d’éviter toute interférence avec votre travail en cours.

<!-- Fastly-related snippets begin -->

## Connexion administrateur {#admin-login-step}

1. [Connectez-vous](/help/get-started/onboarding.md#access-your-admin-panel) à l’administrateur.

## Automatiser le déploiement de fragments de code VCL personnalisés {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>Au lieu de charger manuellement des fragments de code VCL personnalisés, vous pouvez ajouter des fragments de code dans le répertoire `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` de votre environnement. Les fragments de code de ce répertoire sont automatiquement chargés lorsque vous cliquez sur _charger VCL vers Fastly_ dans l’administrateur Commerce. Voir [Déploiement de fragments de code VCL personnalisés automatisé](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) dans la documentation Fastly CDN pour Magento 2.

<!-- Fastly-related snippets end -->
