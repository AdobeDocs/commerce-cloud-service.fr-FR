---
title: paramètres PHP
description: Découvrez les paramètres PHP optimaux pour la configuration de l’application Commerce dans l’infrastructure cloud.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# paramètres PHP

Vous pouvez choisir laquelle [version de PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) pour exécuter votre `.magento.app.yaml` fichier :

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Si vous effectuez une mise à niveau vers PHP 8.1 et versions ultérieures, supprimez JSON de la [`runtime: extensions:` property](properties.md#runtime) dans le `.magento.app.yaml` et redéployez. L’extension JSON est installée dans l’environnement cloud depuis PHP 8.0.

## Configurer PHP

Vous pouvez personnaliser les paramètres PHP de votre environnement à l’aide d’une `php.ini` qui est ajouté à la configuration conservée par Adobe Commerce.

Dans votre référentiel, ajoutez le `php.ini` vers la racine de l’application (racine du référentiel).

>[!TIP]
>
>La configuration incorrecte des paramètres PHP peut entraîner des problèmes. Par conséquent, seuls les administrateurs avancés doivent définir ces options.

### Augmentation de la limite de mémoire PHP

Pour augmenter la limite de mémoire PHP, ajoutez le paramètre suivant au paramètre `php.ini` fichier :

```ini
memory_limit = 1G
```

Pour le débogage, augmentez la valeur à 2G.

### Optimisation de la configuration realpath_cache

Définissez les `realpath_cache` pour améliorer les performances de l’application.

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

Ces paramètres permettent aux processus PHP de mettre en cache les chemins d’accès aux fichiers au lieu de les rechercher pour chaque chargement de page. Voir [Optimisation des performances](https://www.php.net/manual/en/ini.core.php) dans la documentation PHP.

>[!NOTE]
>
>Pour obtenir la liste des paramètres de configuration PHP recommandés, voir [Paramètres PHP requis](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) dans le _Guide d’installation_.

### Vérifier les paramètres PHP personnalisés

Après avoir appuyé sur la variable `php.ini` pour les modifications apportées à votre environnement cloud, vous pouvez vérifier que la configuration PHP personnalisée a été ajoutée à votre environnement. Par exemple, utilisez SSH pour vous connecter à l’environnement distant et afficher le fichier à l’aide de quelque chose comme suit :

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Si vous utilisez Cloud Docker pour Commerce pour le développement local, voir [Conteneurs de service Docker](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) pour plus d’informations sur l’utilisation d’un `php.ini` dans un environnement Docker.

## Activation des extensions

Vous pouvez activer ou désactiver des extensions PHP dans la variable `runtime:extension` . En outre, les extensions spécifiées deviennent disponibles dans les conteneurs PHP Docker.

>[!IMPORTANT]
>
>Avant d’activer les extensions, il est important de comprendre que la version PHP doit être compatible avec le système d’exploitation hébergeant le projet. L’équipe d’infrastructure peut avoir besoin d’une mise à niveau du système d’exploitation pour votre environnement de projet avant de pouvoir continuer.

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

| Extensions par défaut | Extensions installées<br>qui ne peut pas être désinstallé | Extensions qui peuvent être installées<br>et désinstallé selon les besoins |
| ------------------ | --------------------- | --------------------- |
| `bcmath`<br>`bz2`<br>`calendar`<br>`exif`<br>`gd`<br>`gettext`<br> `intl`<br> `mysqli`<br> `openswoole`<br> `pcntl`<br> `pdo_mysql`<br> `soap`<br> `sockets`<br>  `sysvmsg`<br> `sysvsem`<br> `sysvshm`<br> `opcache`<br> `zip` | `ctype`<br> `curl`<br>`date`<br> `dom`<br> `fileinfo`<br> `filter`<br> `ftp`<br> `hash`<br> `iconv`<br> `json`<br> `mbstring`<br> `mysqlnd`<br> `openssl`<br> `pcre`<br> `pdo`<br> `pdo_sqlite`<br> `phar`<br>`posix`<br> `readline`<br> `session`<br> `sqlite3`<br> `tokenizer`<br> `xml`<br> `xmlreader`<br> `xmlwriter`<br> | `geoip`<br>`gmp`<br> `igbinary`<br> `imagick`<br> `imap`<br> `ioncube` <br>`ldap`<br> `mailparse`<br> `mcrypt`<br> `msgpack`<br> `mysqli`<br> `oauth`<br> `pdo_mysql`<br> `propro`<br> `pspell`<br> `raphf`<br> `recode`<br> `redis`<br> `shmop` `sockets`<br> `sodium`<br> `ssh2`<br>`tidy`<br> `xdebug`<br> `xmlrpc`<br> `xsl`<br> `yaml` |

Les exigences du module PHP sont liées à la version Adobe Commerce. Voir [exigences PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Prise en charge des extensions

Pour les projets Pro, les extensions suivantes nécessitent une prise en charge supplémentaire pour l’installation :

- `sourceguardian`

Par exemple, pour configurer PHP afin d’exécuter uniquement les scripts protégés par SourceGuardian dans tous les environnements, l’option suivante doit être définie dans la variable `php.ini` fichier :

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Voir [section 3.5 de la documentation de SourceGuardian](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Lien vers un PDF_.

[Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour obtenir de l’aide sur l’installation de ces extensions PHP dans tous les environnements de production et les environnements d’évaluation Pro. Inclure votre mise à jour `.magento/services.yaml` fichier, `.magento.app.yaml` avec la version PHP mise à jour et toutes les extensions PHP supplémentaires. Pour les modifications apportées à un environnement de production actif, vous devez fournir un préavis d’au moins 48 heures. La mise à jour de votre projet peut prendre jusqu’à 48 heures pour que l’équipe chargée de l’infrastructure du cloud.

>[!WARNING]
>
>Le code PHP compilé avec le débogage n’est pas pris en charge et le proxy peut entrer en conflit avec [!DNL XDebug] ou [!DNL XHProf]. Désactivez ces extensions lors de l’activation de Probe. La propriété Probe entre en conflit avec certaines extensions PHP, telles que [!DNL Pinba] ou IonCube.
