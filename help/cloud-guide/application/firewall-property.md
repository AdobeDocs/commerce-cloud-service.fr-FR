---
title: Propriété du pare-feu
description: Voir des exemples sur la configuration de la propriété de pare-feu dans le fichier de configuration de l’application Commerce.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
source-git-commit: a8ecebc87bfae5deaf0fc7ff3e7dd3b255fe3f24
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Propriété du pare-feu

>[!IMPORTANT]
>
>Projets de démarrage uniquement

Pour les projets de démarrage, la propriété `firewall` ajoute un pare-feu _sortant_ à l’application. Ce pare-feu n’a aucun effet sur les requêtes entrantes. Il définit les `tcp` requêtes sortantes qui peuvent _laisser_ un site Adobe Commerce. Cela s’appelle le filtrage par sortie. Le pare-feu sortant filtre ce qui peut sortir (quitter ou échapper votre site). La limitation de ce qui peut échapper ajoute un puissant outil de sécurité à votre serveur.

## Stratégies de restriction par défaut

Le pare-feu fournit deux stratégies par défaut pour contrôler le trafic sortant : `allow` et `deny`. La stratégie `allow` _permet_ tout le trafic sortant par défaut. Et la stratégie `deny` _refuse_ tout le trafic sortant par défaut. Mais lorsque vous ajoutez une règle, la stratégie par défaut est remplacée et le pare-feu bloque le trafic sortant **all** non autorisé par la règle.

Pour les plans de démarrage, la stratégie par défaut est définie sur `allow`. Ce paramètre garantit que tout le trafic sortant actuel reste débloqué jusqu’à ce que vous ajoutiez vos règles de filtrage de sortie. La stratégie par défaut peut être définie sur `deny` sur demande.

**Pour vérifier votre stratégie par défaut** :

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

À moins que vous n’ayez demandé `deny` pour votre stratégie, la commande doit afficher votre jeu de stratégies sur `allow` :

```json
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Suppression de clés** : lorsque vous ajoutez une règle sortante, vous bloquez tout le trafic sortant, à l’exception des domaines, adresses IP ou ports que vous ajoutez à la règle. Il est donc important de définir et de tester une liste sortante complète avant de l’ajouter à votre site de production.

## Options de pare-feu

L’exemple de configuration suivant dans le fichier `.magento.app.yaml` affiche toutes les options `firewall` que vous pouvez utiliser pour ajouter des règles pour votre filtrage de sortie.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Règles de filtrage sortantes

Les configurations de pare-feu sortantes sont composées de règles. Vous pouvez définir autant de règles que nécessaire. Les exigences relatives aux règles sont les suivantes.

**Chaque règle :**

- Doit commencer par un tiret (`-`). L’ajout d’un commentaire sur la même ligne permet de documenter et de séparer visuellement une règle de la suivante.
- Doit définir au moins une des options suivantes : `domains`, `ips` ou `ports`.
- Doit utiliser le protocole `tcp`. Puisqu’il s’agit du protocole par défaut pour toutes les règles, vous pouvez l’omettre de la règle.
- Peut définir `domains` ou `ips`, mais pas les deux dans la même règle.
- Peut inclure `yaml` commentaires (`#`) et sauts de ligne pour organiser les domaines, adresses IP et ports autorisés.

Chaque règle utilise les propriétés suivantes :

### `domains`

L’option `domains` permet une liste de noms de domaine entièrement qualifiés (FQDN).

Si une règle définit `domains`, mais pas `ports`, le pare-feu autorise les requêtes de domaine sur n’importe quel port.

### `ips`

L’option `ips` permet une liste d’adresses IP dans la notation CIDR. Vous pouvez spécifier des adresses IP uniques ou des plages d’adresses IP.

Pour spécifier une seule adresse IP, ajoutez le préfixe CIDR `/32` à la fin de votre adresse IP :

```
172.217.11.174/32  # google.com
```

Pour spécifier une plage d’adresses IP, utilisez le calculateur [Plage IP vers CIDR](https://ipaddressguide.com/cidr).

Si une règle définit `ips`, mais pas `ports`, le pare-feu autorise les requêtes IP sur n’importe quel port.

### `ports`

L’option `ports` permet une liste de ports compris entre 1 et 65535. Pour la plupart des règles de l’exemple, les ports `80` et `443` autorisent les requêtes HTTP et HTTPS. Toutefois, pour New Relic, les règles n’autorisent que l’accès aux domaines et adresses IP sur le port `443`, comme recommandé dans la documentation New Relic sur le [trafic réseau](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents).

Si une règle définit uniquement `ports`, le pare-feu permet d’accéder à tous les domaines et adresses IP pour les ports définis.

>[!NOTE]
>
>Le port `25`, le port SMTP pour envoyer des emails, est toujours bloqué, sans exception.

### `protocol`

Comme mentionné, TCP est le protocole par défaut et seul le protocole autorisé pour les règles. UDP et ses ports ne sont pas autorisés. Pour cette raison, vous pouvez omettre l’option `protocol` de toutes les règles. Si vous souhaitez l’inclure de toute façon, vous devez définir la valeur sur `tcp`, comme illustré dans la première règle de l’exemple.

## Recherche des noms de domaine à autoriser

Pour vous aider à identifier les domaines à inclure dans vos règles de filtrage de sortie, utilisez la commande suivante pour analyser le fichier `dns.log` de votre serveur et afficher une liste de toutes les requêtes DNS enregistrées par votre site :

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

Cette commande affiche également les demandes DNS qui ont été effectuées mais bloquées par vos règles de filtrage de sortie. La sortie n’affiche pas les domaines bloqués, mais uniquement les demandes effectuées. La sortie n’affiche pas les demandes effectuées à l’aide d’une adresse IP.

```
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Contrairement aux adresses IP, les domaines sont généralement plus spécifiques et sécurisés pour le filtrage de sortie. Par exemple, si vous ajoutez une adresse IP pour un service qui utilise un CDN, vous autorisez l’adresse IP du CDN, qui peut être utilisée par des centaines ou des milliers d’autres domaines. Avec une adresse IP, vous pourriez autoriser l’accès sortant à des milliers d’autres serveurs.

## Test des règles de filtrage de sortie

Après avoir collecté et configuré les règles d’accès pour les domaines et les adresses IP dont votre site a besoin, il est temps de pousser et de tester.

Pour tester vos règles de filtrage de sortie :

1. Créez un script shell de commandes `curl` pour accéder aux domaines et adresses IP de vos règles. Incluez des commandes qui testent l’accès aux domaines et adresses IP qui doivent être bloqués.

1. Configurez un crochet `post_deploy` dans votre fichier `.magento.app.yaml` pour exécuter le script.

1. Poussez votre configuration `firewall` et votre script de test vers votre branche `integration`.

1. Examinez la sortie `post_deploy` de vos commandes `curl`.

1. Affinez vos règles `firewall`, mettez à jour votre script `curl`, validez, push et répétez.

### Exemple de script `curl`

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### Exemple `post_deploy`

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
