---
title: Optimisation rapide des images
description: Découvrez comment optimiser la diffusion d’images et simplifier la gestion des images pour le site Adobe Commerce en activant et en configurant l’optimisation d’images Fastly.
feature: Cloud, Configuration, Media
exl-id: 20f5c5c3-7c43-493b-b651-82b023cf5db5
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# Optimisation rapide des images

L’optimisation rapide des images (E/S) permet une manipulation et une optimisation d’images en temps réel afin d’accélérer la diffusion des images et de simplifier la maintenance des visionneuses de sources d’images pour les applications web réactives. Une fois la configuration Fastly IO effectuée, les fonctionnalités d’optimisation d’image suivantes sont disponibles :

- Forcer la conversion par perte
- Optimisation des images profondes
- Rapports de pixels adaptatifs
- Prise en charge des formats d’image courants : PNG, JPEG, GIF et WebP

Avant d’activer et de configurer l’option d’E/S Fastly, vous devez configurer votre service Fastly et configurer l’isolation de l’origine.

En fonction de vos paramètres de configuration, le fragment de code d’optimisation d’image Fastly (Fastly IO) insère le code VCL pour effectuer l’optimisation de l’image, ce qui accélère la diffusion d’images de produit dans le storefront. Il existe trois étapes pour configurer les E/S rapides : activer, configurer et vérifier.

## Activer les entrées-sorties rapides

Activez l’optimisation d’image Fastly (IO Fastly) dans le panneau Admin en téléchargeant le fragment de code VCL Fastly IO. Le fragment de code fournit des instructions de configuration rapides pour traiter toutes les images par le biais d’optimiseurs d’image, à l’aide des configurations par défaut.

**Conditions préalables :**

- Installation ou mise à niveau vers la version 1.2.62 ou ultérieure du module Fastly
- [Configuration du bouclier d’origine et du serveur principal](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding)

**Activation rapide des E/S**:

