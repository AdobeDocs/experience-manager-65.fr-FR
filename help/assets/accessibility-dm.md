---
title: Accessibilité dans Dynamic Media
description: En savoir plus sur la prise en charge de l’accessibilité dans les visionneuses Dynamic Media et Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Accessibilité dans [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] prend en charge les technologies de contrôle du clavier et d’assistance, telles que les lecteurs d’écran JAWS et NVDA, dans l’interface utilisateur de création.

## Prise en charge de l&#39;accessibilité du clavier dans [!DNL Dynamic Media]

Comme [!DNL Dynamic Media] est un module externe de [!DNL Adobe Experience Manager Assets], la plupart des commandes de clavier se comportent exactement comme dans [!DNL Experience Manager Assets]. Par exemple, le bouton `Cancel` dans [!DNL Dynamic Media] a la même mise en surbrillance que dans [!DNL Experience Manager Assets] et réagit à la clé `Spacebar` comme dans [!DNL Experience Manager Assets]. Voir [Raccourcis clavier dans Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Les touches prises en charge par les éléments d&#39;interface utilisateur individuels dans [!DNL Dynamic Media] sont, dans la plupart des cas, évidentes et faciles à découvrir. Le contrôle clavier dans [!DNL Dynamic Media] est à peu près le suivant :

* Possibilité d’utiliser des touches `Tab` et `Shift+Tab` pour naviguer entre les éléments interactifs de la page.
L’utilisation de `Tab` permet d’activer la cible d’action sur l’élément d’interface utilisateur suivant dans l’ordre de tabulation ; l’utilisation de `Shift+Tab` rétablit la cible d’action sur l’élément d’interface utilisateur précédent.
La traversée de la cible d’action suit l’emplacement de l’élément d’interface utilisateur naturel à l’écran et se déplace de gauche à droite, puis de haut en bas. En outre, si un champ comporte une erreur, vous pouvez appuyer sur `Tab` pour déplacer la cible d’action.
* Possibilité d’utiliser les clés `Spacebar` et `Enter` pour activer les éléments standard de l’interface utilisateur, tels que les boutons, les listes déroulantes, etc.
* Possibilité de voir la mise en surbrillance du clavier sur l’élément principal. L’élément d’interface utilisateur qui a le focus d’entrée peut recevoir une indication de focus visuel sous la forme d’une bordure rendue autour de l’élément d’interface utilisateur.
* Dans l’éditeur de zones réactives, vous pouvez utiliser des touches personnalisées, telles que des touches fléchées, pour interagir avec des éléments complexes de l’interface utilisateur afin de repositionner les zones réactives.
* Dans l’éditeur de vidéo interactive, vous pouvez utiliser `Spacebar` pour sélectionner une image et l’ajouter à un segment. De plus, vous pouvez utiliser la clé `Backspace` pour supprimer l&#39;élément sélectionné de l&#39;onglet **[!UICONTROL Contenu]**. En outre, appuyez sur `Tab` fonctions selon vos besoins pour naviguer entre les éléments interactifs de la page.
* Dans l’éditeur Recadrage d’image/Recadrage dynamique, vous pouvez effectuer les opérations suivantes :
   * Utilisez les touches fléchées pour recadrer la taille du cadre ou repositionner l’image, ou les deux.
   * Le premier arrêt `Tab` met en surbrillance l’ensemble du cadre d’image. Vous pouvez ensuite utiliser les touches fléchées du clavier pour repositionner le cadre.
   * Les quatre arrêts suivants `Tab` sont les quatre coins du cadre. Lorsque la cible d’action est placée sur un angle de cadre, le coin est mis en surbrillance. Encore une fois, vous pouvez utiliser les touches fléchées du clavier pour déplacer le coin ciblé.
Voir [Modification du recadrage intelligent ou de l’échantillon intelligent d’une seule image](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Prise en charge des technologies d&#39;assistance dans [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] les éléments de l’interface utilisateur fonctionnent avec les technologies d’assistance, telles que les lecteurs d’écran. Par exemple, il reconnaît les repères sur une page lorsque vous naviguez entre les repères à l’aide du raccourci clavier `D` ou de régions à l’aide du raccourci clavier `R`. Il décrit également l’en-tête lors de la navigation à l’aide du raccourci clavier de l’en-tête `H`.

## Prise en charge de l’accessibilité du clavier dans les visionneuses {#keyboard-accessibility-for-dm-viewers} [!DNL Dynamic Media]

Tous les composants [!DNL Dynamic Media] prêts à l’emploi des visionneuses prennent en charge l’accessibilité du clavier pour vos clients.

Voir [Accessibilité du clavier et navigation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) dans le Guide de référence des visionneuses Dynamic Media.

## Prise en charge des technologies d’assistance dans les [!DNL Dynamic Media] visionneuses {#assistive-technology-support-for-dm-viewers}

Tous les composants de la visionneuse [!DNL Dynamic Media] prennent en charge les rôles et attributs ARIA (Applications Internet enrichies accessibles) afin d’améliorer l’intégration avec les technologies d’assistance telles que les lecteurs d’écran.
Consultez la rubrique d’aide **Prise en charge des technologies d’assistance** dans toute rubrique de personnalisation de la visionneuse du Guide de référence des visionneuses Dynamic Media. Par exemple, voir [Prise en charge de la technologie d’assistance](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) pour la visionneuse de vidéos ou [Prise en charge de la technologie d’assistance](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) pour la visionneuse d’images interactives.

>[!MORELIKETHIS]
>
>* [Accessibilité pour les solutions d&#39;Adobe](https://www.adobe.com/accessibility.html)
>* [Accessibilité dans [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

