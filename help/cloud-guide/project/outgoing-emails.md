---
title: Configuration des emails sortants
description: Découvrez comment activer les emails sortants pour Adobe Commerce sur l’infrastructure cloud.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 75318be63adcbe23bb8b6699b1c59b2b4a3c1a4d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Configuration des emails sortants

Vous pouvez activer et désactiver les emails sortants pour les environnements d’intégration (et d’évaluation pour les environnements de démarrage uniquement) à partir de [!DNL Cloud Console] ou de la ligne de commande. Activez les courriers électroniques sortants pour envoyer des messages d’authentification à deux facteurs ou réinitialiser des mots de passe pour les utilisateurs de projet Cloud.

Par défaut, les emails sortants sont activés dans les environnements de production et d’évaluation (Pro uniquement). Cependant, le paramètre **[!UICONTROL Enable outgoing emails]** peut apparaître désactivé dans les paramètres de l’environnement, quel que soit l’état, jusqu’à ce que vous définissiez la propriété `enable_smtp` via la [ligne de commande](#enable-emails-in-the-cli) ou la [console cloud](outgoing-emails.md#enable-emails-in-the-cloud-console).

La mise à jour de la valeur de propriété `enable_smtp` par [ligne de commande](#enable-emails-in-the-cli) modifie également la valeur de paramètre [!UICONTROL Enable outgoing emails] pour cet environnement sur la console cloud.

>[!NOTE]
>
>L’activation/désactivation du paramètre **[!UICONTROL Enable outgoing emails]** n’activera pas/ne désactivera pas les emails dans les environnements d’évaluation ou de production Pro.

{{redeploy-warning}}

## Activation des emails dans la console Cloud

Utilisez le bouton d’activation/désactivation **[!UICONTROL Outgoing emails]** de la vue _Configurer l’environnement_ pour activer ou désactiver la prise en charge des courriers électroniques.

Si les emails sortants doivent être désactivés ou réactivés dans les environnements de production ou d’évaluation, vous pouvez envoyer un [ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>L’état du courrier électronique sortant peut ne pas être reflété pour les environnements d’évaluation ou de production Pro dans la console Cloud.

**Pour gérer la prise en charge des emails à partir de[!DNL Cloud Console]** :

1. Connectez-vous à [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Sélectionnez un projet dans la liste _Tous les projets_.
1. Dans le tableau de bord du projet, cliquez sur l’icône de configuration en haut à droite.
1. Cliquez sur **[!UICONTROL Environments]** et sélectionnez un environnement spécifique dans la liste (à l’exception de Test et Production pour Pro).
1. Pour activer ou désactiver les emails sortants, activez _Activer les emails sortants_ **On** ou **Off**.

   ![Activer la configuration des emails sortants](../../assets/outgoing-emails.png)

Une fois le paramètre modifié, l’environnement est créé et déployé avec la nouvelle configuration.

## Activation des emails dans l’interface de ligne de commande

Vous pouvez modifier la configuration des emails pour un environnement actif à l’aide de la commande `magento-cloud` CLI `environment:info` pour définir la propriété `enable_smtp`. L’activation du protocole SMTP met à jour la variable d’environnement `MAGENTO_CLOUD_SMTP_HOST` avec l’adresse IP de l’hôte SMTP pour l’envoi du courrier électronique.

**Pour gérer la prise en charge des emails à partir de la ligne de commande** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Vérifiez le paramètre de l&#39;email sortant pour l&#39;environnement.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Modifiez la configuration de la prise en charge des emails en définissant la variable d&#39;environnement `enable_smtp` sur `true` ou `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Attendez que l’environnement soit créé et déployé.

1. Utilisez un SSH pour vous connecter à l’environnement distant.

1. Vérifiez que l’email fonctionne ; envoyez un email de test à une adresse que vous pouvez vérifier.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. Vérifiez que le courrier électronique est bien récupéré par SendGrid.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
