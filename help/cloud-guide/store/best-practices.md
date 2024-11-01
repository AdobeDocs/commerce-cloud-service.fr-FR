---
title: Bonnes pratiques relatives à la configuration des magasins
description: Découvrez les bonnes pratiques pour configurer votre boutique sur Adobe Commerce sur l’infrastructure cloud.
feature: Cloud, Best Practices
exl-id: 01f528bd-74c2-42e7-8e77-7e6f57a40ef4
source-git-commit: 196efa316b9998c1980412ad96577d7ce42d4aec
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Bonnes pratiques relatives à la configuration des magasins

Pour plus d’informations sur la configuration de votre boutique, de vos sites et de vos sites web, vous pouvez consulter le [Guide de l’utilisateur d’Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html). Cette page fournit des bonnes pratiques, des informations utiles et des instructions pour configurer vos magasins, sites, etc. avec du contenu supplémentaire à publier au fil du temps et entre différentes versions.

## Campagnes marketing et promotions

Ces informations sont utiles pour Adobe Commerce sur l’infrastructure cloud 2.1.X et 2.2.X.

Pour créer des campagnes et des promotions, créez les options et paramètres dans [Content Staging](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html). Cette fonctionnalité vous permet de créer et de prévisualiser vos campagnes avant de les rendre publiques pour les ventes des clients. Les informations suivantes fournissent des informations utiles. Pour obtenir des instructions exactes, reportez-vous au contenu du guide de l’utilisateur Adobe Commerce associé.

_Les campagnes_ sont des événements marketing pour les ventes saisonnières, les nouvelles lignes de produits, etc. Chaque campagne peut inclure des thèmes personnalisés, des blocs pour le contenu, des widgets pour contrôler et afficher le contenu, ainsi que des promotions associées aux règles de prix. En raison de la nature étendue d’une campagne, vous pouvez les créer avec des dates de début et de fin par le biais de l’évaluation du contenu.

_Les promotions_ offrent des remises, des offres ponctuelles, des bons, des avantages pour le premier acheteur, etc. Vous créez ces promotions sous la forme de _Règles de prix_ qui définissent les termes, remises et options pour encourager les clients à acheter. Vous pouvez créer des règles de prix sur le [panier](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart.html) ou le [catalogue](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rules-catalog.html), avec des options supplémentaires pour les bannières, les points de récompense, etc. Vous pouvez planifier des campagnes pour vos promotions, en appliquant des règles de prix pour les événements majeurs, tels qu’une nouvelle gamme de produits ou des ventes saisonnières.

Vous trouverez ci-dessous des conseils pour créer, mettre à jour et gérer des promotions et des campagnes :

* Une promotion peut faire partie d’une campagne. Une campagne ne peut pas faire partie d’une promotion. Vous pouvez avoir des listes de promotions comme règles de prix pour utiliser plusieurs fois, avec plusieurs campagnes.
* Lorsque vous créez une promotion, elle crée toujours une campagne initiale inactive. Il a une date de début mais pas une date de fin. Vous pouvez ignorer cette campagne initiale. Vous pouvez planifier une nouvelle mise à jour avec le planning de campagne correct et l’activer.
* Une campagne comporte des dates de début et de fin, et non une promotion. Le planificateur qui s’affiche lorsque vous créez une promotion ne configure pas les dates de début et de fin de la promotion. Il vous permet de planifier une campagne pour cette promotion lorsque vous vous trouvez sur la page de configuration de la promotion.
* Vous ne pouvez pas modifier directement dans le contenu intermédiaire. Si vous devez modifier les paramètres et les options de la campagne, modifiez l’original ou une réplique et effectuez une notification push pour le remplacer dans le contenu intermédiaire. Par exemple, si vous ne définissez pas de date de fin pour une campagne, vous devez modifier l’original et la notification push à mettre à jour.

## Tarifs avancés et contenu intermédiaire

Ces informations sont utiles pour Adobe Commerce sur l’infrastructure cloud 2.1.X et 2.2.X.

En règle générale, vous pouvez définir des [tarifs avancés](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) pour les produits par l’intermédiaire de la zone **Produits** > **Catalogues** de l’administrateur. Avec le contenu intermédiaire, effectuez quelques étapes supplémentaires pour ajouter le prix à une promotion et à une campagne.

Pour modifier les tarifs avancés et mettre à jour l’évaluation du contenu :

