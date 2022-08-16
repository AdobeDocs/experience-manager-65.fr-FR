---
title: Configuration du composant vidéo
seo-title: Configure the Video component
description: Découvrez comment configurer le composant vidéo.
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 20%

---

# Configuration du composant vidéo {#configure-the-video-component}

Le [Composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer une ressource vidéo prédéfinie prête à l’emploi sur votre page.

Pour qu’un transcodage correct se produise, un administrateur installe FFmpeg séparément. Voir [Installation de FFmpeg et configuration des AEM](#install-ffmpeg). Les administrateurs également [Configuration de profils vidéo](#configure-video-profiles) à utiliser avec les éléments HTML5.

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande d’utiliser la variable [Composant Incorporer des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) au lieu de .

>[!CAUTION]
>
>Ce composant ne doit plus fonctionner d’usine sans une personnalisation étendue au niveau du projet.

## Configuration des profils vidéo {#configure-video-profiles}

Pour utiliser des éléments HTML5, définissez des profils vidéo. Les profils vidéo sélectionnés ici sont utilisés dans l’ordre. Pour y accéder, utilisez le [mode de conception](/help/sites-authoring/default-components-designmode.md) (interface utilisateur classique uniquement) et sélectionnez l’onglet **[!UICONTROL Profils]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Dans cette boîte de dialogue, vous pouvez également configurer la conception du composant vidéo et les paramètres pour [!UICONTROL Lecture], [!UICONTROL Flash], et [!UICONTROL Avancé].

## Installation de FFmpeg et configuration des AEM {#install-ffmpeg}

Le composant Vidéo repose sur le produit Open Source tiers FFmpeg pour le transcodage des vidéos. Téléchargé à partir de [https://ffmpeg.org/](https://ffmpeg.org/). Après avoir installé FFmpeg, configurez AEM pour utiliser un codec audio spécifique et des options d’exécution spécifiques.

Pour installer FFmpeg sur **Windows**, procédez comme suit :

1. Téléchargez le fichier binaire compilé en tant que `ffmpeg.zip`.
1. Désarchivez dans un dossier.
1. Définition de la variable d’environnement système `PATH` à &lt;*your-ffmpeg-location*>`\bin`.
1. Redémarrez AEM.

Pour installer FFmpeg sur **Mac OS X**, procédez comme suit :

1. Installer Xcode disponible à l’adresse [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Installation disponible à l’adresse [XQuartz](https://www.xquartz.org) pour obtenir [X11](https://support.apple.com/fr-fr/HT201341).
1. Installation de MacPorts disponible à l’adresse [www.macports.org](https://www.macports.org/).
1. Dans la console, exécutez `sudo port install ffmpeg` et suivez les instructions affichées à l’écran. Assurez-vous que le chemin d’accès de la variable `FFmpeg` Le fichier exécutable est ajouté à la variable `PATH` Variable système.

Pour installer FFmpeg sur **Mac OS X 10.6**, à l’aide de la version précompilée, procédez comme suit :

1. Téléchargez la version précompilée.
1. Désarchivez-la dans la `/usr/local` répertoire .
1. Dans la console, exécutez `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modifiez les chemins selon les besoins.

À **configuration des AEM**, procédez comme suit :

>[!NOTE]
>
>Ces étapes ne sont nécessaires que si une personnalisation ultérieure des codecs est requise.

1. Ouvrir [!UICONTROL CRXDE Lite] dans votre navigateur web. Accès [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Sélectionnez la `/libs/settings/dam/video/format_aac/jcr:content` et assurez-vous que les propriétés du noeud sont les suivantes :

   * `audioCodec` est `aac`.
   * `customArgs` est `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Pour personnaliser la configuration, créez une superposition dans `/apps/settings/` et déplacez la même structure sous `/conf/global/settings/` noeud . Il ne peut pas être modifié dans `/libs` noeud . Par exemple, pour recouvrir le chemin `/libs/settings/dam/video/fullhd-bp`, créez-le à l’adresse `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Remplacez et modifiez le profile-node entier et pas seulement la propriété ayant besoin d’être modifiée. Ces ressources ne sont pas résolues via SlingResourceMerger.

4. Si vous avez modifié des propriétés, cliquez sur **[!UICONTROL Tout enregistrer]**.

>[!NOTE]
>
>Les modifications apportées aux modèles de workflow d’usine par défaut ne sont pas conservées lorsque vous mettez à niveau votre instance AEM. Adobe recommande de copier les modèles de workflow modifiés avant de les modifier. Par exemple, copiez la [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] avant de modifier l’étape Transcodage FFmpeg dans le [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] pour sélectionner les noms de profil vidéo qui existaient avant la mise à niveau. Vous pouvez ensuite superposer le `/apps` pour permettre AEM récupérer les modifications personnalisées dans le modèle OOTB.
