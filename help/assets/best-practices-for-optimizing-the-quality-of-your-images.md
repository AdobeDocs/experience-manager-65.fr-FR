---
title: Bonnes pratiques relatives à l’optimisation de la qualité des images dans Dynamic Media
description: Découvrez les bonnes pratiques relatives à l’optimisation de la qualité des images dans Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Gestion des ressources
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 88%

---

# Bonnes pratiques relatives à l’optimisation de la qualité des images dans Dynamic Media {#best-practices-for-optimizing-the-quality-of-your-images}

L’optimisation de la qualité des images peut être un processus chronophage, car de nombreux facteurs contribuent à l’obtention de résultats acceptables. Le résultat est en partie subjectif car les individus perçoivent la qualité des images de manière différente. Une expérimentation structurée est la clé.

Adobe Experience Manager inclut plus de 100 commandes de diffusion d’images Dynamic Media permettant d’affiner et d’optimiser les images et les rendus. Les instructions suivantes peuvent vous aider à rationaliser le processus et à obtenir de bons résultats rapidement à l’aide de commandes essentielles et de pratiques recommandées.

## Bonnes pratiques relatives au format d’image (`&fmt=`) {#best-practices-for-image-format-fmt}

* Les formats JPG et PNG sont les mieux adaptés pour obtenir des images de bonne qualité, d’une taille et d’un volume gérables.
* Si aucune commande de format n’est fournie dans l’URL, Dynamic Media Image Delivery utilise par défaut le format JPG pour la distribution.
* Le format JPG compresse selon un ratio 10:1 et produit habituellement des tailles de fichier image plus petites. Le format PNG compresse les images à un ratio d’environ 2:1, sauf parfois, lorsque les images contiennent un arrière-plan blanc. Néanmoins, en règle générale, les fichiers PNG sont plus volumineux que les fichiers JPG.
* Le format JPG utilise une compression avec perte, ce qui signifie que des éléments (pixels) sont supprimés au cours de la compression. Par contre, le format PNG utilise une compression sans perte.
* Généralement, le format JPG compresse les images photographiques avec une plus grande fidélité que les images de synthèse avec des bords nets et un fort contraste.
* Si les images contiennent de la transparence, utilisez le format PNG, car le format JPG ne prend pas en charge cette caractéristique.

La pratique recommandée pour le format d’image consiste à commencer par le paramètre le plus courant : `&fmt=JPG`.

## Bonnes pratiques relatives à la taille des images {#best-practices-for-image-size}

La réduction dynamique de la taille des images est l’une des tâches les plus courantes. Elle implique d’indiquer la taille et, facultativement, le mode de sous-échantillonnage utilisé pour réduire l’image.

* Pour le dimensionnement des images, la meilleure méthode, mais aussi la plus simple, consiste à utiliser `&wid=<value>` et `&hei=<value>,` ou simplement `&hei=<value>`. Ces paramètres définissent automatiquement la largeur de l’image en respectant le format.
* `&resMode=<value>` contrôle l’algorithme utilisé pour le sous-échantillonnage. Commencez par `&resMode=sharp2`. Cette valeur fournit la meilleure qualité d’image. Bien que l’utilisation du sous-échantillonnage `value =bilin` soit plus rapide, elle se traduit souvent par un crénelage des artefacts.

Pour le dimensionnement des images, il est recommandé d’utiliser `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`.

## Bonnes pratiques relatives à l’accentuation des images {#best-practices-for-image-sharpening}

L’accentuation des images est l’aspect le plus complexe du contrôle des images du site web, processus au cours duquel de nombreuses erreurs sont commises. Prenez le temps d’en savoir plus sur le fonctionnement de l’accentuation et du masquage flou dans Experience Manager en vous référant aux ressources suivantes :

Livre blanc des bonnes pratiques [Accentuer les images dans Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf) qui s’applique également à Experience Manager.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Avec Experience Manager, vous pouvez accentuer les images lors de l’ingestion, lors de la diffusion, ou les deux. Toutefois, en règle générale, accentuez les images à l’aide d’une seule méthode ou d’une autre, mais pas des deux. L’accentuation des images lors de la distribution, sur une URL, produit généralement les meilleurs résultats.

Il existe deux méthodes d’accentuation des images que vous pouvez utiliser :

