---
title: Propriété Cron
description: Voir des exemples de configuration de la propriété `crons` dans le fichier de configuration de l’application  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Propriété Cron

Adobe Commerce utilise la propriété `crons` pour planifier des activités répétitives. Il est idéal pour planifier l’exécution d’une tâche spécifique à certains moments de la journée. Une seule tâche cron peut s’exécuter à la fois sur l’instance web pour Adobe Commerce sur les projets d’infrastructure cloud en raison de la nature des environnements en lecture seule. Il est recommandé de ventiler les tâches longues en tâches plus petites et en file d’attente. Vous pouvez également créer une [instance de travail](workers-property.md).

Adobe vous recommande d’exécuter `crons` en tant que [ propriétaire du système de fichiers](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html). Ne _pas_ exécuter `crons` en tant que `root` ou en tant qu’utilisateur du serveur web.

Cette configuration diffère des déploiements sur site d’Adobe Commerce, qui comportent plusieurs tâches cron par défaut. Voir [Configuration de tâches cron](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) dans le _Guide de configuration_.

## Configuration de tâches cron

La propriété `crons` décrit les processus déclenchés selon un planning. Chaque tâche requiert un nom et les options suivantes :

- `spec` : expression cron utilisée pour la planification.
- `cmd` : commande à exécuter sur `start` et `stop`.
- `shutdown_timeout`—(_Facultatif_) Si une tâche cron est annulée, il s’agit du nombre de secondes après lesquelles un signal SIGKILL est envoyé pour arrêter la tâche ou le processus. La valeur par défaut est de 10 secondes.
- `timeout`—(_Facultatif_) La durée maximale pendant laquelle une tâche cron peut s’exécuter avant expiration. La valeur par défaut est de 86 400 secondes (24 heures).

