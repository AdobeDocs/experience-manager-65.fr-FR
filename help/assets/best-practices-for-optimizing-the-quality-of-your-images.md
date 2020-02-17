---
title: Meilleures pratiques relatives à l’optimisation de la qualité des images
description: Découvrez les meilleures pratiques pour optimiser la qualité d’image dans Contenu multimédia dynamique
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Meilleures pratiques relatives à l’optimisation de la qualité des images {#best-practices-for-optimizing-the-quality-of-your-images}

L’optimisation de la qualité des images peut être un processus chronophage car de nombreux facteurs contribuent à l’obtention de résultats acceptables. Le résultat est en partie subjectif car les individus perçoivent la qualité des images de manière différente. Une expérimentation structurée est la clé.

AEM comprend plus de 100 commandes de remise d’images de Contenu multimédia dynamique pour le réglage et l’optimisation des images et des résultats de rendu. Les recommandations suivantes peuvent vous aider à rationaliser le processus et à obtenir rapidement de bons résultats à l’aide de certaines commandes essentielles et de bonnes pratiques.

## Bonnes pratiques relatives au format d’image (`&fmt=`) {#best-practices-for-image-format-fmt}

* Les formats JPG et PNG sont les mieux adaptés pour obtenir des images de bonne qualité, d’une taille et d’un volume gérables.
* Si aucune commande de format n’est fournie dans l’URL, Dynamic Media Image Delivery utilise par défaut le format JPG pour la distribution.
* Le format JPG compresse selon un ratio 10:1 et produit habituellement des tailles de fichier image plus petites. Le format PNG compresse selon un ratio d’environ 2:1, sauf dans certains cas, par exemple lorsque les images comportent un arrière-plan blanc. Néanmoins, en règle générale, les fichiers PNG sont plus volumineux que les fichiers JPG.
* Le format JPG utilise une compression avec perte, ce qui signifie que des éléments (pixels) sont supprimés au cours de la compression. Par contre, le format PNG utilise une compression sans perte.
* Généralement, le format JPG compresse les images photographiques avec une plus grande fidélité que les images de synthèse avec des bords nets et un fort contraste.
* Si les images contiennent de la transparence, utilisez le format PNG, car le format JPG ne prend pas en charge cette caractéristique.

As a best practice for image format, start with the most common setting `&fmt=JPG`.

## Bonnes pratiques relatives à la taille des images {#best-practices-for-image-size}

La réduction dynamique de la taille des images est l’une des tâches les plus courantes. Elle implique d’indiquer la taille et, facultativement, le mode de sous-échantillonnage utilisé pour réduire l’image.

* Pour le dimensionnement des images, la meilleure approche et la plus simple consiste à utiliser `&wid=<value>` ou simplement `&hei=<value>,``&hei=<value>`ou à utiliser. Ces paramètres définissent automatiquement la largeur de l’image en respectant le rapport d’aspect.
* `&resMode=<value>`contrôle l’algorithme utilisé pour le sous-échantillonnage. Commencez par `&resMode=sharp2`. Cette valeur fournit la meilleure qualité d’image. While using the downsampling `value =bilin` is faster, it often results in the aliasing of artifacts.

Il est recommandé d’utiliser `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`

## Bonnes pratiques relatives à l’accentuation des images {#best-practices-for-image-sharpening}

L’accentuation des images est l’aspect le plus complexe du contrôle des images du site Web, processus au cours duquel de nombreuses erreurs sont commises. Prenez le temps d’en savoir plus sur le fonctionnement de l’accentuation et du masquage flou dans AEM en vous référant aux ressources suivantes :

Best practices white paper [Sharpening images in Adobe Scene7 Publishing System and on Image Server](/help/assets/assets/s7_sharpening_images.pdf) applies to AEM as well.

Voir aussi [Accentuation d’une image avec un masque](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html)flou.

Avec AEM, vous pouvez accentuer les images lors de l’assimilation, lors de la distribution, ou les deux. Néanmoins, dans la plupart des cas, vous devez accentuer les images à l’aide d’une seule méthode et non des deux. L’accentuation des images lors de la distribution, sur une URL, produit généralement les meilleurs résultats.

Il existe deux méthodes d’accentuation des images que vous pouvez utiliser :

* Simple sharpening ( `&op_sharpen`) – Similar to the sharpen filter used in Photoshop, simple sharpening applies basic sharpening to the final view of the image following dynamic resizing. Néanmoins, cette méthode ne peut pas être configurée par l’utilisateur. Il est recommandé de ne pas utiliser &amp;op_sharpen, sauf si cela est nécessaire.
* Unsharp masking ( `&op_USM`) – Unsharp masking is an industry standard sharpening filter. Il est recommandé d’accentuer les images par le masquage flou en suivant les instructions ci-dessous. Le masquage flou vous permet de contrôler les trois paramètres suivants :

   * `&op_sharpen=`montant,rayon,seuil

      * **[!UICONTROL quantité]** (0-5, force de l’effet).
      * **[!UICONTROL radius]** (0-250, largeur des &quot;lignes d’accentuation&quot; tracées autour de l’objet accentué, comme mesuré en pixels.)

         N’oubliez pas que les paramètres rayon et quantité fonctionnent les uns par rapport aux autres. La réduction du rayon peut être compensée en augmentant la quantité. Le rayon permet un contrôle plus précis car une valeur plus faible n’accentue que les pixels du bord, tandis qu’une valeur plus élevée accentue une bande de pixels plus large.

      * **[!UICONTROL seuil]** (0-255, sensibilité de l’effet).

         Ce paramètre définit l’écart recherché entre les pixels accentués et la zone environnante avant qu’ils ne soient considérés comme des pixels de contour et que le filtre les accentue. The **[!UICONTROL threshold]** parameter helps to avoid over-sharpening areas with similar colors, such as skin tones. Par exemple, une valeur de seuil de 12 ignore les variations légères de luminosité du ton de peau afin d’éviter d’ajouter du « bruit » tout en ajoutant un contraste de contour aux zones fortement contrastées, par exemple à l’emplacement où les cils rejoignent la peau.
      Pour plus d’informations sur la façon de définir ces trois paramètres, y compris les bonnes pratiques à appliquer avec le filtre, reportez-vous aux ressources suivantes :

      Rubrique d’aide d’AEM sur l’accentuation d’une image.

      Best practices white paper [Sharpening images in Adobe Scene7 Publishing System and on Image Server](/help/assets/assets/s7_sharpening_images.pdf).

   * AEM vous permet également de contrôler un quatrième paramètre : monochrome (0,1). Ce paramètre détermine si le masquage flou est appliqué séparément à chaque composante de couleur à l’aide de la valeur 0 ou à la luminosité/intensité de l’image à l’aide de la valeur 1.


Il est recommandé de commencer par le paramètre rayon du masquage flou. Vous trouverez ci-dessous les paramètres rayon avec lesquels vous pouvez commencer :

* **[!UICONTROL Site Web]**: 0,2 à 0,3 pixel
* **[!UICONTROL Impression photographique (250-300 ppp)]**: 0,3-0,5 pixel
* **[!UICONTROL Impression offset (266-300 ppp)]**: 0,7-1,0 pixel
* **[!UICONTROL Impression de zone de travail (150 ppp)]**: 1,5-2,0 pixels

Augmentez graduellement la valeur de 1,75 à 4. Si l’accentuation ne correspond toujours pas à vos attentes, augmentez le rayon d’un point décimal et raugmentez la valeur de 1,75 à 4. Répétez l’opération si nécessaire.

Laissez le paramètre monochrome sur 0.

### Recommandations relatives à la compression JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Ce paramètre contrôle la qualité du codage JPG. Une valeur élevée produit une image de meilleure qualité mais un fichier plus volumineux ; en revanche, une valeur faible signifie une image de qualité inférieure mais un fichier plus petit. Ce paramètre est compris entre 0 et 100.
* Pour optimiser la qualité, ne définissez pas la valeur du paramètre sur 100. La différence entre une valeur de 90, 95 ou 100 est presque imperceptible. Par contre, la valeur 100 augmente de manière inutile la taille du fichier image. Therefore, to optimize for quality but avoid image files becoming too large, set the `qlt= value` to 90 or 95.
* To optimize for a small image file size but keep image quality at an acceptable level, set the `qlt= value` to 80. Les valeurs inférieures à 70-75 résultent en une dégradation significative de la qualité de l’image.
* As a best practice, to stay in the middle, set the `qlt= value` to 85 to stay in the middle.
* Utilisation du drapeau chromatique dans le paramètre `qlt=`

   * The `qlt=` parameter has a second setting that lets you turn on RGB chromaticity downsampling using the value `,1` or off using the value `,0`.
   * To keep it simple, start with RGB chromaticity downsampling turned off (`,0`). This setting usually results in better image quality, especially for synthetic images with lots of sharp edges and contrast.

La meilleure pratique pour la compression JPG consiste à utiliser `&qlt=85,0`.

## Bonnes pratiques relatives au dimensionnement JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize est un paramètre utile si vous souhaitez garantir qu’une image ne dépasse pas une certaine taille pour être diffusée sur des périphériques ayant une mémoire limitée.

* This parameter is set in kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). It defines the maximum allowed size for image delivery.
* `&jpegSize=` interagit avec le paramètre de compression JPG `&qlt=`. If the JPG response with the specified JPG compression parameter (`&qlt=`) does not exceed the jpegSize value, the image is returned with `&qlt=` as defined. Otherwise, `&qlt=` is gradually decreased until the image fits in the maximum allowed size, or until the system determines it cannot fit and returns an error.

