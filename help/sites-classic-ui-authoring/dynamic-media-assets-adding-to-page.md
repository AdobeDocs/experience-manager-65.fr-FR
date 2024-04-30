---
title: Ajout de ressources Dynamic Media à des pages
description: Pour ajouter la fonctionnalité Dynamic Media aux ressources que vous utilisez sur des sites Web, vous pouvez ajouter le composant Dynamic Media ou Interactive Media directement aux pages.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 100%

---

# Ajout de ressources Dynamic Media à des pages{#adding-dynamic-media-assets-to-pages}

Pour ajouter la fonctionnalité Dynamic Media aux ressources que vous utilisez sur des sites Web, vous pouvez ajouter le composant **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Interactive Media]** directement aux pages. Entrez en mode **[!UICONTROL Conception]** et activez les composants Dynamic Media. Vous pouvez ensuite ajouter ces composants à la page et ajouter des ressources au composant. Les composants Dynamic Media et Interactive Media sont dynamiques : ils détectent si vous ajoutez une image ou une vidéo et les options disponibles changent en conséquence.

Si vous utilisez Adobe Experience Manager comme système de gestion de contenu Web, vous pouvez ajouter les ressources Dynamic Media directement à la page.

>[!NOTE]
>
>Les zones cliquables sont disponibles et prêtes à l’emploi pour les bannières de carrousel.

## Ajout d’un composant Dynamic Media à une page {#adding-a-dynamic-media-component-to-a-page}

L’ajout d’un composant [!UICONTROL Dynamic Media] ou [!UICONTROL Interactive Media] à une page suit le même processus que l’ajout d’un composant sur n’importe quelle page. Les composants [!UICONTROL Dynamic Media] et [!UICONTROL Interactive Media] sont décrits en détail dans les sections suivantes.

Pour ajouter un composant ou une visionneuse Dynamic Media à une page, procédez comme suit :

1. Dans Experience Manager, ouvrez la page où vous souhaitez ajouter le composant Dynamic Media.
1. Si aucun composant Dynamic Media n’est disponible, sélectionnez la règle dans le [!UICONTROL Sidekick] pour entrer en mode **[!UICONTROL Conception]**.
1. Sélectionnez le parsys **[!UICONTROL Modifier]**.
1. Sélectionnez **[!UICONTROL Dynamic Media]** afin de rendre les composants Dynamic Media disponibles.

   >[!NOTE]
   >
   >Pour plus d’informations, consultez [Configuration des composants en mode Création](/help/sites-authoring/default-components-designmode.md).

