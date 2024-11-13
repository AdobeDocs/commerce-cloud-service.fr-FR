---
title: Second environnement d’évaluation
description: Découvrez les avantages et les utilisations d’un second environnement d’évaluation pour les tests parallèles, l’isolation des problèmes, le contrôle des versions, etc.
source-git-commit: 51fa75fff952e3832151d47b80baa7f532aa277f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# Second environnement d’évaluation

Dans l’infrastructure Adobe Commerce Cloud, l’environnement d’évaluation assure des tests et une validation complets dans un paramètre qui peut refléter l’environnement de production. Cet environnement vous permet d’identifier et de résoudre les bogues en toute sécurité, tout en veillant à ce que les nouvelles fonctionnalités ou modifications soient intégrées de manière transparente avant qu’elles n’affectent votre site actif.

Certains projets nécessitent un workflow de développement plus sophistiqué. Pour répondre à ce besoin, Adobe propose un environnement d’évaluation supplémentaire sous la forme d’une option de module complémentaire à votre infrastructure cloud. Avoir deux environnements intermédiaires est avantageux pour les projets complexes et la collaboration simultanée entre les équipes.

La présence d’un environnement intermédiaire secondaire présente les avantages suivants :

- **Test parallèle** : avec deux environnements d’évaluation, les équipes peuvent tester simultanément de nouvelles fonctionnalités et des mises à jour critiques sans interférer avec le développement de l’autre. Par exemple, vous pouvez dédier un environnement aux tests de fonctionnalités, tout en réservant l’autre environnement aux tests de performance et de stress.

- **Isolation des problèmes** : lorsque des bogues ou des problèmes se produisent dans l’environnement d’évaluation principal, vous pouvez les répliquer et les diagnostiquer dans l’environnement secondaire sans interrompre la progression des tests. Cela permet de s’assurer que le dépannage n’interfère pas avec les tests en cours.

- **Contrôle de version** : gérez plus efficacement les différentes versions de votre application. L’environnement d’évaluation principal peut exécuter le dernier build stable, tandis que les fonctions expérimentales des tests secondaires. Vous pouvez ainsi mieux gérer les cycles de publication et vous assurer que les modifications expérimentales ne perturbent pas les builds stables.

- **Amélioration de la planification du déploiement** : vous pouvez simuler différents scénarios de déploiement. L’environnement intermédiaire principal peut imiter la configuration de production actuelle, tandis que l’environnement secondaire peut être configuré pour tester les prochaines versions.

- **Tests d’acceptation utilisateur (UAT)** : lors de l’utilisation de l’environnement principal pour le développement en cours, vous pouvez dédier un environnement secondaire à UAT. Cela permet aux utilisateurs ou aux clients de tester et de fournir des commentaires sur les nouvelles fonctionnalités dans un paramètre contrôlé, sans affecter les tests.

- **Test de régression** : vous pouvez utiliser un environnement pour les tests de ciblage avant et un autre pour les tests de régression, en veillant à ce que les nouvelles modifications ne rompent pas les fonctionnalités existantes.

- **Formation et démonstrations** : utilisez un environnement pour former de nouveaux membres d’équipe ou présenter de nouvelles fonctionnalités aux parties prenantes. Cela permet de s’assurer que les activités de formation n’interrompent pas le test.

- **Configuration de lien privé** : les environnements de Principal et d’intégration ne prennent pas en charge la configuration de lien privé. Si votre workflow de développement nécessite des environnements supplémentaires connectés via Private Link pour le développement, le test ou tout autre objectif, pensez à ajouter un environnement d’évaluation supplémentaire.

Le fait d’avoir deux environnements intermédiaires peut améliorer considérablement l’efficacité de votre workflow, la gestion des risques et la qualité globale de votre application. Ces environnements offrent la sécurité et la flexibilité qu’un environnement intermédiaire ne serait pas en mesure d’offrir.

>[!NOTE]
>
>Cette configuration est un module complémentaire. Les clients qui souhaitent un environnement secondaire doivent contacter leur représentant commercial pour en demander un. Le représentant commercial peut fournir des informations sur la tarification et le processus d’approvisionnement.

Si votre projet comporte déjà un environnement d’évaluation supplémentaire ou si vous envisagez de mettre à niveau votre projet actuel, tenez compte des calendriers d’approvisionnement et des responsabilités suivants :

- Le processus d’approvisionnement peut prendre jusqu’à deux semaines après avoir confirmé la demande auprès de votre représentant commercial Adobe.

- Les nouveaux environnements d’évaluation ne sont disponibles que dans la même région que les environnements d’évaluation et de production actuels.

- Vous devez mettre à jour votre environnement d’intégration ou de Principal et spécifier sur quels environnements votre environnement intermédiaire secondaire sera basé. L’environnement intermédiaire secondaire ne peut pas être copié à partir des environnements d’évaluation ou de production.

- Une fois votre nouvel environnement d’évaluation reçu, vous pouvez l’inclure dans votre flux de développement. Comme pour les autres environnements, il vous appartient de mettre à jour le code et la base de données.

## Demander l’environnement

Pour faciliter votre demande, procédez comme suit :

1. Mettez à niveau votre branche.

   Mettez à niveau votre branche d’intégration ou de Principal avec le code et la base de données que vous souhaitez utiliser pour le nouvel environnement.

1. Contactez votre représentant commercial.

   Contactez votre représentant commercial Adobe et fournissez-lui la branche spécifique que vous souhaitez utiliser comme base pour votre nouvel environnement d’évaluation (intégration ou Principal).

1. Confirmez les détails.

   Une fois que vous avez confirmé les détails auprès de votre représentant commercial, attendez qu’il vous confirme que la demande d’approvisionnement a été reçue et qu’elle est en cours de traitement. Une fois le processus d’approvisionnement terminé, l’équipe d’Adobe vous enverra une confirmation.

1. Déployez sur votre nouvel environnement.

   Suivez les [étapes de déploiement standard](../deploy/staging-production.md) pour déployer votre code et votre base de données dans le nouvel environnement d’évaluation.
