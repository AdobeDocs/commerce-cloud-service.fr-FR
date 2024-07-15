---
title: Propriété Hooks
description: Voir des exemples sur la configuration de la propriété hooks dans le fichier de configuration de l’application  [!DNL Commerce] .
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Propriété Hooks

Utilisez la section `hooks` pour exécuter des commandes shell pendant les phases de création, de déploiement et de post-déploiement :

- **`build`**—Exécuter des commandes _avant_ de grouper votre application. Les services, tels que la base de données ou Redis, ne sont pas disponibles, car l’application n’a pas encore été déployée. Ajoutez des commandes personnalisées _avant_ la commande par défaut `php ./vendor/bin/ece-tools` afin que le contenu généré par les personnalisations continue à la phase de déploiement.

- **`deploy`** : exécutez les commandes _après_ le package et le déploiement de votre application. Vous pouvez accéder à d’autres services à ce stade. Comme la commande par défaut `php ./vendor/bin/ece-tools` copie le répertoire `app/etc` vers l’emplacement correct, vous devez ajouter des commandes personnalisées _après_ la commande de déploiement pour empêcher l’échec des commandes personnalisées.

- **`post_deploy`**—Exécuter des commandes _après_ le déploiement de votre application et _après_ que le conteneur commence à accepter les connexions. Le crochet `post_deploy` efface le cache et précharge (réchauffe) le cache. Vous pouvez personnaliser la liste des pages à l’aide de la variable `WARM_UP_PAGES` dans l’ [étape de déploiement de Post](../environment/variables-post-deploy.md). Bien que cela ne soit pas obligatoire, cela fonctionne en tandem avec la variable d’environnement `SCD_ON_DEMAND`.

L’exemple suivant illustre la configuration par défaut dans le fichier `.magento.app.yaml`. Ajoutez des commandes d’interface de ligne de commande sous les sections `build`, `deploy` ou `post_deploy` _avant_ la commande `ece-tools` :

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

Vous pouvez également personnaliser davantage la phase de génération à l’aide des commandes `generate` et `transfer` afin d’effectuer des actions supplémentaires lors de la création spécifique de code ou du déplacement de fichiers.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e` : entraîne l’échec des hooks sur la première commande qui a échoué, au lieu de la commande finale qui a échoué.
- `build:generate` : applique des correctifs, valide la configuration, génère l’ID et génère du contenu statique si SCD est activé pour la phase de création.
- `build:transfer` : transfère le code généré et le contenu statique vers la destination finale.

Les commandes s’exécutent à partir du répertoire de l’application (`/app`). Vous pouvez utiliser la commande `cd` pour modifier le répertoire. Les hooks échouent si la commande finale échoue. Pour les faire échouer sur la première commande en échec, ajoutez `set -e` au début du point d&#39;extension.

**Pour compiler des fichiers Sass à l’aide de grunt** :

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

Compilez des fichiers Sass en utilisant `grunt` avant le déploiement de contenu statique, ce qui se produit pendant la génération. Placez la commande `grunt` avant la commande `build`.

{{scenarios}}
