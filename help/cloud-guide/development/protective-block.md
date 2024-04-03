---
title: Bloc de protection
description: Découvrez la fonctionnalité de bloc de protection d’Adobe Commerce sur l’infrastructure cloud et comment elle protège votre site contre les vulnérabilités de sécurité connues.
feature: Cloud, Configuration, Security
topic: Security
exl-id: bc1def41-9521-4005-872e-9ecaab1d4d16
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Bloc de protection

Adobe Commerce sur l’infrastructure cloud dispose d’une fonction de blocage de protection qui, dans certaines circonstances, restreint l’accès aux sites web présentant des vulnérabilités de sécurité. Cette méthode de blocage partielle empêche l’exploitation des vulnérabilités de sécurité connues. Les logiciels obsolètes contiennent souvent des exploits, il est donc important de les protéger en bloquant partiellement l&#39;accès à ces sites.

## Fonctionnement du bloc de protection

Adobe Commerce conserve une base de données de signatures de vulnérabilités de sécurité connues dans les logiciels open source, qui sont couramment déployés sur l’infrastructure cloud. Le contrôle de sécurité analyse uniquement les vulnérabilités connues dans les projets Open Source ; il ne peut pas examiner les personnalisations que vous écrivez.

L’analyse de sécurité s’exécute :

- Lorsque vous poussez un nouveau code sur Git
- Ajout de nouvelles vulnérabilités à la base de données

Si une vulnérabilité critique est détectée dans votre application, elle rejette la notification push Git.

Deux types de blocs sont exécutés :

1. **Bloc complet**: pour les sites web de développement. Message d’erreur accompagnant `git push` fournit des informations détaillées sur la vulnérabilité.

1. **Bloc partiel**: pour les sites web de production, qui permettent au site de rester principalement en ligne. Selon la nature de la vulnérabilité, certaines parties d’une requête, telles qu’une chaîne de requête, des cookies ou tout en-tête supplémentaire, peuvent être supprimées des requêtes de GET. Toutes les autres demandes peuvent être bloquées entièrement, telles que la connexion, l’envoi de formulaire ou l’extraction de produit.

Le déblocage est automatisé lors de la résolution du risque de sécurité. Le bloc est supprimé peu de temps après l&#39;application d&#39;une mise à niveau de sécurité qui supprime la vulnérabilité.

## Exclusion du bloc de protection

Le bloc de protection est là pour vous protéger contre les vulnérabilités connues dans le logiciel que vous déployez Adobe Commerce sur l’infrastructure cloud.

Vous pouvez toutefois vous exclure du bloc de protection en ajoutant ce qui suit à la variable [`.magento.app.yaml`](../application/configure-app-yaml.md):

```yaml
   preflight:
      enabled: false
```

Vous pouvez explicitement exclure une vérification spécifique, par exemple :

```yaml
   preflight:
      enabled: true
      ignore_rules: [ "drupal:SA-CORE-2014-005" ]
```
