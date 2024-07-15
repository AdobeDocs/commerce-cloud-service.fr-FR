---
title: Variables ADMIN
description: Consultez la liste des variables d’environnement utilisées lors de l’installation d’Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Variables d’administration

Les utilisateurs disposant d’un accès administratif à Adobe Commerce sur le projet d’infrastructure cloud peuvent utiliser les variables d’environnement de projet suivantes pour remplacer les paramètres de configuration du compte d’utilisateur administrateur afin d’accéder à l’interface utilisateur d’administration.

## Identifiants d’administrateur

Vous pouvez remplacer les informations d’identification de l’utilisateur administrateur lors de l’installation de Commerce par les variables ADMIN dans le tableau suivant.

Si vous souhaitez modifier les valeurs après l’installation, connectez-vous à votre environnement à l’aide du SSH et utilisez la commande [`admin:user` de l’interface de ligne de commande Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) pour créer ou modifier les informations d’identification de l’utilisateur administrateur.

| Variable | Par défaut | Description |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | Adresse électronique du propriétaire de la licence | Nom d’utilisateur pour l’utilisateur administrateur qui peut créer d’autres utilisateurs, y compris des utilisateurs administratifs. |
| `ADMIN_EMAIL` |                             | Adresse électronique de l’utilisateur administrateur. Cette adresse est utilisée pour envoyer des notifications de réinitialisation de mot de passe. |
| `ADMIN_PASSWORD` |                             | Mot de passe de l’utilisateur administrateur. Lorsque le projet est créé, un mot de passe aléatoire est généré et un courrier électronique est envoyé au propriétaire de la licence. Lors de la création du projet, le propriétaire de la licence doit avoir déjà modifié le mot de passe. Contactez le propriétaire de la licence pour le mot de passe mis à jour. |
| `ADMIN_LOCALE` | `en_US` | Paramètre régional par défaut utilisé par l’administrateur. |

## URL d’administration

Utilisez la variable d’environnement suivante pour sécuriser l’accès à votre interface utilisateur d’administration. Si elle est spécifiée, cette valeur remplace l’URL par défaut lors de l’installation.

`ADMIN_URL` : URL relative pour accéder à l’interface utilisateur d’administration. L’URL par défaut est `/admin`. Pour des raisons de sécurité, Adobe vous recommande de remplacer la valeur par défaut par une URL d’administration personnalisée unique, ce qui n’est pas facile à deviner.

### Modification de l’URL d’administration

Adobe recommande de modifier la variable au niveau de l’environnement pour l’URL d’administration après l’installation. Configurez ce paramètre pour des raisons de sécurité avant d’effectuer un embranchement à partir de l’environnement `master` cloné. Toutes les branches créées à partir de la branche `master` héritent des variables au niveau de l’environnement et de leurs valeurs.

Utilisez la commande `magento-cloud variable:update` pour mettre à jour la valeur de la variable. (La commande `variable:set` est obsolète et n’est pas disponible.) L’exemple suivant met à jour ADMIN_URL vers `newAdmin_A8v10` :

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>La valeur `ADMIN_URL` accepte les lettres (a-z ou A-Z), les nombres (0-9) et le caractère de soulignement (_) pour un chemin d’accès d’administrateur personnalisé. Les espaces ou autres caractères sont **non** acceptés.

**Pour modifier l’URL à l’aide de[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Sélectionnez un projet dans la liste _Tous les projets_.

1. Dans la vue d’ensemble du projet, sélectionnez l’environnement et cliquez sur l’icône de configuration.

   ![Configuration du projet](../../assets/icon-configure.png){width="36"}

1. Sélectionnez l’onglet **Variables** .

1. Cliquez sur **Créer une variable**.

1. Saisissez les informations suivantes :

   - **Nom de variable** = `ADMIN_URL`
   - **value** = Nouvelle URL. Par exemple, définissez l’URL d’administration sur `magento_A8v10`.

   Par défaut, `Available during runtime` et `Make inheritable` sont sélectionnés.

1. Cliquez sur **Créer une variable** et attendez que le déploiement soit terminé. Ce bouton n’est visible que lorsque les champs obligatoires contiennent des valeurs.
