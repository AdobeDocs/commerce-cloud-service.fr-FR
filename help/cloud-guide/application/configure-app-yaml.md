---
title: Configuration du déploiement des applications
description: Découvrez comment configurer les propriétés dans le fichier de configuration de l’application qui contrôle la manière dont l’application  [!DNL Commerce] est créée et déployée dans l’environnement cloud.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configuration du déploiement des applications

Le fichier `.magento.app.yaml` contrôle la manière dont votre application est créée et déployée. Bien qu’Adobe Commerce sur l’infrastructure cloud prenne en charge plusieurs applications par projet, généralement, un projet comporte une seule application avec le fichier `.magento.app.yaml` à la racine du référentiel.

`.magento.app.yaml` possède de nombreuses valeurs par défaut, voir [un exemple de fichier `.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Vérifiez toujours le `.magento.app.yaml` pour votre version installée. Ce fichier peut différer d’Adobe Commerce sur les versions de l’infrastructure cloud.

Utilisez le fichier `.magento.app.yaml` pour définir les valeurs de configuration suivantes :

- [Propriétés](properties.md) : définissez les valeurs de propriété pour l’instance d’application.
- [Propriété Variables](variables-property.md) : vérifiez les variables d’environnement requises pour la version de l’application [!DNL Commerce].
- [Paramètres PHP](php-settings.md) : configurez les options PHP du runtime.
- [Définir le cache pour les fichiers statiques](set-cache.md) : définissez la durée de vie du cache pour vos fichiers multimédia et statiques.
