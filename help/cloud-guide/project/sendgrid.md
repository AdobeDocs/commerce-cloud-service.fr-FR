---
title: Service de messagerie SendGrid
description: Découvrez le service de messagerie SendGrid pour Adobe Commerce sur l’infrastructure cloud et comment tester votre configuration DNS.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 7c22dc3b0e736043a3e176d2b7ae6c9dcbbf1eb5
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Service de messagerie SendGrid

Le service proxy SMTP (Simple Mail Transfer Protocol) de SendGrid fournit des services de surveillance de l’authentification et de la réputation des emails sortants, notamment la prise en charge des éléments suivants :

* Tous les emails transactionnels sortants
* Adresses IP dédiées
* Enregistrement de domaine, signatures DomainKeys Identified Mail (DKIM) pour la validation de domaine d’email (pour les environnements d’évaluation et de production uniquement)
* Enregistrement de domaine personnalisé (pour Pro uniquement)
* Intégration automatisée pour les environnements d’intégration Starter et Pro. Les environnements de production et d’évaluation Pro nécessitent un approvisionnement et une configuration manuels pendant le processus d’approvisionnement matériel de l’infrastructure as a Service (IaaS).

Le proxy SMTP SendGrid n’est pas destiné à être utilisé comme serveur de messagerie d’usage général pour recevoir des emails entrants ou pour l’utiliser avec des campagnes de marketing par e-mail.