1. Retournez en mode d’**[!UICONTROL édition]** en cliquant sur l’icône représentant un crayon dans le [!UICONTROL sidekick].
1. Faites glisser le composant **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Interactive Media]** du groupe **[!UICONTROL Autre]** du sidekick jusqu’à l’emplacement souhaité sur la page.
1. Sélectionnez **[!UICONTROL Modifier]** donc le composant s’ouvre.
1. [Modifiez le composant](#dynamic-media-component) selon vos besoins.
1. Sélectionnez **[!UICONTROL OK]** pour enregistrer vos modifications.

## Composants Dynamic Media {#dynamic-media-components}

[!UICONTROL Dynamic Media] et [!UICONTROL Interactive Media] sont disponibles dans le **[!UICONTROL sidekick]** sous [!UICONTROL Dynamic Media]. Vous utilisez le composant **[!UICONTROL Interactive Media]** pour toutes les ressources interactives telles que du contenu vidéo interactif, des images interactives ou des ensembles de carrousels. Pour tous les autres composants Dynamic Media, utilisez le composant **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Ces composants ne sont pas disponibles par défaut et doivent être sélectionnés en mode Conception avant leur utilisation. [Une fois les composants disponibles en mode Conception](/help/sites-authoring/default-components-designmode.md), vous pouvez les ajouter à votre page comme vous le feriez avec tout autre composant Experience Manager.

### Composant Dynamic Media {#dynamic-media-component}

Le composant Média dynamique est dynamique ; il propose des options différentes selon que vous ajoutez une image ou une vidéo. Le composant prend en charge les paramètres d’image prédéfinis, ainsi que les visionneuses d’images telles que les visionneuses d’images, les visionneuses à 360°, les visionneuses de médias mixtes et le contenu vidéo. En outre, la visionneuse est réactive. En d’autres termes, la taille de l’écran change automatiquement en fonction de la taille de l’écran du périphérique. Toutes les visionneuses sont basées sur le HTML5.

>[!NOTE]
>
>Si vous ajoutez le composant [!UICONTROL Dynamic Media] et si les **[!UICONTROL Paramètres de Dynamic Media]** sont vides ou s’il est impossible d’ajouter correctement une ressource, vérifiez les points suivants :
>
>* Vous avez [activé Dynamic Media](/help/assets/config-dynamic.md). Par défaut, Dynamic Media est désactivé.
>* L’image possède un fichier pyramid tiff. Les images importées avant l’activation de Dynamic Media ne possèdent pas de fichier pyramid tiff.
>

#### En cas d’utilisation d’images {#when-working-with-images}

Le composant [!UICONTROL Dynamic Media] permet d’ajouter des images dynamiques, notamment des visionneuses d’images, à 360° et de supports variés. Vous pouvez effectuer un zoom avant et arrière, faire pivoter une image dans une visionneuse à 360° ou sélectionner une image dans un autre type de visionneuse.

Vous pouvez également configurer directement dans le composant les paramètres prédéfinis de la visionneuse ou de l’image ou le format de l’image. Pour rendre une image réactive, vous pouvez définir les points d’arrêt ou appliquer un paramètre prédéfini d’image réactive.

![chlimage_1-72](assets/chlimage_1-72a.png)

Vous pouvez modifier les paramètres de Dynamic Media ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant, puis sur l’onglet **[!UICONTROL Paramètres de Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Par défaut, le composant d’image Dynamic Media est adaptatif. Si vous souhaitez faire en sorte qu’il ait une taille fixe, définissez-la dans le composant de l’onglet **[!UICONTROL Avancé]** à l’aide des propriétés **[!UICONTROL Largeur]** et **[!UICONTROL Hauteur]**.

**[!UICONTROL Paramètre prédéfini de la visionneuse]** : sélectionnez un paramètre prédéfini de visionneuse existant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Consultez [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

Cette option n’est disponible que si vous affichez des visionneuses d’images, à 360° ou de médias mixtes. Les paramètres prédéfinis de visionneuse affichés sont intelligents. En d’autres termes, seuls les paramètres prédéfinis de visionneuse pertinents s’affichent.

**[!UICONTROL Paramètre prédéfini d’image]** : sélectionnez un paramètre prédéfini d’image existant. Si le paramètre prédéfini d’image que vous recherchez n’est pas visible, vous devez le rendre visible. Consultez [Gestion des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de médias mixtes.

**[!UICONTROL Modificateurs d’image]** : vous pouvez modifier des effets d’image en fournissant des commandes d’image supplémentaires. Ces commandes sont décrites dans [Gestion des paramètres prédéfinis d’image](/help/assets/managing-viewer-presets.md) et le [guide de référence des commandes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=fr).

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de médias mixtes.

**[!UICONTROL Points d’arrêt]** : si vous utilisez cette ressource sur un site réactif, vous devez ajouter les points d’arrêt de page. Les points d’arrêt d’image sont séparés par des virgules (,). Cette option fonctionne lorsqu’il n’existe aucune valeur de hauteur ou largeur définie dans un paramètre d’image prédéfini.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de médias mixtes.

Vous pouvez modifier les [!UICONTROL paramètres avancés] ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Titre]** : modifiez le titre de l’image.

**[!UICONTROL Texte secondaire]** : ajoutez un titre à l’image pour les utilisateurs pour lesquels les graphiques sont désactivés.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de médias mixtes.

**[!UICONTROL URL, Ouvrir dans]** : vous pouvez définir une ressource pour ouvrir un lien. Définissez l’**[!UICONTROL URL]**, puis dans **[!UICONTROL Ouvrir dans]**, indiquez si vous souhaitez que la ressource s’ouvre dans la même fenêtre ou dans une nouvelle.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de médias mixtes.

**[!UICONTROL Largeur et Hauteur]** : si vous souhaitez que la taille de l’image soit fixe, saisissez une valeur en pixels. Si vous ne fournissez pas de valeurs, la ressource devient adaptative.

#### En cas d’utilisation de vidéos {#when-working-with-video}

Le composant **[!UICONTROL Dynamic Media]** permet d’ajouter une vidéo dynamique à vos pages Web. Lorsque vous modifiez le composant, vous pouvez choisir d’utiliser un paramètre prédéfini de visionneuse de vidéos pour lire la vidéo sur la page.

![chlimage_1-74](assets/chlimage_1-74a.png)

Vous pouvez modifier les paramètres [!UICONTROL Dynamic Media] ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

>[!NOTE]
>
>Par défaut le composant vidéo Dynamic Media est adaptatif. Si vous souhaitez lui donner une taille fixe, définissez-la sous l’onglet **[!UICONTROL Avancé]** du composant, grâce aux options **[!UICONTROL Largeur]** et **[!UICONTROL Hauteur]**.

**[!UICONTROL Paramètre prédéfini de la visionneuse]** : sélectionnez un paramètre prédéfini de visionneuse existant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Consultez [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md).

Vous pouvez modifier les paramètres [!UICONTROL avancés] ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Titre]** : modifiez le titre de la vidéo.

**[!UICONTROL Largeur et Hauteur]** : si vous souhaitez que la taille de la vidéo soit fixe, saisissez une valeur en pixels. Si vous ne fournissez pas de valeurs, la vidéo devient adaptative.

#### Diffusion d’une vidéo sécurisée {#how-to-delivery-secure-video}

Dans Experience Manager 6.2, lorsque vous installez [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), vous pouvez contrôler si la vidéo est diffusée via une connexion SSL sécurisée (HTTPS) ou une connexion non sécurisée (HTTP). Par défaut, le protocole de diffusion vidéo est automatiquement hérité du protocole de la page web d’intégration. Si la page web est chargée via HTTPS, la vidéo est également diffusée via HTTPS. Inversement, si la page Web est chargée via HTTP, la vidéo est diffusée via HTTP. Dans la plupart des cas, ce comportement par défaut est correct et aucune modification de configuration n’est nécessaire. Vous pouvez toutefois remplacer ce comportement par défaut. Ajoutez `VideoPlayer.ssl=on` à la fin d’un chemin d’URL ou à la liste d’autres paramètres de configuration de la visionneuse dans un fragment de code intégré. L’une ou l’autre des actions force la sécurisation de la diffusion vidéo.

Pour plus d’informations sur la diffusion sécurisée de vidéos et l’utilisation de l’attribut de configuration `VideoPlayer.ssl` dans le chemin d’accès URL, consultez [Diffusion sécurisée de vidéos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html?lang=fr) dans le Guide de référence des visionneuses. Outre la visionneuse vidéo, la diffusion sécurisée de vidéos est disponible pour la visionneuse de médias mixtes et la visionneuse de vidéos interactives.

### Composant Interactive Media {#interactive-media-component}

Le composant Média interactif est destiné aux ressources qui ont une interactivité sur celles-ci, telles que des zones réactives ou des zones cliquables. Si vous disposez d’une image interactive, d’une vidéo interactive ou d’une bannière de carrousel, utilisez le composant **[!UICONTROL Média interactif]**.

Le composant [!UICONTROL Interactive Media] est dynamique : il propose des options différentes selon que vous ajoutez une image ou une vidéo. En outre, la visionneuse est réactive. En d’autres termes, la taille de l’écran change automatiquement en fonction de la taille de l’écran du périphérique. Toutes les visionneuses sont basées sur le HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Vous pouvez modifier les paramètres **[!UICONTROL Général]** ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Paramètre prédéfini de la visionneuse]** : sélectionnez un paramètre prédéfini de visionneuse existant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devez le rendre visible. Les paramètres de visionneuse prédéfinis doivent être publiés avant de pouvoir être utilisés. Consultez [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md).

**[!UICONTROL Titre]** : modifiez le titre de la vidéo.

**[!UICONTROL Largeur et Hauteur]** : si vous souhaitez que la taille de la vidéo soit fixe, saisissez une valeur en pixels. Si vous ne fournissez pas de valeurs, la vidéo devient adaptative.

Vous pouvez modifier les paramètres **[!UICONTROL Ajouter au panier]** ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Afficher les ressources de produit]** : par défaut, cette valeur est sélectionnée. La ressource de produit affiche une image du produit telle que définie dans le module Commerce. Décochez la case pour ne pas afficher la ressource de produit.

**[!UICONTROL Afficher le prix des produits]** : par défaut, cette valeur est sélectionnée. Le prix du produit affiche le prix de l’article tel que défini dans le module Commerce. Décochez la case pour ne pas afficher le prix du produit.

**[!UICONTROL Afficher le formulaire de produit]** : par défaut, cette valeur n’est pas sélectionnée. Le formulaire de produit comprend toutes les variantes de produit, telles que la taille et la couleur. Décochez la case pour ne pas afficher les variantes de produit.