Par défaut, chaque projet cloud Commerce possède la configuration `crons` par défaut suivante dans le fichier `.magento.app.yaml` :

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Si votre projet nécessite des tâches cron personnalisées, vous pouvez les ajouter à la configuration par défaut `crons`. Voir [Création d’une tâche cron](#build-a-cron-job).

### `crontab`

Adobe Commerce a ajouté une option de configuration autocrons uniquement aux projets Pro pour prendre en charge la configuration en libre-service `crons` sur les environnements d’évaluation et de production. Si cette option est activée, vous pouvez utiliser `crontab` pour passer en revue la configuration cron. _not_ disponible avec les projets de démarrage.

Bien que vous puissiez utiliser `crontab` pour passer en revue la configuration des projets Pro, Adobe Commerce n’utilise pas `crontab` pour exécuter des tâches cron pour les sites déployés sur l’infrastructure cloud.

**Pour passer en revue la configuration cron sur les environnements Pro** :

1. Utilisez [SSH](../development/secure-connections.md#use-an-ssh-command) pour vous connecter à l’environnement distant.

1. Liste des processus cron planifiés.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Si la commande `crontab -l` renvoie une erreur `Command not found` (dans les environnements d’évaluation et de production Pro uniquement), vous devez [ envoyer un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour activer l’option de configuration en libre-service auto-crons sur votre projet.

L’exemple suivant montre la sortie `crontab` pour un environnement qui ne possède que la configuration par défaut `crons` :

```
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Création d’une tâche cron

Une tâche cron inclut la spécification de planification et de minutage ainsi que la commande à exécuter à l’heure planifiée. Pour les environnements Starter et Pro `integration`, l’intervalle minimum est une fois toutes les cinq minutes. Pour les environnements d’évaluation et de production professionnels, l’intervalle minimum est d’une fois par minute. Sur Adobe Commerce sur l’infrastructure cloud, vous ajoutez des tâches cron personnalisées au fichier `.magento.app.yaml` dans la section `crons`. Le format général est `spec` pour la planification et `cmd` pour spécifier la commande ou le script personnalisé à exécuter.

### Spécification

Adobe Commerce utilise une expression à cinq valeurs pour une spécification `crons` (spécification) : `* * * * *`

1. Minute (0 à 59) Pour tous les environnements Starter et Pro, la fréquence minimale prise en charge pour les tâches cron est de cinq minutes. Vous devrez peut-être configurer les paramètres dans votre administrateur.
2. Heure (0 à 23)
3. Jour du mois (1 à 31)
4. Mois (1 à 12)
5. Jour de la semaine (0 à 6) (du dimanche au samedi ; 7 est également le dimanche sur certains systèmes)

Quelques exemples :

- `00 */3 * * *` s’exécute toutes les trois heures à la première minute (12 h, 3 h, 6 h)
- `20 */8 * * *` s’exécute toutes les 8 heures à la minute 20 (12 h 20, 8 h 20, 16 h 20)
- `00 00 * * *` s’exécute une fois par jour à minuit
- `00 * * * 1` fonctionne une fois par semaine le lundi à minuit.

>[!NOTE]
>
>L’heure `crons` spécifiée dans le fichier `.magento.app.yaml` est basée sur le fuseau horaire du serveur, et non sur celui spécifié dans les valeurs de configuration du magasin dans la base de données.

Lorsque vous déterminez la planification, tenez compte du temps nécessaire pour terminer la tâche. Par exemple, si vous exécutez une tâche toutes les trois heures et que la tâche prend 40 minutes, vous pouvez envisager de modifier le délai planifié.

### Commande

`cmd` spécifie la commande ou le script personnalisé à exécuter. Le format du script de commande peut être le suivant :

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Par exemple :

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

Dans cet exemple, `<path-to-php-binary>` est `/usr/bin/php`. Le répertoire d’installation, qui inclut l’ID de projet est `/app/abc123edf890/bin/magento` et l’action de script est `export:start catalog_category_product`.

### Ajout de tâches cron personnalisées à votre projet

Sur la plateforme Adobe Commerce on Cloud Infrastructure, vous pouvez ajouter des personnalisations à la section `crons` du fichier [`.magento.app.yaml`](../application/configure-app-yaml.md).

>[!NOTE]
>
>Pour les environnements Starter et Pro `integration`, l’intervalle minimum est une fois toutes les cinq minutes. Pour les environnements d’évaluation et de production professionnels, l’intervalle minimum est d’une fois par minute. Vous ne pouvez pas configurer d’intervalles plus fréquents que les minimums par défaut.

Sur les projets Adobe Commerce Pro, la [fonction auto-crons](#set-up-cron-jobs) doit être activée sur votre projet avant de pouvoir ajouter des tâches cron personnalisées aux environnements d’évaluation et de production à l’aide du fichier `.magento.app.yaml`. Si cette fonctionnalité n’est pas activée, [Envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour activer les auto-crons.

**Pour ajouter des tâches cron personnalisées** :

1. Dans votre environnement de développement local, modifiez le fichier `.magento.app.yaml` dans le répertoire Adobe Commerce `/app` .

1. Dans la section `crons` , ajoutez votre personnalisation en utilisant le format suivant :

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   Dans l’exemple suivant, la tâche `productcatalog` exporte le catalogue de produits toutes les huit heures, 20 minutes après l’heure.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Ajout, validation et modification du code push.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

### Mise à jour des tâches cron

Pour ajouter, supprimer ou mettre à jour une tâche personnalisée, modifiez la configuration dans la section `crons` du fichier `.magento.app.yaml`. Ensuite, testez les mises à jour dans l’environnement distant `integration` avant d’appliquer les modifications aux environnements d’évaluation et de production.

## Désactivation des tâches cron

Vous pouvez désactiver manuellement les tâches cron avant d’effectuer des tâches de maintenance, telles que la réindexation ou le nettoyage du cache, afin d’éviter tout problème de performances. Vous pouvez utiliser la commande `ece-tools` CLI `cron:disable` pour désactiver toutes les tâches cron et arrêter tous les processus cron actifs.

**Pour désactiver les tâches cron** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Désactivez les tâches cron et arrêtez les processus cron actifs.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. Une fois que vous avez effectué les tâches de maintenance requises, veillez à réactiver les tâches cron.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Résolution des problèmes liés aux tâches cron

Adobe a mis à jour le package d’infrastructure de cloud d’Adobe Commerce pour optimiser le traitement cron sur la plateforme d’infrastructure de cloud d’Adobe Commerce et pour résoudre les problèmes liés à cron. Si vous rencontrez des problèmes avec le traitement de cron, assurez-vous que votre projet utilise la version la plus récente du package `ece-tools`. Voir [Mise à jour des outils de CEE](../dev-tools/update-package.md).

Vous pouvez consulter les informations de traitement cron dans les fichiers journaux au niveau de l’application pour chaque environnement. Voir [Logs de l’application](../test/log-locations.md#application-logs).

Pour obtenir de l’aide sur la résolution des problèmes liés à cron, reportez-vous aux articles suivants du support Adobe Commerce :

- [Les tâches de cron verrouillent les tâches d’autres groupes](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Réinitialiser manuellement les tâches cron bloquées sur le cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
