---
title: Mettre à jour le package CEE-Outils
description: Découvrez comment mettre à niveau le package CEE-Outils pour tirer parti des derniers correctifs et fonctionnalités appliqués à Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Mettre à jour le package CEE-Outils

Une mise à jour du package `ece-tools` met également à jour les autres [modules Cloud Tools Suite for Commerce](../release-notes/cloud-tools-suite.md), qui sont des dépendances pour `ece-tools`. Par conséquent, vous devez utiliser une version d’Adobe Commerce sur l’infrastructure cloud qui prend en charge le package `ece-tools`.

{{ece-tools-package}}

**Conditions préalables** :

- Avant de mettre à jour `ece-tools`, passez en revue les [notes de mise à jour de Cloud Tools Suite for Commerce](../release-notes/cloud-tools-suite.md).
- Si vous effectuez une mise à jour de `ece-tools` 2002.0.22 ou version antérieure vers 2002.1.0, passez en revue les [modifications incompatibles sortantes](../release-notes/backward-incompatible-changes.md) et apportez les modifications requises à votre projet d’infrastructure cloud Adobe Commerce.
- Passez en revue les [mises à niveau et correctifs](../development/commerce-version.md#upgrade-from-older-versions) pour déterminer les versions CEE-Outils compatibles avec votre projet d’infrastructure cloud Adobe Commerce.

{{upgrade-tip}}

**Pour mettre à jour le package `ece-tools`** :

1. Sur votre poste de travail local, effectuez une mise à jour à l’aide du compositeur d’expérience.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Si vous ne pouvez pas mettre à jour au-delà de `ece-tools` version 2002.0.8, voir [ Projet de mise à niveau pour utiliser le package CEE-Outils](install-package.md).

1. Ajout, validation et modification du code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Après la validation du test, fusionnez cette branche avec la branche d’intégration.
