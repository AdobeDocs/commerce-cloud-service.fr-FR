---
user-guide-title: Guide de Commerce sur les infrastructures cloud
user-guide-description: Découvrez comment gérer l’application Adobe Commerce sur l’infrastructure cloud.
product: magento
feature: Cloud
source-git-commit: 5f00b20e599b7ba26e483a238d05d99daf1dd1b8
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 7%

---


# Commerce sur l’infrastructure cloud {#user-guide}

+ [Commerce](overview.md)
+ Architecture {#architecture}
   + [infrastructure cloud](architecture/cloud-architecture.md)
   + [Sécurité](architecture/security.md)
   + [Pile de technologie](architecture/tech-stack.md)
   + [Architecture de démarrage](architecture/starter-architecture.md)
   + [Workflow de démarrage](architecture/starter-develop-deploy-workflow.md)
   + [Architecture Pro](architecture/pro-architecture.md)
   + [Workflow professionnel](architecture/pro-develop-deploy-workflow.md)
   + [Architecture mise à l’échelle](architecture/scaled-architecture.md)
   + [Mise à l’échelle automatique](architecture/autoscaling.md)
+ [Prise en main](https://experienceleague.adobe.com/docs/commerce-cloud-service/start/overview.html)
+ Notes de mise à jour {#release-notes}
   + [Suite d’outils cloud](release-notes/cloud-tools-suite.md)
   + [Package de outils CEE](release-notes/ece-tools-package.md)
   + [Correctifs du cloud](release-notes/cloud-patches.md)
   + [Package Cloud Docker](release-notes/cloud-docker.md)
   + [Composants cloud](release-notes/cloud-components.md)
   + [Modules cloud](release-notes/cloud-packages.md)
   + [Modifications incompatibles avec l’arrière](release-notes/backward-incompatible-changes.md)
   + [Archive des notes de mise à jour](release-notes/cloud-release-archive.md)
+ Projet cloud {#project}
   + [Présentation du projet](project/overview.md)
   + [Structure du projet](project/file-structure.md)
   + [Accès utilisateur](project/user-access.md)
   + [Authentification multifactorielle](project/multi-factor-authentication.md)
   + [Flux d’activité](project/activity-stream.md)
   + [Emails sortants](project/outgoing-emails.md)
   + [Service de messagerie SendGrid](project/sendgrid.md)
   + [Gestion des branches de console](project/console-branches.md)
   + [Adresses IP régionales](project/regional-ip-addresses.md)
+ Outils de développement {#dev-tools}
   + [Vue d’ensemble](dev-tools/overview.md)
   + Interface de ligne de commande du cloud {#cloud-cli}
      + [Présentation de la ligne de commande](dev-tools/cloud-cli-overview.md)
      + [Référence de ligne de commande](dev-tools/cloud-cli-reference.md)
   + [Cloud Docker](dev-tools/cloud-docker.md)
   + CEE-Outils {#ece-tools}
      + [Présentation des packages](dev-tools/package-overview.md)
      + [Mise à niveau ponctuelle pour utiliser les outils CEE](dev-tools/install-package.md)
      + [Mettre à jour le package CEE-Outils](dev-tools/update-package.md)
      + [Référence de ligne de commande](dev-tools/ece-tools-cli-reference.md)
      + [Référence d’erreur](dev-tools/error-reference.md)
   + Intégrations {#integrations}
      + [Vue d’ensemble](integrations/overview.md)
      + [Bitbucket](integrations/bitbucket.md)
      + [GitHub](integrations/github.md)
      + [GitLab](integrations/gitlab.md)
      + [Notifications d’intégrité](integrations/health-notifications.md)
+ Développement {#develop}
   + [Vue d’ensemble](development/overview.md)
   + [Clés d’authentification](development/authentication-keys.md)
   + [Gestion des branches de l’interface de ligne de commande](development/cli-branches.md)
   + [Connexions sécurisées](development/secure-connections.md)
   + Déployer {#deploy}
      + [Processus de déploiement](deploy/process.md)
      + [Optimisation](deploy/optimization.md)
      + [Bonnes pratiques](deploy/best-practices.md)
      + [Déploiement basé sur des scénarios](deploy/scenario-based.md)
      + [Déploiement sans interruption](deploy/reduce-downtime.md)
      + [Déploiement de contenu statique](deploy/static-content.md)
      + [Assistant dynamique](deploy/smart-wizards.md)
      + [Déploiement vers l’évaluation et la production](deploy/staging-production.md)
      + [Récupération de l’échec du composant](deploy/recover-failed-deployment.md)
   + Test {#test}
      + [Instructions de test](test/guidance.md)
      + [Journaux](test/log-locations.md)
      + [Xdebug](test/debug.md)
      + [Exemples de données](test/sample-data.md)
      + [Évaluation et production](test/staging-and-production.md)
      + [Second environnement d’évaluation](test/second-staging.md)
   + [Service PrivateLink](development/privatelink-service.md)
   + [Bloc de protection](development/protective-block.md)
   + [Restaurer l’environnement](development/restore-environment.md)
   + Stockage {#storage}
      + [Gestion de l’espace disque](storage/manage-disk-space.md)
      + [Requêtes de base de données de profil](storage/profile-database-queries.md)
      + [Sauvegarde de la base](storage/database-dump.md)
      + [Gestion des sauvegardes](storage/snapshots.md)
   + Mises à niveau et correctifs {#upgrade}
      + [Bonnes pratiques](development/best-practices.md)
      + [Mettre à niveau la version de Commerce](development/commerce-version.md)
      + [Appliquer les correctifs](development/apply-patches.md)
+ Configuration {#configure}
   + [Vue d’ensemble](environment/overview.md)
   + Application {#app}
      + [Configuration du déploiement des applications](application/configure-app-yaml.md)
      + [paramètres PHP](application/php-settings.md)
      + Propriétés {#properties}
         + [Propriétés de l’application](application/properties.md)
         + [Crons](application/crons-property.md)
         + [Pare-feu (lanceur uniquement)](application/firewall-property.md)
         + [Hooks](application/hooks-property.md)
         + [Variables](application/variables-property.md)
         + [Web](application/web-property.md)
         + [Travailleurs](application/workers-property.md)
      + [Définition du cache des fichiers statiques](application/set-cache.md)
   + Environnement {#env}
      + [Configuration du déploiement de l’environnement](environment/configure-env-yaml.md)
      + [Niveaux et options de variable](environment/variable-levels.md)
      + Remplacer les variables {#stage}
         + [Variables d’environnement](environment/variables-intro.md)
         + [ADMIN](environment/variables-admin.md)
         + [Variables cloud](environment/variables-cloud.md)
         + [Global](environment/variables-global.md)
         + [Build](environment/variables-build.md)
         + [Déployer](environment/variables-deploy.md)
         + [Post-déploiement](environment/variables-post-deploy.md)
      + Configurer les notifications {#log}
         + [Notifications](environment/set-up-notifications.md)
         + [Gestionnaires de journaux](environment/log-handlers.md)
   + Itinéraires {#routes}
      + [Configuration des itinéraires](routes/routes-yaml.md)
      + [Mise en cache](routes/caching.md)
      + [Redirections](routes/redirects.md)
      + [Inclusions côté serveur](routes/server-side-includes.md)
   + Services {#service}
      + [Configuration des services](services/services-yaml.md)
      + [Elasticsearch](services/elasticsearch.md)
      + [MySQL](services/mysql.md)
      + [OpenSearch](services/opensearch.md)
      + [RabbitMQ](services/rabbitmq.md)
      + [Redis](services/redis.md)
+ Services rapides {#cdn}
   + [Vue d’ensemble](cdn/fastly.md)
   + Configuration rapide {#setup-fastly}
      + [Configuration des services Fastly](cdn/fastly-configuration.md)
      + [Personnalisation de la configuration du cache](cdn/fastly-custom-cache-configuration.md)
      + [Personnalisation des pages d’erreur et de maintenance](cdn/fastly-custom-response.md)
   + [Pare-feu d’applications web](cdn/fastly-waf-service.md)
   + [Optimisation des images](cdn/fastly-image-optimization.md)
   + Personnalisation avec VCL {#custom-vcl-snippets}
      + [Prise en main](cdn/fastly-vcl-custom-snippets.md)
      + [Restauration des requêtes vers un serveur principal CMS](cdn/fastly-vcl-wordpress.md)
      + [Blocage du courrier indésirable](cdn/fastly-vcl-badreferer.md)
      + [LISTE AUTORISÉE IP](cdn/fastly-vcl-allowlist.md)
      + [LISTE BLOQUÉE IP](cdn/fastly-vcl-blocking.md)
      + [Contournement rapide du cache](cdn/fastly-vcl-bypass-to-origin.md)
   + [Dépannage rapide](cdn/fastly-troubleshooting.md)
+ Paramètres du magasin {#configure-store}
   + [Vue d’ensemble](store/overview.md)
   + [Bonnes pratiques](store/best-practices.md)
   + [Thème personnalisé](store/custom-theme.md)
   + [Extensions](store/extensions.md)
   + [Module B2B](store/b2b-module.md)
   + [Plusieurs sites](store/multiple-sites.md)
   + [Carte de site et robots de moteur de recherche](store/robots-sitemap.md)
   + [Méthodes de paiement PayPal](store/paypal.md)
   + [Gestion des configurations](store/store-settings.md)
+ Site de lancement {#launch}
   + [Vue d’ensemble](launch/overview.md)
   + [Liste de contrôle de lancement](launch/checklist.md)
   + [Étapes de lancement](launch/steps.md)
+ Surveiller le site {#monitor}
   + [Performances](monitor/performance.md)
   + Service New Relic {#new-relic}
      + [Présentation de New Relic](monitor/new-relic-service.md)
      + [Gestion des comptes et des utilisateurs](monitor/account-management.md)
      + Examiner les performances {#investigate}
         + [Stratégies, alertes et workflows](monitor/investigate-performance.md)
         + [Ingestion des données](monitor/ingest-data.md)
         + [Suivi des déploiements](monitor/track-deployments.md)
      + [Gestion des logs](monitor/log-management.md)
