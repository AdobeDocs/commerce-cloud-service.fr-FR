---
title: Récupération de l’échec du composant
description: Découvrez comment récupérer si un composant ne se déploie pas correctement dans Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Deploy
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
source-git-commit: b44d97f82ef09288807c648010202422c9ac04eb
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Récupération de l’échec du composant

Cette rubrique explique comment récupérer si le déploiement d’un composant échoue. Les exemples types incluent les composants dont les dépendances ne sont pas satisfaites par votre environnement distant, comme les versions PHP incompatibles.

Vous pouvez récupérer d’un déploiement en échec de l’une des manières suivantes :

- [Restauration d’une sauvegarde](../storage/snapshots.md#restore-a-snapshot)
- Nettoyer le projet et le code des modifications précédentes et redéployer

## Nettoyer, supprimer et redéployer

Pour nettoyer le déploiement précédent, identifiez le composant qui a été ajouté ou mis à jour, puis supprimez-le. Tout d’abord, connectez-vous à l’environnement distant et effacez manuellement le contenu du répertoire `var`. Supprimez ensuite le composant du fichier `composer.json` et redéployez l’environnement.

**Pour nettoyer les `var` répertoires** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Effacez les répertoires `var`.

   ```shell
   rm -rf var/*
   ```

1. Déconnectez-vous.

**Pour supprimer le composant** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Effacez le cache.

   ```bash
   composer clear-cache
   ```

1. Supprimez le composant du fichier `composer.json`.

   ```bash
   composer remove <component-name>:<version>
   ```

   Si le message suivant s’affiche, vous n’avez rien à faire de plus :

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Patientez pendant la mise à jour des dépendances.

1. Ajout, validation et modification du code push.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Pour en savoir plus sur la restauration d’un environnement sans sauvegarde, voir [Restaurer un environnement](../development/restore-environment.md).

{{stuck-deployment-tip}}
