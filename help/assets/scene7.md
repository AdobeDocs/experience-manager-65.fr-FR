---
title: Ajout de fonctionnalités Dynamic Media Classic à votre page
description: Découvrez comment ajouter des fonctionnalités et des composants Dynamic Media Classic à votre page AEM.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Ajout de fonctionnalités Dynamic Media Classic à votre page {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) est une solution hébergée qui permet de gérer, d’améliorer, de publier et de diffuser des fichiers de média enrichi sur des écrans et des imprimantes Web, mobiles, de courrier électronique et connectés à Internet.

Vous pouvez afficher les fichiers AEM publiés dans Dynamic Media Classic dans différentes visionneuses :

* Zoom
* Fenêtre déroulante
* Vidéo
* Modèle d’image
* Image

Vous pouvez publier des fichiers numériques directement d’AEM vers Dynamic Media Classic et vous pouvez publier des fichiers numériques de Dynamic Media Classic vers AEM.

Ce document décrit comment publier des ressources numériques d’AEM vers Dynamic Media Classic et vice versa. Les visionneuses sont également décrites en détail. Pour plus d’informations sur la configuration d’AEM pour Dynamic Media Classic, voir [Intégration de Dynamic Media Classic à AEM](/help/sites-administering/scene7.md).

Voir aussi [Ajout de zones cliquables](image-maps.md).

