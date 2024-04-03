---
title: Exemple de gestion des paramètres spécifiques au système
description: Consultez un exemple de gestion et de synchronisation des paramètres de configuration du magasin dans tous les environnements Adobe Commerce sur l’infrastructure cloud.
hidefromtoc: true
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Exemple de gestion des paramètres spécifiques au système

Cet exemple montre comment utiliser la gestion de la configuration pour préserver la cohérence des paramètres du magasin dans tous les environnements.

L’exemple utilise la procédure suivante définie dans [Paramètres de magasin](store-settings.md):

1. Saisissez vos configurations dans l’administrateur de la banque d’environnements d’intégration.
1. Créez un `config.php` et transférez-le à votre poste de travail local.
1. Push `config.php` à l’environnement d’intégration distante.
1. Vérifiez que vos paramètres ne sont pas modifiables dans l’administrateur.
1. Apportez les modifications nécessaires :

   * Modifiez les paramètres de configuration dans l’environnement d’intégration.
   * Pour ajouter des configurations, exécutez la commande pour créer `config.php` encore une fois. De nouvelles configurations sont ajoutées au fichier .
   * Pour supprimer ou modifier des configurations existantes, modifiez manuellement le fichier.
   * Validez et poussez.

Par exemple, vous pouvez définir les paramètres suivants :

