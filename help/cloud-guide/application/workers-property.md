---
title: Travailleurs
description: Découvrez comment configurer la propriété des objets Worker dans le [!DNL Commerce] fichier de configuration de l’application.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Propriété des travailleurs

Vous pouvez définir un programme de travail pour qu’il s’exécute indépendamment de l’instance web sans qu’une instance Nginx en cours d’exécution ne soit utilisée par le même espace de stockage réseau que celui utilisé par l’événement [!DNL Commerce] application. Il n’est pas nécessaire de configurer un serveur web sur l’instance de travail (à l’aide de Node.js ou Go), car le routeur ne peut pas diriger de requêtes publiques vers le programme de travail. L’instance de travail est ainsi idéale pour les tâches en arrière-plan ou les tâches en cours d’exécution qui risquent de bloquer un déploiement.

## Configuration d’un programme de travail

Les programmes de travail ne peuvent être utilisés qu’avec les environnements d’évaluation et de production Pro. Les environnements Pro Integration et Starter peuvent choisir d’utiliser la variable [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) Variable .

Pour configurer un programme de travail dans l’environnement intermédiaire ou de production, [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) et incluez les informations suivantes :

- Identifiant de projet
- Identifiant d’environnement
- Nom du traitement
- Commandes de démarrage

Vous pouvez configurer un processus par programme de travail. Une configuration de travail courant de base dans la fonction `.magento.app.yaml` peut ressembler à ce qui suit :

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

Cet exemple définit un seul traitement nommé `queue`, avec un faible niveau (taille S) d’allocation de ressources, et exécute la variable `php ./bin/magento` au démarrage. Le travailleur `queue` s’exécute ensuite sur chaque noeud en tant que processus de travail. Si la commande sort, elle est automatiquement redémarrée.

## Commandes et remplacements

La variable `commands.start` est nécessaire pour lancer des commandes avec l’application de travail. Vous pouvez utiliser n’importe quelle commande shell valide, bien qu’il soit idéal d’utiliser la langue de votre application. Si la commande spécifiée par la propriété `start` se termine, il redémarre automatiquement.

>[!IMPORTANT]
>
>La variable `deploy` et `post_deploy` hooks et `crons` Les commandes s’exécutent uniquement sur le conteneur web, et non sur les instances de programme de travail.

### Héritage

Définitions de la variable `size`, `relationships`, `access`, `disk` et `mount`, et `variables` Les propriétés sont héritées par un programme de travail, sauf si elles sont explicitement remplacées.

Les propriétés suivantes sont les plus couramment utilisées pour remplacer [paramètres de niveau supérieur](properties.md):

- `size`: allouer moins de ressources à un seul processus en arrière-plan
- `variables`: demande à l’application de s’exécuter différemment.

### Minutage et mise en file d’attente

Bien que chaque programme de travail effectue des files d’attente derrière une autre, la configuration suivante produit une séparation cohérente de deux secondes dans les horodatages dans la variable `var/time.txt` , indépendamment du sommeil de huit secondes dans le code PHP :

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
