---
title: Paramètres PHP
description: Découvrez les paramètres PHP optimaux pour la configuration de l’application Commerce dans l’infrastructure cloud.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 94c1e16a07567471d446478e3bd2a33977247ef3
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Paramètres PHP

Vous pouvez choisir lequel [version de PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) pour exécuter dans votre `.magento.app.yaml` fichier :

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Si vous effectuez une mise à niveau vers PHP 8.1 et versions ultérieures, supprimez JSON du [`runtime: extensions:` propriété](properties.md#runtime) dans le `.magento.app.yaml` fichier et redéploiement. L’extension JSON est installée dans un environnement cloud depuis PHP 8.0.

## Configuration de PHP

Vous pouvez personnaliser les paramètres PHP pour votre environnement en utilisant un `php.ini` fichier ajouté à la configuration gérée par Adobe Commerce.

Dans votre référentiel, ajoutez le `php.ini` à la racine de l’application (racine du référentiel).

>[!TIP]
>
>Configurer les paramètres PHP de manière incorrecte peut causer des problèmes, donc seuls les administrateurs avancés devraient définir ces options.

### Augmenter la limite de mémoire PHP

Pour augmenter la limite de mémoire PHP, ajoutez le paramètre suivant à la `php.ini` fichier :

```ini
memory_limit = 1G
```

Pour le débogage, augmentez la valeur sur 2G.

### Optimisation de la configuration realpath_cache

Définissez les éléments suivants : `realpath_cache` paramètres pour améliorer les performances de l’application.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Ces paramètres permettent aux processus PHP de mettre en cache les chemins vers les fichiers au lieu de les rechercher pour chaque chargement de page. Voir [Réglage des performances](https://www.php.net/manual/en/ini.core.php) dans la documentation PHP.

>[!NOTE]
>
>Pour obtenir la liste des paramètres de configuration PHP recommandés, voir [Paramètres PHP requis](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) dans le _Guide d’installation_.

### Vérifier les paramètres PHP personnalisés

Après avoir envoyé le fichier `php.ini` Si vous modifiez votre environnement Cloud, vous pouvez vérifier que la configuration PHP personnalisée a été ajoutée à votre environnement. Par exemple, utilisez SSH pour vous connecter à l’environnement distant et afficher le fichier à l’aide d’un élément similaire à ce qui suit :

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Si vous utilisez Cloud Docker for Commerce pour le développement local, voir [Conteneurs de service Docker](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) pour plus d’informations sur l’utilisation d’une `php.ini` dans un environnement Docker.

## Activer les extensions

Vous pouvez activer ou désactiver les extensions PHP dans `runtime:extension` section. En outre, les extensions spécifiées deviennent disponibles dans les conteneurs PHP Docker.

>[!IMPORTANT]
>
>Avant d&#39;activer les extensions, il est important de comprendre que la version PHP doit être compatible avec le système d&#39;exploitation hébergeant le projet. L’environnement de votre projet peut nécessiter une mise à niveau du système d’exploitation par l’équipe Infrastructure avant de pouvoir continuer.

Exemple dans `.magento.app.yaml` fichier :

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Utilisez SSH pour vous connecter à un environnement et répertorier les extensions PHP.

```bash
php -m
```

Pour plus d’informations sur une extension PHP spécifique, voir [Liste des extensions PHP](https://www.php.net/manual/en/extensions.alphabetical.php).

Le tableau suivant présente les extensions PHP prises en charge lors du déploiement d’Adobe Commerce sur la plateforme Cloud.

{{$include /help/_includes/templated/php-extensions-cloud.md}}

Les exigences du module PHP sont liées à la version Adobe Commerce. Voir [Exigences PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Prise en charge des extensions

Pour les projets Pro, les extensions suivantes nécessitent une prise en charge supplémentaire pour être installées :

- `sourceguardian`

Par exemple, pour paramétrer PHP pour qu&#39;il exécute uniquement des scripts protégés par SourceGuardian dans tous les environnements, l&#39;option suivante doit être définie dans `php.ini` fichier :

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Voir [section 3.5 de la documentation SourceGuardian](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Ceci est un lien vers un PDF_.

[Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour obtenir de l’aide sur l’installation de ces extensions PHP dans tous les environnements de production et environnements d’évaluation Pro. Inclure votre mise à jour `.magento/services.yaml` fichier, `.magento.app.yaml` avec la version PHP mise à jour et toutes les extensions PHP supplémentaires. Pour apporter des modifications à un environnement de production actif, vous devez fournir un préavis minimal de 48 heures. La mise à jour de votre projet par l’équipe en charge de l’infrastructure cloud peut prendre jusqu’à 48 heures.

>[!WARNING]
>
>PHP compilé avec débogage n&#39;est pas pris en charge et la sonde peut entrer en conflit avec [!DNL XDebug] ou [!DNL XHProf]. Désactivez ces extensions lors de l’activation de la sonde. La sonde est en conflit avec certaines extensions PHP comme [!DNL Pinba] ou IonCube.
