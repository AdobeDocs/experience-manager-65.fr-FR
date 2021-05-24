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
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 22%

---

# Configuration du composant vidéo {#configure-the-video-component}

Le [composant vidéo](/help/sites-authoring/default-components-foundation.md#video) vous permet de placer une ressource vidéo prédéfinie prête à l’emploi sur votre page.

Pour qu’un transcodage correct se produise, un administrateur installe FFmpeg séparément. Voir [Installer FFmpeg et configurer AEM](#install-ffmpeg). Les administrateurs peuvent également [configurer des profils vidéo](#configure-video-profiles) à utiliser avec des éléments HTML5.

>[!CAUTION]
>
>Ce composant de base est obsolète. Adobe recommande plutôt d’utiliser le [composant Incorporer des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) .

>[!CAUTION]
>
>Ce composant ne doit plus fonctionner d’usine sans une personnalisation étendue au niveau du projet.

## Configuration des profils vidéo {#configure-video-profiles}

Pour utiliser des éléments HTML5, définissez des profils vidéo. Les profils vidéo sélectionnés ici sont utilisés dans l’ordre. Pour y accéder, utilisez le [mode de conception](/help/sites-authoring/default-components-designmode.md) (interface utilisateur classique uniquement) et sélectionnez l’onglet **[!UICONTROL Profils]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Dans cette boîte de dialogue, vous pouvez également configurer la conception du composant vidéo et les paramètres pour [!UICONTROL Lecture], [!UICONTROL Flash] et [!UICONTROL Avancé].

## Installez FFmpeg et configurez AEM {#install-ffmpeg}

Le composant Vidéo repose sur le produit Open Source tiers FFmpeg pour le transcodage des vidéos. Téléchargé à partir de [https://ffmpeg.org/](https://ffmpeg.org/). Après avoir installé FFmpeg, configurez AEM pour utiliser un codec audio spécifique et des options d’exécution spécifiques.

Pour installer FFmpeg sous **Windows**, procédez comme suit :

1. Téléchargez le fichier binaire compilé en tant que `ffmpeg.zip`.
1. Désarchivez dans un dossier.
1. Définissez la variable d’environnement système `PATH` sur &quot;a1/>your-ffmpeg-location *`\bin`.*
1. Redémarrez AEM.

Pour installer FFmpeg sous **Mac OS X**, procédez comme suit :

1. Installez Xcode disponible à l’adresse [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Installez disponible à l’adresse [XQuartz](https://www.xquartz.org) pour obtenir [X11](https://support.apple.com/fr-fr/HT201341).
1. Installez les MacPorts disponibles à l’adresse [www.macports.org](https://www.macports.org/).
1. Dans la console, exécutez la commande `sudo port install ffmpeg` et suivez les instructions à l’écran. Assurez-vous que le chemin d’accès de l’exécutable `FFmpeg` est ajouté à la variable système `PATH`.

Pour installer FFmpeg sous **Mac OS X 10.6**, à l’aide de la version précompilée, procédez comme suit :

1. Téléchargez la version précompilée.
1. Désarchivez-le dans le répertoire `/usr/local`.
1. Dans la console, exécutez `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Modifiez les chemins selon les besoins.

Pour **configurer AEM**, procédez comme suit :

>[!NOTE]
>
>Ces étapes ne sont nécessaires que si une personnalisation ultérieure des codecs est requise.

1. Ouvrez [!UICONTROL CRXDE Lite] dans votre navigateur web. Accédez à [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Sélectionnez le noeud `/libs/settings/dam/video/format_aac/jcr:content` et vérifiez que les propriétés du noeud sont les suivantes :

   * `audioCodec` est `aac`.
   * `customArgs` est `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Pour personnaliser la configuration, créez une superposition dans le noeud `/apps/settings/` et déplacez la même structure sous le noeud `/conf/global/settings/`. Il ne peut pas être modifié dans le noeud `/libs`. Par exemple, pour recouvrir le chemin `/libs/settings/dam/video/fullhd-bp`, créez-le à l’emplacement `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Remplacez et modifiez le profile-node entier et pas seulement la propriété ayant besoin d’être modifiée. Ces ressources ne sont pas résolues via SlingResourceMerger.

4. Si vous avez modifié des propriétés, cliquez sur **[!UICONTROL Tout enregistrer.]**

>[!NOTE]
>
>Les modifications apportées aux modèles de workflow d’usine par défaut ne sont pas conservées lorsque vous mettez à niveau votre instance AEM. Adobe recommande de copier les modèles de workflow modifiés avant de les modifier. Par exemple, copiez le modèle [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] prêt à l’emploi avant de modifier l’étape Transcodage FFmpeg dans le modèle [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] pour sélectionner les noms de profil vidéo qui existaient avant la mise à niveau. Vous pouvez ensuite superposer le noeud `/apps` pour permettre AEM récupérer les modifications personnalisées apportées au modèle OOTB.
