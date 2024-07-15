---
title: Personnalisation des pages d’erreur et de maintenance
description: Découvrez comment personnaliser la page d’erreur par défaut qui s’affiche en cas d’échec des demandes au serveur d’origine Fastly.
feature: Cloud, Configuration, Security
exl-id: 16722821-b928-4872-8cef-7f049e600f0d
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Personnalisation des pages d’erreur et de maintenance

Lorsqu’une requête à l’origine Fastly échoue, la fonction Rapide renvoie des pages de réponse par défaut avec une mise en forme de base et un message générique pouvant dérouter les utilisateurs. Par exemple, Fastly renvoie la page d’erreur par défaut suivante lorsqu’une requête à l’origine Fastly échoue en raison d’une erreur 503.

![Page d’erreur Fastly par défaut](../../assets/cdn/fastly-503-example.png)

Vous pouvez mettre à jour la configuration de la boutique Adobe Commerce pour remplacer certaines pages de réponse par défaut par des pages qui contiennent des messages plus conviviaux et un style d’HTML amélioré, comme illustré dans l’exemple suivant.

![Page d’erreur personnalisée Fastly](../../assets/cdn/fastly-new-error-page.png)

Actuellement, vous pouvez personnaliser les pages de réponse rapide suivantes pour votre projet d’infrastructure cloud Adobe Commerce.

