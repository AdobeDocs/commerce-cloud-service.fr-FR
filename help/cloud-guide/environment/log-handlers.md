---
title: Gestionnaires de journaux
description: Découvrez comment configurer des gestionnaires de journaux pour Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Logs, Configuration
role: Developer
exl-id: d3be7b6d-5778-4c32-865b-31bdb2852a23
source-git-commit: f8e35ecff4bcafda874a87642348e2d2bff5247b
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Gestionnaires de journaux

Vous pouvez configurer des gestionnaires de journaux pour envoyer des messages à un serveur de journalisation distant. Un gestionnaire de journaux envoie les journaux de création et de déploiement vers d’autres systèmes, de la même manière que vous envoyez les journaux vers Slack et e-mail. Vous pouvez activer un gestionnaire _syslog_, idéal pour consigner les messages liés au matériel, ou un gestionnaire GELF (Graylog Extended Log Format), idéal pour consigner les messages à partir d’applications logicielles.

L’exemple suivant configure ces deux gestionnaires en ajoutant la configuration au fichier `.magento.env.yaml`. Pour obtenir les valeurs de niveau de journalisation minimum (`min_level`), voir [Niveaux de journalisation](#log-levels).

```yaml
log:
  syslog:
    ident: "<syslog-ident>"
    facility: 8 # https://php.net/manual/en/network.constants.php
    min_level: "info"
    logopts: <syslog-logopts>

  syslog_udp:
    host: "<syslog-host>"
    port: <syslog-port>
    facility: 8  # https://php.net/manual/en/network.constants.php
    ident: "<syslog-ident>"
    min_level: "info"

  gelf:
    min_level: "info"
    use_default_formatter: true
    additional: # Some additional information for each log message
      project: "<some-project-id>"
      app_id: "<some-app-id>"
    transport:
      http:
        host: "<http-host>"
        port: <http-port>
        path: "<http-path>"
        connection_timeout: 60
      tcp:
        host: "<tcp-host>"
        port: <tcp-port>
        connection_timeout: 60
      udp:
        host: "<udp-host>"
        port: <udp-port>
        chunk_size: 1024
```

## Niveaux de journalisation

Les niveaux de journal déterminent le niveau de détail dans les messages de notification. Les catégories de niveau journal suivantes incluent chaque niveau de journal situé en dessous. Par exemple, un niveau `debug` comprend la journalisation à partir de chaque niveau, tandis qu’un niveau `alert` affiche uniquement les alertes et les urgences.

- **debug**—informations de débogage détaillées
- **info** : événements intéressants, tels qu’une connexion utilisateur ou un journal SQL
- **notice** : événements normaux mais significatifs
- **warning** : occurrences exceptionnelles qui ne sont pas des erreurs, telles que l’utilisation d’une API obsolète ou l’utilisation incorrecte d’une API
- **error** : erreurs d’exécution qui ne nécessitent pas d’action immédiate
- **critical** : conditions critiques telles qu’un composant d’application indisponible ou une exception inattendue
- **alert** : action immédiate requise (par exemple, un site web est en panne ou la base de données n’est pas disponible) qui déclenche une alerte SMS
- **urgence** : le système est inutilisable
