---
title: Assistant dynamique
description: Découvrez comment utiliser des assistants intelligents pour évaluer si votre projet d’infrastructure cloud d’Adobe Commerce suit les bonnes pratiques de déploiement.
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Assistant dynamique

Les assistants intelligents peuvent vous aider à déterminer si votre configuration cloud suit les bonnes pratiques. Les assistants disponibles aident aux configurations suivantes :

- État idéal pour un temps d’arrêt minimal du déploiement
- Configuration de l’équilibrage de charge pour la base de données et Redis
- Déploiement de contenu statique (SCD) pour les environnements à la demande, de création ou de déploiement

Chacune des commandes de l’assistant dynamique fournit une réponse de vérification et, le cas échéant, une recommandation pour la configuration appropriée.

| Commande | Description |
| ------- | ------------|
| `wizard:ideal-state` | Vérifiez que SCD est sur la page _build_ l’étape `SKIP_HTML_MINIFICATION` est `true`et le crochet post_deploy configuré dans l’environnement cloud. Non à utiliser dans l’environnement de développement local. |
| `wizard:master-slave` | Vérifiez que la variable `REDIS_USE_SLAVE_CONNECTION` et la variable `MYSQL_USE_SLAVE_CONNECTION` est `true`. |
| `wizard:scd-on-demand` | Vérifiez que la variable `SCD_ON_DEMAND` la variable d’environnement globale est `true`. |
| `wizard:scd-on-build` | Vérifiez que la variable `SCD_ON_DEMAND` la variable d’environnement globale est `false` et la variable `SKIP_SCD` la variable d’environnement est `false` pour le _build_ scène. Vérifie que la variable `config.php` contient des informations sur les magasins, les groupes de magasins et les sites web. |
| `wizard:scd-on-deploy` | Vérifiez que la variable `SCD_ON_DEMAND` la variable d’environnement globale est `false` et la variable `SKIP_SCD` la variable d’environnement est `false` pour le _deploy_ scène. Vérifie que la variable `config.php` Le fichier fait office _NOT_ contiennent la liste des magasins, des groupes de magasins et des sites web contenant des informations connexes. |

Par exemple, vous pouvez vérifier que votre configuration active correctement la fonctionnalité SCD à la demande :

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Une configuration réussie renvoie :

```terminal
SCD on-demand is enabled
```

Une configuration en échec renvoie :

```terminal
SCD on-demand is disabled
```

## Vérification d’une configuration idéale

La variable _idéal_ la configuration de votre projet Cloud permet de minimiser les temps d’arrêt du déploiement en réchauffant le cache et en générant du contenu statique lorsque l’utilisateur le demande. Cet assistant s’exécute automatiquement pendant le processus de déploiement. Si votre Cloud n’est pas configuré pour cela _état idéal_, vous recevez ensuite un message similaire à ce qui suit :

```terminal
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

En fonction de la sortie, vous devez apporter les corrections suivantes à votre configuration :

1. Activez la variable de minimisation Ignorer le HTML .

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. Configurez le crochet de post-déploiement.

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. Envoyez vos modifications de code et relancez le test. Lorsque votre configuration est _idéal_, vous recevez le message suivant.

   ```terminal
   Ideal state is configured
   ```
