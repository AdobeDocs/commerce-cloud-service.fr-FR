---
title: Configurer [!DNL Xdebug]
description: Découvrez comment configurer l’extension Xdebug pour déboguer votre Adobe Commerce sur le développement de projets d’infrastructure cloud.
exl-id: bf2d32d8-fab7-439e-8df3-b039e53009d4
source-git-commit: b49a51aba56f79b5253eeacb1adf473f42bb8959
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# Configuration de Xdebug

[!DNL Xdebug] est une extension pour le débogage de votre code PHP. Bien que vous puissiez utiliser un IDE de votre choix, le code suivant explique comment configurer [!DNL Xdebug] et [!DNL PhpStorm] pour le débogage dans votre environnement local.

>[!NOTE]
>
>Vous pouvez configurer [!DNL Xdebug] pour qu’il s’exécute dans l’environnement Cloud Docker pour le débogage local sans modifier votre configuration de projet d’infrastructure cloud Adobe Commerce. Voir [Configuration de Xdebug pour Docker](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/).

Pour activer [!DNL Xdebug], vous devez configurer un fichier dans votre référentiel Git, configurer votre IDE et configurer le transfert de port. Vous pouvez configurer certains paramètres dans le fichier `magento.app.yaml`. Après modification, envoyez les modifications Git à tous les environnements de démarrage et d’intégration Pro pour activer [!DNL Xdebug]. [!DNL Xdebug] est déjà disponible dans les environnements d’évaluation et de production Pro.