- [Erreurs du serveur : erreur interne du serveur, délai d’expiration ou pannes de maintenance du site (code d’erreur 500 ou supérieur)](#customize-the-503-error-page)
- [Blocage de la WAF survenant lorsque la WAF détecte le trafic de demandes suspectes (403 Forbidden)](#customize-the-waf-error-page)

**Exigences en matière de codage d’HTML :**

Le code d’HTML de la page personnalisée doit répondre aux exigences suivantes :

- Le contenu peut contenir jusqu’à 65 535 caractères.
- Spécifiez toutes les feuilles de style CSS intégrées dans la source de l’HTML.
- Regroupez les images dans la page d’HTML à l’aide de base64 afin qu’elles s’affichent même si Fastly est hors ligne. Voir [URI de données sur le site css-tricks](https://css-tricks.com/data-uris/).

## Personnalisation de la page d’erreur 503

Les clients voient la page 503-error par défaut dans les cas suivants :

- Lorsqu’une requête à l’origine Fastly renvoie un état de réponse supérieur à 500
- Lorsque l’origine Fastly est arrêtée, par exemple un dépassement de délai, une activité de maintenance ou des problèmes d’intégrité.

Vous pouvez personnaliser la page par défaut en adaptant le code d’HTML suivant afin d’inclure le style correspondant à votre thème de magasin Adobe Commerce et en modifiant le titre et la messagerie, le cas échéant.

```html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
         <title>503</title>
   </head>
   <body>
      <p>Service unavailable</p>
   </body></html>
```

Vérifiez que la source modifiée s’affiche correctement dans le navigateur. Ajoutez ensuite le code d’HTML personnalisé à la configuration Fastly.

Pour ajouter la page de réponse personnalisée à la configuration Fastly :

{{admin-login-step}}

1. Sélectionnez **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Dans le volet de droite, développez **Full Page Cache** > **Fastly Configuration** > **Custom Synthetic Pages**.

   ![Modifier la page d’erreur 503](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Sélectionnez **Définir l’HTML**.

1. Copiez et collez le code source de votre page de réponse personnalisée dans le champ HTML .

   ![Mise à jour de la page d’erreur 503](../../assets/cdn/fastly-customize-503-response.png)

1. Sélectionnez **Télécharger** en haut de la page pour télécharger la source d’HTML personnalisée sur le serveur Fastly.

1. Sélectionnez **Save Config** en haut de la page pour enregistrer le fichier de configuration mis à jour.

1. Actualisez le cache.

   - Dans la notification située en haut de la page, sélectionnez le lien *Gestion du cache*.

   - Sur la page Gestion du cache, sélectionnez **Vider le cache du Magento**.

## Personnalisation de la page d’erreur WAF

Les clients voient la page d’erreur WAF par défaut suivante lorsqu’une requête à l’origine Fastly échoue avec une erreur `403 Forbidden` provoquée par un événement de blocage [WAF](fastly-waf-service.md).

![Page d’erreur WAF](../../assets/cdn/fastly-waf-403-error.png)

L’exemple de code suivant illustre la source d’HTML de la page par défaut :

```html
<html>
  <head>
    <title>Magento 403 Forbidden</title>
  </head>
  <body>
    <p>The requested URL was rejected.</p>
    <p>For additional information, please contact support and provide this reference ID:</p>
    <p>"} req.http.x-request-id {"</p>
    <p><button onclick='history.back();'>Go Back</button></p>
  </body>
</html>
```

Vous pouvez utiliser l’option **Pages synthétiques personnalisées** > **Modifier la page WAF** dans le menu de configuration Fastly afin de personnaliser le code par défaut de votre projet Adobe Commerce sur l’infrastructure cloud. Lorsque vous modifiez le code, conservez la ligne suivante qui fournit l’ID de référence de l’événement de blocage WAF :

```html
<p>"} req.http.x-request-id {"</p>
```

>[!NOTE]
>
>L’option Modifier le fichier WAF n’est disponible que si le service Managed Cloud WAF est activé pour votre projet d’infrastructure cloud Adobe Commerce.

**Pour modifier la page d’erreur WAF** :

1. [Connectez-vous à l’administrateur](../../get-started/onboarding.md#access-your-admin-panel).

1. Sélectionnez **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Dans le volet de droite, développez **Full Page Cache** > **Fastly Configuration** > **Custom Synthetic Pages**.

   ![Option Modifier la page d’erreur WAF](../../assets/cdn/fastly-custom-synthetic-pages-edit-waf.png)

1. Sélectionnez **Modifier la page WAF**.

1. Renseignez les champs pour mettre à jour l&#39;HTML.

   ![Mettre à jour la page d’erreur WAF](../../assets/cdn/fastly-edit-waf-html.png)

   - **Status** — Sélectionnez l’état `403 Forbidden`.
   - **MIME type** — Type `text/html`.
   - **Contenu** — Modifiez la réponse par défaut de l’HTML pour ajouter une page CSS personnalisée et mettre à jour le titre et la messagerie, le cas échéant.

1. Sélectionnez **Télécharger** en haut de la page pour télécharger la source d’HTML personnalisée sur le serveur Fastly.

1. Sélectionnez **Save Config** en haut de la page pour enregistrer le fichier de configuration mis à jour.

1. Actualisez le cache.

   - Dans la notification située en haut de la page, sélectionnez le lien **Gestion du cache**.

   - Sur la page Gestion du cache, sélectionnez **Vider le cache du Magento**.

## Afficher le numéro du rapport d’erreur

Par défaut, masque Fastly toutes les erreurs Adobe Commerce derrière l&#39;erreur *503 Service Unavailable* . Pour afficher le numéro du rapport du journal des erreurs afin de retrouver et de consulter les détails de l’erreur dans les logs, ouvrez le site web omettant Fastly en procédant comme suit :

1. Récupérez l’adresse IP de votre boutique :

   - Pour les environnements d’évaluation et de production Pro :

     ```bash
     nslookup {your_project_id}.ent.magento.cloud
     ```

   - Pour les environnements d’intégration Pro et les environnements Starter :

     ```bash
     nslookup gw.{your_region}.magentosite.cloud
     ```

1. Ajoutez votre domaine d’application et votre adresse IP au fichier hosts de votre poste de travail local :

   ```text
   {server_IP} {store_domain}
   ```

1. Effacez le cache du navigateur et les cookies (ou passez en mode incognito).

1. Ouvrez à nouveau votre site web de magasin pour afficher le code d’erreur.

1. Utilisez le code d’erreur pour trouver les détails dans le fichier de rapport d’erreur :

   - [Connexion à l’environnement concerné à l’aide de SSH](../development/secure-connections.md#connect-to-a-remote-environment)

   - Recherchez le fichier `./var/report/{error_number}`.