1. Connectez-vous à l’administrateur.
1. Accédez à **Produits** > **Catalogue** et sélectionnez un produit et modifiez-le.
1. Dans l&#39;onglet Tarifs, sélectionnez **Advanced PrTarification**. Modifiez le prix et enregistrez les modifications.
1. En haut de la page, cliquez sur **Planifier une nouvelle mise à jour**.
1. Créez une promotion pour le produit.
1. Renseignez les informations de promotion. Pour le Planificateur, saisissez une date et une heure de début et de fin.
1. Enregistrez la promotion. Une campagne initiale inactive est créée.
1. Vous pouvez prévisualiser pour consulter le prix spécial, le nom de la promotion, le prix normal et la période planifiée de la campagne.

Pour obtenir des instructions supplémentaires, reportez-vous à la section [ Planification des modifications pour les règles de prix du catalogue ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rule-catalog-scheduled-changes.html). Cliquez sur **Suivant** pour parcourir les étapes.

## Règles de prix

Les règles de prix peuvent inclure une logique et des conditions aussi illimitées que votre imagination marketing. Parmi les exemples les plus courants, citons Buy One Get One Free, Buy One Get One 50% Off, 25$ sur des commandes de plus de 100$, et plus encore.

Pour créer une règle de prix, consultez le [Guide de l’utilisateur d’Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rules-catalog-create.html).

Vous trouverez ci-dessous un exemple de création d’une règle de prix pour une remise de première commande uniquement. Pour cette remise, vous souhaitez :

* Créez une règle de prix avec un [segment client](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/segments/customer-segment-price-rule) avec une condition : Nombre total de commandes inférieur à 1
* Ajouter ce segment client en tant que condition à la règle de panier
* Facultatif - Ajoutez des conditions et des règles pour appliquer les remises à des SKU ou catégories spécifiques de produits pour les achats ciblés.

Cela garantit que les nouveaux clients ou les clients existants qui n’ont pas effectué d’achat reçoivent la remise uniquement lors de leur première commande. Vous pouvez créer des bannières et envoyer des promotions par e-mail pour bénéficier d’une remise pour le premier achat.

## Vues du magasin

Vous pouvez configurer et exécuter plusieurs magasins avec une seule mise en oeuvre d’Adobe Commerce sur l’infrastructure cloud. Voir [Configuration de plusieurs sites Web ou magasins](multiple-sites.md).

Pour les magasins qui n’interagissent pas les uns avec les autres, vous pouvez créer plusieurs _sites web_. Chaque site web comporte des articles, des données client, un passage en caisse et un panier spécifiques qui ne sont pas partagés avec d’autres sites web dans Adobe Commerce.

Chaque site web peut inclure un ou plusieurs _magasins_ avec différentes catégories et articles, des données client partagées, un passage en caisse et un panier. Pour ces magasins, un client peut s’inscrire une seule fois et faire ses achats dans différents catalogues de produits en effectuant un seul passage en caisse.

Vous pouvez également créer des _vues de magasin_ pour différentes langues, mises en page et conceptions. Chaque vue peut avoir un domaine, une marque et une langue distincts lors du partage d’articles, de données client, de passage en caisse et de panier.

Vous trouverez ci-dessous des exemples pour mieux expliquer :

* Site web unique avec une boutique et deux vues pour les paramètres régionaux anglais et espagnol. Toutes les données d’article, les clients, le passage en caisse et le panier sont partagés.

  ![Exemple de magasin 1](../../assets/example-store1.png)

* Le site internet unique avec une boutique de vêtements pour femmes offre deux vues : une pour l&#39;anglais et une pour l&#39;espagnol. Le magasin de vêtements pour enfants offre une vue unique en anglais. Toutes les données d’article, les clients, le passage en caisse et le panier sont partagés. Les magasins peuvent avoir des domaines et des thèmes différents.

  ![Exemple de magasin 2](../../assets/example-store2.png)

* Deux sites web : un pour l&#39;habillement et un autre pour le décor avec des catalogues différents et des articles distincts, des données client et un panier. Chaque site web peut comporter plusieurs magasins et vues partageant des articles, des données client, un passage en caisse et un panier uniquement au sein de ce site.

  ![Exemple de magasin 3](../../assets/example-store3.png)

>[!WARNING]
>
>Les données du catalogue s’étendent au fur et à mesure que vous augmentez le nombre de sites web et de magasins. Selon l’architecture de votre projet, les magasins supplémentaires peuvent entraîner un processus d’indexation plus long et des temps de réponse plus lents pour les pages de catalogue non mises en cache. Adobe vous recommande de surveiller de près les performances du site.
