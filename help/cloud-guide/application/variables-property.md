---
title: Propriété Variables
description: Utilisez la propriété de variables pour personnaliser les options de configuration du magasin pour l'application  [!DNL Commerce] .
feature: Cloud, Configuration
exl-id: 5cd92fbb-8bff-48b1-9658-500140591344
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Propriété Variables

Vous pouvez utiliser des variables d’environnement basées sur l’application pour personnaliser les configurations de magasin. Ces variables utilisent une syntaxe spécifique. Voir [Remplacer les paramètres de configuration](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) dans le _Guide de configuration_.

Les variables d’environnement suivantes incluses dans le fichier `.magento.app.yaml` sont requises pour des versions spécifiques de l’application [!DNL Commerce].

Requis pour Adobe Commerce 2.2.x vers 2.3.x :

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Pour Adobe Commerce 2.4.x, définissez les variables suivantes :

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
