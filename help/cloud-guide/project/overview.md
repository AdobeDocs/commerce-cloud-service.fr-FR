---
title: Projet d’infrastructure cloud
description: Lisez un aperçu d’Adobe Commerce sur l’infrastructure cloud  [!DNL Cloud Console]  et apprenez à accéder aux paramètres du compte.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Projet d’infrastructure cloud

Le projet Adobe Commerce sur l’infrastructure cloud comprend tout le code des branches Git, des environnements associés et des scripts pour déployer l’application [!DNL Commerce]. Les environnements contiennent des services pour la prise en charge de l’application [!DNL Commerce], y compris une base de données, un serveur web et un serveur de mise en cache.

Adobe fournit un [!DNL Cloud Console] et des outils de développement pour gérer entièrement tous les aspects de votre projet. En tant que propriétaire du compte, vous disposez d’un accès complet à tous les environnements.

## [!DNL Cloud Console]

[!DNL Cloud Console] fournit des méthodes interactives pour créer, gérer et déployer le code Commerce dans un format convivial. [Connectez-vous à  [!DNL Cloud Console]](https://console.adobecommerce.com) pour afficher la liste de vos projets. Vous ne pouvez afficher que les projets auxquels vous êtes autorisé à accéder en tant qu’administrateur ou pour des types d’environnements spécifiques. Si vous êtes un partenaire de solutions Adobe, vous pouvez voir plusieurs projets pour les clients que vous prenez en charge.

>[!TIP]
>
>Si vous ne voyez aucun projet, vous devez contacter le [propriétaire du compte ou administrateur de projet](../project/user-access.md) associé au projet et demander l’accès. Pour les nouveaux utilisateurs, consultez la [rubrique d’intégration](../../get-started/onboarding.md#cloud-console) du guide _Prise en main_ .

La vue _Tous les projets_ répertorie tous les projets auxquels vous êtes autorisé à accéder. Vous pouvez cliquer sur **[!UICONTROL Show filters]** et filtrer la liste de vos projets par type, région ou plan.

![Liste de projets](../../assets/ui-allprojects-list.png)

### Présentation du projet

La sélection d’un projet dans la liste _Tous les projets_ ouvre la présentation du projet. La présentation du projet affiche toujours une barre de navigation du projet, qui comprend un sélecteur d’environnement et un bouton de configuration :

![Navigation dans le projet](../../assets/project-nav.png)

La présentation du projet, tant qu’aucun environnement n’est sélectionné, affiche un résumé des détails du projet dans la zone d’aperçu :

- Nom du projet
- Région, ID de projet
- Planification, stockage alloué, environnements, utilisateurs
- URL de storefront avec bouton **[!UICONTROL Set a custom domain]**

Et dans la présentation principale du projet :

- La vue Environnements affiche une liste ou une arborescence des environnements ![Active branch](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} (inactif).
- [Le flux d’activités](activity-stream.md) affiche les activités en cours d’exécution, en attente et récentes pour le projet.
<!-- - Apps & Services—Shows a topology of service containers -->

Pour les projets **Starter**, il existe une hiérarchie de branches commençant par `master` (Production). Toute branche que vous créez s’affiche en tant qu’enfant à partir de la branche `master`. Adobe recommande de créer une branche `staging`, puis de créer une branche `integration` pour le développement. Voir [Architecture de démarrage](../architecture/starter-architecture.md).

Pour **Pro**, il existe une hiérarchie de branches allant de `production` à `staging` à `integration`. L’icône ![Icône dédiée](../../assets/icon-dedicated.png){width="32"} indique que la branche se déploie vers un environnement dédié. Toutes les branches que vous créez s’affichent en tant qu’enfants de la branche `integration`. Voir [Architecture Pro](../architecture/pro-architecture.md).

![Liste d’environnements Pro](../../assets/pro-environments.png)

### Présentation de l’environnement

La sélection d’un environnement dans la barre de navigation du projet modifie la vue d’ensemble et la barre de navigation pour mettre l’accent sur l’environnement sélectionné. La barre de navigation comprend des commandes de branche (branche, fusion et synchronisation) et un bouton de configuration :

![Environnement sélectionné](../../assets/environment-selected.png)

La présentation de l’environnement présente un résumé des détails de l’environnement dans la zone d’aperçu :

- Nom de l’environnement, type
- Région, ID de projet
- Date et heure de la dernière activité, y compris la sauvegarde
- Accès HTTP et état du moteur de recherche
- Nom de la machine affecté à l’environnement
- État de l’environnement (actif ou inactif)
- URL de storefront avec bouton **[!UICONTROL Set a custom domain]**

Et dans la présentation de l&#39;environnement principal :

- [ Le ](activity-stream.md) constitue la présentation de l’environnement principal et affiche les activités en cours d’exécution, en attente et récentes pour l’environnement sélectionné.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- L’onglet [Sauvegardes](../storage/snapshots.md#create-a-manual-backup) fournit une liste de sauvegardes stockées, l’historique des actions de sauvegarde et le bouton Sauvegarde.

### Accès à storefront

Chaque environnement actif comporte une vitrine. Sélectionnez un environnement dans le volet de navigation supérieur, puis cliquez sur l’URL dans la présentation de l’environnement. Il existe également une liste **[!UICONTROL URLs]** située à droite au-dessus de la liste Activité.

L&#39;URL d&#39;accès Web peut contenir les éléments suivants :

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **ID unique** = 7 caractères alphanumériques aléatoires
- **ID de projet** = ID de projet de 13 caractères
- **Région** = nom de région AWS ou Azure, voir [Adresses IP régionales](regional-ip-addresses.md)

Les environnements de production et d’évaluation Pro comprennent trois noeuds auxquels vous pouvez accéder à l’aide des liens suivants :

- URL de l’équilibreur de charge :

   - `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

- Accès direct à l&#39;un des trois serveurs redondants :

   - `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

  L&#39;URL de production est utilisée par le réseau de diffusion de contenu (CDN).

## Paramètres

Ouvrez le panneau _Paramètres_ en cliquant sur l’icône ![Configurer le projet](../../assets/icon-configure.png){width="36"} (configurer) sur le côté droit de la navigation du projet.

### Paramètres du projet

**[!UICONTROL Project Settings]** développe un menu de contrôles au niveau du projet pour gérer les utilisateurs, les variables, etc. :

| Option | Description |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Général | Gérez le fuseau horaire à utiliser pour la planification des sauvegardes ou de la maintenance. |
| Accès | Gérez l’ [accès utilisateur](user-access.md) aux types de projet et d’environnement. |
| Certificats | Affichez la liste des certificats SSL associés au projet. |
| Clé de déploiement | Ajoutez et affichez la clé publique au référentiel de code du projet. |
| Domaines | Ajoutez un nom de domaine au projet. Voir [Gestion des domaines](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Intégrations | Ajoutez et gérez des [intégrations](../integrations/overview.md), telles que des notifications d’intégrité et des webhooks. |
| Variables | Ajoutez des [ variables au niveau du projet ](../environment/variable-levels.md) disponibles lors de la création et de l’exécution dans tous les environnements. |

{style="table-layout:auto"}

### Paramètres d’environnement

Cliquez sur **[!UICONTROL Environments]** et sélectionnez un environnement spécifique dans la liste pour les contrôles permettant de gérer les paramètres du site, les variables d’environnement, etc. :

| Option | Description |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Général | Configurez le nom d’affichage, le type d’environnement et l’environnement parent.<br>Basculer entre les différents paramètres d’environnement : |
|           | **Activer les emails sortants** : envoyez des [emails sortants](outgoing-emails.md) à partir de l’environnement à l’aide du protocole SMTP. |
|           | **Masquer dans les moteurs de recherche** : bloquez les indexeurs et les moteurs de recherche du site. |
|           | **Contrôle d’accès HTTP** : activez la configuration de sécurité pour [!DNL Cloud Console] à l’aide d’un contrôle d’accès de connexion et d’adresse IP. |
|           | L’état est `active` ou `inactive`. La plupart de votre travail se fait dans un environnement actif. Vous pouvez désactiver ou supprimer l’environnement. |
| Variables | Affichez, créez et gérez des [variables de niveau environnement](../environment/variable-levels.md) disponibles au moment de l’exécution. |
| Domaines | Affichez la liste des [itinéraires configurés](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**NE PAS** utiliser la méthode de contrôle d’accès HTTP pour sécuriser les environnements d’évaluation et de production Pro. Cela rompt la mise en cache rapide. Utilisez plutôt la fonction [Blocking](../cdn/fastly-vcl-blocking.md) disponible dans le réseau de diffusion de contenu Fastly pour Adobe Commerce.

## Informations d’identification rapides et New Relic

Votre projet comprend [Fastly](../cdn/fastly.md) et [New Relic](../monitor/new-relic-service.md). Les détails du projet affichent des informations sur le plan de votre projet, ainsi que les licences et jetons importants pour ces intégrations. Seul le propriétaire de la licence a un accès initial aux informations d’identification et aux services. Fournissez ces informations d’identification aux ressources techniques et aux développeurs selon les besoins.

- [Fastly](https://www.fastly.com/) fournit des services de diffusion de contenu (CDN), d’optimisation d’images et de sécurité (DDoS et WAF) pour votre Adobe Commerce sur des projets d’infrastructure cloud. Voir [Obtenir des informations d’identification rapides](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) fournit des mesures d’application et des informations de performances pour les environnements d’évaluation et de production.

Utilisez l’ [ interface de ligne de commande de Cloud](../dev-tools/cloud-cli-overview.md) pour examiner vos jetons d’intégration, ID, etc. :

```bash
magento-cloud subscription:info services
```
