---
title: VCL personnalisée pour autoriser les requêtes
description: Filtrez les requêtes entrantes et autorisez l’accès par adresse IP pour les sites Adobe Commerce à l’aide d’une liste de contrôle d’accès Edge rapide et d’un extrait de code VCL personnalisé.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# VCL personnalisée pour autoriser les requêtes

Vous pouvez utiliser une liste ACL Edge Fastly avec un fragment de code VCL personnalisé pour filtrer les requêtes entrantes et autoriser l’accès par adresse IP. La liste ACL spécifie les adresses IP à autoriser.

Créez une liste autorisée pour limiter l’accès à votre environnement d’évaluation de sorte que seules les demandes provenant d’adresses IP spécifiées pour les développeurs internes et les services externes approuvés soient autorisées. Vous pouvez également créer une liste autorisée pour sécuriser l’accès à l’administrateur dans les environnements d’évaluation et de production.

L’exemple suivant montre comment utiliser un extrait de code VCL personnalisé avec une [liste de contrôle d’accès rapide (ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) pour sécuriser l’accès à l’administrateur d’un environnement de projet d’infrastructure cloud Adobe Commerce. Lorsque vous ajoutez le fragment de code VCL personnalisé à l’environnement cloud, Fastly autorise uniquement les requêtes provenant d’adresses IP incluses dans la liste de contrôle d’accès.

>[!TIP]
>
>Pour les environnements d’évaluation et d’intégration qui ne doivent pas être accessibles publiquement, utilisez l’option de contrôle d’accès HTTP disponible dans le [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) pour gérer l’accès à l’ensemble du site par adresse IP.

**Conditions préalables :**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Liste des adresses IP du client à inclure dans la liste autorisée

## Créer une liste de contrôle d’accès Edge pour autoriser les adresses IP du client

Les listes de contrôle d’accès Edge créent des listes d’adresses IP pour gérer l’accès à votre site. Dans cet exemple, vous créez une liste de contrôle d’accès Edge et ajoutez la liste des adresses IP du client autorisées à accéder à l’administrateur de votre environnement de projet.

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **ACL Edge**.

1. Créez le conteneur ACL :

   - Cliquez sur **Ajouter ACL**.

   - Sur la page *Conteneur ACL*, saisissez un **nom ACL**—`allowlist`.

   - Sélectionnez **Activer après la modification** pour déployer vos modifications dans la version de la configuration de service Fastly que vous modifiez.

   - Cliquez sur **Télécharger** pour joindre l’ACL à votre configuration de service Fastly.

1. Ajoutez la liste des adresses IP autorisées pour accéder à l’administrateur :

   - Cliquez sur l’icône Paramètres pour l’ACL `allowlist`.

   - Ajoutez et enregistrez la *valeur IP* pour chaque adresse IP du client.

   - Cliquez sur **Annuler** pour revenir à la page de configuration du système.

1. Cliquez sur **Enregistrer la configuration**.

1. Actualisez le cache en fonction de la notification dans la partie supérieure de la page.

## Créez un extrait de code VCL personnalisé pour sécuriser l’accès administrateur.

Le code de fragment de code VCL personnalisé suivant (format JSON) indique la logique permettant de filtrer les requêtes vers l’administrateur et d’autoriser l’accès si l’adresse IP du client correspond à une adresse dans l’ACL `allowlist`.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Avant de [créer un extrait de code personnalisé](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) à partir de cet exemple, passez en revue les valeurs pour déterminer si vous devez apporter des modifications. Ensuite, saisissez chaque valeur dans les champs respectifs, par exemple `type` dans le champ Type , `content` dans le champ Contenu .

- `name` — Nom du fragment de code VCL. Pour cet exemple, `allowlist`.

- `priority` — Détermine le moment où le fragment de code VCL s’exécute. La priorité est `5` pour s’exécuter immédiatement et vérifier si les demandes d’administration proviennent d’une adresse IP autorisée. L’extrait de code s’exécute avant que l’un des fragments de code VCL par défaut du Magento (`magentomodule_*`) n’ait une priorité de 50. Définissez la priorité de chaque fragment de code personnalisé sur une valeur supérieure ou inférieure à 50 selon le moment où vous souhaitez que votre fragment de code s’exécute. Les fragments de code dont les numéros de priorité sont plus bas s’exécutent en premier.

- `type` — Spécifie un emplacement pour insérer le fragment de code VCL versionné. Ce VCL est un type de fragment de code `recv` qui ajoute le code de fragment de code à la sous-routine `vcl_recv` sous le code VCL Fastly par défaut et au-dessus de tous les objets.

- `content` : extrait de code VCL à exécuter. Dans cet exemple, le code filtre les requêtes envoyées à l’administrateur et permet d’accéder à si l’adresse IP du client correspond à une adresse dans l’ACL `allowlist`. Si l’adresse ne correspond pas, la requête est bloquée avec une erreur `403 Forbidden`.

  Si l’URL de votre administrateur a été modifiée, remplacez l’exemple de valeur `/admin` par l’URL de votre environnement. Par exemple, `/company-admin`.

Dans l’exemple de code, la condition `!req.http.Fastly-FF` est importante lors de l’utilisation du [blindage d’origine](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Ne supprimez pas ou ne modifiez pas ce code.

Après avoir examiné et mis à jour le code de votre environnement, utilisez l’une des méthodes suivantes pour ajouter le fragment de code VCL personnalisé à votre configuration de service Fastly :

- [Ajoutez le fragment de code VCL personnalisé à partir de l’Admin](#add-the-custom-vcl-snippet). Cette méthode est recommandée si vous pouvez accéder à l’administrateur. (Nécessite le module [Fastly CDN pour Magento 2 version 1.2.58](fastly-configuration.md#upgrade) ou ultérieure.)

- Enregistrez l’exemple de code JSON dans un fichier (par exemple, `allowlist.json`) et [téléchargez-le à l’aide de l’API Fastly](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Utilisez cette méthode si vous ne pouvez pas accéder à l’administrateur.

## Ajout du fragment de code VCL personnalisé

{{admin-login-step}}

1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Système**.

1. Développez **Cache de page complète** > **Configuration rapide** > **Fragments de code VCL personnalisés**.

1. Cliquez sur **Créer un fragment de code personnalisé**.

1. Ajoutez les valeurs du fragment de code VCL :

   - **Nom** — `allowlist`

   - **Type** — `recv`

   - **Priorité** — `5`

   - Ajoutez le contenu du fragment de code **VCL** :

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Cliquez sur **Créer** pour générer le fichier de fragment de code VCL avec le modèle de nom `type_priority_name.vcl`, par exemple `recv_5_allowlist.vcl`.

1. Après le rechargement de la page, cliquez sur **Télécharger VCL vers Fastly** dans la section *Configuration Fastly* pour ajouter le fichier à la configuration de service Fastly.

1. Une fois le transfert terminé, actualisez le cache en fonction de la notification dans la partie supérieure de la page.

Valide rapidement la version mise à jour du code VCL pendant le processus de chargement. Si la validation échoue, modifiez le fragment de code VCL personnalisé pour résoudre le problème. Ensuite, chargez à nouveau le VCL.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
