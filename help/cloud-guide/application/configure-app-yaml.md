---
title: Configuration du déploiement des applications
description: Découvrez comment configurer les propriétés dans le fichier de configuration de l’application qui contrôle la manière dont la variable [!DNL Commerce] l’application est créée et déployée dans l’environnement cloud.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configuration du déploiement des applications

La variable `.magento.app.yaml` contrôle la manière dont votre application est créée et déployée. Bien qu’Adobe Commerce sur l’infrastructure cloud prenne en charge plusieurs applications par projet, généralement, un projet comporte une seule application avec l’événement `.magento.app.yaml` à la racine du référentiel.

La variable `.magento.app.yaml` contient de nombreuses valeurs par défaut, voir [un exemple `.magento.app.yaml` fichier](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Toujours vérifier la variable `.magento.app.yaml` pour la version installée. Ce fichier peut différer d’Adobe Commerce sur les versions de l’infrastructure cloud.

Utilisez la variable `.magento.app.yaml` pour définir les valeurs de configuration suivantes :

- [Propriétés](properties.md)—Définissez les valeurs de propriété de l’instance de l’application.
- [Propriété Variables](variables-property.md): vérifiez les variables d’environnement requises pour la variable [!DNL Commerce] version de l’application.
- [paramètres PHP](php-settings.md): configurez les options PHP du runtime.
- [Définition Du Cache Pour Les Fichiers Statiques](set-cache.md): définissez la durée de vie du cache pour vos fichiers multimédia et statiques.
