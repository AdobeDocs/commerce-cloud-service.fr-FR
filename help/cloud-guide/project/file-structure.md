---
title: Structure du projet
description: Découvrez la structure de fichiers et les modèles de projet pour Adobe Commerce sur l’infrastructure cloud.
exl-id: 6dc559bd-116b-4745-a85b-731508e113ff
source-git-commit: 47ef728ea46b137eeaabbdbada940143d8773ef0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Structure du projet

Un projet Adobe Commerce sur l’infrastructure cloud comprend des fichiers essentiels pour la configuration des informations d’identification et des applications. Ces fichiers sont disponibles dans en tant que modèle en fonction de la version d’Adobe Commerce. Reportez-vous aux modèles cloud basés sur la version d’Adobe Commerce dans la [`magento/magento-cloud` Référentiel GitHub](https://github.com/magento/magento-cloud).

Le tableau suivant décrit les fichiers inclus dans un projet cloud :

| Fichier | Description |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Fichier de configuration qui redirige `www` au domaine apex et `php` application pour servir le protocole HTTP. Voir [Configuration des itinéraires](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | Fichier de configuration qui définit une instance MySQL (MariaDB), Redis et OpenSearch ou Elasticsearch. Voir [Configuration des services](../services/services-yaml.md). |
| `/app` | La variable `code` est utilisé pour les modules personnalisés. La variable `design` Le dossier est utilisé pour [thèmes personnalisés](../store/custom-theme.md). La variable `etc` contient les fichiers de configuration de l’application. |
| `/m2-hotfixes` | Utilisé pour les correctifs personnalisés. |
| `/update` | Dossier de service utilisé par le module de support. |
| `.gitignore` | Spécifiez les fichiers et répertoires à ignorer. Voir [`.gitignore` reference](#ignoring-files). |
| `.magento.app.yaml` | Fichier de configuration qui définit les propriétés à utiliser pour créer votre application. Voir [Configuration de l’application](../application/configure-app-yaml.md). |
| `.magento.env.yaml` | Fichier de configuration pour les phases de création, de déploiement et de post-déploiement. La variable `ece-tools` comprend un exemple de ce fichier. Voir [Configuration des environnements](../environment/configure-env-yaml.md). |
| `composer.json` | Récupère Adobe Commerce et les scripts de configuration pour préparer votre application. Voir [Packages requis](../development/overview.md#required-packages). |
| `composer.lock` | Stocke les dépendances de version pour chaque module. Voir [Packages requis](../development/overview.md#required-packages). |
| `magento-vars.php` | Utilisé pour définir [magasins multiples](../store/multiple-sites.md) et les sites qui utilisent des variables. |

{style="table-layout:auto"}

>[!NOTE]
>
>Lorsque vous envoyez vos modifications locales au serveur distant, le script de déploiement utilise les valeurs définies par les fichiers de configuration dans la variable `.magento` , puis le script supprime le répertoire et son contenu. Votre environnement de développement local n’est pas affecté.

## Répertoire racine de l’application

L’emplacement du répertoire racine de l’application dépend de l’environnement.

- **Intégration de Starter et Pro**: `/app`
- **Production de démarrage**: `/<project-ID>`
- **Pro Staging**: `/<project-ID>_stg`
- **Pro Production**: `/<project-ID>`

### Répertoires accessibles en écriture

Les environnements d’intégration, d’évaluation et de production distants sont en lecture seule. Les répertoires suivants sont : *only* répertoires modifiables pour des raisons de sécurité :

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>Dans les environnements de production et d’évaluation, chaque noeud de la grappe à trois noeuds comporte une `/tmp` répertoire qui n’est pas partagé avec les autres noeuds.

## Ignorer les fichiers

Il y a une base `.gitignore` avec Adobe Commerce dans le référentiel de projet d’infrastructure cloud. Consultez la dernière version [fichier .gitignore dans le référentiel magento-cloud](https://github.com/magento/magento-cloud/blob/master/.gitignore). Pour ajouter un fichier qui se trouve dans la variable `.gitignore` , vous pouvez utiliser la variable `-f` (force) lors de l’évaluation d’une validation :

```bash
git add <path/filename> -f
```

## Modifier le modèle de base

Vous pouvez utiliser les étapes suivantes pour modifier la structure d’un projet existant afin de refléter le dernier modèle de base pour Adobe Commerce sur l’infrastructure cloud.

1. Cloner le projet vers un poste de travail local.

1. Mettez à jour le `composer.json` avec les valeurs suivantes pour la variable `extra` .

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Ajoutez la variable `.gitignore` fichier conçu pour le modèle de base. Par exemple, si vous avez besoin de la variable `.gitignore` pour le modèle de version 2.2.6, utilisez la méthode [.gitignore pour 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) comme référence.

1. Effacez le cache git.

   ```bash
   git rm -r --cached .
   ```

1. Ajoutez et validez les modifications.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
