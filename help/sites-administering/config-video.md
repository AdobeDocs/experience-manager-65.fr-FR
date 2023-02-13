---
title: Configurer le composant vidéo
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
workflow-type: ht
source-wordcount: '489'
ht-degree: 100%

---

# Configurer le composant vidéo {#configure-the-video-component}

Le [composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer sur votre page une ressource vidéo prédéfinie et prête à l’emploi.

Pour qu’un transcodage correct se produise, un administrateur installe FFmpeg séparément. Consultez [Installation de FFmpeg et configuration d’AEM](#install-ffmpeg). De même, les administrateurs [configurent vos profils vidéo](#configure-video-profiles) pour les utiliser avec les éléments HTML5.

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande plutôt l’utilisation du [composant intégré aux composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html?lang=fr).

>[!CAUTION]
>
>Ce composant n’est plus censé fonctionner sans nécessiter une personnalisation détaillée au niveau du projet.

## Configuration des profils vidéo {#configure-video-profiles}

Pour utiliser des éléments HTML5, définissez des profils vidéo. Les profils vidéo sélectionnés ici sont utilisés dans l’ordre. Pour y accéder, utilisez le [mode de conception](/help/sites-authoring/default-components-designmode.md) (interface utilisateur classique uniquement) et sélectionnez l’onglet **[!UICONTROL Profils]** :

![chlimage_1-317](assets/chlimage_1-317.png)

À partir de cette boîte de dialogue, vous pouvez également configurer la conception du composant Vidéo et des paramètres de [!UICONTROL Lecture], [!UICONTROL Flash] et [!UICONTROL Avancés].

## Installation de FFmpeg et configuration d’AEM {#install-ffmpeg}

Le composant Vidéo repose sur le produit open-source tiers FFmpeg pour le transcodage des vidéos. Téléchargé à partir de [https://ffmpeg.org/](https://ffmpeg.org/). Après avoir installé FFmpeg, configurez AEM pour pouvoir utiliser un codec audio et des options d’exécution spécifiques.

Pour installer FFmpeg sur **Windows**, procédez comme suit :

1. Téléchargez le fichier binaire compilé en tant que `ffmpeg.zip`.
1. Désarchivez dans un dossier.
1. Définissez la variable d’environnement système `PATH` à &lt;*your-ffmpeg-location*>`\bin`.
1. Redémarrez AEM.

Pour installer FFmpeg sur **Mac OS X**, procédez comme suit :

1. Installez Xcode, disponible à l’adresse [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Rendez-vous à l’adresse [XQuartz](https://www.xquartz.org) pour obtenir [X11](https://support.apple.com/fr-fr/HT201341).
1. Installez MacPorts, disponible à l’adresse [www.macports.org](https://www.macports.org/).
1. Dans la console, exécutez `sudo port install ffmpeg` et suivez les instructions affichées à l’écran. Assurez-vous que le chemin d’accès du fichier l’exécutable `FFmpeg` est ajouté à la variable système `PATH`.

Pour installer FFmpeg sur **Mac OS X 10.6**, à l’aide de la version précompilée, procédez comme suit :

1. Téléchargez la version précompilée.
1. Désarchivez-la dans le répertoire `/usr/local`.
1. Dans la console, exécutez `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modifiez les chemins selon les besoins.

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
>Les modifications apportées aux modèles de workflows prêts à l’emploi ne sont pas conservées lorsque vous mettez à niveau votre instance AEM. Adobe recommande de copier les modèles de workflow modifiés avant de les modifier. Par exemple, copiez le modèle de [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] prêt à l’emploi avant de modifier l’étape de transcodage FFmpeg dans le modèle de [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] afin de choisir des noms de vidéo-profil qui existaient avant la mise à niveau. Ensuite, vous pouvez remplacer le nœud `/apps` pour permettre à AEM de récupérer les modifications personnalisées apportées au modèle prêt à l’emploi.
