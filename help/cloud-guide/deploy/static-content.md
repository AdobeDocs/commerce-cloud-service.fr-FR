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

Le déploiement de contenu statique (SCD) a un impact significatif sur le processus de déploiement de magasin qui dépend de la quantité de contenu à générer (images, scripts, CSS, vidéos, thèmes, paramètres régionaux et pages web) et du moment auquel générer le contenu. Par exemple, la stratégie par défaut génère du contenu statique pendant la [phase de déploiement](process.md#deploy-phase-deploy-phase) lorsque le site est en mode de maintenance ; toutefois, cette stratégie de déploiement prend du temps pour écrire directement le contenu sur le `pub/static` répertoire . Vous disposez de plusieurs options ou stratégies pour vous aider à améliorer le temps de déploiement en fonction de vos besoins.

## Optimisation du contenu JavaScript et des HTMLS

Vous pouvez utiliser le regroupement et la minification pour créer du contenu JavaScript et de HTML optimisé lors du déploiement de contenu statique.

### Minimiser le contenu

Vous pouvez améliorer le temps de chargement du SCD au cours du processus de déploiement si vous ne copiez pas les fichiers d’affichage statique dans le `var/view_preprocessed` et générer _minified_ HTML sur demande. Vous pouvez l’activer en définissant la variable [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) variable d’environnement globale vers `true` dans le `.magento.env.yaml` fichier .

>[!NOTE]
>
>Commencer par le `ece-tools` version 2002.0.13 du package, la valeur par défaut de la variable SKIP_HTML_MINIFICATION est définie sur `true`.

Vous pouvez enregistrer **more** temps de déploiement et espace disque en réduisant le nombre de fichiers de thème inutiles. Vous pouvez, par exemple, déployer le `magento/backend` en anglais et un thème personnalisé dans d’autres langues. Vous pouvez configurer ces paramètres de thème avec la fonction [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) Variable d’environnement.

## Choix d’une stratégie de déploiement

Les stratégies de déploiement diffèrent selon que vous choisissez de générer du contenu statique pendant la _build_ , la _deploy_ phase, ou _à la demande_. Comme le montre le graphique suivant, la génération de contenu statique pendant la phase de déploiement est le choix le moins optimal. Même avec un HTML réduit, chaque fichier de contenu doit être copié dans le fichier monté. `~/pub/static` qui peut prendre beaucoup de temps. La génération de contenu statique à la demande semble être le choix optimal. Cependant, si le fichier de contenu n’existe pas dans le cache qu’il génère au moment où il est demandé, cela ajoute du temps de chargement à l’expérience utilisateur. Par conséquent, la génération de contenu statique lors de la phase de création est la plus optimale.

![Comparaison de chargement SCD](../../assets/scd-load-times.png)

### Définition du SCD sur la version

La génération de contenu statique lors de la phase de création avec un HTML minimisé est la configuration optimale pour [**zéro temps d’arrêt** déploiements](reduce-downtime.md), également appelé **état idéal**. Au lieu de copier des fichiers sur un lecteur monté, il crée un lien symbolique à partir de la fonction `./init/pub/static` répertoire .

La génération de contenu statique nécessite l’accès aux thèmes et aux paramètres régionaux. Adobe Commerce stocke les thèmes dans le système de fichiers, qui est accessible pendant la phase de création. Toutefois, Adobe Commerce stocke les paramètres régionaux dans la base de données. La base est _not_ disponible pendant la phase de création. Pour générer le contenu statique pendant la phase de création, vous devez utiliser la variable `config:dump` dans la fonction `ece-tools` pour déplacer les paramètres régionaux vers le système de fichiers. Il lit les paramètres régionaux et les enregistre dans le `app/etc/config.php` fichier .

**Pour configurer votre projet afin de générer un SCD sur la version**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.
1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Déplacez les paramètres régionaux vers le système de fichiers, puis mettez à jour la variable [`config.php` fichier](../development/commerce-version.md#create-a-configphp-file).

1. La variable `.magento.env.yaml` Le fichier de configuration doit contenir les valeurs suivantes :

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) is `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) sur l’étape de création : `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) is `compact`

1. Vérification de la configuration de la variable [crochet après déploiement](../application/hooks-property.md) dans le `.magento.app.yaml` fichier .

1. Vérifiez vos paramètres en exécutant la fonction [Assistant dynamique pour l’état idéal](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### Définir le SCD à la demande

La génération de SCD à la demande est optimale pour un workflow de développement dans l’environnement d’intégration. Cela réduit le temps de déploiement afin que vous puissiez rapidement passer en revue vos mises en oeuvre et exécuter des tests d’intégration. Activez la variable [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) Variable d’environnement à l’étape globale de la variable `.magento.env.yaml` fichier . La variable SCD_ON_DEMAND remplace toutes les autres configurations liées à SCD et efface le contenu existant de la variable `~/pub/static` répertoire .

Lors de l’utilisation de la stratégie SCD à la demande, il est utile de précharger le cache avec les pages que vous prévoyez de demander, telles que la page d’accueil. Ajoutez la liste des pages attendues dans le [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) dans l’étape de post-déploiement de la variable `.magento.env.yaml` fichier .

>[!WARNING]
>
>N’utilisez pas la stratégie SCD à la demande dans l’environnement de production.

### SCD ignoré

Parfois, vous pouvez choisir d’ignorer la génération complète de contenu statique. Vous pouvez définir la variable [SKIP_SCD](../environment/variables-build.md#skipscd) Variable d’environnement dans la scène globale pour ignorer d’autres configurations liées à SCD. Cela n’a aucune incidence sur le contenu existant dans la variable `~/pub/static` répertoire .
