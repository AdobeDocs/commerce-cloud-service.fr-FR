---
title: Instructions de test
description: Découvrez les types de test et les bonnes pratiques pour lancer Adobe Commerce sur l’infrastructure cloud.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Instructions de test

Après avoir configuré et personnalisé votre projet Adobe Commerce sur l’infrastructure cloud, il est recommandé de tester minutieusement votre application avant de lancer le site web du magasin. Les tests permettent de gérer correctement les attentes relatives à la taille de la grappe et de les adapter de manière appropriée aux besoins futurs de l’entreprise.

## Tests fonctionnels

Lors du développement, il est important d’effectuer des tests fonctionnels de bout en bout sur votre projet d’infrastructure cloud Adobe Commerce. Consultez les instructions suivantes pour effectuer des tests fonctionnels dans l’environnement Docker :

- **Test d’application** : utilisez la [structure de test fonctionnel Magento (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) pour tester les applications dans l’environnement Cloud Docker.

- **Test du code** : utilisez la [structure de test de la codeception pour PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) pour valider le code destiné à la contribution aux référentiels de modules Cloud.

## Bonnes pratiques avant le lancement

Tenez compte des types de test suivants comme une bonne pratique à exécuter avant le lancement du site :

- **Test de charge** : effectuez un test de charge pour comprendre le comportement du système sous une charge attendue. Par exemple, testez un nombre simultané d’utilisateurs actifs sur l’application, en demandant à chaque utilisateur d’effectuer un nombre spécifique de transactions pendant la durée définie. Ce test révèle le temps de réponse des transactions importantes critiques de l’entreprise, telles que le comportement de la base de données ou du serveur d’applications. Un test de charge peut aider à identifier les goulets d’étranglement.

- **Test de contrainte** : contestez les limites supérieures de capacité du système pour déterminer si le système fonctionne suffisamment lorsque la charge actuelle dépasse largement la charge maximale attendue.

- **Analyse de sécurité** : Adobe fournit un [ outil d’analyse de sécurité](../launch/overview.md#set-up-the-security-scan-tool) gratuit pour vos sites.

- **Test de pénétration** : il s’agit d’une cyber-attaque simulée autorisée sur un système informatique conçu pour évaluer la sécurité du système. Le test de pénétration permet d’identifier les faiblesses ou les vulnérabilités, y compris la possibilité pour des tiers non autorisés d’accéder aux fonctionnalités et données du système.

>[!WARNING]
>
>Les clients ne sont pas autorisés à effectuer des évaluations de sécurité de l’infrastructure AWS ou des services AWS eux-mêmes. Si vous constatez un problème de sécurité dans l’un des services AWS observés dans votre évaluation de sécurité, [ contactez immédiatement AWS Security](mailto:aws-security@amazon.com). Voir [Stratégies du client AWS pour le test de pénétration](https://aws.amazon.com/security/penetration-testing/).