>[!TIP]
>
>Vous trouverez les détails de SendGrid pour votre compte dans la section [Interface utilisateur de l’intégration](https://cloud.magento.com) et sélectionnez la variable **Détails du projet** > **Informations sur l’hébergement** .

## Activation ou désactivation d’un email

Par défaut, les emails sortants sont activés dans les environnements Pro Production et Test. La variable [!UICONTROL Outgoing emails] peut apparaître dans les paramètres d’environnement, quel que soit l’état, jusqu’à ce que vous définissiez la variable `enable_smtp` . Vous pouvez activer les courriers électroniques sortants pour d’autres environnements afin d’envoyer des courriers électroniques d’authentification à deux facteurs aux utilisateurs de projet Cloud. Voir [Configuration d’emails à des fins de test](outgoing-emails.md).

## Tableau de bord SendGrid

Tous les projets Cloud sont gérés sous un compte central. Dès lors, seul l’assistance a accès au tableau de bord SendGrid. SendGrid ne fournit pas de fonctions de restriction de sous-compte.

Pour consulter les logs d’activité pour connaître l’état de la diffusion ou une liste des adresses email bloquées, rejetées ou rebonds, [envoyer un ticket d’assistance Adobe Commerce ;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). L’équipe d’assistance **cannot** récupérer les journaux d’activité de plus de 30 jours.

Si possible, incluez les informations suivantes dans votre requête :

* l’adresse électronique ou les adresses concernées ;
* la période en question (au cours des 30 derniers jours uniquement) ;
* l’objet de l’email

## DomainKeys Identified Mail (DKIM)

DKIM est une technologie d&#39;authentification d&#39;email qui permet aux fournisseurs d&#39;accès à Internet (FAI) d&#39;identifier les adresses d&#39;expéditeur légitimes et fausses, une technique couramment utilisée pour le phishing et les escroqueries par e-mail. DKIM s’appuie sur un propriétaire de domaine qui gère les enregistrements DNS. Lors de l&#39;utilisation de DKIM, le serveur expéditeur utilise une clé privée pour signer les messages. Le propriétaire du domaine ajoute également un enregistrement DKIM, qui est une modification `TXT` enregistrement, dans les enregistrements DNS du domaine de l’expéditeur. Ceci `TXT` L’enregistrement contient une clé publique que les serveurs de messagerie des destinataires utilisent pour vérifier la signature d’un message. La procédure de cryptographie à clé publique DKIM permet aux destinataires de vérifier l&#39;authenticité d&#39;un expéditeur. Voir [Explication des enregistrements DKIM](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>Les signatures DKIM SendGrid et la prise en charge de l’authentification de domaine sont disponibles uniquement pour les projets Pro et non pour Starter. Par conséquent, les emails transactionnels sortants sont susceptibles d’être marqués par des filtres de spam. L’utilisation de DKIM améliore le taux de diffusion en tant qu’expéditeur d’email authentifié. Pour améliorer le taux de diffusion des messages, vous pouvez effectuer une mise à niveau de Starter vers Pro ou utiliser votre propre serveur SMTP ou votre propre fournisseur de services de diffusion par email. Voir [Configuration des connexions par e-mail](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html) dans le _Guide sur les systèmes d’administration_.

### Authentification de l&#39;expéditeur et du domaine

Pour que SendGrid envoie des emails transactionnels en votre nom depuis des environnements de production ou d’évaluation, vous devez configurer vos paramètres DNS pour inclure les trois entrées DNS du sous-domaine SendGrid. Chaque compte SendGrid se voit attribuer une variable `TXT` enregistrement utilisé pour authentifier les emails sortants.

**Pour activer l’authentification de domaine**:

1. Envoyer un [ticket de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) qui demande d’activer le DKIM pour un domaine spécifique (**Environnements d’évaluation et de production professionnels uniquement**).
1. Mettez à jour votre configuration DNS avec la fonction `TXT` et `CNAME` les enregistrements vous ont été fournis dans le ticket d’assistance.

**Exemple `TXT` enregistrement avec ID de compte**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Exemple `CNAME` records**:

| Domaine | Points à | Type d’enregistrement |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### Signatures DKIM et sécurité automatisée

Vous pouvez choisir entre la sécurité automatisée et manuelle lors de la configuration d’un domaine authentifié. Si vous choisissez la sécurité automatisée, SendGrid gère automatiquement vos enregistrements DKIM et SPF. Lorsque vous ajoutez une nouvelle adresse IP d’envoi dédiée à votre compte, SendGrid met immédiatement à jour les paramètres DNS et la signature DKIM. Si vous désactivez la sécurité automatisée, vous êtes responsable de la mise à jour de votre signature DKIM chaque fois que vous changez de domaine d’envoi.

**Exemple de sécurité automatisée activée**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Exemple de sécurité automatisée désactivée**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Une fois l’authentification de domaine configurée, SendGrid gère automatiquement les enregistrements SPF (Security Policy Framework) et DKIM pour vous. After SendGrid fournit la variable `CNAME` enregistrements à ajouter à vos enregistrements DNS, vous pouvez ajouter des adresses IP dédiées et effectuer d’autres mises à jour de compte sans avoir à gérer vos enregistrements SPF manuellement. Voir [Sécurité automatisée et votre signature DKIM](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Pour tester votre configuration DNS :

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Seuil d&#39;email transactionnel

Le seuil de courriel transactionnel fait référence au nombre de messages électroniques transactionnels que vous pouvez envoyer à partir des environnements Pro au cours d’une période spécifique, comme 12 000 emails par mois provenant d’environnements hors production. Le seuil est conçu pour empêcher l’envoi de spam et d’endommager potentiellement la réputation de votre email.

Il n’existe aucune limite stricte au nombre d’emails pouvant être envoyés dans l’environnement de production, à condition que le score de réputation de l’expéditeur soit supérieur à 95 %. La réputation est affectée par le nombre d’emails rejetés ou rebonds et si les registres de spam basés sur DNS ont marqué votre domaine comme source potentielle de spam. Voir [Emails non envoyés lorsque les crédits SendGrid ont été dépassés sur Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded.html) dans le _Base de connaissances pour l’assistance commerciale_.

**Pour vérifier si le nombre maximal de crédits est dépassé**:

1. Sur votre poste de travail local, modifiez le répertoire de votre projet.

1. Utilisez SSH pour vous connecter à l’environnement distant.

   ```bash
   magento-cloud ssh
   ```

1. Vérifiez les `/var/log/mail.log` pour `authentication failed : Maxium credits exceeded` entrées.

   Si vous voyez des `authentication failed` les entrées du journal et la variable **Email sending réputation** est d’au moins 95, vous pouvez [Envoi d’un ticket d’assistance Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) pour demander une augmentation des crédits alloués.

### Email sending réputation

Une réputation d’envoi d’email est un score attribué par un fournisseur d’accès Internet (FAI) à une entreprise qui envoie des emails. Plus le score est élevé, plus un FAI est susceptible de diffuser des messages vers la boîte de réception d’un destinataire. Si le score est inférieur à un certain niveau, le FAI peut acheminer les messages vers le dossier spam des destinataires, voire rejeter complètement les messages. Le score de réputation est déterminé par plusieurs facteurs, tels qu’une moyenne de 30 jours de vos adresses IP par rapport à d’autres adresses IP et au taux de plaintes pour spam. Voir [5 façons de vérifier votre réputation d’envoi](https://sendgrid.com/blog/5-ways-check-sending-reputation/).