Pour plus d’informations sur l’utilisation de composants vidéo avec AEM, consultez la section [Vidéo](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## Publication manuelle dans Dynamic Media Classic à partir de fichiers {#manually-publishing-to-scene-from-assets}

Vous pouvez publier des fichiers numériques dans Dynamic Media Classic comme suit :

* [Dans l’interface utilisateur classique de la console Ressources](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Dans l’interface utilisateur classique d’une ressource](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Dans l’interface utilisateur classique à partir du dossier cible CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM publie dans Dynamic Media Classic de manière asynchrone. After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Composants Dynamic Media Classic {#scene-components}

Les composants Dynamic Media Classic suivants sont disponibles dans AEM :

* Zoom
* Fenêtre déroulante (Zoom)
* Modèle d’image
* Image
* Vidéo

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. Les fichiers qui n’ont pas encore été publiés dans Dynamic Media Classic sont publiés dans Dynamic Media Classic s’ils se trouvent dans un dossier synchronisé ou sur une page ou avec une configuration de cloud Dynamic Media Classic.

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Notification de fin de prise en charge de la visionneuse Flash {#flash-viewers-end-of-life-notice}

Depuis le 31 janvier 2017, Adobe Dynamic Media Classic ne prend plus en charge la plate-forme du lecteur Flash.

Pour plus d’informations sur cette importante modification, reportez-vous aux [questions fréquentes sur la fin de prise en charge de la visionneuse Flash](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

L’ajout d’un composant Dynamic Media Classic (Scene7) à une page équivaut à l’ajout d’un composant à une page. Les composants Dynamic Media Classic sont décrits en détail dans les sections suivantes.

**Pour ajouter un composant Dynamic Media Classic (Scene7) à une page**

1. Dans AEM, ouvrez la page dans laquelle vous souhaitez ajouter le composant Dynamic Media Classic (Scene7).

1. If no Dynamic Media Classic components are available, click **[!UICONTROL Design]** mode, tap any component with a blue border, tap the **[!UICONTROL Parent]** icon, and then the **[!UICONTROL Configuration]** icon. In **[!UICONTROL Parsys (Design)]**, select all the Dynamic Media Classic components to make them available and click **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Click **[!UICONTROL Edit]** to return to **[!UICONTROL Edit]** mode.

1. Faites glisser un composant du groupe Contenu multimédia dynamique classique du panneau latéral sur la page à l’emplacement souhaité.

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. Modifiez le composant comme requis et cliquez sur **[!UICONTROL OK]** pour enregistrer les modifications.
1. Faites glisser votre image ou vidéo depuis l’explorateur de contenu vers le composant Dynamic Media Classic que vous avez ajouté à la page.

   >[!NOTE]
   >
   >Dans l’interface utilisateur tactile uniquement, vous devez faire glisser l’image ou la vidéo sur le composant Dynamic Media Classic que vous avez placé sur la page. La sélection et la modification du composant Dynamic Media Classic, puis le choix du fichier ne sont pas prises en charge.

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

Une conception réactive signifie que les éléments s’adaptent selon l’emplacement où ils sont affichés. Avec la conception réactive, les mêmes éléments peuvent être affichés sur plusieurs appareils.

Voir aussi [Conception réactive pour les pages Web](/help/sites-developing/responsive.md).

**Pour ajouter une expérience de visualisation interactive à un site réactif**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Si les composants Dynamic Media Classic ne sont pas disponibles, veillez [à les activer en mode](/help/sites-authoring/default-components-designmode.md)Création.

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. Sélectionnez le composant et appuyez sur l’icône de configuration.
1. Dans l’onglet Paramètres **[!UICONTROL de]** Dynamic Media Classic, ajustez les points d’arrêt.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Confirmez que les visionneuses se redimensionnent de manière réactive et que toutes les interactions sont optimisées pour les ordinateurs de bureau, les tablettes et les appareils mobiles.

### Paramètres communs à tous les composants Dynamic Media Classic {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL Référence]** de fichier : accédez à un fichier que vous souhaitez référencer. La référence de fichier montre l’URL du fichier et pas nécessairement l’URL complète de Dynamic Media Classic, y compris les commandes et paramètres d’URL. Vous ne pouvez pas ajouter de commandes et de paramètres d’URL Dynamic Media Classic dans ce champ. Ils doivent être ajoutés par l’intermédiaire de la fonctionnalité correspondante du composant.
* **[!UICONTROL Largeur]** : permet de définir la largeur.
* **[!UICONTROL Hauteur]** : permet de définir la hauteur.

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

L’élément comporte des outils de zoom dans sa partie inférieure. Appuyez sur **[!UICONTROL +]** pour agrandir. Appuyez sur **[!UICONTROL -]** pour réduire. Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. Appuyez sur les flèches diagonales pour les afficher en plein écran. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flyout {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. Sachez toutefois qu’il existe une limitation sur la configuration réactive du composant. When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### Image {#image}

Le composant **[!UICONTROL Image]** Dynamic Media Classic vous permet d’ajouter la fonctionnalité Contenu multimédia dynamique à vos images, comme les modificateurs de Contenu multimédia dynamique, les paramètres prédéfinis d’image ou de visionneuse et l’accentuation. Le composant d’ **[!UICONTROL image]** Dynamic Media Classic est similaire à d’autres composants d’image dans AEM avec une fonctionnalité spéciale Dynamic Media Classic. Dans cet exemple, le modificateur URL Dynamic Media Classic `&op_invert=1` est appliqué à l’image.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Titre, Texte]** de remplacement : dans l’onglet **[!UICONTROL Avancé]** , ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs dont les graphiques sont désactivés.

**[!UICONTROL URL, Ouvrir dans]** : vous pouvez définir un fichier à partir duquel ouvrir un lien. Définissez l’**[!UICONTROL URL]**, puis dans le champ **[!UICONTROL Ouvrir dans]**, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Paramètre]** prédéfini de visionneuse : sélectionnez un paramètre prédéfini de visionneuse existant dans le menu déroulant. Si le paramètre prédéfini de visionneuse que vous recherchez n’est pas visible, vous devrez le rendre visible. Voir [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**[!UICONTROL Configuration]** de Dynamic Media Classic - Sélectionnez la configuration de Dynamic Media Classic que vous souhaitez utiliser pour récupérer les paramètres d’image prédéfinis actifs à partir de SPS.

**[!UICONTROL Paramètre]** d’image prédéfini : sélectionnez un paramètre d’image prédéfini existant dans le menu déroulant. Si le paramètre prédéfini d’image que vous recherchez n’est pas visible, vous devrez le rendre visible. Voir [Gestion des paramètres d’image prédéfinis](/help/assets/managing-image-presets.md). Si vous utilisez un paramètre prédéfini d’image, vous ne pouvez pas sélectionner de paramètre prédéfini de visionneuse, et inversement.

**[!UICONTROL Format]** de sortie : sélectionnez le format de sortie de l’image, par exemple jpeg. Selon le format de sortie que vous sélectionnez, vous pouvez ajouter des options de configuration supplémentaires. Voir [Bonnes pratiques relatives aux paramètres d’image prédéfinis](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Accentuation]** : sélectionnez le mode d’accentuation de l’image. L’accentuation est expliquée en détails dans les rubriques [Bonnes pratiques relatives aux paramètres d’image prédéfinis](/help/assets/managing-image-presets.md#image-preset-options) et [Bonnes pratiques relatives à l’accentuation](/help/assets/assets/s7_sharpening_images.pdf).

**[!UICONTROL Modificateurs]** d’URL : vous pouvez modifier les effets d’image en fournissant d’autres commandes d’image Dynamic Media Classic. Ces commandes sont décrites dans la section [Paramètres prédéfinis d’image](/help/assets/managing-image-presets.md) et le [guide de référence des commandes](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

**[!UICONTROL Points d’arrêt]** : si votre site Web est réactif, vous souhaitez ajuster les points d’arrêt. Les points d’arrêt doivent être séparés par des virgules ( , ).

### Modèle d’image {#image-template}

[Les modèles](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) d’image Dynamic Media Classic sont un contenu Photoshop superposé importé dans Dynamic Media Classic, où le contenu et les propriétés ont été paramétrés en fonction de la variabilité. Le composant **[!UICONTROL Modèle d’image]** permet d’importer des images et de modifier le texte dynamiquement dans AEM. En outre, vous pouvez configurer le composant **[!UICONTROL Modèle d’image]** afin d’utiliser des valeurs provenant de ClientContext de sorte que chaque utilisateur voit l’image d’une manière personnalisée.

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Référence du fichier, Largeur, Hauteur]** - Voir les paramètres communs à tous les composants ScDynamic Media Classicene7.

>[!NOTE]
>
>Les commandes et paramètres d’URL de Dynamic Media Classic ne peuvent pas être ajoutés directement à l’URL de référence du fichier. Ils ne peuvent être définis que dans l’interface utilisateur du composant, dans le panneau **[!UICONTROL Paramètre]**.

**[!UICONTROL Titre, Texte]** de remplacement : dans l’onglet Modèle d’image dynamique Media Classic, ajoutez un titre à l’image et un texte de remplacement pour les utilisateurs dont les graphiques sont désactivés.

**[!UICONTROL URL, Ouvrir dans]** : vous pouvez définir un fichier à partir duquel ouvrir un lien. Définissez l’URL, puis dans le champ Ouvrir dans, indiquez si vous souhaitez l’ouvrir dans la même fenêtre ou une nouvelle fenêtre.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Panneau]** de paramètres - Lors de l&#39;importation d&#39;une image, les paramètres sont prérenseignés avec les informations de l&#39;image. En l’absence de contenu pouvant être modifié dynamiquement, cette fenêtre est vide.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Modification dynamique du texte {#changing-text-dynamically}

Pour une modification dynamique du texte, saisissez le nouveau texte dans les champs, puis cliquez sur **[!UICONTROL OK]**. Dans cet exemple, le **[!UICONTROL Prix]** est désormais de 50 $ et l’expédition de 99 cents.

![chlimage_1-234](assets/chlimage_1-234.png)

Le texte de l’image change. You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Modification du texte afin de refléter une valeur ClientContext {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK]**. Dans cet exemple, le nom change selon la liaison entre le Nom et le nom formaté du profil.

![chlimage_1-236](assets/chlimage_1-236.png)

Le texte reflète le nom de l’utilisateur actuellement connecté. Vous pouvez réinitialiser le texte sur la valeur d’origine en cliquant sur **[!UICONTROL Réinitialiser]** en regard du champ.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Création d’un lien dans le modèle d’image Dynamic Media Classic {#making-the-scene-image-template-a-link}

1. Sur la page contenant le composant Modèle **[!UICONTROL d’]** image Dynamic Media Classic, appuyez sur **[!UICONTROL Modifier]**.
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. Dans le champ **[!UICONTROL Ouvrir dans]**, choisissez où vous souhaitez que la cible s’ouvre (une nouvelle fenêtre ou la même fenêtre).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Appuyez sur **[!UICONTROL OK]**.

### Composant vidéo {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. Ce composant est un lecteur vidéo HTML5. Il s’agit d’une visionneuse unique pouvant être utilisée sur plusieurs canaux.

Il peut être utilisé pour des ensembles de vidéos adaptables, une vidéo MP4 unique ou une vidéo F4V unique.

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. En outre, voir [le composant vidéo Dynamic Media Classic par rapport au composant](s7-video.md)vidéo Foundation.

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitations connues du composant vidéo {#known-limitations-for-the-video-component}

La gestion des actifs numériques et la gestion de contenu web d’Adobe indiquent si une vidéo maître est téléchargée. Elles n’affichent pas les éléments proxy suivants :

* Rendus codés Dynamic Media Classic
* Visionneuses de vidéos adaptatives Dynamic Media Classic

Lorsque vous utilisez une visionneuse de vidéos adaptative avec le composant vidéo Contenu multimédia dynamique classique, vous devez redimensionner le composant pour l’adapter aux dimensions de la vidéo.

## Explorateur de contenu Dynamic Media Classic {#scene-content-browser}

L’explorateur de contenu Dynamic Media Classic vous permet d’afficher le contenu de Contenu de Contenu Dynamic Media Classic directement dans AEM. To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. La fonctionnalité est identique pour les deux interfaces utilisateur.

Si vous disposez de plusieurs configurations, AEM affiche la [configuration par défaut](/help/sites-administering/scene7.md#configuring-a-default-configuration). Vous pouvez sélectionner différentes configurations directement dans l’explorateur de contenu Dynamic Media Classic du menu déroulant.

>[!NOTE]
>
>* Les fichiers situés dans le dossier ad hoc n’apparaîtront pas dans l’explorateur de contenu Dynamic Media Classic.
>* Lorsque l’option [Aperçu sécurisé est activée](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), les fichiers publiés et non publiés dans Dynamic Media Classic apparaissent dans le navigateur de contenu Dynamic Media Classic.
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* Pour la vidéo, le navigateur de contenu Dynamic Media Classic prend en charge :
   >
   >  
* Les ensembles de vidéos adaptables. Il s’agit de conteneurs de tous les rendus vidéo requis pour lire la vidéo sans difficultés sur plusieurs écrans.
>  * La vidéo MP4 unique
>  * Vidéo F4V simple


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

Vous pouvez accéder au navigateur de contenu depuis l’interface utilisateur optimisée pour les écrans tactiles ou l’interface utilisateur classique. A l’heure actuelle, l’interface utilisateur optimisée pour les écrans comporte la limitation suivante :

* Les fichiers FXG et Flash de Dynamic Media Classic ne sont pas pris en charge.

Parcourez les fichiers Dynamic Media Classic en sélectionnant **[!UICONTROL Contenu multimédia classique]** dans le troisième menu déroulant. Dynamic Media Classic n’apparaît pas dans la liste si vous n’avez pas configuré l’intégration de Dynamic Media Classic/AEM.

>[!NOTE]
>
>* L’explorateur de contenu Dynamic Media Classic charge environ 100 fichiers et les trie par nom.
>* Si vous disposez d’un serveur d’aperçu sécurisé, le navigateur l’utilise pour effectuer le rendu des miniatures et des éléments.
>



![chlimage_1-240](assets/chlimage_1-240.png)

En outre, vous pouvez parcourir les informations de résolution, de taille, de nombre de jours depuis la modification et de nom de fichier en pointant la souris sur un élément du navigateur.

![chlimage_1-241](assets/chlimage_1-241.png)

* Pour les ensembles de vidéos adaptables et les modèles, aucune information sur la taille n’est générée pour les miniatures.
* Pour les ensembles de vidéos adaptables, aucune résolution n’est générée pour les miniatures.

### Recherche de fichiers Dynamic Media Classic dans l’explorateur de contenu {#searching-for-scene-assets-with-the-content-browser}

La recherche de fichiers Dynamic Media Classic est similaire à la recherche de fichiers AEM, sauf que lorsque vous effectuez une recherche, une vue à distance des fichiers s’affiche dans le système Dynamic Media Classic, plutôt que de les importer directement dans AEM.

Vous pouvez utiliser l’interface utilisateur classique ou l’interface utilisateur optimisée pour les écrans tactiles pour visualiser et rechercher des éléments. Selon l’interface, le mode de recherche est légèrement différent.

Lors d’une recherche dans l’une ou l’autre des interfaces, vous pouvez filtrer selon les critères suivants (présentés ici dans l’interface utilisateur optimisée pour les écrans tactiles) :

**[!UICONTROL Entrez des mots-clés]** : vous pouvez rechercher des fichiers par nom. Lors de la recherche par mots-clés, vous saisissez le début du nom du fichier. Par exemple, la saisie du mot « swimming » recherche tous les noms de fichier qui commencent par ces lettres, dans cet ordre. Veillez à appuyer sur Entrée après avoir saisi le terme pour trouver le fichier.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Dossier/chemin]** : le nom du dossier qui s’affiche dépend de la configuration que vous avez sélectionnée. Vous pouvez descendre aux niveaux inférieurs en appuyant sur l’icône du dossier et en sélectionnant un sous-dossier, puis en appuyant sur la coche pour le sélectionner.

Si vous saisissez un mot-clé et sélectionnez un dossier, AEM recherche ce dossier et tous les sous-dossiers. Néanmoins, si vous ne saisissez pas de mots-clés lors de la recherche, la sélection du dossier n’affiche que les éléments de ce dossier et n’inclut pas les sous-dossiers.

Par défaut, AEM recherche le dossier sélectionné et tous les sous-dossiers.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Type de fichier]** - Sélectionnez **[!UICONTROL Contenu multimédia classique]** dynamique pour parcourir le contenu Contenu multimédia classique dynamique. Cette option n’est disponible que si Dynamic Media Classic a été configuré.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuration]** - Si plusieurs configurations de Contenu multimédia dynamique classique sont définies dans les services Cloud, vous pouvez les sélectionner ici. De ce fait, le dossier change selon la configuration que vous avez choisie.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Type]** de fichier : dans le navigateur de Dynamic Media Classic, vous pouvez filtrer les résultats pour inclure l’un des éléments suivants : images, modèles, vidéos et visionneuses de vidéos adaptatives. Si vous ne sélectionnez aucun type d’élément, AEM recherche par défaut tous les types d’élément.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Dans l’interface utilisateur classique, vous pouvez rechercher des éléments **Flash** et **FXG**. Le filtrage de ces deux éléments n’est actuellement pas pris en charge par l’interface utilisateur optimisée pour les écrans tactiles.
   >
   >
* Lors de la recherche de vidéos, vous recherchez un seul rendu. Les résultats renvoient le rendu d’origine (uniquement &amp;ast;.mp4) et le rendu codé.
>* Lors de la recherche d’une visionneuse de vidéos adaptative, vous recherchez le dossier et tous les sous-dossiers, mais uniquement si vous avez ajouté un mot-clé à la recherche. Si vous n’avez pas ajouté de mot-clé, AEM ne recherche pas les sous-dossiers.
>



**[!UICONTROL Etat]** de publication : vous pouvez filtrer les fichiers en fonction de l’état de publication : **[!UICONTROL Non publié]** ou **[!UICONTROL Publié]**. If you do not select any **[!UICONTROL Publish Status]**, AEM by default searches all publish statuses.

![chlimage_1-247](assets/chlimage_1-247.png)

