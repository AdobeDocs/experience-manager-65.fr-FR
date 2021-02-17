---
title: Ajout de ressources Dynamic Media aux pages
seo-title: Ajout de ressources Dynamic Media aux pages
description: Pour ajouter la fonctionnalité de média dynamique aux ressources que vous utilisez sur des sites web, vous pouvez ajouter le composant Dynamic Media ou Interactive Media directement aux pages.
seo-description: Pour ajouter la fonctionnalité de média dynamique aux ressources que vous utilisez sur des sites web, vous pouvez ajouter le composant Dynamic Media ou Interactive Media directement aux pages.
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 60%

---


# Ajout de ressources Dynamic Media aux pages{#adding-dynamic-media-assets-to-pages}

Pour ajouter la fonctionnalité Dynamic Media aux ressources que vous utilisez sur vos sites Web, vous pouvez ajouter directement le composant **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Interactive Media]** sur la page. Pour ce faire, saisissez le mode [!UICONTROL Conception] et activez les composants de média dynamique. Vous pouvez ensuite ajouter ces composants à la page et ajouter des ressources au composant. Les composants Dynamic Media et Interactive Media sont dynamiques : ils détectent si vous ajoutez une image ou une vidéo et les options disponibles changent en conséquence.

Vous pouvez ajouter directement des fichiers multimédias dynamiques à la page si vous utilisez AEM comme gestion de contenu Web.

>[!NOTE]
>
>Les zones cliquables sont disponibles et prêtes à l’emploi pour les bannières de carrousel.

## Ajout d’un composant Dynamic Media à une page {#adding-a-dynamic-media-component-to-a-page}

Ajouter le composant [!UICONTROL Dynamic Media] ou [!UICONTROL Interactive Media] à une page revient à ajouter un composant à une page. Les composants [!UICONTROL Dynamic Media] et [!UICONTROL Interactive Media] sont décrits en détail dans les sections suivantes.

Pour ajouter un composant/une visionneuse Dynamic Media à une page, procédez comme suit :

1. Dans AEM, ouvrez la page où vous souhaitez ajouter le composant Dynamic Media.
1. Si aucun composant Dynamic Media n&#39;est disponible, cliquez sur la règle dans le [!UICONTROL Sidekick] pour passer en mode **[!UICONTROL Conception]**, cliquez sur **[!UICONTROL Modifier]** paramètres, puis sélectionnez **[!UICONTROL Dynamic Media]** pour rendre les composants Dynamic Media disponibles.

   >[!NOTE]
   >
   >Pour plus d’informations, voir [Configuration des composants en mode Création](/help/sites-authoring/default-components-designmode.md).