* Désactiver [locale](https://glossary.magento.com/locale) Paramètres d’optimisation des fichiers statiques et dans votre environnement d’intégration
* Activation de l’optimisation des fichiers statiques dans les environnements d’évaluation et de production
* Configuration rapide dans les environnements d’évaluation et de production avec des informations d’identification spécifiques pour chaque

_Optimisation statique des fichiers_ signifie la fusion et la minimisation de feuilles de style JavaScript et en cascade et la minimisation de modèles de HTML. Voir [Stratégies de déploiement de contenu statique](../deploy/static-content.md).

## Conditions préalables

Pour effectuer ces tâches de gestion de la configuration, vous devez disposer des éléments suivants :

* Rôle de lecteur de projet avec [environnement &quot;admin&quot;](../project/user-access.md) privilèges
* URL et informations d’identification d’administrateur pour les environnements d’intégration, d’évaluation et de production

## Configuration de l’administrateur Commerce

Dans l’environnement d’intégration, vous pouvez vous connecter à l’administrateur afin de modifier les paramètres de configuration du système pour les magasins, sites web, modules ou extensions, l’optimisation des fichiers statiques et les valeurs système liées au déploiement de contenu statique. Voir [Données de configuration](store-settings.md#scd-performance).

**Pour modifier les paramètres régionaux et les paramètres d’optimisation des fichiers statiques**:

1. Connectez-vous à l’administrateur de l’environnement d’intégration. Vous pouvez accéder à cette URL via la fonction [[!DNL Cloud Console]](../project/overview.md).
1. Accédez à **Magasins** > Paramètres > **Configuration** > Général > **Général**.
1. Dans la navigation de la page, développez **Options de paramètres régionaux**.
1. Dans la **Paramètres régionaux** , modifiez le paramètre régional. Vous pouvez la modifier à nouveau plus tard.

   ![Modifier le paramètre régional](../../assets/locale-options.png)

1. Cliquez sur **Enregistrer la configuration**.
1. Si vous y êtes invité, [vider le cache](https://docs.magento.com/user-guide/system/cache-management.html).
1. Déconnectez-vous de l’administrateur.

## Exportez des valeurs et transférez config.php vers votre système local.

Cette étape crée et transfère la variable `config.php` fichier de configuration sur l’environnement d’intégration à l’aide d’une commande que vous exécutez sur votre ordinateur local.

Cette procédure correspond à l’étape 2 de la section [procédure recommandée](store-settings.md). Après avoir créé `config.php`, transférez-le vers votre système local pour pouvoir l’ajouter à Git.

**Pour créer et transférer`config.php`**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Modifiez l’environnement d’intégration.

   ```bash
   magento-cloud environment:checkout integration
   ```

1. Créez un vidage local de la base distante.

   ```bash
   magento-cloud db:dump
   ```

Le fragment de code suivant de `config.php` affiche un exemple de changement du paramètre régional par défaut `en_GB` et de modifier les paramètres d’optimisation des fichiers statiques :

```php?start_inline=1
'general' => [
     'locale' => [
         'code' => 'en_GB',
         'timezone' => 'UTC',
     ],

     ... more ...

 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],
     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],

     ... more ...
```

## Push et déploiement de config.php dans les environnements

Maintenant que vous avez créé `config.php` et l’avez transféré sur votre système local, validez sur Git et poussez-le dans vos environnements. Cette procédure correspond aux étapes 3 et 4 de la section [procédure recommandée](store-settings.md).

La commande suivante ajoute, valide et envoie la commande `master` branche :

```bash
git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
```

Terminez le déploiement du code vers l’évaluation et la production. Pour commencer, appuyez sur `staging` et `master` branches. Pour plus d’informations sur les commandes de déploiement, voir [Déployer votre boutique](../deploy/staging-production.md).

Attendez que le déploiement soit terminé dans tous les environnements.

## Vérification des modifications apportées à la configuration

Après avoir appuyé `config.php` dans vos environnements, toutes les valeurs que vous avez modifiées doivent être en lecture seule dans l’administrateur. Dans cet exemple, les paramètres régionaux par défaut et les paramètres d’optimisation des fichiers statiques modifiés ne doivent pas être modifiables dans l’Admin. Ces paramètres de configuration sont définis dans `config.php`.

Pour vérifier les modifications apportées à la configuration :

1. Déconnectez-vous de l’administrateur dans l’un des environnements.
1. Connectez-vous à nouveau à l’administrateur.
1. Cliquez sur **Magasins** > Paramètres > **Configuration** > Général > **Général**.
1. Dans le volet de droite, développez **Options de paramètres régionaux**.

   Notez que plusieurs champs ne peuvent pas être modifiés, comme illustré dans l’exemple suivant. Ces paramètres de configuration sont conservés par `config.php`.

   ![Certaines valeurs ne peuvent plus être modifiées dans l’Admin](../../assets/locale-options-disabled.png)

1. Déconnectez-vous de l’administrateur.

## Modification et mise à jour des paramètres de configuration spécifiques au système

Si vous devez modifier l’un de ces paramètres, modifiez la variable `config.php` à l’aide d’un éditeur de texte. Une fois les modifications ou les suppressions terminées, vous pouvez les valider et les envoyer vers l’environnement distant en suivant les étapes précédentes.

Pour ajouter des configurations, modifiez votre environnement d’intégration et relancez la commande pour générer le fichier. Toutes les nouvelles configurations sont ajoutées au code du fichier . Passez-le à Git en suivant les étapes précédentes.

Dans cet exemple, modifiez les paramètres d’optimisation des fichiers statiques et ajoutez un nouveau paramètre pour JavaScript.

### Ajout de configurations à l’intégration

Pour ajouter des valeurs de configuration dans l’administrateur de l’environnement d’intégration. Cet exemple fusionne des fichiers JavaScript.

1. Déconnectez-vous de l’administrateur d’intégration.
1. Connectez-vous à nouveau à l’administrateur d’intégration.
1. Cliquez sur **Magasins** > Paramètres > **Configuration** > **Avancé** > **Développeur**.
1. Dans le volet de droite, développez **Paramètres JavaScript**.
1. Dans la **Fusionner les fichiers JavaScript** liste, cliquez sur **Oui**.
1. Cliquez sur **Enregistrer la configuration**.
1. Si vous y êtes invité, [vider le cache](https://docs.magento.com/user-guide/system/cache-management.html).
1. Déconnectez-vous de l’administrateur.

En exécutant à nouveau la commande de vidage, la nouvelle configuration est ajoutée au fichier.

```bash
magento-cloud db:dump
```

### Modifier config.php avec de nouveaux paramètres

Sur votre instance locale, utilisez un éditeur de texte pour modifier la mise à jour `app/etc/config.php` fichier . Modifiez ces paramètres pour activer la minification pour les fichiers JavaScript, HTML et CSS.

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],
```

Pour modifier les paramètres afin d’autoriser la minimisation, modifiez les `'0'` to `'1'` pour `'minify_html'` et chaque `'minify_files'` option :

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '1',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '1',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '1',
     ],
```

Enregistrez les modifications dans le fichier.

### Poussez les modifications vers Git.

Pour pousser vos modifications, saisissez les informations suivantes :

```bash
git add app/etc/config.php
```

```bash
git commit -m "Add system-specific configuration and edit settings"
```

```bash
git push origin master
```

Attendez que le déploiement soit terminé.

Répétez le processus de déploiement pour envoyer le code à tous les environnements.
