---
title: Propriété Hooks
description: Voir des exemples de configuration de la propriété hooks dans la section [!DNL Commerce] fichier de configuration de l’application.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Propriété Hooks

Utilisez la variable `hooks` pour exécuter des commandes shell pendant les phases de création, de déploiement et de post-déploiement :

- **`build`**—Exécuter les commandes _before_ emballer votre application. Les services, tels que la base de données ou Redis, ne sont pas disponibles, car l’application n’a pas encore été déployée. Ajout de commandes personnalisées _before_ par défaut `php ./vendor/bin/ece-tools` afin que le contenu généré par les utilisateurs puisse continuer jusqu’à la phase de déploiement.

- **`deploy`**—Exécuter les commandes _after_ création d’un package et déploiement de votre application. Vous pouvez accéder à d’autres services à ce stade. Depuis la valeur par défaut `php ./vendor/bin/ece-tools` copie la commande `app/etc` à l’emplacement approprié, vous devez ajouter des commandes personnalisées. _after_ la commande deploy pour empêcher l’échec des commandes personnalisées.

- **`post_deploy`**—Exécuter les commandes _after_ déploiement de votre application et _after_ le conteneur commence à accepter les connexions. La variable `post_deploy` hook efface le cache et précharge (warms) le cache. Vous pouvez personnaliser la liste des pages à l’aide de la variable `WARM_UP_PAGES` dans la variable [Etape post-déploiement](../environment/variables-post-deploy.md). Bien que cela ne soit pas obligatoire, cela fonctionne en tandem avec la fonction `SCD_ON_DEMAND` Variable d’environnement.

L’exemple suivant illustre la configuration par défaut dans la variable `.magento.app.yaml` fichier . Ajoutez des commandes d’interface de ligne de commande sous la propriété `build`, `deploy`, ou `post_deploy` sections _before_ la valeur `ece-tools` command :

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Vous pouvez également personnaliser davantage la phase de création à l’aide de la fonction `generate` et `transfer` pour effectuer des actions supplémentaires lors de la création spécifique de code ou du déplacement de fichiers.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e`—entraîne l’échec des hooks sur la première commande qui a échoué, au lieu de la commande finale qui a échoué.
- `build:generate`: applique des correctifs, valide la configuration, génère l’ID et génère du contenu statique si SCD est activé pour la phase de création.
- `build:transfer`: transfère le code généré et le contenu statique vers la destination finale.

Les commandes s’exécutent à partir de l’application (`/app`). Vous pouvez utiliser la variable `cd` pour modifier le répertoire. Les hooks échouent si la commande finale échoue. Pour les provoquer à l’échec de la première commande en échec, ajoutez `set -e` au début du crochet.

**Pour compiler des fichiers Sass à l’aide de grunt**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Compilation de fichiers Sass à l’aide de `grunt` avant le déploiement du contenu statique, qui se produit pendant la génération. Placez le `grunt` avant la commande `build` .

{{scenarios}}
