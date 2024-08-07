---
title: Déploiement de contenu statique
description: Découvrez les stratégies de déploiement de contenu statique, tel que des images, des scripts et des CSS, sur Adobe Commerce dans les projets d’infrastructure cloud.
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Stratégies de déploiement de contenu statique

Le déploiement de contenu statique (SCD) a un impact significatif sur le processus de déploiement de magasin qui dépend de la quantité de contenu à générer (images, scripts, CSS, vidéos, thèmes, paramètres régionaux et pages web) et du moment auquel générer le contenu. Par exemple, la stratégie par défaut génère du contenu statique pendant la [phase de déploiement](process.md#deploy-phase-deploy-phase) lorsque le site est en mode de maintenance ; toutefois, cette stratégie de déploiement prend du temps pour écrire directement le contenu dans le répertoire `pub/static` monté. Vous disposez de plusieurs options ou stratégies pour vous aider à améliorer le temps de déploiement en fonction de vos besoins.

## Optimisation du contenu JavaScript et HTML

Vous pouvez utiliser le bundling et la minification pour créer du contenu JavaScript et d’HTML optimisé lors du déploiement de contenu statique.

### Minimiser le contenu

Vous pouvez améliorer le temps de chargement du SCD pendant le processus de déploiement si vous ignorez la copie des fichiers d’affichage statique dans le répertoire `var/view_preprocessed` et générez l’HTML _minified_ si nécessaire. Vous pouvez l’activer en définissant la variable d’environnement global [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) sur `true` dans le fichier `.magento.env.yaml`.

>[!NOTE]
>
>À partir de la version 2002.0.13 du package `ece-tools`, la valeur par défaut de la variable SKIP_HTML_MINIFICATION est définie sur `true`.

Vous pouvez économiser **plus** de temps de déploiement et d’espace disque en réduisant le nombre de fichiers de thème inutiles. Par exemple, vous pouvez déployer le thème `magento/backend` en anglais et un thème personnalisé dans d’autres langues. Vous pouvez configurer ces paramètres de thème avec la variable d&#39;environnement [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix).

## Choix d’une stratégie de déploiement

Les stratégies de déploiement diffèrent selon que vous choisissez de générer du contenu statique pendant la phase _build_, la phase _deploy_ ou _on-demand_. Comme le montre le graphique suivant, la génération de contenu statique pendant la phase de déploiement est le choix le moins optimal. Même avec un HTML minimisé, chaque fichier de contenu doit être copié dans le répertoire `~/pub/static` monté, ce qui peut prendre beaucoup de temps. La génération de contenu statique à la demande semble être le choix optimal. Cependant, si le fichier de contenu n’existe pas dans le cache qu’il génère au moment où il est demandé, cela ajoute du temps de chargement à l’expérience utilisateur. Par conséquent, la génération de contenu statique lors de la phase de création est la plus optimale.

![Comparaison de chargement SCD](../../assets/scd-load-times.png)

### Définition du SCD sur la version

La génération de contenu statique lors de la phase de création avec un HTML minimisé est la configuration optimale pour les [**déploiements sans interruption**](reduce-downtime.md), également appelé **état idéal**. Au lieu de copier des fichiers sur un lecteur monté, il crée un lien symbolique à partir du répertoire `./init/pub/static`.

La génération de contenu statique nécessite l’accès aux thèmes et aux paramètres régionaux. Adobe Commerce stocke les thèmes dans le système de fichiers, qui est accessible pendant la phase de création. Toutefois, Adobe Commerce stocke les paramètres régionaux dans la base de données. La base de données est _not_ disponible pendant la phase de création. Pour générer le contenu statique pendant la phase de génération, vous devez utiliser la commande `config:dump` du package `ece-tools` pour déplacer les paramètres régionaux vers le système de fichiers. Il lit les paramètres régionaux et les enregistre dans le fichier `app/etc/config.php`.

**Pour configurer votre projet de génération de SCD sur le build** :

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.
1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Déplacez les paramètres régionaux vers le système de fichiers, puis mettez à jour le fichier [`config.php` ](../development/commerce-version.md#create-a-configphp-file).

1. Le fichier de configuration `.magento.env.yaml` doit contenir les valeurs suivantes :

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) est `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) sur l’étape de création est `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) est `compact`

1. Vérifiez la configuration du [crochet de déploiement de Post](../application/hooks-property.md) dans le fichier `.magento.app.yaml`.

1. Vérifiez vos paramètres en exécutant l’assistant [Smart pour l’état idéal](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### Définir le SCD à la demande

La génération de SCD à la demande est optimale pour un workflow de développement dans l’environnement d’intégration. Cela réduit le temps de déploiement afin que vous puissiez rapidement passer en revue vos mises en oeuvre et exécuter des tests d’intégration. Activez la variable d’environnement [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) à l’étape globale du fichier `.magento.env.yaml`. La variable SCD_ON_DEMAND remplace toutes les autres configurations liées à SCD et efface le contenu existant du répertoire `~/pub/static`.

Lors de l’utilisation de la stratégie SCD à la demande, il est utile de précharger le cache avec les pages que vous prévoyez de demander, telles que la page d’accueil. Ajoutez la liste des pages attendues dans la variable d&#39;environnement [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) lors de l&#39;étape de post-déploiement du fichier `.magento.env.yaml`.

>[!WARNING]
>
>N’utilisez pas la stratégie SCD à la demande dans l’environnement de production.

### SCD ignoré

Parfois, vous pouvez choisir d’ignorer la génération complète de contenu statique. Vous pouvez définir la variable d’environnement [SKIP_SCD](../environment/variables-build.md#skipscd) sur la scène globale afin d’ignorer d’autres configurations liées à SCD. Cela n’a aucune incidence sur le contenu existant dans le répertoire `~/pub/static`.
