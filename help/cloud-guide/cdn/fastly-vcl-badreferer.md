---
title: Blocage du courrier indésirable
description: Bloquez le courrier indésirable de référence de votre site à l’aide du dictionnaire Edge Fastly et d’un fragment de code VCL personnalisé.
feature: Cloud, Configuration, Security
exl-id: 665bac93-75db-424f-be2c-531830d0e59a
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Blocage du courrier indésirable

L’exemple suivant montre comment configurer [Fastly Edge Dictionary](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) avec un extrait de code VCL personnalisé pour bloquer le courrier indésirable de référence de votre Adobe Commerce sur le site d’infrastructure cloud.

>[!NOTE]
>
>Nous vous recommandons d’ajouter des configurations VCL personnalisées à un environnement d’évaluation dans lequel vous pouvez les tester avant de les exécuter par rapport à l’environnement de production.

**Conditions préalables :**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Recherchez dans les journaux de votre site de fausses URL de référence et créez une liste de domaines à bloquer.

## Création d’une liste bloquée de référent

Les dictionnaires Edge créent des paires clé-valeur accessibles aux fonctions VCL pendant le traitement des fragments de code VCL. Dans cet exemple, vous créez un dictionnaire Edge qui fournit la liste des sites Web de référents à bloquer.

{{admin-login-step}}

1. Cliquez sur **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **Dictionnaires Edge**.

1. Créez le conteneur de dictionnaire :

   - Cliquez sur **Ajouter un conteneur**.

   - Sur la page *Container*, saisissez un **nom du dictionnaire**—`referrer_blocklist`.

   - Sélectionnez **Activer après la modification** pour déployer vos modifications dans la version de la configuration de service Fastly que vous modifiez.

   - Cliquez sur **Télécharger** pour joindre le dictionnaire à votre configuration de service Fastly.

1. Ajoutez la liste des noms de domaine à bloquer au dictionnaire `referrer_blocklist` :

   - Cliquez sur l’icône Paramètres pour le dictionnaire `referrer_blocklist`.

   - Ajoutez et enregistrez des paires clé-valeur dans le nouveau dictionnaire. Pour cet exemple, chaque **Clé** est le nom de domaine d’une URL de référent à bloquer et **Valeur** est `true`.

     ![Ajouter des éléments de dictionnaire de référent incorrect](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   - Cliquez sur **Annuler** pour revenir à la page de configuration du système.

1. Cliquez sur **Enregistrer la configuration**.

1. Actualisez le cache en fonction de la notification dans la partie supérieure de la page.

Pour plus d’informations sur les dictionnaires Edge, voir [Création et utilisation des dictionnaires Edge](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) et [fragments de code VCL personnalisés](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) dans la documentation Fastly.

## Création d’un fragment de code VCL personnalisé pour bloquer le courrier indésirable d’un référent

Le code de fragment de code VCL personnalisé suivant (format JSON) indique la logique permettant de vérifier et de bloquer les requêtes. Le fragment de code VCL capture l’hôte d’un site web référent dans un en-tête, puis compare le nom d’hôte à la liste des URL dans le dictionnaire `referrer_blocklist`. Si le nom d’hôte correspond, la requête est bloquée avec une erreur `403 Forbidden`.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "set req.http.Referer-Host = regsub(req.http.Referer, \"^https?:\/\/?([^:\/s]+).*$\", \"\\1\"); if (table.lookup(referrer_blocklist, req.http.Referer-Host)) { error 403 \"Forbidden\"; }"
}
```

Avant de créer un fragment de code basé sur cet exemple, vérifiez les valeurs pour déterminer si vous devez apporter des modifications :

- `name` — Nom du fragment de code VCL. Pour cet exemple, nous avons utilisé `block_bad_referrer`.

- `dynamic` — La valeur 0 indique un [fragment de code normal](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) à charger vers le VCL versionné pour la configuration Fastly.

- `priority` — Détermine le moment où le fragment de code VCL s’exécute. La priorité est `5` pour exécuter ce code de fragment de code avant l’un des fragments de code VCL de Magento par défaut (`magentomodule_*`) auxquels une priorité de 50 est affectée. Définissez la priorité de chaque fragment de code personnalisé sur une valeur supérieure ou inférieure à 50 selon le moment où vous souhaitez que votre fragment de code s’exécute. Les fragments de code dont les numéros de priorité sont plus bas s’exécutent en premier.

- `type` — Spécifie un emplacement pour insérer le fragment de code dans la version VCL. Dans cet exemple, le fragment de code VCL est un fragment de code `recv`. Lorsque le fragment de code est inséré dans la version VCL, il est ajouté à la sous-routine `vcl_recv`, sous le code VCL Fastly par défaut et au-dessus de tout objet.

- `content` : extrait de code VCL à exécuter sur une ligne, sans saut de ligne.

Après avoir examiné et mis à jour le code de votre environnement, utilisez l’une des méthodes suivantes pour ajouter le fragment de code VCL personnalisé à votre configuration de service Fastly :

- [Ajoutez le fragment de code VCL personnalisé à partir de l’Admin](#add-the-custom-vcl-snippet). Cette méthode est recommandée si vous pouvez accéder à l’administrateur. (Nécessite [Fastly version 1.2.58](fastly-configuration.md#upgrade) ou ultérieure.)

- Enregistrez l’exemple de code JSON dans un fichier (par exemple, `allowlist.json`) et [téléchargez-le à l’aide de l’API Fastly](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Utilisez cette méthode si vous ne pouvez pas accéder à l’administrateur.

## Ajout du fragment de code VCL personnalisé

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

1. Cliquez sur **Créer un fragment de code personnalisé**.

1. Ajoutez les valeurs du fragment de code VCL :

   - **Nom** — `block_bad_referrer`

   - **Type** — `recv`

   - **Priorité** — `5`

   - **VCL** contenu de fragment de code —

     ```conf
     set req.http.Referer-Host = regsub(req.http.Referer,
     "^https?://?([^:/\s]+).*$", "1");
     if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
       error 403 "Forbidden";
     }
     ```

1. Cliquez sur **Créer**.

   ![Créer un fragment de code VCL de bloc de référent personnalisé](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. Après le rechargement de la page, cliquez sur **Télécharger VCL vers Fastly** dans la section *Configuration Fastly* .

1. Une fois le transfert terminé, actualisez le cache en fonction de la notification dans la partie supérieure de la page.

Valide rapidement la version mise à jour de VCL pendant le processus de chargement. Si la validation échoue, modifiez votre extrait de code VCL personnalisé pour résoudre les problèmes. Ensuite, chargez à nouveau le VCL.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
