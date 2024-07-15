---
title: Affichage et gestion des journaux
description: Découvrez les types de fichiers journaux disponibles dans l’infrastructure cloud et où les trouver.
last-substantial-update: 2023-05-23T00:00:00Z
exl-id: d7f63dab-23bf-4b95-b58c-3ef9b46979d4
source-git-commit: 86af69eed16e8fe464de93bd0f33cfbfd4ed8f49
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Affichage et gestion des journaux

Les journaux d’Adobe Commerce sur les projets d’infrastructure cloud sont utiles pour résoudre les problèmes liés aux [hooks de version et de déploiement](../application/hooks-property.md), aux services cloud et à l’application Adobe Commerce.

Vous pouvez afficher les journaux à partir du système de fichiers, de [!DNL Cloud Console] et de l’interface de ligne de commande `magento-cloud`.

- **Système de fichiers** : le répertoire système `/var/log` contient des journaux pour tous les environnements. Le répertoire `var/log/` contient des journaux spécifiques à l’application propres à un environnement particulier. Ces répertoires ne sont pas partagés entre les noeuds d’une grappe. Dans les environnements de production et d’évaluation Pro, vous devez vérifier les journaux de chaque noeud.

- **[!DNL Cloud Console]** : vous pouvez voir les informations de journal de création, de déploiement et de post-déploiement dans la liste _messages_ de l’environnement.

- **Cloud CLI** : vous pouvez afficher les journaux d’environnement local à l’aide de la commande `magento-cloud log` ou des journaux d’environnement distant à l’aide de la commande `magento-cloud ssh`.

## Emplacements des journaux

Les journaux système sont stockés aux emplacements suivants :

- Intégration : `/var/log/<log-name>.log`
- Pro Staging : `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro Production : `/var/log/platform/<project-ID>/<log-name>.log`

La valeur de `<project-ID>` dépend du projet et de l’environnement : évaluation ou production. Par exemple, avec un ID de projet de `yw1unoukjcawe`, l’utilisateur de l’environnement d’évaluation est `yw1unoukjcawe_stg` et l’utilisateur de l’environnement de production est `yw1unoukjcawe`.

En utilisant cet exemple, le journal de déploiement est : `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### Affichage des journaux d’environnement distants

La plupart des journaux incluent des événements qui se produisent dans l’environnement distant. Pour Pro, il existe plusieurs noeuds et chaque noeud comporte des journaux uniques. Utilisez ce qui suit pour afficher une liste de tous les hôtes :

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Exemple de réponse :

```terminal
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**Pour afficher la liste des journaux d’environnement distant** :

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Exemple pour Pro :

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**Pour afficher un journal distant** :

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Exemple pour Pro :

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>Dans les environnements d’évaluation et de production, la rotation, la compression et la suppression automatiques des journaux sont activées pour les fichiers journaux dont le nom est fixe. Chaque type de fichier journal a un modèle et une durée de vie rotatifs. Les environnements de démarrage n’ont pas de rotation de journal. Vous trouverez des détails complets sur la rotation des journaux de l’environnement et la durée de vie des journaux compressés dans : `/etc/logrotate.conf` et `/etc/logrotate.d/<various>`. La rotation du journal ne peut pas être configurée dans les environnements Pro Integration. Pour l’intégration Pro, vous devez mettre en oeuvre une solution/un script personnalisé et [configurer votre cron](../application/crons-property.md) pour exécuter le script selon vos besoins.

## Création et déploiement des journaux

Après avoir apporté des modifications à votre environnement, vous pouvez passer en revue la journalisation à partir de chaque point d’extension du fichier `var/log/cloud.log`. Le journal contient des messages de début et d’arrêt pour chaque point d’extension. Dans l’exemple suivant, les messages sont &quot;`Starting post-deploy.`&quot; et &quot;`Post-deploy is complete.`&quot;

Vérifiez les horodatages sur les entrées du journal, vérifiez et localisez les journaux pour un déploiement spécifique. Voici un exemple condensé de sortie de journal que vous pouvez utiliser pour le dépannage :

```terminal
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>Lorsque vous configurez votre environnement Cloud, vous pouvez configurer des [notifications par Slack et par e-mail de journalisation](../environment/set-up-notifications.md) pour les actions de création et de déploiement.

Les journaux suivants ont un emplacement commun pour tous les projets cloud :

- **Log de déploiement** : `var/log/cloud.log`
- **Dernier journal d’erreur de déploiement** : `var/log/cloud.error.log`
- **Journal de débogage** : `var/log/debug.log`
- **Journal des exceptions** : `var/log/exception.log`
- **Journal système** : `var/log/system.log`
- **Journal d’assistance** : `var/log/support_report.log`
- **Rapports** : `var/report/`

Bien que le fichier `cloud.log` contienne des commentaires à chaque étape du processus de déploiement, les journaux créés par le crochet de déploiement sont propres à chaque environnement. Le journal de déploiement spécifique à l’environnement se trouve dans les répertoires suivants :

- **Intégration de Starter et Pro** : `/var/log/deploy.log`
- **Pro Staging** : `/var/log/platform/<project-ID>_stg/deploy.log`
- **Pro Production** : `/var/log/platform/<project-ID>/deploy.log`

### Journal de déploiement

Le journal de chaque déploiement se concatène au fichier `deploy.log` spécifique. L’exemple suivant imprime le journal de déploiement de l’environnement actuel dans le terminal :

```bash
magento-cloud log -e <environment-ID> deploy
```

