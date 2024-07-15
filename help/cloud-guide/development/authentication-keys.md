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

- **fichier d’authentification** : fichier contenant vos [informations d’identification d’autorisation](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) Adobe Commerce dans votre répertoire racine d’infrastructure cloud Adobe Commerce.
- **variable d’environnement** : variable d’environnement permettant de configurer des clés d’authentification dans votre projet d’infrastructure cloud Adobe Commerce pour empêcher une exposition accidentelle.

>[!BEGINSHADEBOX]

**Note de sécurité**

Adobe recommande d’utiliser la méthode [environment variable](#composer-auth-environment-variable) avec votre projet cloud afin d’éviter l’exposition accidentelle de vos informations d’identification d’autorisation.

La méthode de fichier d’authentification est idéale lorsque vous utilisez Cloud Docker pour Commerce comme outil de développement local, mais veillez à ne pas télécharger le fichier `auth.json` vers un référentiel Git public. Vous pouvez ajouter le fichier `auth.json` au fichier [`.gitignore` ](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Fichier d’authentification

**Pour créer un fichier `auth.json`** :

1. Si votre répertoire racine de projet ne contient pas de fichier `auth.json`, créez-en un.

   - À l’aide d’un éditeur de texte, créez un fichier `auth.json` dans le répertoire racine de votre projet.
   - Copiez le contenu de l&#39; [exemple `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) dans le nouveau fichier `auth.json`.

1. Remplacez `<public-key>` et `<private-key>` par vos informations d’authentification Adobe Commerce.

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

**Pour ajouter des clés d’authentification à l’aide d’une variable d’environnement** :

1. Dans le _[!DNL Cloud Console]_, cliquez sur l’icône de configuration sur le côté droit de la navigation du projet.

   ![Configurer le projet](../../assets/icon-configure.png){width="36"}

1. Dans la liste _Paramètres du projet_, cliquez sur **[!UICONTROL Variables]**.

1. Cliquez sur **[!UICONTROL Create variable]**.

1. Dans le champ **[!UICONTROL Variable name]**, saisissez `env:COMPOSER_AUTH`.

1. Dans le champ _Value_ , ajoutez les éléments suivants et remplacez `<public-key>` et `<private-key>` par vos informations d’identification d’authentification Adobe Commerce :

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

1. Sélectionnez **[!UICONTROL Available during buildtime]** et désélectionnez **[!UICONTROL Available during runtime]**.

1. Cliquez sur **[!UICONTROL Create variable]**.

1. Supprimez le fichier `auth.json` de chaque environnement.