* Accentuation simple (`&op_sharpen`) : à l’instar du filtre d’accentuation utilisé dans Photoshop, l’accentuation simple applique une accentuation de base à l’affichage final de l’image à la suite d’un redimensionnement dynamique. Cependant, cette méthode ne peut pas être configurée par l’utilisateur. Il est recommandé de ne pas utiliser &amp;op_sharpen sauf si cette méthode est requise.
* Masquage flou (`&op_USM`) : le masquage flou est un filtre d’accentuation standard. Il est recommandé d’accentuer les images par le masquage flou en suivant les instructions ci-dessous. Le masquage flou vous permet de contrôler les trois paramètres suivants :

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *quantité&#x200B;*]**(0 à 5, intensité de l’effet)
      * **[!UICONTROL *rayon *]**(0 à 250, largeur des « lignes d’accentuation » tracées autour de l’objet accentué, mesurées en pixels.)

      Gardez à l’esprit que les paramètres rayon et quantité fonctionnent l’un par rapport à l’autre. La réduction du rayon peut être compensée en augmentant la quantité. Le rayon permet un contrôle plus précis, car une valeur inférieure accentue uniquement les pixels de contour, tandis qu’une valeur supérieure traite une plus grande plage de pixels.

      * **[!UICONTROL *seuil *]**(0 à 255, sensibilité de l’effet)

             Ce paramètre définit l’écart recherché entre les pixels accentués et la zone environnante avant qu’ils ne soient considérés comme des pixels de contour et que le filtre les accentue. Le paramètre **[!UICONTROL seuil]** permet d’éviter l’accentuation excessive de zones aux couleurs similaires, telles que les tons chair. Par exemple, une valeur de seuil de 12 permet d’ignorer les légères variations de la luminosité de la peau pour éviter d’ajouter du « bruit », tout en ajoutant un contraste sur les bords dans les zones à fort contraste, comme l’endroit où les cils rencontrent la peau.
         
         Pour plus d’informations sur la façon de définir ces trois paramètres, y compris les bonnes pratiques à appliquer avec le filtre, reportez-vous aux ressources suivantes :

         Rubrique d’aide du Experience Manager sur l’accentuation d’une image.

         Livre blanc des bonnes pratiques [Accentuer les images dans Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager permet également de contrôler un quatrième paramètre : monochrome (0,1). Ce paramètre détermine si le masquage flou est appliqué séparément à chaque composante de couleur en utilisant la valeur 0, ou à la luminosité/l’intensité de l’image en utilisant la valeur 1.


Il est recommandé de commencer par le paramètre rayon du masquage flou. Vous trouverez ci-dessous les paramètres rayon avec lesquels vous pouvez commencer :

* **[!UICONTROL Site web]**  : 0,2 à 0,3 pixel
* **[!UICONTROL Impression photographique (250 à 300 ppp)]**  - 0,3 à 0,5 pixel
* **[!UICONTROL Impression offset (266 à 300 ppp)]**  - 0,7 à 1,0 pixel
* **[!UICONTROL Impression sur toile (150 ppp)]**  - 1,5 à 2,0 pixels

Augmentez graduellement la valeur de 1,75 à 4. Si l’accentuation ne correspond toujours pas à vos attentes, augmentez le rayon d’un point décimal et raugmentez la valeur de 1,75 à 4. Répétez l’opération si nécessaire.

Laissez le paramètre monochrome sur 0.

### Bonnes pratiques relatives à la compression JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Ce paramètre contrôle la qualité du codage JPG. Une valeur élevée produit une image de meilleure qualité, mais un fichier plus volumineux ; en revanche, une valeur faible signifie une image de qualité inférieure mais un fichier plus petit. Ce paramètre est compris entre 0 et 100.
* Pour optimiser la qualité, ne définissez pas la valeur du paramètre sur 100. La différence entre une valeur de 90, 95 ou 100 est presque imperceptible. Par contre, la valeur 100 augmente de manière inutile la taille du fichier image. En conséquence, pour optimiser la qualité, mais éviter que les fichiers image deviennent trop volumineux, définissez `qlt= value` sur 90 ou 95.
* Pour optimiser pour une petite taille de fichier image tout en conservant la qualité de l’image à un niveau acceptable, définissez la `qlt= value` sur 80. Les valeurs inférieures à 70-75 entraînent une dégradation significative de la qualité de l’image.
* Une bonne pratique pour rester dans la moyenne consiste à définir `qlt= value` sur 85.
* Utilisation du drapeau chromatique dans le paramètre `qlt=`

   * Le paramètre `qlt=` possède un deuxième paramètre qui vous permet d’activer le sous-échantillonnage chromatique RVB à l’aide de la valeur `,1` ou de le désactiver à l’aide de la valeur `,0`.
   * Pour faire simple, commencez par désactiver le sous-échantillonnage chromatique RVB (`,0`). Ce paramètre produit généralement une image de meilleure qualité, en particulier pour les images de synthèse contenant beaucoup de contours nets et un fort contraste.

La bonne pratique pour la compression JPG consiste à utiliser `&qlt=85,0`.

## Bonnes pratiques relatives au dimensionnement JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

Le paramètre jpegSize est utile pour garantir qu’une image n’excède pas une certaine taille pour sa diffusion sur les appareils dont la mémoire est limitée.

* Ce paramètre est défini en kilo-octets (`jpegSize=&lt;size_in_kilobytes&gt;`). Il définit la taille maximale autorisée pour la diffusion de l’image.
* `&jpegSize=` interagit avec le paramètre de compression JPG `&qlt=`. Si la réponse JPG avec le paramètre de compression JPG spécifié (`&qlt=`) ne dépasse pas la valeur jpegSize, l’image est renvoyée avec la valeur `&qlt=` définie. Sinon, `&qlt=` est graduellement diminué jusqu’à ce que l’image soit ajustée à la taille maximale autorisée ou jusqu’à ce que le système détermine qu’il ne peut pas procéder à l’ajustement et renvoie une erreur.

Une bonne pratique consiste à définir `&jpegSize=` et à ajouter le paramètre `&qlt=` si vous diffusez des images JPG vers des appareils dont la mémoire est limitée.

## Résumé des bonnes pratiques {#best-practices-summary}

En règle générale, pour obtenir une image de qualité élevée mais un fichier de petite taille, commencez par la combinaison de paramètres suivante :

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Cette combinaison de paramètres produit d’excellents résultats dans la plupart des cas.

Si l’image doit être davantage optimisée, accentuez-la progressivement (masquage flou) en commençant par un rayon de 0,2 ou 0,3. Ensuite, augmentez graduellement la quantité entre 1,75 et 4 (équivalent de 400 % dans Photoshop). Vérifiez que le résultat escompté est obtenu.

Si le résultat de l’accentuation n’est toujours pas satisfaisant, augmentez le rayon par incréments décimaux. Pour chaque incrément décimal, repartez de la valeur 1,75 et augmentez graduellement jusqu’à 4. Répétez ce processus jusqu’à obtention du résultat souhaité. Bien que les valeurs ci-dessus représentent une approche que les studios de création ont validée, gardez à l’esprit que vous pouvez commencer par d’autres valeurs et suivre d’autres stratégies. Le résultat, et sa réussite, sont subjectifs. C’est pourquoi l’expérimentation est si importante.

Au fur et à mesure que vous testez, les suggestions générales suivantes peuvent s’avérer utiles pour optimiser davantage votre workflow :

* Testez différents paramètres en temps réel, directement sur une URL.
* Gardez à l’esprit que vous pouvez regrouper les commandes de diffusion d’images Dynamic Media dans un paramètre d’image prédéfini. Il s’agit en outre d’une bonne pratique. Un paramètre d’image prédéfini est, en fait, constitué de macros de commande d’URL avec des noms de paramètres prédéfinis personnalisés tels que `$thumb_low$` et `&product_high$`. Le nom du paramètre prédéfini personnalisé dans un chemin URL appelle ces paramètres prédéfinis. Cette fonctionnalité vous aide à gérer les commandes et les paramètres de qualité pour différents modèles d’utilisation des images sur vos sites web et raccourcit la longueur globale des URL.
* Experience Manager propose également des méthodes plus élaborées permettant d’optimiser la qualité des images, par exemple en accentuant les images lors de l’ingestion. Pour les cas d’utilisation avancés où il existe des options pour optimiser les résultats de rendu, [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) peut vous aider à personnaliser les informations et les bonnes pratiques.
