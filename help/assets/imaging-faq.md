---
title: Imagerie dynamique
description: L’imagerie dynamique applique les caractéristiques de visualisation uniques de chaque personne pour diffuser automatiquement des images optimisées selon leur expérience, offrant ainsi des performances accrues et un meilleur engagement.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 99%

---

# Imagerie dynamique {#smart-imaging}

L’imagerie dynamique applique les caractéristiques de visualisation uniques de chaque personne pour diffuser automatiquement des images optimisées selon leur expérience, offrant ainsi des performances accrues et un meilleur engagement.

## À propos de l’imagerie dynamique {#what-is-smart-imaging}

La technologie d’imagerie dynamique applique les fonctionnalités d’intelligence artificielle d’Adobe Sensei et fonctionne avec les « paramètres d’image prédéfinis » existants. Elle permet d’améliorer les performances de la diffusion d’images en optimisant automatiquement le format, la taille et la qualité des images en fonction des fonctionnalités du navigateur client.

De plus, obtenez désormais un meilleur score Google Core Web Vital pour LCP (Large Contentful Paint) grâce à l’amélioration de l’imagerie dynamique, qui s’accompagne désormais de la prise en charge d’AVIF et de WebP.

>[!IMPORTANT]
>
>L’imagerie intelligente nécessite l’utilisation du réseau de diffusion de contenu prêt à l’emploi fourni avec Adobe Experience Manager - Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité.

