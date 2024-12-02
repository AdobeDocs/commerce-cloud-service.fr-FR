---
title: Gestion des branches avec le  [!DNL Cloud Console]
description: Découvrez comment gérer les branches d’environnement pour Adobe Commerce sur l’infrastructure cloud à l’aide de la  [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Gérer les branches avec le [!DNL Cloud Console]

Vous pouvez gérer vos environnements à l’aide de l’interface de ligne de commande [!DNL Cloud Console] ou `magento-cloud`. Les fichiers de votre projet sont stockés dans un référentiel Git. Vous pouvez utiliser des commandes Git pour gérer votre code, mais l’interface de ligne de commande `magento-cloud` est conçue pour interagir avec les fonctionnalités de la plateforme, contrairement aux commandes Git. Voir [Commandes Git](../dev-tools/cloud-cli-overview.md#git-commands) dans la rubrique d’interface de ligne de commande du cloud.

Cette rubrique explique comment utiliser le [!DNL Cloud Console] pour :

- Ajouter ou supprimer un environnement
- Synchronisation (`git pull`) à partir de l’environnement parent
- Fusionner (`git push`) vers l’environnement parent

>[!TIP]
>
>Vous ne pouvez pas créer de branches à partir des environnements d’évaluation et de production Pro. Vous pouvez créer une branche à partir de la branche `master`.

## Créer un environnement

La stratégie d’embranchement utilise un workflow Git courant dans lequel vous développez du code et ajoutez des extensions dans une branche de développement. Voir les vues d&#39;ensemble de l&#39;architecture [Starter](../architecture/starter-architecture.md) et [Pro](../architecture/starter-develop-deploy-workflow.md).

- Pour commencer, créez une branche `staging` à partir de la branche `master`, puis une branche à partir de `staging` pour le développement.
- Pour Pro, créez une branche de développement à partir de l’environnement `Integration`.

Votre compte prend en charge un nombre limité de branches de développement ![branche active](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} (inactives). Gérez les branches actives et inactives en ajoutant ou en supprimant une branche à l’aide de l’interface de ligne de commande [!DNL Cloud Console] ou de l’interface de ligne de commande Cloud. Avant de pouvoir supprimer une branche, vous devez la désactiver, qui reste dans la liste _Environnements_ avec la valeur _inactive_. Vous pouvez réactiver la branche ultérieurement ou [supprimer la branche](../dev-tools/cloud-cli-overview.md#) dans les paramètres d’environnement ou à l’aide de l’interface de ligne de commande de Cloud.

Si vous avez besoin d’environnements actifs supplémentaires pour le développement, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**Pour ajouter une branche** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Sélectionnez un environnement.

   >[!TIP]
   >
   >Votre nouvelle branche est clonée à partir de cet environnement. Choisissez un environnement parent similaire à l’environnement que vous êtes sur le point de créer.

1. Cliquez sur **[!UICONTROL Branch]**.

   ![Créer une branche](../../assets/button-branch.png){width="150"}

1. Dans le formulaire _Branchement à partir de ..._, saisissez un nom de branche.

   L&#39;environnement _name_ diffère de l&#39;environnement _ID_ uniquement si vous utilisez des espaces ou des majuscules dans le nom de l&#39;environnement. Un ID d’environnement se compose de toutes les lettres minuscules, de tous les nombres et de tous les symboles autorisés. Les majuscules d’un nom d’environnement sont converties en minuscules dans l’identifiant ; les espaces d’un nom d’environnement sont convertis en tirets.

   Un nom d’environnement **ne peut pas** inclure des caractères réservés à votre shell Linux ou à des expressions régulières. Les caractères interdits incluent des accolades (`{ }`), des parenthèses, un astérisque (`*`), des chevrons (`>`), une esperluette (`&`), un pourcentage (<code> %)</code>), et autres caractères.

1. Sélectionnez un **[!UICONTROL Environment type]**.

1. Cliquez sur **[!UICONTROL Create Branch]**.

1. Attendez le déploiement de l’environnement.

   Pendant le déploiement, l’état de l’environnement est **En cours**. Après un déploiement réussi, l’état passe à une coche verte pour **success**.

## Création d’une branche inactive

Vous ne pouvez pas créer de branche inactive à partir de la console Adobe Commerce Cloud ou de l’interface de ligne de commande. Si vous souhaitez créer une branche inactive, créez-la sur le référentiel Git et effectuez une notification push à l’aide de l’option `environment.Parent` de la commande .

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Supprimer un environnement

Avant de pouvoir supprimer un environnement, vous devez le désactiver. Une fois qu’un environnement est inactif, vous pouvez le supprimer.

**Pour désactiver un environnement** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Sélectionnez l’environnement dans la liste _Environnement_ de la barre de navigation.

1. Cliquez sur l’icône de configuration située sur le côté droit de la barre de navigation supérieure, ce qui ouvre les paramètres d’environnement.

1. Sur l’onglet _[!UICONTROL General]_, faites défiler l’écran jusqu’à la section_[!UICONTROL Deactivate environment]_, cliquez sur **[!UICONTROL Deactivate environment and delete data]** et suivez les instructions.

## Synchroniser un environnement

La synchronisation d’un environnement (ou d’une branche) est identique à `git pull origin <parent>`. Vous pouvez synchroniser le code mis à jour à partir d’un environnement parent. Vous pouvez utiliser cette fonctionnalité par le biais de [!DNL Cloud Console] pour tous les environnements Starter et Pro.

Pour la planification Pro, vous pouvez effectuer une synchronisation entre l’évaluation et la production et votre branche `master`. Cette synchronisation extrait et envoie uniquement le code, et non les données. Pour synchroniser les données, videz les données de la base de données et placez-les dans la base de données d’un autre environnement. Voir [Migration et déploiement de fichiers statiques et de données](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**Pour synchroniser un environnement** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Dans la liste des environnements, cliquez sur le nom de la branche à synchroniser.

1. Cliquez sur (synchronisation).

   ![Synchroniser un environnement](../../assets/button-sync.png){width="150"}

1. Sélectionnez les éléments à synchroniser.

   - Remplacez les modifications de la synchronisation des données (données et fichiers) dans la base de données et les fichiers de contenu de la branche parente.
   - Fusion : (code) synchronise le code mis à jour de la branche parente.

   Cette opération génère également une commande d’interface de ligne de commande que vous pouvez copier et utiliser.

1. Cliquez sur **Sync**.

## Fusionner avec l’environnement parent

La fusion d’un environnement (ou d’une branche) est identique à `git push origin`. Vous fusionnez pour transférer du code mis à jour d’un environnement vers son environnement parent. Vous pouvez fusionner ce code avec `master`. Vous pouvez déployer vers les environnements d’évaluation et de production à l’aide de la commande `merge`.

**Pour fusionner avec l’environnement parent** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Dans la liste des environnements, cliquez sur le nom de la branche à fusionner.

1. Cliquez sur (fusionner).

   ![Fusionner un environnement](../../assets/button-merge.png){width="150"}

1. Cliquez sur **Fusionner** et confirmez l’action.

## Afficher les journaux

Grâce à [!DNL Cloud Console], vous pouvez consulter divers journaux pour les environnements, y compris l’historique de création, de déploiement et de déploiement.

Pour **Starter**, vous pouvez consulter les journaux de création et de déploiement et l’historique de déploiement. Ces environnements incluent la branche `master` (Production) et toutes les branches créées à partir de celle-ci.

Pour **Pro**, vous pouvez consulter les journaux suivants dans chaque environnement :

- Historique d’intégration : création et déploiement
- Évaluation : créez les journaux et l’historique de déploiement. Utilisez SSH pour vous connecter au serveur afin d’afficher les journaux de déploiement.
- Production : créez les journaux et l’historique de déploiement. Utilisez SSH pour vous connecter au serveur afin d’afficher les journaux de déploiement.

**Pour afficher les journaux dans le[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Sélectionnez un environnement.

   La vue d’environnement fournit une [liste d’activités](activity-stream.md) qui affiche les _événements_ récents, une entrée par action tentée, y compris les synchronisations, les fusions, les branches, les sauvegardes, etc. Cliquez sur **All** pour accéder à l’historique complet du déploiement.

1. Pour afficher le journal de génération, sélectionnez le lien Succès ou Échec par enregistrement de déploiement sur le compte.

>[!TIP]
>
>Cliquez sur l&#39;icône **Filtrer par** pour obtenir une liste déroulante et sélectionnez le type de messages à afficher.

## Extraction de code à partir d’un référentiel Git privé

Votre projet Adobe Commerce sur l’infrastructure cloud peut inclure du code provenant d’un référentiel Git privé. Par exemple, vous pouvez avoir du code pour un module ou un thème personnalisé dans un référentiel privé. Pour ce faire, vous devez ajouter la clé SSH publique de votre projet à votre référentiel Git privé et mettre à jour votre fichier de projet `composer.json`.

Pour ajouter une clé de déploiement à votre référentiel GitHub privé, vous devez être l’administrateur de ce référentiel. GitHub vous permet d’utiliser une clé de déploiement pour un seul référentiel.

Si vous préférez que votre projet accède à plusieurs référentiels, vous pouvez joindre une clé SSH à un compte utilisateur automatisé. Ce compte n’étant pas utilisé par un humain, il est appelé [utilisateur de machine](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Ajoutez le compte de la machine en tant que collaborateur ou ajoutez l’utilisateur de la machine à une équipe ayant accès aux référentiels.

>[!INFO]
>
>Adobe recommande d’ajouter et de fusionner ce code dans les référentiels Git de votre projet. Si vous ne configurez pas la connexion, vous pouvez rencontrer des problèmes de création.

**Pour trouver votre clé SSH publique** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Cliquez sur l’icône de configuration sur le côté droit de la barre de navigation supérieure.

1. Dans _Paramètres du projet_, cliquez sur **[!UICONTROL Deploy Key]**.

1. Copiez la clé de déploiement dans le Presse-papiers pour l’utiliser dans l’une des méthodes Git suivantes :

>[!BEGINTABS]

>[!TAB GitHub]

### Saisissez votre clé de déploiement GitHub .

Sur GitHub, les clés de déploiement sont en lecture seule par défaut.

**Pour entrer la clé publique de votre projet en tant que clé de déploiement GitHub** :

1. Connectez-vous à votre référentiel GitHub en tant qu’administrateur.
1. Cliquez sur l’onglet Référentiel **[!UICONTROL Settings]** .

   >[!NOTE]
   >
   >Si vous ne voyez pas cette option, vous n’êtes pas connecté en tant qu’administrateur de référentiel et vous ne pouvez pas terminer cette tâche. Demandez à votre administrateur de référentiel GitHub de le faire.

1. Dans l’onglet _Paramètres_ du volet de navigation de gauche, cliquez sur **[!UICONTROL Deploy Keys]**.
1. Cliquez sur **[!UICONTROL Add deploy key]**.
1. Suivez les invites.

Dans `composer.json`, utilisez le format `<user>@<host>:<.git</code>` ou `ssh://<user>@<host>:<port>/<path>.git` si vous utilisez un port non standard.

>[!TAB Bitbucket]

### Entrez votre clé de déploiement Bitbucket

**Pour entrer la clé publique de votre projet en tant que clé de déploiement Bitbucket** :

1. Connectez-vous à votre référentiel Bitbucket en tant qu’administrateur.
1. Dans le volet de navigation de gauche, cliquez sur **[!UICONTROL Settings]**.
1. Cliquez sur Général > **[!UICONTROL Deployment Keys]**.
1. Cliquez sur **[!UICONTROL Add Key]**.
1. Suivez les invites.

>[!TAB GitLab]

### Saisissez votre clé de déploiement GitLab.

**Pour ajouter la clé SSH publique de votre projet en tant que clé de déploiement GitLab** :

1. Connectez-vous à votre référentiel GitLab en tant que propriétaire.
1. Vérifiez que l’option _Pipelines_ est activée pour votre projet :

   1. Dans les paramètres du projet, développez la section **[!UICONTROL Visibility, project, features, permissions]** .
   1. Si nécessaire, cliquez sur **[!UICONTROL Pipelines]** pour activer l’option.

1. Ajoutez votre clé SSH publique aux paramètres CI/CD.

   1. Dans le volet de navigation de gauche, cliquez sur Paramètres > **[!UICONTROL CI / CD]**.
   1. Cliquez sur Déployer les clés **Développer** pour configurer la clé.
   1. Dans le formulaire _Déployer la clé_, ajoutez un nom de clé de déploiement au champ **[!UICONTROL Title]** et collez votre clé SSH publique dans le champ **[!UICONTROL Key]**.
   1. Cliquez sur **[!UICONTROL Add Key]** pour enregistrer la configuration.

>[!ENDTABS]

## Environnements et branches sécurisés

Vous pouvez accéder à votre projet et à vos environnements à partir de n’importe quel emplacement via un navigateur web à l’aide de [!DNL Cloud Console]. La sécurité de votre environnement de production, des magasins et des sites peut être définie. Cette section vous aide à sécuriser vos environnements d’intégration et d’évaluation pour vos développeurs, DBA, etc.

>[!WARNING]
>
>**DO NOT** utilisez les méthodes suivantes pour sécuriser les environnements d’évaluation et de production Pro. Cela rompt la mise en cache rapide. Utilisez la fonction [Blocking](../cdn/fastly-vcl-blocking.md) disponible dans le réseau de diffusion de contenu Fastly pour Adobe Commerce.

**Pour sécuriser les environnements** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Sélectionnez un environnement et cliquez sur l’icône de configuration dans la barre de navigation.

1. Dans l’onglet _Général_ des paramètres d’environnement, cliquez sur **ON** pour **[!UICONTROL HTTP access control enabled]** afin d’activer un accès sécurisé. Vous pouvez choisir entre les informations d’identification ou les adresses IP pour filtrer l’accès.

1. Pour filtrer par informations d’identification, cliquez sur **[!UICONTROL Add Login]**, saisissez un nom d’utilisateur et un mot de passe, puis cliquez sur **[!UICONTROL Add Login]** à ajouter.

1. Pour filtrer par adresse IP, saisissez les adresses IP dans une liste de `deny` ou `allow`. Par exemple :

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Cliquez sur **[!UICONTROL Save]**. Cela redéploie l’environnement pour mettre à jour la sécurité et les paramètres. Adobe recommande de tester l’environnement après avoir terminé les paramètres de sécurité.
