---
title: Assistant dynamique
description: Découvrez comment utiliser des assistants intelligents pour évaluer si votre projet d’infrastructure cloud d’Adobe Commerce suit les bonnes pratiques de déploiement.
feature: Cloud, Build, Deploy, SCD
exl-id: eb79431c-8835-4ae4-b453-9c4932c5d5ac
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
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
| `wizard:ideal-state` | Vérifiez que SCD se trouve sur l’étape _build_, que la variable `SKIP_HTML_MINIFICATION` est `true` et que le crochet post_deploy est configuré dans l’environnement cloud. Non à utiliser dans l’environnement de développement local. |
| `wizard:master-slave` | Vérifiez que la variable `REDIS_USE_SLAVE_CONNECTION` et la variable `MYSQL_USE_SLAVE_CONNECTION` sont `true`. |
| `wizard:scd-on-demand` | Vérifiez que la variable d&#39;environnement global `SCD_ON_DEMAND` est `true`. |
| `wizard:scd-on-build` | Vérifiez que la variable d&#39;environnement global `SCD_ON_DEMAND` est `false` et que la variable d&#39;environnement `SKIP_SCD` est `false` pour l&#39;étape _build_. Vérifie que le fichier `config.php` contient des informations sur les magasins, les groupes de magasins et les sites web. |
| `wizard:scd-on-deploy` | Vérifiez que la variable d&#39;environnement global `SCD_ON_DEMAND` est `false` et que la variable d&#39;environnement `SKIP_SCD` est `false` pour l&#39;étape _deploy_. Vérifie que le fichier `config.php` ne contient _NOT_ la liste des magasins, des groupes de magasins et des sites Web contenant des informations connexes. |

Par exemple, vous pouvez vérifier que votre configuration active correctement la fonctionnalité SCD à la demande :

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Une configuration réussie renvoie :

```
SCD on-demand is enabled
```

Une configuration en échec renvoie :

```
SCD on-demand is disabled
```

## Vérification d’une configuration idéale

La configuration _idéale_ pour votre projet Cloud permet de minimiser le temps d’arrêt du déploiement en réchauffant le cache et en générant du contenu statique lorsque l’utilisateur le demande. Cet assistant s’exécute automatiquement pendant le processus de déploiement. Si votre Cloud n’est pas configuré pour cet _état idéal_, vous recevez un message similaire à ce qui suit :

```
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

En fonction de la sortie, vous devez apporter les corrections suivantes à votre configuration :

1. Activez la variable de minimisation Ignorer l’HTML .

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

   ```
   Ideal state is configured
   ```
