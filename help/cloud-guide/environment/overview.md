---
title: Présentation des fichiers de configuration
description: Découvrez comment configurer l’environnement d’infrastructure cloud pour prendre en charge le déploiement et la gestion de votre boutique Adobe Commerce personnalisée.
feature: Cloud, Configuration, Services, Iaas, Paas
exl-id: f469a0ec-e459-413f-9725-66a0fbf34f01
source-git-commit: 47b66d0d2bbff14e76ce49182a68d5e6c9fb13a7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Présentation des fichiers de configuration

Les environnements d’Adobe Commerce sur l’infrastructure cloud comprennent des conteneurs avec des applications, des services et une base de données qui fournissent un système complet pour le code base et les fichiers de votre application Adobe Commerce.

Vous pouvez configurer les paramètres de l’application, les itinéraires, les actions de création et de déploiement et les notifications pour prendre en charge vos environnements de projet à l’aide des fichiers de configuration suivants :

| Configuration | Nom du fichier | Description |
| ------------- | -------- | ----------- |
| [Application](../application/configure-app-yaml.md) | `.magento.app.yaml` | Définit comment créer et déployer Adobe Commerce, y compris les services, les hooks et les tâches cron. |
| [Environnement](configure-env-yaml.md) | `.magento.env.yaml` | Centralise la gestion des actions de création et de déploiement dans tous vos environnements, y compris Pro Staging et Production, à l’aide de variables d’environnement. |
| [Itinéraires](../routes/routes-yaml.md) | `.magento/routes.yaml` | Configurez la mise en cache, les redirections et les inclusions côté serveur. |
| [Service](../services/services-yaml.md) | `.magento/services.yaml` | Définit les services utilisés par Adobe Commerce par nom et version. Par exemple, ce fichier peut inclure des versions de MariaDB, des extensions PHP, Redis, RabbitMQ et Elasticsearch ou OpenSearch. Vous devez ouvrir un ticket d’assistance pour transmettre ces modifications aux environnements d’évaluation et de production ProPlan. |
| [paramètres PHP](../application/php-settings.md#configure-php) | `php.ini` | Fichier facultatif pouvant être ajouté au projet. Les paramètres contenus dans ce fichier sont ajoutés à ceux conservés par l’infrastructure cloud. |

{style="table-layout:auto"}

## Mises à jour de configuration des environnements Pro

Pour les environnements d’évaluation et de production d’Adobe Commerce sur l’infrastructure cloud, vous pouvez mettre à jour de nombreuses options de configuration dans votre environnement de développement local et valider les modifications pour les appliquer à ces environnements. Cependant, vous devez [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour mettre à jour les options de configuration suivantes :

- Installez ou mettez à jour les services dans le `.magento/services.yaml` fichier .
- Modifiez la configuration de la variable `mounts` et `disk` dans le `.magento.app.yaml` fichier .

{{pro-self-service-warning}}
