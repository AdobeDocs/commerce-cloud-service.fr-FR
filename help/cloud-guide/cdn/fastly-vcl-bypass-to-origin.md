---
title: VCL personnalisé pour contourner le cache rapide
description: Dépannez le trafic de demande au serveur d’origine en créant un extrait de code VCL personnalisé pour contourner le cache Fastly.
feature: Cloud, Configuration, Cache
exl-id: a2e9dc57-9b5e-4716-9965-a4324442ad00
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# VCL personnalisé pour contourner le cache rapide

Vous pouvez créer un extrait de code VCL personnalisé pour contourner le cache Fastly afin de pouvoir résoudre les problèmes de demande de trafic au serveur d’origine. Vous pouvez, par exemple, créer un extrait de code pour déterminer si les problèmes du site sont causés par la mise en cache ou pour résoudre les problèmes liés aux en-têtes.

Vous pouvez configurer l’extrait de code pour contourner la mise en cache rapide des requêtes provenant d’une adresse IP ou d’une URL spécifique.

>[!NOTE]
>
>Avant de fusionner une configuration VCL personnalisée dans un environnement de production, veillez à tester le code dans l’environnement d’évaluation.

**Conditions préalables :**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Pour contourner le cache rapide en fonction de l’adresse IP ou de l’URL**:

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système**.

1. Développer **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

1. Cliquez sur **Créer un fragment de code personnalisé**.

1. Ajoutez les valeurs du fragment de code VCL :

   - **Nom** — `bypass_fastly`

   - **Type** — `recv`

   - **Priorité** — `5`

   - **VCL** fragment de contenu —

     L’exemple suivant contourne Fastly une adresse IP spécifique :

     ```conf
     if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
       return(pass);
     }
     ```

     L’exemple suivant contourne Fastly un modèle d’URL spécifique :

     ```conf
     if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
     ```

     Pour établir une correspondance d’URL exacte, utilisez la variable `==` plutôt que l’opérateur `~` de l’opérateur. Voir [Référence VCL très rapide] pour plus d’informations.

1. Cliquez sur **Créer**.

   ![Créer un fragment de code VCL Contournement rapide](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. Une fois la page rechargée, cliquez sur **Chargement rapide de VCL** dans le *Configuration rapide* .

1. Une fois le transfert terminé, actualisez le cache en fonction de la notification dans la partie supérieure de la page.

   Valide rapidement la version mise à jour de VCL pendant le processus de chargement. Si la validation échoue, modifiez votre extrait de code VCL personnalisé pour résoudre les problèmes. Ensuite, chargez à nouveau le VCL.

Après avoir ajouté le fragment de code VCL, vous pouvez utiliser les commandes cURL pour envoyer des requêtes au serveur d’origine à partir de l’adresse IP ou de l’URL spécifiée, comme illustré dans l’exemple suivant :

```bash
curl -svo /dev/null www.example.com/index.html
```

Examinez ensuite la réponse pour résoudre les problèmes liés au contenu non mis en cache.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!--External link definitions-->

[Référence VCL très rapide]: https://docs.fastly.com/vcl/