1. Revenez au mode **[!UICONTROL Modifier]** en cliquant sur l&#39;icône représentant un crayon dans le Sidekick] [!UICONTROL Sidekick.
1. Faites glisser le composant **[!UICONTROL Dynamic Media]** ou **[!UICONTROL Interactive Media]** du groupe **[!UICONTROL Other]** du panneau latéral sur la page à l’emplacement souhaité.
1. Cliquez sur l’icône **[!UICONTROL Modifier]** pour ouvrir le composant.
1. [](#dynamic-media-component)Modifiez le composant comme requis et cliquez sur **[!UICONTROL OK]** pour enregistrer les modifications.

## Composants Dynamic Media {#dynamic-media-components}

[!UICONTROL Les ] médias dynamiques et les  [!UICONTROL médias ] interactifs sont disponibles dans le   Sidekickunder  **[!UICONTROL Dynamic Media.]** Vous utilisez le composant **[!UICONTROL Interactive Media]** pour toutes les ressources interactives telles que du contenu vidéo interactif, des images interactives ou des ensembles de carrousels. Pour tous les autres composants Dynamic Media, utilisez le composant **[!UICONTROL Dynamic Media]**.

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Ces composants ne sont pas disponibles par défaut et doivent être sélectionnés en mode Conception avant leur utilisation. [Une fois les composants disponibles en mode Conception](/help/sites-authoring/default-components-designmode.md), vous pouvez les ajouter à votre page comme vous le feriez avec tout autre composant AEM.

### Composant Dynamic Media {#dynamic-media-component}

Le composant Dynamic Media est intelligent ; selon que vous ajoutez une image ou une vidéo, vous disposez de différentes options. Le composant prend en charge les paramètres d’image prédéfinis, ainsi que les visionneuses d’images telles que les visionneuses d’images, les visionneuses à 360°, les visionneuses de médias mixtes et le contenu vidéo. En outre, le lecteur est réactif. Autrement dit, la taille de l’écran change automatiquement en fonction de la taille de l’écran. Toutes les visionneuses sont des visionneuses HTML5.

>[!NOTE]
>
>Lorsque vous ajoutez le composant [!UICONTROL Dynamic Media] et que **[!UICONTROL Paramètres de Dynamic Media]** est vide ou que vous ne pouvez pas ajouter correctement un fichier, vérifiez les éléments suivants :
>
>* Vous avez [activé Dynamic Media](/help/assets/config-dynamic.md). Par défaut, ce module complémentaire est désactivé.
>* L’image possède un fichier pyramid tiff. Les images importées avant l’activation de Dynamic Media ne possèdent pas de fichier pyramid tiff.

>



#### En cas d’utilisation d’images  {#when-working-with-images}

Le composant [!UICONTROL Dynamic Media] permet d’ajouter des images dynamiques, notamment des visionneuses d’images, des visionneuses à 360° et des visionneuses de supports mixtes. Vous pouvez effectuer un zoom avant et arrière, faire pivoter une image dans une visionneuse à 360° ou sélectionner une image dans un autre type de visionneuse.

Vous pouvez également configurer directement dans le composant les paramètres prédéfinis de la visionneuse ou de l’image ou le format de l’image. Pour rendre une image réactive, vous pouvez définir les points d’arrêt ou appliquer un paramètre prédéfini d’image réactive.

![chlimage_1-72](assets/chlimage_1-72a.png)

Vous pouvez modifier les paramètres Dynamic Media suivants en cliquant sur **[!UICONTROL Modifier]** dans le composant, puis en cliquant sur l&#39;onglet **[!UICONTROL Paramètres de Dynamic Media]**.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>Par défaut, le composant d’image Dynamic Media est adaptatif. Si vous souhaitez en faire une taille fixe, définissez-la dans le composant de l&#39;onglet **[!UICONTROL Avancé]** avec les propriétés **[!UICONTROL Largeur]** et **[!UICONTROL Hauteur]**.

**[!UICONTROL Paramètre]**  prédéfini de visionneuse : sélectionnez un paramètre prédéfini de visionneuse existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devrez le rendre visible. Voir [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

Il s’agit de la seule option disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés. Les paramètres prédéfinis de la visionneuse affichés sont également intelligents ; seuls les paramètres prédéfinis pertinents de la visionneuse s’affichent.

**[!UICONTROL Paramètre]**  d’image prédéfini : sélectionnez un paramètre d’image prédéfini existant dans le menu déroulant. Si le paramètre d’image prédéfini que vous recherchez n’est pas visible, vous devrez le rendre visible. Voir [Gestion des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés.

**[!UICONTROL Modificateurs]**  d&#39;image : vous pouvez modifier les effets d&#39;image en fournissant des commandes d&#39;image supplémentaires. Ils sont décrits dans [Gestion des paramètres d’image prédéfinis](/help/assets/managing-viewer-presets.md) et la [référence de commande](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés.

**[!UICONTROL Points d’arrêt]**  : si vous utilisez cette ressource sur un site réactif, vous devez ajouter les points d’arrêt de page. Les points d’arrêt d’image doivent être séparés par des virgules (,). Cette option fonctionne lorsqu’il n’existe aucune valeur de hauteur ou largeur définie dans un paramètre d’image prédéfini.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés.

Vous pouvez modifier les [!UICONTROL Paramètres avancés] suivants en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Titre]**  - Modifie le titre de l&#39;image.

**[!UICONTROL Texte]**  de remplacement : Ajoutez un titre à l&#39;image pour les utilisateurs dont les graphiques sont désactivés.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés.

**[!UICONTROL URL, Ouvrir dans]**  : vous pouvez définir un fichier à partir duquel ouvrir un lien. Définissez les options **[!UICONTROL URL]** et **[!UICONTROL Ouvrir dans]** pour indiquer si vous souhaitez qu’il s’ouvre dans la même fenêtre ou dans une nouvelle fenêtre.

Cette option n’est pas disponible si vous affichez des visionneuses d’images, à 360° ou de supports variés.

**[!UICONTROL Largeur et Hauteur]**  : entrez une valeur en pixels si vous souhaitez que l&#39;image soit d&#39;une taille fixe. Si vous ne fournissez pas de valeurs, la ressource devient adaptative.

#### Utilisation de la vidéo {#when-working-with-video}

Utilisez le composant [!UICONTROL Dynamic Media] pour ajouter de la vidéo dynamique à vos pages Web. Lorsque vous modifiez le composant, vous pouvez choisir d’utiliser un paramètre prédéfini de la visionneuse de vidéos pour lire la vidéo sur la page.

![chlimage_1-74](assets/chlimage_1-74a.png)

Vous pouvez modifier les [!UICONTROL Paramètres de Dynamic Media] suivants en cliquant sur **[!UICONTROL Modifier]** dans le composant.

>[!NOTE]
>
>Par défaut le composant vidéo Dynamic Media est adaptatif. Si vous souhaitez lui donner une taille fixe, définissez-la sous l’onglet **[!UICONTROL Avancé]** du composant, grâce aux options **[!UICONTROL Largeur]** et **[!UICONTROL Hauteur]**.

**[!UICONTROL Paramètre]**  prédéfini de visionneuse : sélectionnez un paramètre prédéfini existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devrez le rendre visible. Voir [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md).

Vous pouvez modifier les paramètres [!UICONTROL Avancés] suivants en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Titre]**  - Modifiez le titre de la vidéo.

**[!UICONTROL Largeur et Hauteur]**  - Saisissez une valeur en pixels si vous souhaitez que la vidéo soit d’une taille fixe. Si vous ne fournissez pas de valeurs, la vidéo devient adaptative.

#### Mode de diffusion d’une vidéo sécurisée {#how-to-delivery-secure-video}

Dans AEM 6.2, lorsque vous installez [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480), vous pouvez contrôler si la vidéo est diffusée via une connexion SSL sécurisée (HTTPS) ou une connexion non sécurisée (HTTP). Par défaut, le protocole de diffusion vidéo est automatiquement hérité du protocole de la page web d’incorporation. Si la page web est chargée via HTTPS, la vidéo est également diffusée via HTTPS. Inversement, si la page web est chargée via HTTP, la vidéo est diffusée via HTTP. Dans la plupart des cas, ce comportement par défaut est correct et aucune modification de configuration n’est nécessaire. Vous pouvez toutefois remplacer ce comportement par défaut en ajoutant `VideoPlayer.ssl=on` à la fin d’un chemin d’URL ou à la liste des autres paramètres de configuration de la visionneuse dans un fragment de code intégré afin de forcer la diffusion sécurisée de la vidéo.

Pour plus d’informations sur la diffusion sécurisée de vidéos et l’utilisation de l’attribut de configuration `VideoPlayer.ssl` dans le chemin d’accès URL, voir [Diffusion sécurisée de vidéos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) dans le Guide de référence des visionneuses. Outre la visionneuse vidéo, la diffusion sécurisée de vidéos est disponible pour la visionneuse de médias mixtes et la visionneuse de vidéos interactives.

### Composant Interactive Media {#interactive-media-component}

Le composant Interactive Media est destiné aux ressources présentant des éléments interactifs tels que des zones réactives ou des zones cliquables. Si vous disposez d’une image interactive, d’une vidéo interactive ou d’une bannière de carrousel, utilisez le composant **[!UICONTROL Interactive Media]**.

Le composant [!UICONTROL Média interactif] est intelligent. Selon que vous ajoutez une image ou une vidéo, vous disposez de différentes options. En outre, le lecteur est réactif. Autrement dit, la taille de l’écran change automatiquement en fonction de la taille de l’écran. Toutes les visionneuses sont des visionneuses HTML5.

![chlimage_1-75](assets/chlimage_1-75a.png)

Vous pouvez modifier les paramètres **[!UICONTROL Général]** ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Paramètre]**  prédéfini de visionneuse : sélectionnez un paramètre prédéfini de visionneuse existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devrez le rendre visible. Les paramètres de visionneuse prédéfinis doivent être publiés avant de pouvoir être utilisés. Voir Gestion des paramètres prédéfinis de visionneuse.

**[!UICONTROL Titre]**  - Modifiez le titre de la vidéo.

**[!UICONTROL Largeur et Hauteur]**  - Saisissez une valeur en pixels si vous souhaitez que la vidéo soit d’une taille fixe. Si vous ne fournissez pas de valeurs, la vidéo devient adaptative.

Vous pouvez modifier les paramètres **[!UICONTROL Ajouter au panier]** ci-après en cliquant sur **[!UICONTROL Modifier]** dans le composant.

**[!UICONTROL Afficher le fichier]**  de produit : par défaut, cette valeur est sélectionnée. La ressource de produit affiche une image du produit telle que définie dans le module Commerce. Désactivez la case pour ne pas afficher la ressource de produit.

**[!UICONTROL Afficher le prix]**  du produit - Par défaut, cette valeur est sélectionnée. Le prix du produit affiche le prix de l’élément tel qu’il est défini dans le module Commerce. Désactivez la case pour ne pas afficher le prix du produit.

**[!UICONTROL Afficher le formulaire]**  de produit - Par défaut, cette valeur n&#39;est pas sélectionnée. Le formulaire de produit contient toutes les variantes de produit, telles que la taille et la couleur. Désactivez la case pour ne pas afficher les variantes de produit.
