---
title: Configuration de Commerce sur le cloud
description: Découvrez comment préparer un conseiller technique client Adobe pour approvisionner votre Adobe Commerce en projets d’infrastructure cloud.
recommendations: noDisplay, catalog
role: Admin
exl-id: cfb354b0-c255-4b6e-94aa-c5a6bf7230d6
source-git-commit: 269681efb9925d78ffb608ecbef657be740b5531
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Conditions préalables à la configuration de Commerce on Cloud

Commençons et initialisons votre projet Commerce sur l’infrastructure cloud !

Avant que Adobe ne mette en service votre Commerce dans les environnements de projet cloud, il est recommandé d’étudier les stratégies suivantes et de préparer les réponses pour votre première consultation avec votre équipe de compte d’Adobe. Utilisez les sections suivantes comme liste de contrôle pour vous aider à préparer votre conversation avec un conseiller technique du client pour configurer un projet cloud :

## Définition de domaine

**Question 1** : _Quels domaines avez-vous l’intention d’utiliser pour le lancement du site ?_

Préparez-vous à intégrer les services Fastly et Nginx en définissant vos domaines et sous-domaines de niveau supérieur pour les environnements d’évaluation et de production Pro. Après la configuration initiale, vous pouvez uniquement ajouter des domaines en envoyant un ticket d’assistance Adobe Commerce. Il est donc recommandé de préparer les informations sur les domaines.

Exemples pour les domaines de production et d’évaluation :

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Pour plus d’informations sur les domaines multiples ou uniques, voir [Configuration de plusieurs sites Web ou magasins](../cloud-guide/store/multiple-sites.md) dans le guide _Commerce on Cloud Infrastructure_ .

Voir [Plusieurs comptes et domaines attribués à un instant donné](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly#multiple-fastly-accounts-and-assigned-domains){target="_blank"} si vous disposez d’un compte Fastly existant qui lie les mêmes apex et sous-domaines utilisés sur votre site Adobe Commerce.

## Domaine de l’email transactionnel

**Question 2** : _Quels domaines avez-vous l’intention d’utiliser pour les emails transactionnels ?_

Adobe Commerce on Cloud utilise le service proxy SMTP (Simple Mail Transfer Protocol) SendGrid, qui fournit des services de surveillance de réputation et d’authentification des emails sortants. SendGrid envoie des emails transactionnels en votre nom, ce qui nécessite des informations sur le domaine.

Exemple pour le domaine SendGrid : `example@your-store.com`

Voir [SendGrid mail service](../cloud-guide/project/sendgrid.md) dans le guide _Commerce on Cloud Infrastructure_ pour plus d’informations sur les emails transactionnels et les paramètres de domaine.

## Allocation de stockage

**Question 3** : _Quelle quantité de stockage sous contrat prévoyez-vous d&#39;allouer pour le téléchargement de fichiers et pour la base de données ?_

Adobe Commerce sur l’infrastructure cloud utilise le stockage pour la structure de fichiers, l’indexation de recherche et la base de données. Vous pouvez subdiviser le stockage selon vos besoins en commençant par 10 Go pour chaque partition.

La quantité d’espace de stockage sous contrat pour votre projet cloud représente l’espace de stockage total pour chaque environnement. Par exemple, si vous avez acheté 50 Go d’espace de stockage, vous disposez alors de 50 Go de stockage pour chaque environnement. Il existe 50 Go de stockage distinct pour la production, l’évaluation et chaque environnement d’intégration, respectivement.

Vous pouvez augmenter à tout moment votre capacité de stockage sous contrat. Pour les environnements de production et d’évaluation, vous devez envoyer un ticket d’assistance Adobe Commerce pour modifier l’allocation de l’espace disque. Une augmentation de la taille des environnements de production et d’évaluation peut uniquement survenir à certains intervalles. Selon l’utilisation actuelle de l’espace disque, l’équipe d’assistance peut recommander une augmentation de l’allocation de l’espace disque d’au moins 10 Go. Une fois allouée, l’augmentation de stockage pour l’environnement d’évaluation et de production Pro peut **et non** être annulée.

Voir [Gestion de l’espace disque](../cloud-guide/storage/manage-disk-space.md) dans le guide _Commerce on Cloud Infrastructure_.

## Région de service cloud

**Question 4** : _Quelle région de service cloud est la plus proche de votre proximité ?_

Choisissez Amazon Web Services (AWS) ou Microsoft Azure en tant que base d’infrastructure en tant que service (IaaS) pour vos projets Adobe Commerce sur l’infrastructure cloud Pro. Chaque prestataire opère dans plusieurs régions et fournit plusieurs zones de disponibilité. Sélectionnez une région qui vous convient le mieux et réduisez le risque de latence et d’augmentation des coûts.

Voir [une carte des régions cloud Adobe Commerce](../cloud-guide/overview.md).

## Service de connexion

**Question 5** : _Avez-vous besoin d’un service PrivateLink ? Si oui, dans quelle région est la connexion PrivateLink ?_

Adobe Commerce sur l’infrastructure cloud prend en charge l’intégration au service AWS PrivateLink ou Azure Private Link. Bien que ce service soit facultatif, PrivateLink est utilisé pour établir une communication privée sécurisée entre les environnements d’infrastructure cloud avec des services et des applications hébergés sur des systèmes externes.

Il est important de tenir compte de votre stratégie de service cloud (AWS ou Azure) afin que l’instance Adobe Commerce soit accessible dans la même région. Pour plus d’informations sur l’accessibilité régionale, voir [Service PrivateLink](../cloud-guide/development/privatelink-service.md) dans le guide _Commerce on Cloud Infrastructure_.

## Lancement du site Target

**Question 6** : _Quelle est la date prévue de lancement de votre projet ?_

Le lancement d’un site nécessite une configuration itérative et des tests pour garantir le succès de votre lancement. La définition d’une date cible vous permet, ainsi qu’à votre équipe de compte d’Adobe, de vous préparer aux activités finales de prélancement, qui incluent un appel pour coordonner les étapes finales.

Consultez la [présentation du site Launch](../cloud-guide/launch/overview.md) dans le guide _Commerce on Cloud Infrastructure_ pour passer en revue l’ensemble du processus et télécharger une copie de la liste de contrôle de Launch.

>[!TIP]
>
> Jetez un coup d’oeil rapide au portail Cloud et accédez à votre nouveau projet cloud.
>
>**Étape suivante** : [Intégration à Commerce](onboarding.md)
