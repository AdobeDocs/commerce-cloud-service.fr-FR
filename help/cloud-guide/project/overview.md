---
title: Projet d’infrastructure cloud
description: Lire une présentation d’Adobe Commerce sur l’infrastructure cloud [!DNL Cloud Console] et découvrez comment accéder aux paramètres du compte.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Projet d’infrastructure cloud

Le projet Adobe Commerce on Cloud Infrastructure comprend tout le code des branches Git, des environnements associés et des scripts pour déployer le [!DNL Commerce] application. Les environnements contiennent des services pour la prise en charge de la variable [!DNL Commerce] , y compris une base de données, un serveur web et un serveur de mise en cache.

Adobe fournit un [!DNL Cloud Console] et des outils de développement pour gérer entièrement tous les aspects de votre projet. En tant que propriétaire du compte, vous disposez d’un accès complet à tous les environnements.

## [!DNL Cloud Console]

La variable [!DNL Cloud Console] fournit des méthodes interactives pour créer, gérer et déployer le code Commerce dans un format convivial. [Connectez-vous au [!DNL Cloud Console]](https://console.adobecommerce.com) pour afficher la liste de vos projets. Vous ne pouvez afficher que les projets auxquels vous êtes autorisé à accéder en tant qu’administrateur ou pour des types d’environnements spécifiques. Si vous êtes un partenaire de solutions Adobe, vous pouvez voir plusieurs projets pour les clients que vous prenez en charge.

>[!TIP]
>
>Si vous ne voyez aucun projet, vous devez contacter le [Propriétaire du compte ou administrateur de projet](../project/user-access.md) associée au projet et demande d’accès. Pour les nouveaux utilisateurs, voir [Rubrique d’intégration](../../get-started/onboarding.md#cloud-console) dans le _Prise en main_ guide.

La variable _Tous les projets_ affiche la liste de tous les projets auxquels vous êtes autorisé à accéder. Cliquez sur **[!UICONTROL Show filters]** et filtrez votre liste de projets par type, région ou plan.

![Liste des projets](../../assets/ui-allprojects-list.png)

### Présentation du projet

Sélection d’un projet à partir du _Tous les projets_ La liste ouvre la présentation du projet. La présentation du projet affiche toujours une barre de navigation du projet, qui comprend un sélecteur d’environnement et un bouton de configuration :

![Navigation dans le projet](../../assets/project-nav.png)

La présentation du projet, tant qu’aucun environnement n’est sélectionné, affiche un résumé des détails du projet dans la zone d’aperçu :

- Nom du projet
- Région, ID de projet
- Planification, stockage alloué, environnements, utilisateurs
- URL de storefront avec **[!UICONTROL Set a custom domain]** button

Et dans la présentation principale du projet :

- La vue Environnements affiche une liste ou une arborescence de ![branche active](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} environnements (inactifs).
- [Flux d’activité](activity-stream.md) affiche les activités en cours d’exécution, en attente et récentes du projet.
<!-- - Apps & Services—Shows a topology of service containers -->

Pour **Starter** projets, il existe une hiérarchie de branches commençant par `master` (Production). Toutes les branches que vous créez s’affichent en tant qu’enfants à partir de `master` branche. Adobe recommande de créer une `staging` , puis créez une `integration` branche pour le développement. Voir [Architecture de démarrage](../architecture/starter-architecture.md).

Pour **Pro**, il existe une hiérarchie de branches commençant par `production` to `staging` to `integration`. La variable ![Icône dédiée](../../assets/icon-dedicated.png){width="32"} indique que la branche se déploie vers un environnement dédié. Toutes les branches que vous créez s’affichent en tant qu’enfants des `integration` branche. Voir [Architecture Pro](../architecture/pro-architecture.md).

![Liste des environnements Pro](../../assets/pro-environments.png)

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
- URL de storefront avec **[!UICONTROL Set a custom domain]** button

Et dans la présentation de l&#39;environnement principal :

- [Flux d’activité](activity-stream.md) constitue la présentation de l’environnement principal et affiche les activités en cours d’exécution, en attente et récentes pour l’environnement sélectionné.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- [Onglet Sauvegardes](../storage/snapshots.md#create-a-manual-backup) fournit une liste des sauvegardes stockées, l’historique des actions de sauvegarde et le bouton Sauvegarde.

### Accès à storefront

Chaque environnement actif comporte une vitrine. Sélectionnez un environnement dans le volet de navigation supérieur, puis cliquez sur l’URL dans la présentation de l’environnement. Il y a également une **[!UICONTROL URLs]** liste située à droite au-dessus de la liste Activité.

L&#39;URL d&#39;accès Web peut contenir les éléments suivants :

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Identifiant unique** = 7 caractères alphanumériques aléatoires
- **Identifiant de projet** = ID de projet de 13 caractères
- **Région** = nom de la région AWS ou Azure, voir [Adresses IP régionales](regional-ip-addresses.md)

Les environnements de production et d’évaluation Pro comprennent trois noeuds auxquels vous pouvez accéder à l’aide des liens suivants :

- URL de l’équilibreur de charge :

   - `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

- Accès direct à l&#39;un des trois serveurs redondants :

   - `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

  L&#39;URL de production est utilisée par le réseau de diffusion de contenu (CDN).

## Paramètres

Ouvrez le _Paramètres_ en cliquant sur la ![icône de configuration de projet](../../assets/icon-configure.png){width="36"} (configurer) sur le côté droit de la navigation du projet.

### Paramètres du projet

**[!UICONTROL Project Settings]** développe un menu de contrôles au niveau du projet pour gérer les utilisateurs, les variables, etc. :

| Option | Description |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Général | Gérez le fuseau horaire à utiliser pour la planification des sauvegardes ou de la maintenance. |
| Accès | Gérer [accès utilisateur](user-access.md) vers les types de projet et d’environnement. |
| Certificats | Affichez la liste des certificats SSL associés au projet. |
| Clé de déploiement | Ajoutez et affichez la clé publique au référentiel de code du projet. |
| Domaines | Ajoutez un nom de domaine au projet. Voir [Gestion des domaines](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Intégrations | Ajouter et gérer [intégrations](../integrations/overview.md), comme les notifications d’intégrité et les webhooks. |
| Variables | Ajouter [variables au niveau du projet](../environment/variable-levels.md) qui sont disponibles lors de la création et de l’exécution dans tous les environnements. |

{style="table-layout:auto"}

### Paramètres d’environnement

Cliquez sur **[!UICONTROL Environments]** et sélectionnez un environnement spécifique dans la liste pour les contrôles permettant de gérer les paramètres du site, les variables d’environnement, etc. :

| Option | Description |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Général | Configurez le nom d’affichage, le type d’environnement et l’environnement parent.<br>Activation/désactivation des différents paramètres d’environnement : |
|           | **Activer les emails sortants**: Envoyer [emails sortants](outgoing-emails.md) à partir de l’environnement à l’aide du protocole SMTP. |
|           | **Masquer dans les moteurs de recherche**: bloque les indexeurs et les moteurs de recherche du site. |
|           | **Contrôle d’accès HTTP**: activez la configuration de la sécurité pour le [!DNL Cloud Console] à l’aide d’un contrôle de connexion et d’accès aux adresses IP. |
|           | Status est `active` ou `inactive`. La plupart de votre travail se fait dans un environnement actif. Vous pouvez désactiver ou supprimer l’environnement. |
| Variables | Afficher, créer et gérer [variables au niveau de l’environnement](../environment/variable-levels.md) disponible au moment de l’exécution. |
| Domaines | Afficher une liste de [routes configurées](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**NE PAS** utilisez la méthode de contrôle d’accès HTTP pour sécuriser les environnements d’évaluation et de production Pro. Cela rompt la mise en cache rapide. Utilisez plutôt la variable [Blocage](../cdn/fastly-vcl-blocking.md) fonctionnalité disponible dans le réseau de diffusion de contenu Fastly pour Adobe Commerce.

## Informations d’identification rapides et New Relic

Votre projet comprend [Fastly](../cdn/fastly.md) et [New Relic](../monitor/new-relic-service.md). Les détails du projet affichent des informations sur le plan de votre projet, ainsi que les licences et jetons importants pour ces intégrations. Seul le propriétaire de la licence a un accès initial aux informations d’identification et aux services. Fournissez ces informations d’identification aux ressources techniques et aux développeurs selon les besoins.

- [Fastly](https://www.fastly.com/) fournit des services de diffusion de contenu (CDN), d’optimisation des images et de sécurité (DDoS et WAF) pour votre Adobe Commerce sur des projets d’infrastructure cloud. Voir [Obtention des informations d’identification rapides](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) fournit des mesures d’application et des informations de performances pour les environnements d’évaluation et de production.

Utilisez la variable [Interface de ligne de commande du cloud](../dev-tools/cloud-cli-overview.md) pour consulter vos jetons d’intégration, identifiants, etc. :

```bash
magento-cloud subscription:info services
```
