---
title: Configurer le composant vidéo
description: Découvrez comment utiliser le composant vidéo dans Adobe Experience Manager pour placer une ressource vidéo prédéfinie prête à l’emploi sur votre page.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 64%

---

# Configurer le composant vidéo {#configure-the-video-component}

La variable [Composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer une ressource vidéo prédéfinie prête à l’emploi sur votre page.

Pour qu’un transcodage correct se produise, un administrateur installe FFmpeg séparément. Consultez [Installation de FFmpeg et configuration d’AEM](#install-ffmpeg). De même, les administrateurs [configurent vos profils vidéo](#configure-video-profiles) pour les utiliser avec les éléments HTML5.

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande plutôt l’utilisation du [composant principal Composant intégré](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html?lang=fr).

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

## Configuration des profils vidéo {#configure-video-profiles}

Pour utiliser des éléments HTML5, définissez des profils vidéo. Les profils vidéo sélectionnés ici sont utilisés dans l’ordre. Pour y accéder, utilisez [Mode de conception](/help/sites-authoring/default-components-designmode.md) (IU classique uniquement) et sélectionnez l’option **[!UICONTROL Profils]** tab :

![chlimage_1-317](assets/chlimage_1-317.png)

À partir de cette boîte de dialogue, vous pouvez également configurer la conception du composant Vidéo et des paramètres de [!UICONTROL Lecture], [!UICONTROL Flash] et [!UICONTROL Avancés].

## Installation de FFmpeg et configuration d’AEM {#install-ffmpeg}

Le composant Vidéo repose sur le produit open-source tiers FFmpeg pour le transcodage des vidéos. Téléchargé à partir de [https://ffmpeg.org/](https://ffmpeg.org/). Après avoir installé FFmpeg, configurez AEM pour pouvoir utiliser un codec audio et des options d’exécution spécifiques.

Pour installer FFmpeg sur **Windows**, procédez comme suit :

1. Téléchargez le fichier binaire compilé en tant que `ffmpeg.zip`.
1. Désarchivez dans un dossier.
1. Définissez la variable d’environnement système `PATH` à &lt;*your-ffmpeg-location*>`\bin`.
1. Redémarrez AEM.

Pour installer FFmpeg sur **MACOS X**, procédez comme suit :

1. Installez Xcode, disponible à l’adresse [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Rendez-vous à l’adresse [XQuartz](https://www.xquartz.org) pour obtenir [X11](https://support.apple.com/en-us/100724).
1. Installez MacPorts, disponible à l’adresse [www.macports.org](https://www.macports.org/).
1. Dans la console, exécutez `sudo port install ffmpeg` et suivez les instructions affichées à l’écran. Assurez-vous que le chemin d’accès du fichier l’exécutable `FFmpeg` est ajouté à la variable système `PATH`.

Pour installer FFmpeg sur **macOS X 10.6**, à l’aide de la version précompilée, procédez comme suit :

1. Téléchargez la version précompilée.
1. Désarchivez-la dans le répertoire `/usr/local`.
1. Dans la console, exécutez `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modifiez le chemin selon les besoins.

Pour **configurer AEM**, procédez comme suit :

>[!NOTE]
>
>Ces étapes ne sont nécessaires que si une personnalisation ultérieure des codecs est requise.

1. Ouvrez [!UICONTROL CRXDE Lite] dans un navigateur Web. Naviguez vers [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Sélectionnez le nœud `/libs/settings/dam/video/format_aac/jcr:content` et vérifiez que les propriétés du nœud sont les suivantes :

   * `audioCodec` est `aac`.
   * `customArgs` est `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Pour personnaliser la configuration, créez une superposition dans `/apps/settings/` et déplacez la même structure sous le nœud `/conf/global/settings/`. Elle ne peut pas être modifiée dans le nœud `/libs`. Par exemple, pour recouvrir le chemin `/libs/settings/dam/video/fullhd-bp`, créez-le à l’adresse `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Remplacez et modifiez le profile-node entier et pas seulement la propriété ayant besoin d’être modifiée. Ces ressources ne sont pas résolues via SlingResourceMerger.

4. Si vous avez modifié des propriétés, cliquez sur **[!UICONTROL Tout enregistrer]**.

>[!NOTE]
>
>Les modifications apportées aux modèles de workflow d’usine par défaut ne sont pas conservées lors de la mise à niveau de votre instance AEM. Adobe recommande de copier les modèles de workflow modifiés avant de les modifier. Par exemple, copiez le fichier d’usine [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] avant de modifier l’étape Transcodage FFmpeg dans le [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] pour sélectionner les noms de profil vidéo qui existaient avant la mise à niveau. Vous pouvez ensuite superposer la variable `/apps` pour permettre AEM récupérer les modifications personnalisées dans le modèle d’usine.
