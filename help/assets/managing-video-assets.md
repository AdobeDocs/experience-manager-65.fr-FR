---
title: Gestion des ressources vidéo
description: Découvrez comment télécharger, prévisualiser, annoter et publier les ressources vidéo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gestion des ressources vidéo {#manage-video-assets}

Découvrez comment gérer et modifier les ressources vidéo dans Adobe Experience Manager (AEM) Assets. De plus, si vous possédez une licence d’utilisation Dynamic Media, reportez-vous à la [documentation vidéo sur Dynamic Media](/help/assets/video.md).

## Upload and preview video assets {#upload-and-preview-video-assets}

Adobe Experience Manager Assets génère des aperçus pour les fichiers vidéo avec l’extension MP4. Si le format du fichier n’est pas MP4, installez le pack FFmpeg pour générer un aperçu. FFmpeg crée des rendus vidéo de type OGG et MP4. Vous pouvez prévisualiser ces rendus dans l’interface utilisateur d’AEM Assets.

1. Dans le dossier Ressources numériques ou ses sous-dossiers, accédez à l’emplacement où vous souhaitez ajouter les ressources numériques.
1. Pour télécharger le contenu, cliquez ou appuyez sur **[!UICONTROL Créer]** dans la barre d’outils, puis sélectionnez **[!UICONTROL Fichiers]**. Vous pouvez également le faire glisser directement jusqu’à la zone des ressources. See [Uploading assets](managing-assets-touch-ui.md#uploading-assets) for details around the upload operation.
1. To preview a video in the Card view, tap the **[!UICONTROL Play]** button on the video asset.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   Vous pouvez suspendre ou lire la vidéo uniquement en mode Carte. Les boutons [!UICONTROL Lecture] et [!UICONTROL Pause] ne sont pas disponibles dans la vue Liste.

1. To preview the video in the asset details page, click or tap the **[!UICONTROL Edit]** icon on the card.

   La vidéo se joue dans le lecteur vidéo natif du navigateur. Vous pouvez lire, suspendre, afficher la vidéo en plein écran et en contrôler le volume.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## Configuration to upload assets that are larger than 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Par défaut, les ressources d’Experience Manager ne vous permettent pas de télécharger des fichiers de plus de 2 Go en raison d’une limite de taille de fichier. However, you can overwrite this limit by going into CRXDE Lite and creating a node under the `/apps` directory. Le nœud doit comporter le même nom, la même structure de répertoire et des propriétés comparables.

Outre la configuration Ressources d’Experience Manager, modifiez les configurations suivantes pour télécharger des fichiers volumineux :

* Augmentez le délai d’expiration du jeton. Reportez-vous à [!UICONTROL Adobe Granite CSRF Servlet] dans la console Web à `https://[aem_server]:[port]/system/console/configMgr`. Pour plus d’informations, voir Protection [CSRF](/help/sites-developing/csrf-protection.md).
* Augmentez la configuration `receiveTimeout` du répartiteur. Pour plus d’informations, voir Configuration [du répartiteur](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)Experience Manager.

>[!NOTE]
>
>L’interface utilisateur classique AEM ne comporte pas de limite de taille de fichier à 2 Go. Par ailleurs, le processus de bout en bout pour des vidéos volumineuses n’est pas entièrement pris en charge.

To configure a higher file size limit, perform the following steps in the `/apps` directory.

1. Dans AEM, appuyez sur **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. In CRXDE Lite, navigate to `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. To see the directory window, touch the `>>` icon.
1. From the toolbar, tap the **[!UICONTROL Overlay Node]**. Alternatively, select **[!UICONTROL Overlay Node]** from the context menu.
1. In the **[!UICONTROL Overlay Node]** dialog, tap **[!UICONTROL OK]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. Actualisez le navigateur. Le noeud d’incrustation `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` est sélectionné.
1. In the **[!UICONTROL Properties]** tab, enter the appropriate value in bytes to increase the size limit to the desired size. Par exemple, pour augmenter la taille limite à 30 Go, entrez `{sizeLimit : "32212254720"}` une valeur.

1. From the toolbar, touch **[!UICONTROL Save All]**.
1. Dans AEM, appuyez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
1. On the Adobe Experience Manager Web Console Bundles page, under the Name column of the table, locate and tap **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. Dans la page Adobe Granite Workflow External Process Job Handler, définissez les secondes pour les champs de **[!UICONTROL dépassement de délai par défaut]** et de **[!UICONTROL délai dépassé maximum]** sur `18000` (cinq heures).
1. Appuyez sur **[!UICONTROL Enregistrer]**.
1. Dans AEM, appuyez sur **[!UICONTROL Outils]** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]**.
1. Dans la page Modèles de processus, sélectionnez **[!UICONTROL Vidéo de codage de média dynamique]**, puis appuyez sur **[!UICONTROL Modifier]**.
1. Dans la page du processus, appuyez deux fois sur le composant **[!UICONTROL Processus de service vidéo de média dynamique]**.
1. In the [!UICONTROL Step Properties] dialog box, under the **[!UICONTROL Common]** tab, expand **Advanced Settings**.
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then tap **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. Dans la partie supérieure de la page, sous le titre de la page Vidéo de codage de média dynamique, appuyez sur **[!UICONTROL Enregistrer]**.

## Publication de ressources vidéo {#publish-video-assets}

Une fois vos ressources vidéo publiées, vous pouvez les inclure dans une page web au moyen d’une URL ou d’une incorporation. See [publishing assets](/help/assets/publishing-dynamicmedia-assets.md).

## Annotation de ressources vidéo {#annotate-video-assets}

1. From the Assets console, click or tap the [!UICONTROL Edit] icon on the asset card to display the asset details page.
1. To play the video, click or tap the [!UICONTROL Preview] icon.
1. To annotate the video, click the **[!UICONTROL Annotate]** button. Une annotation est ajoutée à un moment spécifique de la vidéo. Lors de l’annotation, vous pouvez dessiner sur la trame et inclure un commentaire dans le dessin. Les commentaires sont automatiquement enregistrés.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   Pour quitter l’assistant d’annotation, cliquez sur **[!UICONTROL Fermer]**.

1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. Par exemple, pour sauter les 20 premières secondes de la vidéo, saisissez 10 dans le champ texte.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. Pour l’afficher dans la chronologie, cliquez sur une annotation. Pour supprimer l’annotation de la chronologie, cliquez sur **[!UICONTROL Supprimer]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
