---
title: Configuration des méthodes de paiement PayPal
description: Configurez les méthodes de paiement PayPal pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Checkout, Payments
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
source-git-commit: aa1a334ca1383559194ca75247679c6fb5411802
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Configuration des méthodes de paiement PayPal

Adobe Commerce sur l’infrastructure cloud fournit un outil d’intégration pour configurer les comptes de paiement express PayPal directement via l’administrateur. Cet outil est disponible pour les versions 2.1.8 et ultérieures de la CEE. Pour mieux prendre en charge la mise en ligne et le test des méthodes de paiement PayPal, vous pouvez activer et configurer votre compte PayPal Express Checkout pour les comptes sandbox ou de production.

Vous pouvez configurer l’environnement de test ou le compte de production dans chaque environnement :

* Pour les environnements d’intégration et d’évaluation, définissez les informations d’identification Sandbox.
* Pour votre environnement de production, définissez les informations d’identification Sandbox pour le test initial, puis remplacez par les informations d’identification de production en direct pour un magasin lancé.

## Compte PayPal

Bien qu’il soit préférable d’utiliser un compte marchand PayPal préparé et configuré, vous pouvez créer un compte ou mettre à niveau un compte personnel par l’intermédiaire de l’administrateur.

[!DNL PayPal onboarding] prend en charge la connexion avec les comptes suivants :

* Compte PayPal Business
* Compte personnel PayPal, conversion en compte professionnel. Si vous disposez d’un compte personnel PayPal existant, vous pouvez vous connecter à l’aide de ces informations d’identification et mettre à niveau ce compte vers un compte professionnel lorsque vous terminez la synchronisation.

Si vous ne disposez pas d’un compte PayPal existant, créez-en un. Entrez l’adresse électronique d’un nouveau compte. Si aucun compte PayPal correspondant n’est trouvé, suivez les invites pour créer un compte PayPal Business. Vous pouvez également créer un compte directement via [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection).

### Limites de PayPal

PayPal prend en charge la connexion de PayPal Express Checkout pour les pays du monde entier, à l&#39;exception des limitations suivantes :

* Inde et Japon (les futures mises à jour de PayPal pourraient prendre en charge ces comptes)
* Israël

Pour le Brésil, vous devez disposer d’un compte professionnel PayPal existant pour vous connecter. Vous ne pouvez pas convertir un compte personnel PayPal existant pour le Brésil au cours de ce processus. Si vous avez besoin d&#39;un compte, [créez un compte PayPal ](https://www.paypal.com/us/webapps/mpp/account-selection) commercial.

## Configuration du paiement express PayPal

Pour configurer le paiement express PayPal :

1. Accédez à l’administrateur de l’environnement.
1. Dans le volet de navigation de gauche, sélectionnez **Magasins** > **Configuration**, puis sélectionnez **Ventes** > **Méthodes de paiement**.
1. Pour PayPal, sélectionnez **Configurer**. Les champs de configuration s’affichent dans des sections extensibles pour le passage en caisse express, le crédit PayPal Advertising et les paramètres de base et avancés.
1. Connectez votre compte PayPal. Tant que le compte n’est pas connecté, les options d’activation sont désactivées. Pour plus d’informations sur les comptes disponibles et pris en charge pour la connexion et les limitations, voir [Compte PayPal](#paypal-account).

   * Pour connecter votre compte en direct PayPal, cliquez sur Se connecter avec PayPal et suivez les invites. Tout achat de client à l’aide d’un véritable PayPal et facturez activement des clients dans un magasin en ligne.
   * Pour connecter votre compte sandbox à des fins de test, cliquez sur Informations d’identification sandbox et suivez les invites. Tout achat de clients utilisant un sandbox PayPal se termine sans facturer activement les clients.

1. Configurez les paramètres de paiement express pour vous authentifier et utiliser l’API PayPal :

   * **Email associé à un compte marchand PayPal** (facultatif) saisissez l’adresse électronique associée à votre compte marchand PayPal. Cet email est sensible à la casse.
   * **Méthodes d’authentification API** en tant que signature d’API ou certificat API.
   * Nom d’utilisateur, mot de passe et signature de l’API capturés à partir de votre compte PayPal.
   * **Mode sandbox** sélectionnez Oui ou Non pour indiquer si les informations d’identification que vous avez saisies sont pour sandbox. Si vous avez saisi des informations d’identification de production, sélectionnez Non.
   * **L’API utilise le proxy** sélectionnez Oui ou Non pour définir si le système utilise un serveur proxy pour établir une connexion entre Adobe Commerce et le système de paiement PayPal. Si Oui, saisissez l’hôte proxy et le port.

1. Pour obtenir des informations détaillées et connaître les étapes de configuration de votre compte, reportez-vous à la section [Passage en caisse express PayPal](https://docs.magento.com/user-guide/payment/paypal-express-checkout.html) à partir de l’étape 2 : remplissez les paramètres requis.

Une fois le compte configuré et authentifié, vous pouvez activer et désactiver les options de paiement PayPal sous Paramètres PayPal requis :

* **Activer cette solution** affiche le mode de paiement PayPal aux clients par le biais du site web.
* **Activer l’expérience de passage en caisse dans le contexte**
* **Activer le crédit PayPal** permet aux clients de financer le crédit PayPal sans frais supplémentaires. PayPal paie la commande au préalable, en gérant tous les remboursements pour le crédit directement avec le client.

## Variables PayPal

Lors de l’utilisation de l’outil d’intégration PayPal avec Adobe Commerce sur l’infrastructure cloud, ajoutez la variable suivante à la section `variables:env` du fichier `magento.app.yaml`.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

Si vous effectuez une mise à niveau vers la version 2.1.8 ou ultérieure, vous devez ajouter cette variable.