As a best practice, set `&jpegSize=` and add the parameter `&qlt=` if you are delivering JPG images to devices with limited memory.

## Résumé des bonnes pratiques {#best-practices-summary}

En règle générale, pour obtenir une image de qualité élevée mais un fichier de petite taille, commencez par la combinaison de paramètres suivante :

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Cette combinaison de paramètres produit d’excellents résultats dans la plupart des cas.

Si l’image doit être davantage optimisée, accentuez-la progressivement (masquage flou) en commençant par un rayon de 0,2 ou 0,3. Ensuite, augmentez graduellement la quantité entre 1,75 et 4 (équivalent de 400 % dans Photoshop). Vérifiez que le résultat escompté est obtenu.

Si le résultat de l’accentuation n’est toujours pas satisfaisant, augmentez le rayon par incréments décimaux. Pour chaque incrément décimal, repartez de la valeur 1,75 et augmentez graduellement jusqu’à 4. Répétez ce processus jusqu’à obtention du résultat souhaité. Bien que les valeurs ci-dessus représentent une approche que les studios de création ont validée, gardez à l’esprit que vous pouvez commencer par d’autres valeurs et suivre d’autres stratégies. Le résultat, et sa réussite, sont subjectifs. C’est pourquoi l’expérimentation est si importante.

Tandis que vous testez différentes valeurs, vous trouverez peut-être également les suggestions générales suivantes utiles pour optimiser le workflow :

* Testez différents paramètres en temps réel, soit directement sur une URL, soit à l’aide de la fonctionnalité de réglage d’image de Scene7 Publishing System, qui fournit des aperçus en temps réel pour les opérations de réglage.
* En règle générale, n’oubliez pas que vous pouvez regrouper les commandes de diffusion d’images de médias dynamiques dans un paramètre d’image prédéfini. An image preset is basically URL command macros with custom preset names such as `$thumb_low$` and `&product_high$`. Le nom du paramètre prédéfini personnalisé d’un chemin URL appelle ces paramètres prédéfinis. Cette fonctionnalité vous aide à gérer les commandes et les paramètres de qualité pour différents modèles d’utilisation des images sur vos sites Web et raccourcit la longueur globale des URL.
* AEM propose également des méthodes plus élaborées permettant d’optimiser la qualité des images, par exemple en accentuant les images lors de l’assimilation. For advanced use cases where this may be an option to further tune and optimize rendering results, [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) can help you with customized insight and best practices.

