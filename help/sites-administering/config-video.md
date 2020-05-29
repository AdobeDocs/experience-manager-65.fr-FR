---
title: Configuration du composant vidéo
seo-title: Configuration du composant vidéo
description: Découvrez comment configurer le composant vidéo.
seo-description: Découvrez comment configurer le composant vidéo.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: 44dbabeeea4e4e8d17cc69a2d8ea791c98be2bd2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 37%

---


# Configuration du composant vidéo {#configure-the-video-component}

The [Video component](/help/sites-authoring/default-components-foundation.md#video) lets you place a predefined, OOTB (out-of-the-box) video element on your page.

For proper transcoding to occur, your administrator must [Install FFmpeg and configure AEM](#install-ffmpeg) separately. Vous pouvez aussi [configurer vos profils vidéo](#configure-video-profiles) pour les utiliser avec les éléments HTML5.

## Configuration des profils vidéo {#configure-video-profiles}

Vous pouvez définir des profils vidéo à utiliser pour les éléments HTML5. Les profils vidéo sélectionnés ici sont utilisés dans l’ordre. Pour y accéder, utilisez le [mode de conception](/help/sites-authoring/default-components-designmode.md) (interface utilisateur classique uniquement) et sélectionnez l’onglet **[!UICONTROL Profils]** :

![chlimage_1-317](assets/chlimage_1-317.png)

You can also configure the design of the video components and parameters for [!UICONTROL Playback], [!UICONTROL Flash], and [!UICONTROL Advanced].

## Installation de mpeg et configuration d’AEM {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). Après avoir installé FFmpeg, vous devez configurer AEM pour pouvoir utiliser un codec audio et des options d’exécution spécifiques.

**Pour installer FFmpeg pour votre plate-forme**:

* **Sous Windows :**

   1. Téléchargez le fichier binaire compilé en tant que `ffmpeg.zip`
   1. Décompressez-le dans un dossier.
   1. Définissez la variable d’environnement système `PATH` sur `<*your-ffmpeg-locatio*n>\bin`
   1. Redémarrez AEM.

* **Sur Mac OS X :**

   1. Install Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. Installez XQuartz/X11.
   1. Install MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. Dans la console, exécutez la commande suivante et suivez les instructions :

      `sudo port install ffmpeg`

      `FFmpeg` doit se trouver dans `PATH` le afin qu’AEM puisse le récupérer via la ligne de commande.

* **Utilisation de la version précompilée d’OS X 10.6 :**

   1. Téléchargez la version précompilée.
   1. Extract it to the `/usr/local` directory.
   1. Depuis le terminal, exécutez :

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**Pour configurer AEM**:

>[!NOTE]
>
>Ces étapes ne sont nécessaires que si une personnalisation plus poussée des codecs est requise.

1. Open [!UICONTROL CRXDE Lite] in your web browser. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
2. Select the `/libs/settings/dam/video/format_aac/jcr:content` node and ensure that the node properties are as follows:

   * audioCodec :

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

3. To customize the configuration, create an overlay in `/apps/settings/` node and move the same structure under `/conf/global/settings/` node. It cannot be edited in `/libs` node. Par exemple, pour superposer un chemin `/libs/settings/dam/video/fullhd-bp`, créez-le à `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Remplacez et modifiez le profile-node entier et pas seulement la propriété ayant besoin d’être modifiée. Ces ressources ne sont pas résolues via SlingResourceMerger.

4. Si vous avez modifié des propriétés, cliquez sur **[!UICONTROL Tout enregistrer]**.

>[!NOTE]
>
>Les modèles de processus prêtes à l’emploi ne sont pas conservés lors de la mise à niveau de votre instance AEM. Adobe recommande de copier les modèles de processus prêtes à l’emploi avant de les modifier. For example, copy the OOTB [!UICONTROL DAM Update Asset] model before editing the FFmpeg Transcoding step in the [!UICONTROL DAM Update Asset] model to pick video-profile names that existed before the upgrade. Then, you can overlay the `/apps` node to let AEM retrieve the custom changes to the OOTB model.