1. Connectez-vous à votre compte local [Administration](../../get-started/onboarding.md#access-your-admin-panel) en tant qu’administrateur.

1. Sélectionner **Magasins** > **Paramètres** > **Configuration** > **Avancé** > **Système**.

1. Dans le volet de droite, développez **Cache de page complète**.

1. Sélectionner **Configuration rapide** > **Optimisation des images** pour spécifier les paramètres de configuration.

1. Dans le _Fragment d’E/S Fastly_ champ, sélectionnez **Activer/Désactiver**.

1. Téléchargez le fragment de code d’E/S Fastly :

   - Sélectionner **Options de configuration d’E/S par défaut** pour ouvrir la page Options de configuration par défaut de l’optimisation des images .
   - Sélectionner **Télécharger** pour charger le fragment de code VCL sur votre serveur.

## Configurer des entrées-sorties rapides

Vérifiez et mettez à jour les paramètres de configuration d’E/S par défaut pour l’optimisation des images, si nécessaire. Par exemple, vous pouvez modifier les niveaux de qualité WebP et JPEG pour les formats avec perte ou modifier le format de diffusion des images de JPEG en _Progressif_ ou _Ligne de base_. Vous pouvez également utiliser des E/S rapides pour des fonctionnalités d’optimisation d’image plus granulaires, telles que :

- Forcer la conversion par perte
- Optimisation des images profondes
- Rapports de pixels adaptatifs

**Mise à jour rapide des E/S**:

1. Sur le _Configuration rapide_ dans la _Options de configuration d’E/S par défaut_ champ, sélectionnez **Configurer**.

   ![Affichage rapide des paramètres de configuration des E/S](../../assets/cdn/fastly-io-default-config.png)

1. Passez en revue et mettez à jour les paramètres de configuration d’E/S rapides sur la page _Options de configuration par défaut de l’optimisation des images_ page :

   ![Vérification rapide de la configuration des E/S](../../assets/cdn/fastly-io-config-options.png)

   - **Auto WebP ?**: laissez le paramètre par défaut (`Yes`) pour convertir des images au format WebP dans les navigateurs qui les prennent en charge. Si vous définissez sur **Non**, utilise rapidement le type de fichier image au lieu de convertir l’image au format WebP.

   - **Qualité WebP par défaut (perte)**: laissez le paramètre par défaut (`85`) ou saisissez le niveau de compression pour les images au format fichier avec perte. Vous pouvez indiquer tout nombre entier compris entre 1 et 100.

   - **Contrôles de format de JPEG par défaut** — conservez le paramètre par défaut (`Auto`) ou sélectionnez le type de JPEG à utiliser lors de la diffusion d’une image. Si la valeur est définie sur la valeur _Auto_, diffuse rapidement des images avec le type de sortie correspondant au type d’entrée. Sélectionner _Ligne de base_ pour afficher les images ligne par ligne en partant du haut à gauche et en descendant vers le bas à droite. Sélectionner _Progressif_ pour afficher une image floue qui devient claire au fur et à mesure du chargement.

   - **Qualité de JPEG par défaut**: laissez le paramètre par défaut (`85`) ou saisissez le niveau de compression correspondant à la qualité des formats de fichiers avec perte. Indiquez un nombre entier compris entre 1 et 100.

   - **Autoriser la mise à l’échelle ?**—laissez le paramètre par défaut (`No`) ou sélectionnez `Yes` pour renvoyer des images plus volumineuses que le fichier source d’origine afin qu’elles puissent s’adapter aux dimensions demandées.

   - **Redimensionner le filtre**: laissez le paramètre par défaut (`Lancsoz3`) ou sélectionnez une alternative. Ce paramètre spécifie le filtre utilisé pour diffuser une image redimensionnée. Selon le filtre sélectionné, l’image redimensionnée peut avoir un nombre de pixels supérieur ou inférieur.

      - `Lanczos3` (par défaut) : diffuse l’image de meilleure qualité. Cela permet de détecter les contours et les fonctionnalités linéaires d’une image et d’utiliser _[!DNL sinc]_rééchantillonnage pour offrir la meilleure reconstruction possible.
      - `Lanczos2`: utilise le même filtre que `Lancsoz3` mais avec une approximation moins précise de la fonction _[!DNL sinc]_fonction de rééchantillonnage.
      - `Bicubic`: produit un effet d’accentuation naturel lors de la réduction d’une image.
      - `Bilinear`: a un effet de lissage naturel lors de la agrandissement d’une image.
      - `Nearest`: a un effet de pixellisation naturel lors du redimensionnement de l’art pixel.

1. Après avoir défini les paramètres de configuration des E/S pour le service Fastly, sélectionnez **Annuler** pour revenir aux paramètres de configuration Fastly.

1. Dans la configuration de l’optimisation des images _Activer l’optimisation des images profondes_ champ, sélectionnez **Oui** pour activer l’optimisation des images profondes.

   ![Activer l’optimisation rapide des images profondes d’E/S](../../assets/cdn/fastly-io-deep-image-config.png)

   L’optimisation des images profondes est désactivée par défaut. Lorsque cette fonction est activée, la fonction de redimensionnement intégrée d’Adobe Commerce est désactivée et le travail de redimensionnement est déchargé vers le service d’E/S Fastly. L’optimisation des images s’applique uniquement aux images de produit. Les images CMS ne sont pas redimensionnées. Voir [Documentation rapide](#deep-image-optimization).

1. Après avoir activé l’optimisation des images profondes, activez la variable [rapports de pixels adaptatifs](#adaptive-pixel-ratios) pour générer des images optimisées pour une utilisation sur des sites web réactifs.

   ![Activation rapide des rapports de pixels adaptatifs IO](../../assets/cdn/fastly-io-config-adaptive-pixel.png)

   - Dans le _Activation des rapports de pixels d’appareil adaptatif_ champ, sélectionnez **Oui**.
   - Dans le _Nombre de pixels de l’appareil_ , acceptez le paramètre par défaut ou sélectionnez l’option **Entrée système** pour supprimer le paramètre. Sélectionnez ensuite le rapport souhaité. Un rapport de pixels d’appareil plus élevé fournit des images plus grandes.

1. Sélectionner **Enregistrer la configuration**.

### Forcer la conversion par perte

Par défaut, le service d’E/S rapide force la conversion de formats sans perte tels que PNG, BMP ou WEBP au format JPEG/WEBP.

L’avantage de forcer la conversion par perte est que les images plus petites sont diffusées.
Par exemple, en utilisant le format JPEG ou WEBp au lieu de PNG, la taille peut être réduite de 60 à 70 % en fonction du niveau de qualité spécifié dans la configuration d’E/S rapide.

Selon le niveau de qualité sélectionné pour l’optimisation des images, vous pouvez percevoir des différences visuelles dans les images. Par exemple, les canaux/transparences d’Alpha sont supprimés et remplacés par un arrière-plan blanc, sauf si vous utilisez l’optimisation d’image profonde qui utilise la couleur d’arrière-plan de votre thème.

Si vous désactivez la conversion de perte (`WebP Auto? = No`), la fonction d’E/S rapide ne modifie que les images de JPEG au format WEBP pour les navigateurs compatibles. Aucun autre type d’image n’est modifié. Par exemple, si l’image d’origine est au format PNG, la sortie du service d’E/S Fastly est au format PNG.

### Optimisation des images profondes

L’optimisation des images profondes est désactivée par défaut. L’activation de cette option désactive le redimensionnement Adobe Commerce intégré et le décharge complètement vers le service d’E/S Fastly.
Cette fonctionnalité redimensionne uniquement _product_ images. Les images CMS ne sont pas redimensionnées.

L’activation de l’optimisation des images profondes ajoute une définition de couleur d’arrière-plan à chaque image, comme défini dans votre thème. Par conséquent, les images WebP passent de WebP sans perte à WebP avec perte. L’une des principales différences entre les pertes et les pertes réside dans le fait que la perte supprime le canal alpha des images PNG, qui fournit des images beaucoup plus petites. Cependant, les images avec des transparences peuvent sembler étranges sur les pages de produits et de campagnes qui utilisent un arrière-plan différent.

Par exemple, le code suivant représente la source d’origine d’une image à partir du thème Luma :

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/cache/f073062f50e48eb0f0998593e568d857/m/b/mb02-gray-0.jpg"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Lorsque la fonction d’optimisation d’image profonde d’E/S est activée, le code source d’origine de l’image est réécrit, comme illustré dans l’exemple suivant :

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

### Rapports de pixels adaptatifs

La fonctionnalité de rapports de pixels adaptatifs est utile pour optimiser les images pour les applications web progressives. Il vous permet de diffuser plusieurs tailles et résolutions d’image à partir d’un fichier source d’image en ajoutant une `srcset` pour chaque image de produit.

Lorsque la fonction de rapports de pixels adaptatifs est activée, le service d’E/S rapide fournit une image à largeur fixe qui peut s’adapter à divers `device-pixel-ratios`.
Par exemple, le service modifie la définition de l’image du produit comme illustré dans l’exemple suivant :

```html
<img class="product-image-photo"
     srcset="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=2 2x,
  https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=3 3x"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Voir `srcset` [prise en charge des navigateurs](https://caniuse.com/#feat=srcset) et [spécification](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset).

## Validation rapide des E/S

Une fois que vous avez activé et configuré les E/S rapides, validez votre configuration en effectuant des tests de vitesse de page web avec et sans E/S rapide activé. En outre, passez en revue les images de votre boutique afin de vérifier la taille et l’apparence de l’image pour les problèmes.