>[!TIP]
>
>Testez et découvrez les avantages des modificateurs d’image Dynamic Media et de l’imagerie dynamique à l’aide de Dynamic Media [_Snapshot_](https://snapshot.scene7.com/).
>
>Snapshot est un outil de démonstration visuel, conçu pour illustrer la puissance de Dynamic Media pour une diffusion d’images optimisée et dynamique. Effectuez des essais avec des images de test ou des URL Dynamic Media afin d’observer visuellement le résultat de divers modificateurs d’images Dynamic Media et les optimisations de l’imagerie dynamique pour les éléments suivants :
>
>* Taille de fichier (avec diffusion WebP et AVIF)
>* Bande passante réseau
>* DPR (rapport de pixels de l’appareil)
>
>Pour découvrir à quel point il est facile d’utiliser Snapshot, regardez la [vidéo de formation Snapshot](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minutes et 17 secondes).

L’imagerie dynamique tire parti de sa parfaite intégration dans le meilleur service premium CDN (réseau de diffusion de contenu) de sa catégorie proposé par Adobe afin d’offrir un gain de performance accru. Ce service trouve l’itinéraire Internet optimal entre les serveurs, les réseaux et les points de connexion. Au lieu d’utiliser l’itinéraire par défaut sur Internet, le service établit celui possédant la latence et le taux de perte de paquets les plus faibles.

Les exemples de ressources d’image suivants illustrent l’optimisation supplémentaire qu’apporte l’imagerie dynamique :

| Image(URL) | Miniature | Taille (JPEG) | Taille (WebP) avec l’imagerie dynamique | Taille (AVIF) avec l’imagerie dynamique | % de réduction avec WebP | % de réduction avec AVIF |
|---|---|---|---|---|---|---|
| [Image 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 Ko | 106 Ko | 90,2 Ko | 26,89 % | 37,79 % |
| [Image 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 Ko | 346 Ko | 113 Ko | 16,01 % | 72,57 % |
| [Image 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 Ko | 189 Ko | 87,1 Ko | 14,47 % | 60,58 % |
| [Image 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 Ko | 545 Ko | 286 Ko | 8,25 % | 51,85 % |

Comme ci-dessus, Adobe a également exécuté un test avec un ensemble d’échantillons plus grand. Le format AVIF a permis une réduction supplémentaire de 20 % de la taille par rapport au WebP, qui lui-même a permis une réduction de 27 % par rapport au JPEG. Tout cela avec la même qualité visuelle. Au total, l’AVIF offre une réduction de taille moyenne de 41 % par rapport au JPEG.

Comparez WebP et AVIF à PNG, vous pouvez constater une réduction de la taille de 84 % avec WebP et de 87 % avec AVIF. Et, puisque les formats WebP et AVIF prennent en charge la transparence et plusieurs animations d’images, ils remplacent efficacement les fichiers PNG et de GIF transparents.

Consultez également la section [Optimisation des images avec des formats d’image de nouvelle génération (WebP et AVIF)](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4).

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Avantages de l’imagerie dynamique {#what-are-the-key-benefits-of-smart-imaging}

L’imagerie dynamique améliore la diffusion des images en optimisant automatiquement la taille du fichier en fonction du navigateur utilisé, de l’affichage de l’appareil et des conditions du réseau. Cette approche garantit des temps de chargement plus rapides et une meilleure expérience d’affichage dans différents environnements. Comme les images constituent la majeure partie du temps de chargement d’une page, toute amélioration des performances peut avoir un impact profond sur les indicateurs de performance clés de l’entreprise :

* Taux de conversion plus élevés.
* Temps passé sur le site.
* Taux de rebond inférieur pour le site.

Les principaux avantages de la dernière technologie d’imagerie dynamique sont les suivants :

* Le format AVIF de nouvelle génération est pris en charge.
* La conversion avec perte des PNG en WebP et AVIF est désormais possible. Le format PNG étant sans perte, les WebP et AVIF étaient auparavant livrés sans perte.
* Conversion au format du navigateur (`bfc`)
* Rapport pixel de l’appareil (`dpr`)
* Bande passante réseau (`network`)

### À propos de la conversion au format du navigateur (bfc) {#bfc}

L’activation de la conversion au format du navigateur en ajoutant `bfc=on` dans l’URL de l’image convertit automatiquement les JPEG et PNG en AVIF avec perte, WebP avec perte, JPEGXR avec perte, JPEG2000 avec perte, en fonction des différents navigateurs. Pour les navigateurs qui ne prennent pas en charge ces formats, l’imagerie dynamique continue de délivrer le JPEG ou le fichier PNG. L’imagerie dynamique recalcule la qualité du nouveau format avec le changement de format.

Vous pouvez désactiver l’imagerie dynamique en ajoutant le modificateur `bfc=off` à l’URL de l’image.

Consultez également la section [bfc](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc) dans l’API de diffusion et de rendu d’images Dynamic Media.

### À propos de l’optimisation du rapport pixel d’appareil {#dpr}

Le rapport pixel d’appareil (DPR), également appelé rapport pixel CSS, est la relation entre les pixels physiques et les pixels logiques d’un appareil. Avec l’apparition des écrans Retina, la résolution en pixels des appareils mobiles modernes augmente rapidement.

L’activation de l’optimisation du rapport de pixels de l’appareil effectue le rendu de l’image à la résolution native de l’écran, ce qui la fait paraître nette.

Actuellement, la densité en pixels de l’affichage provient des valeurs d’en-tête du CDN Akamai.

| Valeurs autorisées dans l’URL d’une image | Description |
|---|---|
| `dpr=off` | Désactivez l’optimisation du DPR au niveau de l’URL d’une image individuelle. |
| `dpr=on,dprValue` | Remplacez la valeur DPR détectée par l’imagerie intelligente par une valeur personnalisée (telle que détectée par une logique côté client ou par d’autres moyens). La valeur autorisée pour `dprValue` est n’importe quel nombre supérieur à 0. |

>[!NOTE]
>
>* Vous pouvez utiliser `dpr=on,dprValue` même si le paramètre DPR au niveau de la société est désactivé.
>* En raison de l’optimisation du DPR, lorsque l’image créée est supérieure au paramètre MaxPix Dynamic Media, la largeur MaxPix est toujours reconnue en conservant les proportions de l’image.

| Taille de l’image demandée | Valeur de Ratio pixel de l’appareil (dpr) | Taille de l’image diffusée |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Consultez également la section [Lorsque vous utilisez des images](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) et [Lorsque vous utilisez le recadrage intelligent](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### À propos de l’optimisation de la bande passante du réseau {#network}

L’activation de la bande passante du réseau ajuste automatiquement la qualité de l’image diffusée en fonction de la bande passante du réseau réelle. Lorsque la bande passante réseau est insuffisante, l’optimisation du DPR est automatiquement désactivée, même si elle est déjà activée.

Votre entreprise peut désactiver l’optimisation de la bande passante du réseau pour chaque image individuellement en ajoutant `network=off` à l’URL de l’image.

| Valeur autorisée dans l’URL d’une image | Description |
|---|---|
| `network=off` | Désactive l’optimisation du réseau au niveau de l’URL d’une image individuelle. |

Les valeurs DPR et de bande passante réseau sont basées sur les valeurs côté client détectées du réseau de diffusion de contenu groupé. Ces valeurs sont parfois inexactes. Par exemple, l’iPhone5 avec un DPR=2 et l’iPhone12 avec un `dpr=3` affichent tous deux un `dpr=2`. Néanmoins, pour les appareils haute résolution, envoyer un `dpr=2` est préférable à envoyer un `dpr=1`. La meilleure façon de surmonter cette inexactitude consiste toutefois à utiliser le RPD côté client, pour obtenir des valeurs parfaitement précises. Cette méthode fonctionne pour n’importe quel appareil, qu’il s’agisse d’Apple ou de tout autre appareil existant. Consultez la section [Utilisation de l’imagerie dynamique avec Rapport pixel d’appareil côté client](/help/assets/client-side-dpr.md).

### Autres principaux avantages de l’imagerie dynamique

* Amélioration du classement d’optimisation du référencement Google pour les pages web qui utilisent la technologie d’imagerie dynamique la plus récente.
* Diffusion immédiate de contenus optimisés (au moment de l’exécution).
* Mise en œuvre de la technologie Adobe Sensei pour effectuer la conversion en fonction de la qualité (`qlt`) spécifiée dans la demande d’image.
* Indépendance vis-à-vis du temps de vie (TTL). Auparavant, un TTL minimal de 12 heures était obligatoire pour le fonctionnement de l’imagerie dynamique.
* Auparavant également, les images d’origine et dérivées étaient mises en cache et un processus en deux étapes était nécessaire pour invalider le cache. Avec la technologie d’imagerie dynamique la plus récente, seules les images dérivées sont mises en cache, ce qui rend possible un processus d’invalidation du cache en une seule étape.
* Les clients qui utilisent des en-têtes personnalisés dans leur ensemble de règles bénéficient de la dernière version de l’imagerie dynamique, car ces en-têtes ne sont pas bloqués, contrairement à la version précédente.

## Questions fréquentes

+++L’imagerie dynamique entraîne-t-elle des frais de licence ?

Non. L’imagerie dynamique est incluse dans votre licence existante. Cette règle est vraie pour Dynamic Media Classic ou pour Experience Manager Dynamic Media (On-premise, AMS et Experience Manager as a Cloud Service).

>[!NOTE]
>
>L’imagerie dynamique n’est pas disponible pour les utilisateurs Dynamic Media – Hybrid.

+++

+++Comment fonctionne l’imagerie dynamique ?

Lorsqu’une image est demandée, l’imagerie dynamique analyse les caractéristiques d’utilisation et la convertit au format approprié en fonction du navigateur. Ces conversions de format s’effectuent de manière à garantir une représentation fidèle. L’imagerie dynamique convertit automatiquement les images dans différents formats en fonction des capacités du navigateur de la manière suivante.

* Conversion automatique au format AVIF si le navigateur prend en charge le format
* Conversion automatique au format WebP si la conversion AVIF n’est pas adéquate ou si le navigateur ne prend pas en charge le format AVIF
* Conversion automatique vers le JPEG2000 si Safari ne prend pas en charge le WebP
* Conversion automatique vers le JPEGXR pour IE 9+ ou si Edge ne prend pas en charge WebP

  | Format d’image | Navigateurs pris en charge |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* Pour les navigateurs qui ne prennent pas en charge ces formats, le format d’image demandé initialement est diffusé.

Si la taille de l’image d’origine est inférieure à celle produite par l’imagerie dynamique, l’image d’origine est diffusée.

+++

+++Quels sont les formats d’image pris en charge ?

Les formats suivants sont pris en charge dans le cadre de l’imagerie dynamique :

* JPEG
* PNG

L’imagerie dynamique recalcule la qualité des formats de fichiers image JPEG lors de la conversion en un nouveau format.

Pour les formats de fichiers image qui prennent en charge la transparence, tels que le PNG, vous pouvez configurer l’imagerie dynamique pour qu’elle diffuse des fichiers AVIF et WebP avec perte. Pour la conversion en formats avec perte, l’imagerie dynamique utilise la qualité mentionnée dans l’URL de l’image, ou la qualité configurée dans le compte d’entreprise Dynamic Media.

+++

+++Comment l’imagerie dynamique fonctionne-t-elle avec les paramètres prédéfinis d’image qui sont déjà utilisés ?

L’imagerie dynamique s’intègre facilement à vos paramètres d’image prédéfinis existants et conserve tous vos paramètres d’image.

Les seuls réglages concernent le format de l’image, la qualité, ou les deux. Pour la conversion de format, l’imagerie dynamique conserve une totale fidélité visuelle selon vos paramètres d’image prédéfinis, mais avec une plus petite taille de fichier. Il vous suffit de l’activer en ajoutant `bfc=on`, `dpr=on,dprValue` ou `network=on`, ou bien ces trois paramètres à vos URL ou paramètres prédéfinis existants.

Par exemple, supposons qu’un paramètre d’image prédéfini spécifie un format JPEG de 500 × 500 pixels, avec `quality=85` et `unsharp mask=0.1,1,5`. L’imagerie dynamique détecte si la personne se trouve dans un navigateur Chrome. Elle convertit ensuite l’image en WebP avec les mêmes dimensions (500 × 500) et une accentuation correspondant aux paramètres du JPEG. Le système compare ensuite la taille des fichiers des versions WebP et JPEG et affiche la plus petite.

+++

<!--

### Do I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? 

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++L’imagerie dynamique est-elle compatible avec le protocole HTTPS ? Et qu’en est-il du protocole HTTP/2 ?

L’imagerie dynamique fonctionne avec les images diffusées sur HTTP ou HTTPS. Elle fonctionne également sur HTTP/2.

+++

+++Puis-je utiliser l’imagerie dynamique ?

L’imagerie dynamique est disponible immédiatement pour l’ensemble de la clientèle. Pour commencer à profiter de ses avantages, ajoutez simplement `bfc=on`, `dpr=on,dprValue` ou `network=on`, ou bien ces trois paramètres à vos URL ou paramètres prédéfinis existants.

Pour utiliser l’imagerie dynamique, le compte Dynamic Media Classic ou Dynamic Media sur Experience Manager de votre entreprise doit inclure le réseau de diffusion de contenu (CDN) d’Adobe dans votre licence.

+++

+++Quelle est la marche à suivre afin d’activer l’imagerie dynamique pour un compte ?

Pour commencer à utiliser l’imagerie dynamique, ajoutez `bfc=on`, `dpr=on,dprValue` ou `network=on`, ou bien ces trois paramètres à vos URL ou paramètres prédéfinis existants. Si vous préférez ne pas apporter ces modifications manuellement, vous pouvez activer l’imagerie dynamique par défaut en créant un cas de prise en charge.

Lors de la création du cas de prise en charge, spécifiez les fonctionnalités d’imagerie dynamique à activer sur votre compte :

* Conversion du format du navigateur (WebP ou AVIF)
* Optimisation de la bande passante du réseau

>[!NOTE]
>
>Le DPR nécessite des ajustements côté client pour déterminer la `dprValue` correcte. Par conséquent, Adobe recommande d’activer le DPR par le biais des URL en ajoutant `dpr=on,dprValue`.

**Pour créer un dossier de support permettant d’activer l’imagerie dynamique sur votre compte :**

1. [Utilisez l’Admin Console pour commencer la création d’un nouveau dossier de support.](https://helpx.adobe.com/fr/enterprise/using/support-for-experience-cloud.html).
1. Indiquez les informations suivantes dans votre dossier d’assistance :

   * **Détails du contact principal :**

      * Fournissez le nom, l’adresse électronique et le numéro de téléphone du contact principal.

   * **Fonctionnalités d’imagerie dynamique à activer :**

      * Liste des fonctionnalités que vous souhaitez pour votre compte :

         * Conversion du format du navigateur : WebP ou AVIF
         * Optimisation de la bande passante du réseau
         * DPR : le DPR nécessite des ajustements côté client pour déterminer la `dprValue` correcte. Par conséquent, Adobe recommande d’activer le DPR par le biais des URL en ajoutant `dpr=on,dprValue`.

   * **Domaine pour l’imagerie dynamique :**

      * Répertorier tous les domaines pertinents, tels que *`company.com`* ou *`mycompany.scene7.com`*
      * L’imagerie dynamique prend en charge les domaines génériques et personnalisés.
      * Pour trouver vos domaines, ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/fr/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started), puis connectez-vous à votre compte.

         1. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**.
         1. Recherchez le champ **[!UICONTROL Nom du serveur publié]** pour confirmer votre domaine.
         1. Vérifiez que vous utilisez le réseau de diffusion de contenu d’Adobe plutôt qu’un réseau géré par un autre fournisseur.

   * **Indique la prise en charge HTTP/2 :**

      * Indiquez si l’imagerie dynamique doit également fonctionner sur HTTP/2.

1. Le service clientèle d’Adobe active par défaut les fonctionnalités d’imagerie dynamique demandées, éliminant ainsi la nécessité d’ajouter des paramètres manuellement aux URL.
1. Adobe recommande de définir la durée de vie (TTL) sur au moins 24 heures afin d’optimiser les performances grâce à la mise en cache.
Pour ajuster la durée de vie (TTL) :

   1. Pour **Dynamic Media Classic :**
      1. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Configuration de la publication]** > **[!UICONTROL Serveur d’images]**.
      1. Définissez la valeur **[!UICONTROL Durée de vie par défaut du cache]** sur 24 heures ou plus.
   1. **Pour Dynamic Media sur Adobe Experience Manager :**
      1. Suivez [ces instructions](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab).
      1. Définissez la valeur **[!UICONTROL Expiration]** sur 24 heures ou plus.

+++

+++Dans quel délai puis-je m’attendre à ce qu’un compte soit activé avec l’imagerie dynamique ?

Le service clientèle traite les demandes dans l’ordre dans lequel elles sont reçues, en suivant la liste d’attente.

>[!NOTE]
>
>Le délai d’exécution peut être relativement long, car l’activation de l’imagerie dynamique implique qu’Adobe efface le cache. Seul un petit nombre de transitions peut donc être traité simultanément.

+++

+++Quels sont les risques liés au passage à l’imagerie dynamique ?

La page web d’un client ne présente aucun risque. Cependant, la transition à l’imagerie dynamique efface votre cache CDN. Cette opération implique de passer à une nouvelle configuration de Dynamic Media Classic ou Dynamic Media sur Experience Manager.

Au cours de la transition initiale, les images non mises en cache accèdent directement aux serveurs d’origine d’Adobe jusqu’à ce que le cache soit reconstitué. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes du site d’origine. Pour la plupart des utilisateurs, le cache est entièrement reconstitué au niveau du réseau CDN sous 1 à 2 jours.

+++

+++Comment puis-je vérifier si l’imagerie dynamique fonctionne comme prévu ?

1. Une fois que l’imagerie dynamique est activée sur votre compte, chargez une URL d’image Dynamic Media Classic ou Adobe Experience Manager sur le navigateur.
1. Ouvrez le volet de Chrome pour les développeurs en accédant à **[!UICONTROL Afficher]** > **[!UICONTROL Développeur]** > **[!UICONTROL Outils de développement]** dans le navigateur. Vous pouvez également sélectionner l’outil de développement de navigateur de votre choix.

1. Assurez-vous que le cache est désactivé lorsque les outils de développement sont ouverts.

   * Sous Windows®, accédez aux paramètres dans le volet de l’outil de développement, puis cochez la case **[!UICONTROL Désactiver le cache (lorsque les outils de développement sont ouverts)]**.
   * Sous macOS, sélectionnez **[!UICONTROL Désactiver le cache]** dans l’onglet **[!UICONTROL Réseau]** du volet de développement.

1. Vérifiez que le type de contenu est converti au format approprié. L’écran ci-dessous illustre la conversion dynamique d’une image PNG au format WebP sur Chrome. Si l’AVIF est activé pour votre domaine, vous pouvez également vous attendre à voir AVIF dans le type de contenu.
1. Répétez ce test sur différents navigateurs et conditions d’utilisation.

>[!NOTE]
>
>Toutes les images ne sont pas converties. L’imagerie dynamique détermine si la conversion peut améliorer les performances. Parfois, si aucune amélioration des performances n’est attendue, ou que le format n’est pas JPEG ou PNG, l’image n’est pas convertie.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

+++

+++Comment puis-je connaître les possibilités d’amélioration des performances ? Existe-t-il un moyen de connaître les avantages de l’imagerie dynamique ?

L’en-tête d’imagerie dynamique détermine les avantages de l’imagerie dynamique. Lorsque l’imagerie dynamique est activée, après avoir demandé une image, vous pouvez voir `-X-Adobe-Smart-Imaging` sous le titre **[!UICONTROL En-têtes de réponse]**, comme illustré dans l’exemple en surbrillance suivant :

![En-tête d’imagerie dynamique](/help/assets/assets-dm/smart-imaging-header2.png)

Cet en-tête vous indique ce qui suit :

* L’imagerie dynamique fonctionne pour l’entreprise.
* Une valeur positive signifie que la conversion a réussi. Dans ce cas, une nouvelle image WebP est renvoyée.
* Une valeur négative signifie que la conversion a échoué. Dans ce cas, l’image demandée d’origine est renvoyée (en JPEG par défaut, si le format n’est pas spécifié).
* Une valeur positive indique la différence en octets entre l’image demandée et la nouvelle image. Dans l’exemple ci-dessus, les octets enregistrés sont `75048`, soit environ 75 Ko pour une image.
* Une valeur négative signifie que l’image demandée est plus petite que la nouvelle image. La différence de taille négative s’affiche, mais l’image diffusée reste l’image d’origine demandée.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 avec diffusion en WebP**
>
>Si la valeur de `X-Adobe-Smart-Imaging` est -1 et que WebP est toujours en cours de diffusion, l’imagerie dynamique est active. Toutefois, les avantages de taille n’étaient pas calculés en raison d’un cache obsolète. Vous pouvez utiliser `cache=update` (une seule fois) dans l’URL de l’image pour résoudre ce problème.
>&#x200B;>Exemple d’utilisation du modificateur :
>&#x200B;>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>&#x200B;>Pour invalider l’intégralité du cache, vous devez créer un dossier de support.

+++

+++Comment puis-je désactiver l’optimisation AVIF dans l’imagerie dynamique ?

Si vous souhaitez revenir au service WebP par défaut, créez un dossier de support de la même façon. Vous pouvez comme d’habitude désactiver l’imagerie dynamique en ajoutant le paramètre `bfc=off` à l’URL de l’image. Cependant, vous ne pouvez pas sélectionner le format WebP ou AVIF dans le modificateur d’URL pour l’imagerie dynamique. Cette fonctionnalité est maintenue au niveau du compte de votre société.

+++

+++Est-il possible de désactiver l’imagerie dynamique quelle que soit la raison ? 

Oui. Vous pouvez désactiver l’imagerie dynamique en ajoutant l’un des modificateurs suivants :

* `bfc=off` pour désactiver la conversion au format du navigateur. Consultez également la section [Conversion au format du navigateur](#bfc).
* `dpr=off` pour désactiver le rapport pixel de l’appareil. Consultez également la section [Rapport pixel de l’appareil](#dpr).
* `network=off` pour désactiver la bande passante réseau. Consultez également la section [Bande passante réseau](#network).

+++

+++Quel « réglage » est disponible ? Existe-t-il des paramètres ou des comportements pouvant être définis ? 

L’imagerie dynamique offre trois options que vous pouvez activer ou désactiver.

* [Conversion au format du navigateur](#bfc)
* [Rapport pixel de l’appareil](#dpr)
* [Bande passante réseau](#network)

+++

+++Je dispose d’une URL avec fmt=tif sur le navigateur web Chrome. Mais ma requête échoue avec une erreur ImageServer. Pourquoi ?

Cette erreur ne se produit pas si l’imagerie dynamique n’est pas activée sur votre compte. L’imagerie dynamique fonctionne uniquement avec les formats JPEG ou PNG.

Pour éviter cette erreur, vous pouvez effectuer l’une des opérations suivantes :

* Spécifiez JPEG ou PNG.
* N’utilisez pas le modificateur `fmt`.
* Utilisez un format de navigateur préféré tel que défini par l’imagerie dynamique. Par exemple, vous pouvez utiliser WebP pour le navigateur web Chrome.

+++

+++Je veux télécharger une image TIFF à partir de l’URL d’une image. Comment puis-je faire ?

Ajoutez `fmt=tif` et `bfc=off` au chemin d’URL de l’image.

+++

+++L’imagerie dynamique gère-t-elle uniquement le format d’image ou gère-t-elle également les paramètres de qualité de l’image pour obtenir de meilleurs résultats ?

L’imagerie dynamique utilise le format et la qualité. Le reste des paramètres restent inchangés, tels que prévus pour l’URL de l’image.

+++

+++Si l’imagerie dynamique gère les paramètres de qualité, existe-t-il des valeurs minimales et maximales que je peux définir ? En d’autres termes, une qualité qui n’est pas inférieure à 60 et pas supérieure à 80 ?

Il n’existe actuellement aucune configuration de ce type.

+++

+++L’imagerie dynamique ajuste-t-elle automatiquement le paramètre de sortie de qualité en pourcentage ou s’agit-il d’un paramètre ajusté manuellement qui s’applique à toutes les images ? Dans quelle plage ?

L’imagerie dynamique ajuste automatiquement le pourcentage de qualité. La qualité est déterminé à l’aide d’un algorithme de machine learning développé par Adobe. Ce pourcentage n’est pas spécifique à la plage.

+++

+++Avec l’imagerie dynamique, quelles commandes de traitement d’images sont prises en charge ou ignorées ?

Les seules commandes à être ignorées sont `fmt` et `qlt`. Toutes les commandes restantes sont prises en charge.

+++

+++Seules les images JPEG sont-elles remplacées par l’imagerie dynamique ? Que se passe-t-il si je demande le remplacement d’une image au format WebP, PNG ou autre ?

Cette fonctionnalité fonctionne uniquement pour les JPEG et PNG.

+++

+++Pourquoi une image JPEG est-elle parfois renvoyée à Chrome, au lieu d’une image WebP ?

L’imagerie dynamique détermine si la conversion apporte ou non un bénéfice. Elle renvoie la nouvelle image uniquement si la conversion est bénéfique.

+++

+++Pourquoi la fonctionnalité Rapport pixel de l’appareil (dpr) ne fonctionne-t-elle pas comme prévu avec les images composites ?

Si une image composite implique un trop grand nombre de calques, la fonctionnalité dpr peut être affectée lors de l’utilisation d’un modificateur de position. Ce problème est connu et sera corrigé dans les prochaines versions de l’imagerie dynamique. Si d’autres fonctionnalités d’imagerie dynamique ne fonctionnent pas comme prévu, vous pouvez créer un dossier d’assistance pour signaler le problème.

+++

+++Pourquoi un PNG en imagerie dynamique est-il toujours converti en WebP/AVIF sans perte ?

Le format PNG étant un format sans perte, les fichiers WebP et AVIF diffusés antérieurement l’étaient sans perte, ce qui entraînait des fichiers d’une taille plus grande que prévue. L’imagerie dynamique prend désormais en charge la conversion avec perte. Vous pouvez utiliser le modificateur `cache=update` (une seule fois) dans une demande d’image pour résoudre ce problème. Exemple d’utilisation de ce modificateur :

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Pour invalider l’intégralité du cache, vous devez créer un dossier de support à cet effet.

+++

+++Comment puis-je continuer à utiliser le format PNG pour une conversion sans perte dans l’imagerie dynamique ?

L’imagerie dynamique prend désormais en charge la conversion avec perte en fonction du niveau de qualité. Vous pouvez continuer à utiliser une conversion sans perte en définissant la qualité sur 100, soit par le biais des paramètres de votre entreprise, soit en ajoutant `qlt=100` au chemin d’accès de l’URL de l’image.

+++

