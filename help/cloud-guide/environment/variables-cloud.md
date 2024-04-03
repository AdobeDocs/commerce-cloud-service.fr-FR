---
title: Variables spécifiques au cloud
description: Consultez la liste des variables d’environnement spécifiques à Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Variables spécifiques au cloud

Les variables d’environnement spécifiques à Adobe Commerce sur l’infrastructure cloud utilisent la variable `MAGENTO_CLOUD_*` préfixe :

| Variable | Description |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Chemin d’accès absolu au répertoire de l’application. |
| `MAGENTO_CLOUD_APPLICATION` | Objet JSON codé en base 64 qui décrit l’application. Il est mappé sur le `.magento.app.yaml` contenu du fichier et comporte des sous-clés. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | Nom de l’application configuré dans la variable `.magento.app.yaml` fichier . |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Le chemin d’accès absolu à la racine du document web, le cas échéant. |
| `MAGENTO_CLOUD_ENVIRONMENT` | Nom de la branche d’environnement. |
| `MAGENTO_CLOUD_PROJECT` | Identifiant de projet. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Objet JSON codé en base64 qui représente la définition de point de terminaison de clé (nom de relation) et de valeur (tableaux de paires de relation). Chaque définition de point de terminaison de relation est une forme décomposée d’une URL. Il dispose d’un `scheme`, un `host`, un `port`, et _facultatif_ a `username`, `password`, `path`, ainsi que quelques informations supplémentaires dans `query`. |
| `MAGENTO_CLOUD_ROUTES` | Décrire les itinéraires définis dans l’environnement `.magento/routes.yaml` fichier . |
| `MAGENTO_CLOUD_TREE_ID` | ID d’arborescence de l’application, qui correspond au SHA de l’arborescence dans Git. |
| `MAGENTO_CLOUD_VARIABLES` | Objet JSON codé en base64 avec des paires clé-valeur, telles que `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | Fournit le chemin d’accès au point de montage du fournisseur de verrouillage sur l’infrastructure cloud. Le fournisseur de verrouillage empêche le lancement de tâches cron en double et de groupes cron. |

>[!WARNING]
>
>Pour ajouter des variables d’environnement à [remplacer les paramètres de configuration](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) en utilisant la variable [[!DNL Cloud Console]](../project/overview.md), vous devez ajouter en préfixe le nom de la variable `env:` comme dans l’exemple suivant :
>
>![Exemple de variable d’environnement](../../assets/set-env-variable-ui.png)

Comme les valeurs peuvent changer au fil du temps, il est préférable d’examiner la variable au moment de l’exécution et de l’utiliser pour configurer votre application. Par exemple, utilisez la variable `MAGENTO_CLOUD_RELATIONSHIPS` pour récupérer les relations liées à l’environnement comme suit :

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## Affichage des variables d’environnement

Vous pouvez utiliser la variable `env:config:show` à partir de [la valeur `ece-tools` package](../dev-tools/package-overview.md) pour afficher une liste de variables pour l’environnement actuel.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Exemple de sortie pour le `variables` option :

```terminal
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
