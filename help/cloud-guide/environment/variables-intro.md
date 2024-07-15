---
title: Variables d’environnement
description: Consultez la liste des variables d’environnement spécifiques à Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Variables d’environnement

Adobe Commerce sur l’infrastructure cloud vous permet d’affecter des variables d’environnement pour remplacer les options de configuration. Le package `ece-tools` définit des valeurs dans le fichier `env.php` en fonction des valeurs des [variables cloud](variables-cloud.md), des variables définies dans le fichier [!DNL Cloud Console] et du fichier de configuration `.magento.env.yaml`.

Les variables d’environnement du fichier `.magento.env.yaml` personnalisent l’environnement cloud en remplaçant votre configuration Commerce existante. Si une valeur par défaut est `Not Set`, le package `ece-tools` effectue l’action **NO** et utilise la valeur par défaut [!DNL Commerce] ou la valeur de la configuration `MAGENTO_CLOUD_RELATIONSHIPS`. Si la valeur par défaut est définie, le package `ece-tools` agit pour définir cette valeur par défaut.

Les types de variables d’environnement incluent :

- [ADMIN](variables-admin.md) : les variables remplacent les variables ADMIN du projet
- [MAGENTO_CLOUD](variables-cloud.md) : variables spécifiques à l’infrastructure cloud
- Variables utilisées dans le fichier `.magento.env.yaml` :
   - [Global](variables-global.md) : les variables affectent les étapes de création, de déploiement et de post-déploiement
   - [Build](variables-build.md) : les variables contrôlent les actions de création
   - [Deploy](variables-deploy.md) : les variables contrôlent les actions de déploiement
   - [Post-deploy](variables-post-deploy.md) : les variables contrôlent les actions après le déploiement

Les variables sont _hiérarchiques_, ce qui signifie que si une variable n’est pas remplacée, elle est héritée de l’environnement parent.

Vous pouvez définir des [variables ADMIN](variables-admin.md) à partir de [!DNL Cloud Console] ou à l’aide de l’interface de ligne de commande Adobe Commerce. Vous pouvez gérer d’autres variables d’environnement à partir du fichier [`.magento.env.yaml`](configure-env-yaml.md) pour gérer les actions de création et de déploiement dans tous vos environnements (y compris Pro Staging et Production), sans avoir besoin d’un ticket d’assistance.

>[!TIP]
>
>Les fichiers YAML sont sensibles à la casse et n’autorisent pas les onglets. Veillez à utiliser une mise en retrait cohérente dans tout le fichier `.magento.env.yaml` ou votre configuration risque de ne pas fonctionner comme prévu. Les exemples de cette documentation et de l’exemple de fichier utilisent la mise en retrait _à deux espaces_. Utilisez la commande [ece-tools validate](configure-env-yaml.md#validate-configuration-file) pour vérifier votre configuration.
