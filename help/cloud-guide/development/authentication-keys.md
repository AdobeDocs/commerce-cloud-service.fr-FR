---
title: Clés d’authentification
description: Découvrez comment appliquer des clés d’authentification à un projet de développement dans Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Clés d’authentification

Vous devez disposer d’une clé d’authentification pour accéder au référentiel Adobe Commerce et activer les commandes d’installation et de mise à jour d’Adobe Commerce sur le projet d’infrastructure cloud. Il existe deux méthodes pour spécifier les informations d’identification d’autorisation du compositeur.

- **fichier d&#39;authentification**: fichier contenant votre Adobe Commerce. [informations d’identification d’autorisation](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) dans votre répertoire racine d’infrastructure cloud Adobe Commerce.
- **variable d&#39;environnement**: variable d’environnement permettant de configurer des clés d’authentification dans votre projet d’infrastructure cloud Adobe Commerce pour éviter une exposition accidentelle.

>[!BEGINSHADEBOX]

**Note de sécurité**

Adobe recommande d’utiliser la variable [variable d&#39;environnement](#composer-auth-environment-variable) avec votre projet cloud pour éviter l’exposition accidentelle de vos informations d’identification d’autorisation.

La méthode de fichier d’authentification est idéale lors de l’utilisation de Cloud Docker pour Commerce en tant qu’outil de développement local, mais veillez à ne pas transférer la variable `auth.json` vers un référentiel Git public. Vous pouvez ajouter la variable `auth.json` vers le fichier [`.gitignore` fichier](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Fichier d’authentification

**Pour créer une `auth.json` fichier**:

1. Si vous n’avez pas de `auth.json` dans le répertoire racine du projet, créez-en un.

   - Créez un `auth.json` dans le répertoire racine du projet.
   - Copiez le contenu de la [sample `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) dans la nouvelle `auth.json` fichier .

1. Remplacer `<public-key>` et `<private-key>` avec vos informations d’authentification Adobe Commerce.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Enregistrez vos modifications et quittez l’éditeur de texte.

## Variable d’environnement du compositeur

La méthode suivante est le meilleur moyen d’empêcher l’exposition accidentelle d’informations d’identification sensibles dans un référentiel Git public.

**Pour ajouter des clés d’authentification à l’aide d’une variable d’environnement**:

1. Dans le _[!DNL Cloud Console]_, cliquez sur l’icône de configuration sur le côté droit de la navigation du projet.

   ![Configuration du projet](../../assets/icon-configure.png){width="36"}

1. Dans le _Paramètres du projet_ liste, cliquez sur **[!UICONTROL Variables]**.

1. Cliquez sur **[!UICONTROL Create variable]**.

1. Dans le **[!UICONTROL Variable name]** champ, entrer `env:COMPOSER_AUTH`.

1. Dans le _Valeur_ , ajoutez les éléments suivants et remplacez `<public-key>` et `<private-key>` avec vos informations d’identification d’authentification Adobe Commerce :

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Sélectionner **[!UICONTROL Available during buildtime]** et désélectionner **[!UICONTROL Available during runtime]**.

1. Cliquez sur **[!UICONTROL Create variable]**.

1. Supprimez le `auth.json` à partir de chaque environnement.
