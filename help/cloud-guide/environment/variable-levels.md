---
title: Niveaux et options de variable
description: Découvrez les différents niveaux de variable et options utilisés pour personnaliser votre Adobe Commerce dans l’environnement d’exécution de projet d’infrastructure cloud.
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Niveaux de variable

Les variables de projet s’appliquent à tous les environnements du projet. Les variables d’environnement s’appliquent à un environnement ou à une branche spécifique. Un environnement _hérite des définitions de variable_ de l’environnement parent.

Vous pouvez remplacer une valeur héritée en définissant la variable spécifiquement pour l’environnement. Par exemple, pour définir des variables pour le développement, définissez les valeurs de variable dans le fichier `.magento.env.yaml` de l’environnement d’intégration. Tous les environnements embranchement de l’environnement d’intégration héritent de ces valeurs. Voir [Configuration du déploiement](configure-env-yaml.md) pour plus d’informations sur la configuration de votre environnement à l’aide du fichier `.magento.env.yaml`.

>[!BEGINTABS]

>[!TAB CLI]

**Pour définir des variables à l’aide de l’interface de ligne de commande de Cloud** :

- **Variables spécifiques au projet** : pour définir la même valeur pour tous les environnements _tous_ de votre projet. Ces variables sont disponibles lors de la création et de l’exécution dans tous les environnements.

  ```bash
  magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
  ```

- **Variables spécifiques à un environnement** : pour définir une valeur unique pour un environnement _spécifique_. Ces variables sont disponibles au moment de l’exécution et héritées par les environnements enfants. Spécifiez l’environnement dans votre commande à l’aide de l’option `-e`.

  ```bash
  magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
  ```

Après avoir défini des variables spécifiques au projet, vous devez redéployer manuellement l’environnement distant pour que la modification soit prise en compte. Envoyez les nouvelles validations pour déclencher un redéploiement.

>[!TAB Console]

**Pour définir des variables à l’aide de[!DNL Cloud Console]** :

1. Dans le _[!DNL Cloud Console]_, cliquez sur l’icône de configuration sur le côté droit de la navigation du projet.

   ![Configurer le projet](../../assets/icon-configure.png){width="36"}

1. Pour définir une variable au niveau du projet, sous _Paramètres du projet_, cliquez sur **Variables**.

   ![Variables de projet](../../assets/ui-project-variables.png)

1. Pour définir une variable au niveau de l’environnement, dans la liste _Environments_ , sélectionnez un environnement et cliquez sur l’onglet **[!UICONTROL Variables]** .

   ![Onglet Variables d’environnement](../../assets/ui-environment-variables.png)

1. Cliquez sur **[!UICONTROL Create variable]**.

1. Attribuez un nom et une valeur à la variable. Choisissez l’une des options suivantes :

   - Disponible pendant l’exécution
   - Disponible pendant la période de création
   - Valeur JSON
   - Variable sensible (valeur masquée dans la console et réponses de l’interface de ligne de commande)
   - Rendre héritable (les environnements enfants peuvent hériter de variables au niveau de l’environnement)

1. Cliquez sur **[!UICONTROL Create variable]**.

>[!CAUTION]
>
>La définition de variables spécifiques à l’environnement dans le [!DNL Cloud Console] redéploie automatiquement l’environnement.

>[!ENDTABS]

## Visibilité

Vous pouvez limiter la visibilité d’une variable pendant la génération ou l’exécution à l’aide de la commande `--visible-<build|runtime>`. Il existe également des options pour définir l’héritage et la sensibilité.

Utilisez les options suivantes pour empêcher l’affichage ou l’héritage d’une variable :

- `--inheritable false` : désactive l’héritage pour les environnements enfants. Cela s’avère utile pour définir des valeurs de production uniques sur la branche `master` et permettre à tous les autres environnements d’utiliser une variable de niveau projet du même nom.
- `--sensitive true`—Marque la variable comme _non lisible_ dans le [!DNL Cloud Console]. Vous ne pouvez pas afficher la variable dans l’interface utilisateur. Cependant, vous pouvez afficher la variable à partir du conteneur de l’application, comme toute autre variable.

L’exemple suivant illustre un cas spécifique qui empêche l’affichage ou l’héritage d’une variable. Vous pouvez uniquement spécifier ces options dans l’interface de ligne de commande. Ce cas ne concerne pas toutes les variables d’environnement disponibles.

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## Vérifier les niveaux et les valeurs des variables

Vous pouvez afficher une liste de variables existantes à l’aide de l’interface de ligne de commande de Cloud.

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
