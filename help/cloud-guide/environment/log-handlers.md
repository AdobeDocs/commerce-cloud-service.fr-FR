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

Vous pouvez configurer des gestionnaires de journaux pour envoyer des messages à un serveur de journalisation distant. Un gestionnaire de journaux envoie les journaux de création et de déploiement vers d’autres systèmes, de la même manière que vous envoyez les journaux vers Slack et e-mail. Vous pouvez activer une _syslog_ gestionnaire, idéal pour la journalisation des messages liés au matériel, ou gestionnaire GELF (Graylog Extended Log Format), idéal pour la journalisation des messages à partir d’applications logicielles.

L’exemple suivant configure ces deux gestionnaires en ajoutant la configuration à la variable `.magento.env.yaml` fichier . Pour le niveau de journalisation minimal (`min_level`), voir [Niveaux de journalisation](#log-levels).

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

Les niveaux de journal déterminent le niveau de détail dans les messages de notification. Les catégories de niveau journal suivantes incluent chaque niveau de journal situé en dessous. Par exemple, un `debug` inclut la journalisation à partir de tous les niveaux, tandis qu’un `alert` n’affiche que les alertes et les urgences.

- **debug**—informations de débogage détaillées
- **info**: événements intéressants, tels qu’une connexion utilisateur ou un journal SQL
- **notice**—événements normaux mais significatifs
- **warning**: occurrences exceptionnelles qui ne sont pas des erreurs, telles que l’utilisation d’une API obsolète ou une mauvaise utilisation d’une API
- **error**—erreurs d’exécution qui ne nécessitent pas d’action immédiate
- **critique**: conditions critiques, telles qu’un composant d’application indisponible ou une exception inattendue
- **alerte**: action immédiate requise (par exemple, un site web est hors service ou la base de données est indisponible) qui déclenche une alerte SMS
- **urgence**—system est inutilisable