Une fois la configuration effectuée, vous pouvez déboguer des commandes d’interface de ligne de commande, des requêtes Web et du code. N’oubliez pas que tous les environnements d’infrastructure de cloud sont en lecture seule. Cloner le code vers votre environnement de développement local pour effectuer le débogage. Pour les environnements d’évaluation et de production Pro, voir [instructions supplémentaires](#debug-for-pro-staging-and-production) pour [!DNL Xdebug].

## Conditions

Pour exécuter et utiliser [!DNL Xdebug], vous avez besoin de l’URL SSH pour l’environnement. Vous pouvez localiser les informations via [[!DNL Cloud Console]](../project/overview.md) ou votre [!DNL Cloud Onboarding UI].

## Configuration de Xdebug

Pour configurer [!DNL Xdebug], procédez comme suit :

- [Utilisation d’une branche pour pousser les mises à jour des fichiers](#get-started-with-a-branch)
- [Activer [!DNL Xdebug] pour les environnements](#enable-xdebug-in-your-environment)
- [Configuration de votre IDE](#configure-phpstorm)
- [Configuration du transfert de port](#set-up-port-forwarding)

### Prise en main d’une branche

Pour ajouter [!DNL Xdebug], Adobe recommande de travailler dans [une branche de développement](../dev-tools/cloud-cli-overview.md#create-an-environment-branch).

### Activation de Xdebug dans votre environnement

Vous pouvez activer [!DNL Xdebug] directement dans tous les environnements Starter et les environnements d’intégration Pro. Cette étape de configuration n’est pas requise pour les environnements de production et d’évaluation Pro. Voir [Débogage pour l’évaluation et la production Pro](#debug-for-pro-staging-and-production).

Pour activer [!DNL Xdebug] pour votre projet, ajoutez `xdebug` à la section `runtime:extensions` du fichier `.magento.app.yaml`.

**Pour activer Xdebug** :

1. Dans votre terminal local, ouvrez le fichier `.magento.app.yaml` dans un éditeur de texte.

1. Dans la section `runtime`, sous `extensions`, ajoutez `xdebug`. Par exemple :

   ```yaml
   runtime:
       extensions:
           - redis
           - xsl
           - newrelic
           - sodium
           - xdebug
   ```

1. Enregistrez vos modifications dans le fichier `.magento.app.yaml` et quittez l’éditeur de texte.

1. Ajoutez, validez et poussez les modifications pour redéployer l’environnement.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Add xdebug"
   ```

   ```bash
   git push origin <environment-ID>
   ```

Lors du déploiement dans les environnements Starter et les environnements d’intégration Pro, [!DNL Xdebug] est désormais disponible. Continuez à configurer votre IDE. Pour PhpStorm, voir [Configuration de PhpStorm](#configure-phpstorm).

### Configuration de PhpStorm

L&#39;IDE [PhpStorm](https://www.jetbrains.com/phpstorm/) doit être configuré pour fonctionner correctement avec [!DNL Xdebug].

**Pour configurer PhpStorm de sorte qu’il fonctionne avec Xdebug** :

1. Dans votre projet PhpStorm, ouvrez le panneau **Paramètres**.

   - _macOS_ : sélectionnez **PhpStorm** > **Préférences**.
   - _Windows/Linux_ : Sélectionnez **Fichier** > **Paramètres**.

1. Dans le panneau _Settings_, développez et localisez la section **Languages &amp; Frameworks** > **PHP** > **Servers** .

1. Cliquez sur **+** pour ajouter une configuration de serveur. Le nom du projet est en gris dans la partie supérieure.

1. [Facultatif] Configurez les paramètres suivants pour la nouvelle configuration de serveur. Voir [Aucun serveur de débogage configuré](https://www.jetbrains.com/help/phpstorm/troubleshooting-php-debugging.html#no-debug-server-is-configured) dans la documentation _PHPStorm_.

   - **Nom** : saisissez le même nom que le nom d’hôte. Cette valeur doit correspondre à la valeur de la variable `PHP_IDE_CONFIG` dans les [commandes de l’interface de ligne de commande de débogage](#debug-cli-commands) pour utiliser l’interface de ligne de commande pour le débogage.
   - **Hôte** : saisissez le nom d’hôte.
   - **Port**—Entrez `443`.
   - **Debugger**—Sélectionnez `Xdebug`.

1. Sélectionnez **Utiliser les mappages de chemin d’accès**. Dans le volet _File/Directory_, la racine du projet pour `serverName` s’affiche.

1. Dans la colonne **Chemin absolu sur le serveur**, cliquez sur l&#39;icône **Modifier** et ajoutez un paramètre basé sur l&#39;environnement.

   - Pour tous les environnements Starter et les environnements d’intégration Pro, le chemin d’accès distant est `/app`.
   - Pour les environnements d’évaluation et de production Pro :

      - Production : `/app/<project_code>/`
      - Évaluation : `/app/<project_code>_stg/`

1. Remplacez le port [!DNL Xdebug] par 9000 dans le panneau **Languages &amp; Frameworks** > **PHP** > **Debug** > **Xdebug** > **Debug Port**.

1. Cliquez sur **Apply**.

### Configuration du transfert de port

Mappez la connexion `XDEBUG` du serveur à votre système local. Pour effectuer n’importe quel type de débogage, vous devez transférer le port 9000 de votre Adobe Commerce sur le serveur d’infrastructure cloud vers votre ordinateur local. Consultez l’une des sections suivantes :

- [Transfert de port sous Mac ou UNIX](#port-forwarding-on-mac-or-unix)
- [Transfert de port sous Windows](#port-forwarding-on-windows)

#### Transfert de port sur Mac ou UNIX®

**Pour configurer le transfert de port dans un Mac ou dans un environnement UNIX®** :

1. Ouvrez un terminal.

1. Utilisez SSH pour établir la connexion.

   ```bash
   ssh -R 9000:localhost:9000 <ssh url>
   ```

   Utilisez l’option `-v` (verbose) de sorte que chaque fois qu’un socket est connecté au port transféré, il s’affiche dans le terminal.

   Si une erreur &quot;impossible de se connecter&quot; ou &quot;impossible d’écouter le port à distance&quot; s’affiche, une autre session SSH active peut persister sur le serveur qui occupe le port 9000. Si cette connexion n&#39;est pas utilisée, vous pouvez l&#39;arrêter.

**Pour résoudre les problèmes de connexion** :

1. Utilisez SSH pour vous connecter à l’environnement d’intégration, d’évaluation ou de production distant.

1. Afficher la liste des sessions SSH : `who`

1. Affichage des sessions SSH existantes par utilisateur. Veillez à ne pas affecter un utilisateur autre que vous !

   - intégration : les noms d’utilisateur sont similaires à `dd2q5ct7mhgus`
   - Évaluation : les noms d’utilisateur sont similaires à `dd2q5ct7mhgus_stg`
   - Production : les noms d’utilisateur sont similaires à `dd2q5ct7mhgus`

1. Pour une session utilisateur plus ancienne que la vôtre, recherchez la valeur pseudo-terminal (PTS), telle que `pts/0`.

1. Exécutez l’ID de processus (PID) correspondant à la valeur PTS.

   ```bash
   ps aux | grep ssh
   kill <PID>
   ```

   Exemple de réponse :

   ```
   dd2q5ct7mhgus        5504  0.0  0.0  82612  3664 ?      S    18:45   0:00 sshd: dd2q5ct7mhgus@pts/0
   ```

   Pour mettre fin à la connexion, saisissez une commande de suppression avec l’ID de processus (PID).

   ```bash
   kill 3664
   ```

#### Transfert de port sous Windows

Pour configurer le transfert de port (tunnel SSH) sous Windows, vous devez configurer votre application de terminal Windows. Cet exemple passe par la création d’un tunnel SSH à l’aide de [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). Vous pouvez utiliser d’autres applications telles que Cygwin. Pour plus d’informations sur les autres applications, consultez la documentation du fournisseur fournie avec ces applications.

**Pour configurer un tunnel SSH sous Windows à l’aide de Putty** :

1. Si vous ne l&#39;avez pas déjà fait, téléchargez [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

1. Démarrez Putty.

1. Dans le volet Catégorie, cliquez sur **Session**.

1. Renseignez les informations suivantes :

   - **Nom d’hôte (ou adresse IP)** : Entrez l’ [URL SSH](../development/secure-connections.md#connect-to-a-remote-environment) pour votre serveur cloud
   - Champ **Port** : Entrée `22`

   ![Configurer Putty](../../assets/xdebug/putty-session.png)

1. Dans le volet _Category_, cliquez sur **Connection** > **SSH** > **Tunnels**.

1. Renseignez les informations suivantes :

   - Champ **Port Source** : Entrée `9000`
   - Champ **Destination** : Entrez `127.0.0.1:9000`
   - Cliquez sur **Remote**

1. Cliquez sur **Ajouter**.

   ![Création d’un tunnel SSH dans Putty](../../assets/xdebug/putty-tunnels.png)

1. Dans le volet _Category_, cliquez sur **Session**.

1. Dans le champ **Sessions enregistrées** , saisissez un nom pour ce tunnel SSH.

1. Cliquez sur **Enregistrer**.

   ![Enregistrer votre tunnel SSH](../../assets/xdebug/putty-session-save.png)

1. Pour tester le tunnel SSH, cliquez sur **Load**, puis sur **Open**.

   Si une erreur &quot;impossible de se connecter&quot; s’affiche, vérifiez les éléments suivants :

   - Tous les paramètres de coupure sont corrects
   - Vous exécutez Putty sur l’ordinateur sur lequel se trouvent vos clés SSH de votre Adobe Commerce privée sur l’infrastructure cloud

## Accès SSH aux environnements Xdebug

Pour lancer le débogage, effectuer la configuration, etc., vous avez besoin des commandes SSH pour accéder aux environnements. Vous pouvez obtenir ces informations par le biais de [[!DNL Cloud Console]](../development/secure-connections.md#use-an-ssh-command) et de la feuille de calcul de votre projet.

Pour les environnements Starter et les environnements d’intégration Pro, vous pouvez utiliser la commande d’interface de ligne de commande `magento-cloud` suivante pour SSH dans ces environnements :

```bash
magento-cloud environment:ssh --pipe -e <environment-ID>
```

Pour utiliser [!DNL Xdebug], SSH vers l’environnement comme suit :

```bash
ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH-URL>
```

Par exemple,

```bash
ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud
```

## Débogage pour l’évaluation et la production Pro

>[!NOTE]
>
>Dans les environnements d’évaluation et de production Pro, [!DNL Xdebug] est toujours disponible, car ces environnements ont une configuration spéciale pour [!DNL Xdebug]. Toutes les requêtes web normales sont acheminées vers un processus PHP dédié qui n’a pas [!DNL Xdebug]. Par conséquent, ces requêtes sont traitées normalement et ne sont pas soumises à la dégradation des performances lorsque [!DNL Xdebug] est chargé. Lorsqu’une requête web est envoyée avec la clé [!DNL Xdebug], elle est acheminée vers un processus PHP distinct dont [!DNL Xdebug] est chargé.

Pour utiliser [!DNL Xdebug] spécifiquement sur l’environnement d’évaluation et de production Pro-plan, vous créez un tunnel SSH distinct et une session web à laquelle vous avez accès. Cette utilisation diffère de l’accès type, en ce qu’elle ne vous permet d’accéder qu’à vous et non à tous les utilisateurs.

Vous avez besoin des éléments suivants :

- Commandes SSH pour accéder aux environnements. Vous pouvez obtenir ces informations via [[!DNL Cloud Console]](../project/overview.md) ou votre [!DNL Cloud Onboarding UI].
- La valeur `xdebug_key` définie lors de la configuration des environnements d’évaluation et Pro.

  L’ `xdebug_key` est accessible en utilisant SSH pour se connecter au noeud principal et s’exécuter :

  ```bash
  cat /etc/platform/*/nginx.conf | grep xdebug.sock | head -n1
  ```

**Pour configurer un tunnel SSH vers un environnement d’évaluation ou de production** :

1. Ouvrez un terminal.

1. Nettoyez toutes les sessions SSH pour chaque noeud web de la grappe.

   ```bash
   ssh USERNAME@CLUSTER.ent.magento.cloud 'rm /run/platform/USERNAME/xdebug.sock'
   ```

1. Configurez le tunnel SSH pour Xdebug pour chaque noeud web de la grappe.

   ```bash
   ssh -R /run/platform/USERNAME/xdebug.sock:localhost:9000 -N USERNAME@CLUSTER.ent.magento.cloud
   ```

**Pour commencer le débogage à l’aide de l’URL d’environnement** :

1. Activez le débogage à distance. Rendez-vous sur le site dans le navigateur et ajoutez ce qui suit à l’URL où `KEY` est la valeur de `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_START=KEY
   ```

   Cette étape définit le cookie qui envoie les demandes du navigateur pour déclencher [!DNL Xdebug].

1. Effectuez votre débogage avec [!DNL Xdebug].

1. Lorsque vous êtes prêt à mettre fin à la session, utilisez la commande suivante pour supprimer le cookie et terminer le débogage dans le navigateur où `KEY` est la valeur de `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_STOP=KEY
   ```

   >[!NOTE]
   >
   >Les demandes `XDEBUG_SESSION_START` transmises par `POST` ne sont pas prises en charge.

## Commandes de l’interface de ligne de commande de débogage

Cette section décrit les commandes de l’interface de ligne de commande du débogage.

Pour déboguer les commandes de l’interface de ligne de commande :

1. SSH dans le serveur que vous souhaitez déboguer à l’aide des commandes de l’interface de ligne de commande.

1. Créez les variables d’environnement suivantes :

   ```bash
   export XDEBUG_CONFIG='PHPSTORM'
   ```

   ```bash
   export PHP_IDE_CONFIG="serverName=<name of the server that is configured in PHPSTORM>"
   ```

   Ces variables sont supprimées lorsque la session SSH se termine.

1. Commencer le débogage

   Dans les environnements de démarrage et d’intégration Pro, exécutez la commande d’interface de ligne de commande pour déboguer.
Vous pouvez ajouter des options d’exécution, par exemple :

   ```bash
   php -d xdebug.profiler_enable=On -d xdebug.max_nesting_level=9999 bin/magento cache:clean
   ```

   Dans les environnements d’évaluation et de production Pro, vous devez spécifier le chemin d’accès au fichier de configuration PHP [!DNL Xdebug] lors du débogage des commandes de l’interface de ligne de commande, par exemple :

   ```bash
   php -c /etc/platform/USERNAME/php.xdebug.ini bin/magento cache:clean
   ```

## Déboguer les requêtes web

Les étapes suivantes vous aident à déboguer les requêtes web.

1. Dans le menu _Extension_, cliquez sur **Débogage** pour activer.

1. Cliquez avec le bouton droit de la souris, sélectionnez le menu Options, puis définissez la clé IDE sur **PHPSTORM**.

1. Installez le client [!DNL Xdebug] sur le navigateur. Configurez-le et activez-le.

### Exemple : configuration de Chrome

Cette section explique comment utiliser [!DNL Xdebug] dans Chrome à l’aide de l’extension [!DNL Xdebug] Helper. Pour plus d’informations sur les outils [!DNL Xdebug] d’autres navigateurs, consultez la documentation du navigateur.

**Pour utiliser l’assistant Xdebug avec Chrome** :

1. Créez un [tunnel SSH](#ssh-access-to-xdebug-environments) vers le serveur cloud.

1. Installez l’ [extension d’assistance Xdebug](https://chromewebstore.google.com/detail/eadndfjplgieldjbigjakmdgkmoaaaoc) à partir du magasin Chrome.

1. Activez l’extension dans Chrome comme illustré dans la figure suivante.

   ![Activez l’extension Xdebug dans Chrome](../../assets/xdebug/enable-chrome-ext.png)

1. Dans Chrome, cliquez avec le bouton droit de la souris sur l’icône d’assistance verte de la barre d’outils Chrome.

1. Dans le menu contextuel, cliquez sur **Options**.

1. Dans la liste _Clé IDE_, cliquez sur **PhpStorm**.

1. Cliquez sur **Enregistrer**.

   ![Options d’assistance Xdebug](../../assets/xdebug/helper-options.png)

1. Ouvrez votre projet PhpStorm.

1. Dans la barre de navigation supérieure, cliquez sur l’icône **Démarrer l’écoute** .

   Si la barre de navigation ne s’affiche pas, cliquez sur **Afficher** > **Barre de navigation**.

1. Dans le volet de navigation de PhpStorm, double-cliquez sur le fichier PHP à tester.

## Déboguer le code local

En raison des environnements en lecture seule, vous devez extraire du code vers le poste de travail local à partir d’un environnement ou d’une branche Git spécifique pour effectuer le débogage.

La méthode que vous choisissez dépend de vous. Vous disposez des options suivantes :

- Extraction de code à partir de Git et exécution `composer install`

  Cette méthode fonctionne à moins que `composer.json` ne référence des modules dans des référentiels privés auxquels vous n’avez pas accès. Cette méthode permet d’obtenir le code base Adobe Commerce entier.

- Copiez les répertoires `vendor`, `app`, `pub`, `lib` et `setup`

  Avec cette méthode, vous disposez de tout le code que vous pouvez tester. Selon le nombre de ressources statiques dont vous disposez, le transfert avec un volume de fichiers important peut être long.

- Copiez le répertoire `vendor` uniquement

  Étant donné que la plupart du code se trouve dans le répertoire `vendor`, cette méthode est susceptible d’entraîner de bons tests, même si elle ne teste pas l’ensemble du code base.

**Pour compresser des fichiers et les copier sur votre ordinateur local** :

1. Utilisez SSH pour vous connecter à l’environnement distant.

1. Compressez les fichiers.

   ```bash
   tar -czf /tmp/<file-name>.tgz <directory list>
   ```

   Par exemple, pour compresser uniquement le répertoire `vendor` :

   ```bash
   tar -czf /tmp/vendor.tgz vendor
   ```

1. Dans votre environnement local, utilisez PhpStorm pour compresser les fichiers.

   ```bash
   cd <phpstorm project root dir>
   ```

   ```bash
   rsync <SSH-URL>:/tmp/<file-name>.tgz .
   ```

   ```bash
   tar xzf <file-name>.tgz
   ```
