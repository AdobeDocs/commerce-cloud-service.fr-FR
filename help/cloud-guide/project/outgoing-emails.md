---
title: Configuration des emails sortants
description: Découvrez comment activer les emails sortants pour Adobe Commerce sur l’infrastructure cloud.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Configuration des emails sortants

Vous pouvez activer et désactiver les emails sortants pour chaque environnement à partir du [!DNL Cloud Console] ou à partir de la ligne de commande. Activez les e-mails sortants pour les environnements d’intégration et d’évaluation afin d’envoyer des e-mails d’authentification à deux facteurs ou de réinitialisation de mot de passe pour les utilisateurs de projet Cloud.

Par défaut, les emails sortants sont activés dans les environnements de production. La variable [!UICONTROL Enable outgoing emails] peut apparaître désactivée dans les paramètres d’environnement, quel que soit l’état, jusqu’à ce que vous définissiez la variable [`enable_smtp` property](#enable-emails-in-the-cli).

{{redeploy-warning}}

## Activation des emails dans [!DNL Cloud Console]

Utilisez la variable **[!UICONTROL Outgoing emails]** bascule dans le _Configuration de l’environnement_ pour activer ou désactiver la prise en charge des emails.

**Pour gérer la prise en charge des courriers électroniques à partir du[!DNL Cloud Console]**:

1. Connectez-vous au [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Sélectionnez un projet dans le _Tous les projets_ liste.
1. Dans le tableau de bord du projet, cliquez sur l’icône de configuration en haut à droite.
1. Cliquez sur **[!UICONTROL Environments]** et sélectionnez un environnement spécifique dans la liste.
1. Pour activer ou désactiver les emails sortants, basculez _Activer les emails sortants_ **Activé** ou **Off**.

   ![Activer la configuration des emails sortants](../../assets/outgoing-emails.png)

Une fois le paramètre modifié, l’environnement est créé et déployé avec la nouvelle configuration.

## Activation des emails dans l’interface de ligne de commande

Vous pouvez modifier la configuration de l’email pour un environnement actif à l’aide de l’option `magento-cloud` CLI `environment:info` pour définir la variable `enable_smtp` . Activer les mises à jour SMTP `MAGENTO_CLOUD_SMTP_HOST` Variable d’environnement avec l’adresse IP de l’hôte SMTP pour l’envoi du courrier.

**Gestion de la prise en charge des emails à partir de la ligne de commande**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Vérifiez le paramètre de l&#39;email sortant pour l&#39;environnement.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Modifiez la configuration de la prise en charge des courriers électroniques en définissant la variable `enable_smtp` Variable d’environnement vers `true` ou `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Attendez que l’environnement soit créé et déployé.

1. Utilisez un SSH pour vous connecter à l’environnement distant.

1. Vérifiez que l’email fonctionne ; envoyez un email de test à une adresse que vous pouvez vérifier.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```
