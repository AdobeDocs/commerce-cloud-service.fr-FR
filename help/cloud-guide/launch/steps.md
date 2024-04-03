---
title: Étapes de lancement
description: Découvrez comment terminer le lancement du site.
exl-id: cf75f89c-94c8-47c1-a23d-93cd9921aab7
source-git-commit: e62236a8937ae1dd10df3c736b2e945be155d236
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Étapes de lancement

Une fois que vous avez testé et terminé votre liste de contrôle de lancement, vous pouvez commencer les étapes finales de lancement. Ces étapes comprennent la saisie de tickets, le transfert de l’accès au site et enfin le test de votre boutique lorsqu’elle est active.

Le personnel de l’assistance Adobe travaille avec vous tout au long du processus, en vérifiant l’état et en cas de questions ou de problèmes. Tous les problèmes doivent être suivis avec les tickets pour capturer au mieux ce qui s’est passé et comment il a été résolu. Lorsque vous commencez des itérations continues à déployer des mises à jour dans votre magasin lancé, des problèmes similaires peuvent se produire à nouveau. Ces tickets peuvent vous aider à identifier les problèmes et à ajuster vos tâches de déploiement.

## Contactez l’Adobe pour lancer votre site.

Contactez l’assistance d’Adobe Commerce et mettez à jour les tickets de lancement (mise en ligne) de votre site avec la date et l’heure prévues pour basculer et lancer votre boutique.

## Basculer le DNS vers le nouveau site

La valeur Modification de la durée de vie est importante pour vérifier votre domaine modifié. Lorsque vous modifiez les enregistrements A et CNAME, la mise à jour prend le temps configuré TTL pour se mettre à jour correctement. Pour plus d’informations sur les paramètres DNS, voir [Paramétrages DNS](checklist.md#update-dns-configuration-with-production-settings).

### Pour accéder au nouveau site :

1. Accédez à votre service DNS.

1. Mettez à jour vos enregistrements A et CNAME pour vos domaines et noms d’hôtes.

1. Patientez jusqu’à ce que le délai d’activation soit écoulé et redémarrez votre navigateur web.

1. Accédez à votre boutique à l’aide du domaine storefront.

## Test de la boutique en ligne

Effectuez quelques tests UAT dans votre live store pour confirmer que tout se charge et que les actions sont correctement exécutées. Pour obtenir la liste des tests, voir [Test du déploiement](../test/staging-and-production.md#complete-uat-testing).

## Après le lancement

Adobe vérifie et surveille le site pour s’assurer que tous les services et accès sont en vert. Nous restons à portée de main si nécessaire pour vérifier que tous les journaux, services, mises en cache et fonctions du système fonctionnent selon vos besoins et ceux de vos clients.

Si des problèmes se produisent, créez et effectuez le suivi des problèmes avec l’assistance. Incluez autant d’informations que possible, notamment la date et l’heure, une fonctionnalité spécifique avec un problème, les symptômes et les comportements impaires, des extensions, etc. Nous enquêtons sur les journaux, le problème et collaborons avec vous pour résoudre le problème le plus rapidement possible.
