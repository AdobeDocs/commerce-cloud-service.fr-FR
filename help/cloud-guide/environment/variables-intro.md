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

Adobe Commerce sur l’infrastructure cloud vous permet d’affecter des variables d’environnement pour remplacer les options de configuration. La variable `ece-tools` définit les valeurs dans la variable `env.php` fichier en fonction des valeurs de [Variables cloud](variables-cloud.md), variables définies dans la variable [!DNL Cloud Console], et la variable `.magento.env.yaml` fichier de configuration.

Les variables d’environnement dans la variable `.magento.env.yaml` personnalisez l’environnement cloud en remplaçant votre configuration Commerce existante. Si une valeur par défaut est `Not Set`, puis la variable `ece-tools` prises de package **NON** et utilise la variable [!DNL Commerce] valeur par défaut ou de la variable `MAGENTO_CLOUD_RELATIONSHIPS` configuration. Si la valeur par défaut est définie, la variable `ece-tools` Le package agit pour définir cette valeur par défaut.

Les types de variables d’environnement incluent :

- [ADMIN](variables-admin.md): les variables remplacent les variables ADMIN du projet
- [MAGENTO_CLOUD](variables-cloud.md): variables spécifiques à l’infrastructure cloud
- Variables utilisées dans la variable `.magento.env.yaml` fichier :
   - [Global](variables-global.md): les variables affectent les étapes de création, de déploiement et de post-déploiement.
   - [Build](variables-build.md)—les variables contrôlent les actions de création
   - [Déployer](variables-deploy.md)—variables contrôle les actions de déploiement
   - [Post-déploiement](variables-post-deploy.md)—les variables contrôlent les actions après déploiement

Les variables sont _hiérarchique_, ce qui signifie que si une variable n’est pas remplacée, elle est héritée de l’environnement parent.

Vous pouvez définir [Variables ADMIN](variables-admin.md) de la [!DNL Cloud Console] ou en utilisant l’interface de ligne de commande d’Adobe Commerce. Vous pouvez gérer d’autres variables d’environnement à partir du [`.magento.env.yaml`](configure-env-yaml.md) pour gérer les actions de création et de déploiement dans tous vos environnements, y compris Pro Staging et Production, sans avoir besoin d’un ticket d’assistance.

>[!TIP]
>
>Les fichiers YAML sont sensibles à la casse et n’autorisent pas les onglets. Veillez à utiliser une mise en retrait cohérente dans l’ensemble des `.magento.env.yaml` ou votre configuration peut ne pas fonctionner comme prévu. Les exemples de cette documentation et de l’exemple de fichier utilisent _deux espaces_ retrait. Utilisez la variable [commande de validation d’outils-pièce](configure-env-yaml.md#validate-configuration-file) pour vérifier votre configuration.