Exemple de réponse :

```terminal
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Journal des erreurs

Les messages d’erreur et d’avertissement générés pendant le processus de déploiement sont écrits dans les fichiers `var/log/cloud.log` et `var/log/cloud.error.log`. Le fichier journal des erreurs Cloud contient uniquement les erreurs et les avertissements du dernier déploiement. Un fichier vide indique un déploiement réussi sans erreur.

Vous pouvez afficher le fichier journal à l’aide de l’interface de ligne de commande [Cloud CLI SSH](#view-remote-environment-logs), ou vous pouvez utiliser les outils de la CEE pour afficher les erreurs avec des suggestions :

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Exemple de réponse :

```terminal
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

La plupart des messages d’erreur contiennent une description et une action suggérée. Utilisez la [référence de message d’erreur pour les outils de la CEE](../dev-tools/error-reference.md) pour rechercher le code d’erreur afin d’obtenir des instructions supplémentaires. Pour plus d’informations, reportez-vous à l’[outil de dépannage du déploiement Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Logs d’application

Comme pour les journaux de déploiement, les journaux d’application sont uniques pour chaque environnement :

| Fichier journal | Intégration de Starter et Pro | Description |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Déployer le journal** | `/var/log/deploy.log` | Activité à partir du [crochet de déploiement](../application/hooks-property.md). |
| **Journal de déploiement Post** | `/var/log/post_deploy.log` | Activité à partir du [crochet post-déploiement](../application/hooks-property.md). |
| **Journal Cron** | `/var/log/cron.log` | Sortie des tâches cron. |
| **Journal d’accès Nginx** | `/var/log/access.log` | Au démarrage de Nginx, erreurs HTTP pour les répertoires manquants et les types de fichiers exclus. |
| **Journal d’erreur Nginx** | `/var/log/error.log` | Messages de démarrage utiles pour le débogage des erreurs de configuration associées à Nginx. |
| **Journal d’accès PHP** | `/var/log/php.access.log` | Demandes au service PHP. |
| **Journal FPM PHP** | `/var/log/app.log` | |

Pour les environnements d’évaluation et de production Pro, les journaux Déploiement, Déploiement Post et Cron sont disponibles uniquement sur le premier noeud de la grappe :

| Fichier journal | Pro Staging | Pro Production |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Déployer le journal** | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>_stg/deploy.log` | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Journal de déploiement Post** | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **Journal Cron** | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>_stg/cron.log` | Premier noeud uniquement :<br>`/var/log/platform/<project-ID>/cron.log` |
| **Journal d’accès Nginx** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Journal d’erreur Nginx** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **Journal d’accès PHP** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **Journal FPM PHP** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### Fichiers journaux archivés

Les journaux d’application sont compressés et archivés une fois par jour et conservés pendant un an. Les journaux compressés sont nommés à l’aide d’un identifiant unique qui correspond au `Number of Days Ago + 1`. Par exemple, dans les environnements de production Pro, un journal d’accès PHP de 21 jours dans le passé est stocké et nommé comme suit :

```terminal
/var/log/platform/<project-ID>/php.access.log.22.gz
```

Les fichiers journaux archivés sont toujours stockés dans le répertoire où se trouvait le fichier d’origine avant la compression.

>[!NOTE]
>
>Les fichiers journaux **Deploy** et **Post-deploy** ne sont pas pivotés et archivés. L’historique complet du déploiement est écrit dans ces fichiers journaux.

## Journaux des services

Comme chaque service s’exécute dans un conteneur distinct, les journaux de service ne sont pas disponibles dans l’environnement d’intégration. Adobe Commerce sur l’infrastructure cloud permet d’accéder au conteneur de serveurs web uniquement dans l’environnement d’intégration. Les emplacements de journaux de service suivants sont pour les environnements de production et d’évaluation Pro :

- **Redis log** : `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **Journal des Elasticsearch** : `/var/log/elasticsearch/elasticsearch.log`
- **Journal de nettoyage de la mémoire Java** : `/var/log/elasticsearch/gc.log`
- **Journal du courrier** : `/var/log/mail.log`
- **Journal des erreurs MySQL** : `/var/log/mysql/mysql-error.log`
- **Log lent MySQL** : `/var/log/mysql/mysql-slow.log`
- **Journal RabbitMQ** : `/var/log/rabbitmq/rabbit@host1.log`

Les journaux de service sont archivés et enregistrés pendant différentes périodes, selon le type de journal. Par exemple, les journaux MySQL ont la durée de vie la plus courte, supprimée après sept jours.

>[!TIP]
>
>L’emplacement des fichiers journaux dans l’architecture mise à l’échelle dépend du type de noeud. Voir la rubrique [Emplacements de journal dans l’architecture mise à l’échelle](../architecture/scaled-architecture.md#log-locations) .

## Données de journal pour la production et l’évaluation Pro

Dans les environnements de production et d’évaluation Pro, utilisez la [gestion des journaux New Relic](../monitor/log-management.md) intégrée à votre projet pour gérer les données de journaux agrégées de tous les journaux associés à votre projet d’infrastructure cloud Adobe Commerce.

L’application New Relic Logs fournit un tableau de bord de gestion des journaux centralisé pour dépanner et surveiller Adobe Commerce sur les environnements de production et d’évaluation de l’infrastructure cloud. Le tableau de bord permet également d’accéder aux données de journal pour les services Fastly CDN, Image Optimization et WAF (pare-feu d’applications web). Voir [Services New Relic](../monitor/new-relic-service.md).
