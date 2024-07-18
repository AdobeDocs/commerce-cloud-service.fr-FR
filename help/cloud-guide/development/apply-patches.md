---
title: Appliquer les correctifs
description: Découvrez comment appliquer des correctifs dans Adobe Commerce sur le projet d’infrastructure cloud.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Appliquer les correctifs

[Correctifs de cloud pour Commerce](https://github.com/magento/magento-cloud-patches) et l’[ outil de correctifs de qualité](https://github.com/magento/quality-patches) livrent des correctifs à votre application Adobe Commerce installée.

- Le module Correctifs Cloud pour Commerce fournit les correctifs requis avec des correctifs critiques.
- Les correctifs de qualité proposent des correctifs de qualité facultatifs à faible impact sous la forme de [correctifs individuels](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) qui ne contiennent pas de modifications rétrocompatibles.

Pour consulter la liste complète des correctifs publiés, reportez-vous à la section [Correctifs disponibles](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) du _Guide des outils d’exploitation Commerce_.

Les deux packages améliorent l’intégration de toutes les versions d’Adobe Commerce avec les environnements cloud et prennent en charge la livraison rapide de correctifs critiques, facultatifs et personnalisés. Vous pouvez utiliser ces packages pour appliquer, rétablir et afficher des informations générales sur tous les correctifs individuels disponibles pour Commerce.

>[!TIP]
>
>Vous pouvez utiliser l’ [ outil de correctifs de qualité ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) et les correctifs cloud pour Commerce en tant que packages autonomes pour les projets Magento Open Source et Adobe Commerce. Nous vous recommandons d’utiliser l’outil de correctifs de qualité pour les projets non cloud.

Lorsque vous déployez des modifications sur l’environnement distant, le package `ece-tools` utilise `magento/magento-cloud-patches` et `magento/quality-patches` pour rechercher les correctifs en attente et les applique automatiquement dans l’ordre suivant :

1. Appliquez tous les correctifs Commerce requis inclus dans le package Cloud Patches for Commerce .
1. Appliquez certains correctifs Commerce facultatifs inclus dans l’outil Correctifs de qualité.
1. Appliquez des correctifs personnalisés dans le répertoire `/m2-hotfixes` par ordre alphabétique par nom de correctif.

>[!NOTE]
>
>Lorsque vous mettez à jour le package `ece-tools` ou le package Cloud Patches for Commerce, les derniers correctifs requis sont appliqués la prochaine fois que vous déployez votre projet. Vous pouvez également les déployer immédiatement à l’aide de la commande d’interface de ligne de commande `ece-patches apply` et redéployer votre environnement cloud. Vous ne pouvez pas ignorer les [correctifs requis](https://github.com/magento/magento-cloud-patches/tree/develop/patches) pendant le processus de déploiement.

## Conditions préalables

{{upgrade-tip}}

L’outil de correctifs de qualité est une dépendance pour les correctifs Cloud pour Commerce et le package `ece-tools`. Pour appliquer les derniers correctifs, [la dernière version de CEE-Tools](../dev-tools/update-package.md) doit être installée. La version minimale requise des outils CEE est 2002.1.2.

## Afficher les correctifs disponibles et l’état

Pour afficher la liste des correctifs individuels disponibles :

```bash
php ./vendor/bin/ece-patches status
```

Exemple de réponse :

```
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

Le tableau d’état contient les types d’informations suivants :

- **Type** :
   - `Optional` : tous les correctifs de l’outil de correctifs de qualité et du package de correctifs cloud sont facultatifs pour les installations Adobe Commerce et Magento Open Source. Pour Adobe Commerce sur l’infrastructure cloud, tous les correctifs sont facultatifs.
   - `Required` : tous les correctifs du package Cloud Patches pour Commerce sont requis pour les clients Cloud.
   - `Deprecated` : le correctif individuel est marqué comme obsolète et nous vous recommandons de le rétablir si vous l’avez appliqué. Une fois que vous avez rétabli un correctif obsolète, il ne s’affichera plus dans le tableau d’état.
   - `Custom` : tous les correctifs du répertoire &#39;m2-hotfixes&#39;.

- **Status** :
   - `Applied` : le correctif a été appliqué.
   - `Not applied` : le correctif n’a pas été appliqué.
   - `N/A` : l’état du correctif ne peut pas être défini en raison de conflits.

- **Détails** :
   - `Affected components` : liste des modules affectés.
   - `Required patches` : liste des correctifs requis (dépendances).
   - `Recommended replacement` : correctif recommandé pour remplacer un correctif obsolète.

## Application d’un correctif dans un environnement local

Vous pouvez appliquer des correctifs manuellement dans un environnement local et les tester avant de les déployer.

**Pour appliquer des correctifs individuels dans un environnement de développement local** :

1. Ajoutez la variable &#39;QUALITY_PATCH&#39; au fichier `.magento.env.yaml` et répertoriez les correctifs requis sous .

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. Appliquez les correctifs à partir de la racine du projet.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   La commande `ece-patches apply` applique les correctifs dans l’ordre suivant :
   - Correctifs requis
   - Correctifs individuels facultatifs
   - Correctifs personnalisés du répertoire `/m2-hotfixes`

1. Effacez le cache.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Testez les correctifs, apportez les modifications nécessaires aux correctifs personnalisés.

## Application d’un correctif dans un environnement distant

>[!WARNING]
>
>Nous vous recommandons vivement de tester tous les correctifs d’une intégration ou d’un environnement d’évaluation avant de procéder au déploiement dans l’environnement de production.

**Pour appliquer des correctifs dans un environnement distant** :

1. Ajoutez la variable `QUALITY_PATCHES` au fichier `.magento.env.yaml` et répertoriez les correctifs requis sous .

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >Après la mise à niveau vers une nouvelle version d’Adobe Commerce, vous devez réappliquer les correctifs si ceux-ci ne sont pas inclus dans la nouvelle version.

1. Ajoutez, validez et envoyez le fichier `.magento.env.yaml` mis à jour.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Appliquer un correctif personnalisé

Lorsque vous déployez, les outils ECE appliquent tous les correctifs d’Adobe et tous les correctifs personnalisés que vous ajoutez au répertoire `/m2-hotfixes` dans la racine du projet.

>[!NOTE]
>
>Tous les noms de fichier de correctif doivent se terminer par l’extension `.patch`.

**Pour appliquer et tester un correctif personnalisé dans un environnement cloud** :

1. Dans la racine du projet, créez un répertoire appelé `m2-hotfixes` s’il n’existe pas.

   ```bash
   mkdir m2-hotfixes
   ```

1. Copiez le fichier de correctif dans le répertoire `/m2-hotfixes`.

1. Ajout, validation et modification du code push.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Veillez à tester tous les correctifs dans un environnement de pré-production. Pour Adobe Commerce sur l’infrastructure cloud, vous pouvez créer des branches avec la commande d’interface de ligne de commande `magento-cloud environment:branch <branch-name>`.

## Rétablissement d’un correctif personnalisé

Pour rétablir ou désinstaller un correctif personnalisé précédemment appliqué :

1. Supprimez le fichier de correctif du répertoire `/m2-hotfixes`.

1. Ajout, validation et modification du code push.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Veillez à effectuer un test dans un environnement de pré-production. Pour Adobe Commerce sur l’infrastructure cloud, vous pouvez créer des branches avec la commande d’interface de ligne de commande `magento-cloud environment:branch <branch-name>`.

## Application de correctifs à un projet non cloud

Utilisez l’ [ outil de correctifs de qualité](https://github.com/magento/quality-patches) pour les projets Magento Open Source et Adobe Commerce.

## Rétablir un correctif dans un environnement local

Vous pouvez annuler tous les correctifs précédemment appliqués dans un environnement de développement local à l’aide de l’interface de ligne de commande `ece-patches`.

Pour annuler tous les correctifs appliqués :

```bash
php ./vendor/bin/ece-patches revert
```

Cette commande rétablit tous les correctifs dans l’ordre suivant :

- Annule tous les correctifs personnalisés appliqués du répertoire /m2-hotfixes .
- Annule tous les correctifs individuels facultatifs appliqués.
- Annule tous les correctifs requis appliqués.

## Journalisation

L’outil Correctifs de qualité consigne toutes les opérations dans le fichier `<Project_root>/var/log/patch.log`.
