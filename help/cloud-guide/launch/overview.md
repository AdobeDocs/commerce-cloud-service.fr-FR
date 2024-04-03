---
title: Lancement du site
description: Découvrez comment commencer la préparation du lancement du site.
exl-id: a7b3f260-b76e-4220-b521-699548a9928a
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Lancement du site

Une fois le déploiement et les tests terminés dans les environnements d’intégration et d’évaluation, vous pouvez commencer la préparation du lancement du site. Tout d’abord, vous devez terminer tous les tests et le développement avant de travailler dans l’environnement de production. Vous êtes prêt à démarrer ? Consultez les listes de contrôle, les bonnes pratiques et les dernières étapes pour lancer votre site.

Si vous avez vérifié ces informations avant de procéder au déploiement et au test dans l’environnement d’évaluation, pensez à passer en revue les avantages des tests dans l’environnement d’évaluation en premier dans la section suivante. L’évaluation est un environnement de quasi-production s’exécutant sur des composants matériels, des configurations, une architecture et des services similaires. Il peut réduire vos temps d’arrêt et rendre vos extensions, services, configurations personnalisées et tests d’acceptation des utilisateurs du marché indispensables à la publication de vos sites et magasins.

## Pourquoi tester entièrement l’intégration, l’évaluation et la production ?

Nous vous recommandons vivement de tester dans les environnements d’intégration, d’évaluation et de production en raison de la complexité liée à la garantie que votre code personnalisé, vos thèmes, extensions et intégrations tierces fonctionnent tous ensemble pour exploiter vos magasins. Vous trouverez ci-dessous des problèmes courants que vous pouvez résoudre lorsque vous effectuez des tests dans les environnements d’intégration et d’évaluation avant de mettre à jour votre environnement de production :

- L’évaluation prend en charge tous les services de production, fonctionnalités, données de base de données, pile de technologie, architecture, etc. Cela reflète la production, ce qui signifie que si des erreurs se produisent dans l’évaluation, vous avez un avertissement avant qu’elles ne se produisent dans l’environnement de production.

- Le code qui fonctionne dans votre environnement d’intégration local peut ne pas fonctionner dans les environnements d’évaluation et de production.

- Les environnements d’intégration ne prennent pas en charge certains services disponibles dans les environnements d’évaluation et de production, tels que Fastly et New Relic.

- [Test complet](../test/guidance.md) votre site avec divers outils d’évaluation pour le chargement, le stress, les performances et les ressources du site.

- Dans la mesure où les environnements d’intégration peuvent uniquement comporter des bases de données remplies de données de test, ne correspondant pas à un environnement de type production, vous risquez de rencontrer des erreurs supplémentaires ou un comportement inattendu lors des tests dans les environnements d’évaluation ou de production.

## Conditions préalables au lancement du site

Vous avez besoin des informations et ressources suivantes pour vous préparer au lancement du site :

- Informations d’enregistrement CNAME pour la configuration du DNS

- Liste de tous les domaines storefront à ajouter au certificat

- Certificat SSL/TLS

