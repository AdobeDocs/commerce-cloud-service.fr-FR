---
title: Définition du cache des fichiers statiques
description: Découvrez comment définir les options de stockage du cache dans le fichier de configuration de l'application  [!DNL Commerce] .
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Définition du cache des fichiers statiques

La durée de vie (TTL) du cache de vos fichiers multimédia et statiques est définie dans le fichier de configuration `.magento.app.yaml` à l’aide de la clé `expires`.

>[!NOTE]
>
>Avant de mettre à jour votre environnement de production, il est important de tester les modifications dans votre environnement d’évaluation. [Envoyez un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour obtenir de l’aide sur la mise à jour de la configuration sur ces environnements.

1. Spécifiez la durée TTL (en secondes) dans la propriété [`web`](web-property.md) du fichier `.magento.app.yaml`. Vous pouvez ajouter la clé `expires` sous `locations` ou sous `"/media"` et `"/static"`.

   Pour empêcher l’expiration du cache, utilisez la paire clé-valeur `expires: -1`. Voir l’exemple suivant :

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. Ajoutez, validez et poussez vos modifications de code.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
