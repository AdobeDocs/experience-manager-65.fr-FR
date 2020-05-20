---
title: Gestion des ressources vidéo
description: Découvrez comment télécharger, prévisualiser, annoter et publier les ressources vidéo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 69%

---


# Gestion des ressources vidéo  {#manage-video-assets}

Découvrez comment gérer et modifier les ressources vidéo dans Adobe Experience Manager (AEM) Assets. De plus, si vous possédez une licence d’utilisation Dynamic Media, reportez-vous à la [documentation vidéo sur Dynamic Media](/help/assets/video.md).

## Chargement et prévisualisation des ressources vidéo {#upload-and-preview-video-assets}

Adobe Experience Manager Assets génère des prévisualisations pour les ressources vidéo avec l’extension MP4. Si le format de la ressource n’est pas MP4, installez le pack FFmpeg pour générer une prévisualisation. FFmpeg crée des rendus vidéo de type OGG et MP4. Vous pouvez prévisualiser ces rendus dans l’interface utilisateur d’AEM Assets.

1. Dans le dossier Ressources numériques ou ses sous-dossiers, accédez à l’emplacement où vous souhaitez ajouter les ressources numériques.
1. To upload the asset, click **[!UICONTROL Create]** from the toolbar and then choose **[!UICONTROL Files]**. Vous pouvez également le faire glisser directement jusqu’à la zone des ressources. Pour plus d’informations sur l’opération de téléchargement, voir [Téléchargement des ressources](managing-assets-touch-ui.md#uploading-assets).
1. To preview a video in the Card view, click the **[!UICONTROL Play]** button on the video asset.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   Vous pouvez suspendre ou lire une vidéo en mode Carte uniquement. Les boutons [!UICONTROL Lecture] et [!UICONTROL Pause] ne sont pas disponibles dans la vue Liste.

1. To preview the video in the asset details page, click the **[!UICONTROL Edit]** icon on the card.

   La vidéo se joue dans le lecteur vidéo natif du navigateur. Vous pouvez lire, suspendre, afficher la vidéo en plein écran et en contrôler le volume.

   ![chlimage_1-66](assets/chlimage_1-202.png)

## Configuration pour télécharger des ressources d’une taille supérieure à 2 Go {#configuration-to-upload-assets-that-are-larger-than-gb}

Par défaut, Experience Manager Assets ne vous permet pas de télécharger des contenus d’une taille supérieure à 2 Go en raison d’une limite portant sur la taille des fichiers. Néanmoins, vous pouvez contourner cette limite en accédant à CRXDE Lite et en créant un nœud dans le répertoire `/apps`. Le nœud doit comporter le même nom, la même structure de répertoire et des propriétés comparables.

Outre la configuration d’Experience Manager Assets, modifiez les configurations suivantes pour télécharger des fichiers volumineux :

* Augmentez le délai d’expiration du jeton. Voir [!UICONTROL Adobe Granite CSRF Servlet] dans la console Web à l’adresse `https://[aem_server]:[port]/system/console/configMgr`. Pour plus d’informations, voir Protection [](/help/sites-developing/csrf-protection.md)CSRF.
* Augmentez la configuration `receiveTimeout` du répartiteur. Pour plus d’informations, voir [Configuration du répartiteur Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>L’interface utilisateur classique AEM ne comporte pas de limite de taille de fichier à 2 Go. Par ailleurs, le processus de bout en bout pour des vidéos volumineuses n’est pas entièrement pris en charge.

Pour configurer une limite de taille de fichier supérieure, procédez comme suit dans le répertoire `/apps`.

1. Dans AEM, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL CRXDE Lite]**.
1. Dans CRXDE Lite, accédez à `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Pour afficher la fenêtre du répertoire, appuyez sur l’icône `>>`.
1. From the toolbar, click the **[!UICONTROL Overlay Node]**. Vous pouvez également sélectionner **[!UICONTROL Nœud de recouvrement]** dans le menu contextuel.
1. In the **[!UICONTROL Overlay Node]** dialog, click **[!UICONTROL OK]**.

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. Actualisez le navigateur. Le nœud de recouvrement `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` est sélectionné.
1. Dans l’onglet **[!UICONTROL Propriétés]**, saisissez la valeur appropriée en octets pour définir la taille maximale souhaitée. Par exemple, pour augmenter la taille limite à 30 Go, entrez la valeur `{sizeLimit : "32212254720"}`.

1. Dans la barre d’outils, appuyez sur **[!UICONTROL Tout enregistrer]**.
1. In AEM, click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. On the Adobe Experience Manager Web Console Bundles page, under the Name column of the table, locate and click **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. Dans la page Gestionnaire des tâches du processus externe de processus Adobe Granite, définissez les secondes pour les champs de **[!UICONTROL dépassement de délai par défaut]** et de **[!UICONTROL délai dépassé maximum]** sur `18000` (cinq heures).
1. Cliquez sur **[!UICONTROL Enregistrer]**.
1. In AEM, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Dynamic Media Encode Video]**, then click **[!UICONTROL Edit]**.
1. On the workflow page, double-click the **[!UICONTROL Dynamic Media Video Service Process]** component.
1. Dans la boîte de dialogue [!UICONTROL Propriétés des étapes], sous l’onglet **[!UICONTROL Commun]**, développez **Paramètres avancés**.
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then click **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. Near the top of the page, below the Dynamic Media Encode Video page title, click **[!UICONTROL Save]**.

## Publication de ressources vidéo {#publish-video-assets}

Une fois vos ressources vidéo publiées, vous pouvez les inclure dans une page web au moyen d’une URL ou d’une incorporation. Voir [Publication de ressources](/help/assets/publishing-dynamicmedia-assets.md).

## Annotation de ressources vidéo {#annotate-video-assets}

1. From the Assets console, click the [!UICONTROL Edit] icon on the asset card to display the asset details page.
1. To play the video, click the [!UICONTROL Preview] icon.
1. Pour annoter la vidéo, cliquez sur le bouton **[!UICONTROL Annoter]**. Une annotation est ajoutée à un moment spécifique de la vidéo. Lorsque vous annotez, vous pouvez dessiner sur le canevas et inclure un commentaire avec le dessin. Les commentaires sont automatiquement enregistrés.

   ![chlimage_1-68](assets/chlimage_1-204.png)

   Pour quitter l’assistant d’annotation, cliquez sur **[!UICONTROL Fermer]**.

1. Pour passer à un point spécifique de la vidéo, indiquez le moment en secondes dans le champ **texte** et cliquez sur **Aller**. Par exemple, pour sauter les 20 premières secondes de la vidéo, saisissez 10 dans le champ texte.

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. Pour l’afficher dans la chronologie, cliquez sur une annotation. Pour supprimer l’annotation de la chronologie, cliquez sur **[!UICONTROL Supprimer]**.

   ![chlimage_1-70](assets/chlimage_1-206.png)