Dans le cadre d’Adobe Commerce sur l’abonnement à l’infrastructure cloud, Adobe fournit un certificat SSL/TLS validé par le domaine, émis par Let’s Encrypt. Chaque production, évaluation et démarrage (`master`) a un certificat unique qui couvre tous les domaines et sous-domaines de cet environnement. Ces certificats sont configurés et téléchargés automatiquement sur votre site après la mise à jour de votre configuration DNS pour le développement et la production. Voir [Configuration de certificats SSL/TLS](../cdn/fastly-configuration.md#provision-ssltls-certificates).

>[!NOTE]
>
>Si vous souhaitez déployer votre propre certificat SSL de validation étendue pour votre entreprise au lieu d’utiliser le certificat de chiffrement, contactez votre CTA ou [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

## Configuration de l’outil d’analyse de sécurité

>[!NOTE]
>
>L’outil d’analyse de sécurité utilise les adresses IP publiques suivantes :
>
>```text
>52.87.98.44
>34.196.167.176
>3.218.25.102
>```
>
>Ajoutez ces adresses IP à une liste autorisée dans les règles de pare-feu de votre réseau pour permettre à l’outil d’analyser votre site. L’outil publie des requêtes sur les ports 80 et 443 uniquement.

L’outil d’analyse de sécurité vous permet de surveiller régulièrement vos sites web de magasin et de recevoir des mises à jour concernant les risques de sécurité connus, les logiciels malveillants et les logiciels obsolètes. Cet outil est un service gratuit disponible pour toutes les mises en oeuvre et versions d’Adobe Commerce sur l’infrastructure cloud. Vous accédez à l’outil via votre [Compte de Commerce Marketplace](https://account.magento.com/customer/account/login).

- Surveiller l’état de sécurité de vos sites et appliquer les mises à jour de sécurité

- Recevoir les mises à jour de sécurité et les notifications spécifiques au site

Voir [Guide de l’utilisateur](https://docs.magento.com/user-guide/magento/security-scan.html) pour plus d’informations sur la configuration et l’utilisation de l’outil d’analyse de sécurité. En règle générale, vous commencez à utiliser cet outil lorsque vous commencez les tests d’acceptation utilisateur (UAT).

Chaque site que vous analysez doit être enregistré via l’onglet Analyse de sécurité . Pendant le processus d’enregistrement, vous devez accepter la clause de non-responsabilité avant de pouvoir commencer l’analyse. Vous contrôlez le planning et autorisez l’utilisateur à recevoir des notifications une fois chaque analyse terminée. Vous pouvez planifier des analyses pour une date et une heure récurrentes spécifiques, ou exécuter une analyse à la demande, si nécessaire.

L’outil d’analyse de sécurité utilise plusieurs chaînes d’agent utilisateur pour simuler l’activité des logiciels malveillants en temps réel. Les agents utilisateur suivants peuvent s’afficher dans vos journaux d’analyse ou d’accès :

```text
Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0
GuzzleHttp/6.3.3 curl/7.29.0 PHP/7.1.18
Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.120 Safari/537.36
Visbot/2.0 (+http://www.visvo.com/en/webmasters.jsp;bot@visvo.com)
```

## Analyser votre site

1. Accédez à [Compte de Commerce Marketplace](https://account.magento.com/customer/account/login).

1. Cliquez sur l’onglet Analyse de sécurité et sélectionnez **Accéder à l’analyse de sécurité**.

1. Dans le _Actions_ pour le site, sélectionnez **Exécution de l’analyse**. Un état de notification affiche l’analyse planifiée.

### Pour consulter le rapport :

1. Une fois le rapport terminé, une notification s’affiche.

1. Sur la ligne du site, sélectionnez le rapport à afficher dans la **Rapports** colonne . La commande est la plus récente à la plus ancienne.

Le rapport répertorie les problèmes, notamment les analyses ayant échoué, les résultats non identifiés et les analyses ayant réussi. Chaque entrée fournit des informations détaillées sur l’analyse, une liste des problèmes à examiner et des actions à entreprendre. Certaines de ces actions peuvent nécessiter le téléchargement et l’installation de correctifs de sécurité. Ajoutez les correctifs requis à une branche de développement sur votre poste de travail local avant de les ajouter à la branche de production.

Les résultats de l’analyse incluent un libellé qui décrit l’état de réussite ou d’échec de l’analyse avec des informations détaillées sur les vérifications effectuées :

- &quot;Failed&quot; indique que le site web contient une vulnérabilité majeure.

- &quot;Non identifié&quot; suggère qu’une révision plus approfondie est requise par votre équipe ou votre fournisseur d’hébergement pour déterminer si d’autres actions sont nécessaires.

Les résultats de l’analyse fournissent également des solutions suggérées pour chaque test de sécurité ayant échoué. Les résultats de l’analyse de sécurité sont protégés et visibles uniquement par l’utilisateur enregistré. Seuls les utilisateurs désignés dans le processus d’enregistrement du site reçoivent des notifications de fin de l’analyse.

## Prêt à lancer votre site

Lorsque vous êtes prêt à lancer le processus de lancement du site, reportez-vous aux sections suivantes :

- [Liste de contrôle de lancement](checklist.md)

- [Étapes de lancement](steps.md)
