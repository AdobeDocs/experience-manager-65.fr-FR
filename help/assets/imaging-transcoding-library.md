---
title: Bibliothèque ITL
description: Apprenez à configurer et à utiliser la bibliothèque de transcodage de l’imagerie (ou ITL, de l’anglais Imaging Transcoding Library) d’Adobe, une solution de traitement des images qui peut réaliser des fonctions essentielles de manipulation graphique, y compris le codage, le transcodage, le rééchantillonnage et le redimensionnement des images.
contentOwner: AG
role: Administrator
feature: Rendus,Outils de développement,Traitement des ressources
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 38%

---


# Bibliothèque ITL {#imaging-transcoding-library}

La bibliothèque ITL (Imaging Transcoding Library) d’Adobe est une solution de traitement d’images propriétaire qui effectue des fonctions de gestion d’images essentielles, notamment :

* Encodage
* Transcodage (conversion des formats pris en charge)
* Rééchantillonnage d’images à l’aide des algorithmes PS et Intel IPP
* Préservation de la résolution binaire et du profil colorimétrique
* compression de qualité JPEG
* Redimensionnement de l’image

La bibliothèque de transcodage d’images offre une prise en charge CMJN et une prise en charge alpha complète, à l’exception de CMJN -Alpha.

Outre la prise en charge d’un large éventail de formats de fichier et de profils, la bibliothèque de transcodage d’images présente des avantages significatifs par rapport aux autres solutions tierces en matière de performances, d’évolutivité et de qualité. Voici quelques-uns des principaux avantages de l’utilisation de la bibliothèque de transcodage d’images :

* **Mise à l’échelle avec augmentation de la taille ou de la résolution du fichier** : la mise à l’échelle est principalement réalisée grâce à la fonctionnalité ITL brevetée de redimensionnement des fichiers lors de leur décodage. Cette capacité garantit que l’utilisation de la mémoire d’exécution est toujours optimale et n’est pas une fonction quadratique de l’augmentation de la taille du fichier ou de la résolution de l’image. La bibliothèque ITL peut traiter des fichiers haute résolution plus volumineux et haute résolution (contenant un nombre supérieur de mégapixels). Les outils tiers, tels qu’ImageMagick, ne peuvent pas gérer les fichiers volumineux et les blocages système lors du traitement de ces fichiers.
* **Algorithmes de compression de la qualité et du redimensionnement Photoshop** : cohérence avec les normes du secteur en terme de qualité de l’échantillonnage descendant (lisse, pointu et bicubique automatique) et de la qualité de compression. Imaging Transcoding Library (Bibliothèque de transcodage d’images) analyse plus avant le facteur de qualité de l’image d’entrée et utilise intelligemment des tables et des paramètres de qualité optimaux pour l’image de sortie. Cela permet de produire des fichiers de taille optimale sans compromettre la qualité visuelle.
* **Débit élevé :** le temps de réponse est inférieur et le débit est constamment supérieur à ImageMagick. Par conséquent, la bibliothèque de transcodage d’images doit réduire le temps d’attente des utilisateurs et le coût de l’hébergement.
* **Optimisation de l’évolutivité avec le chargement simultané :** Imaging Transcoding Library fonctionne de manière optimale dans des conditions de chargement simultanées. La bibliothèque offre un débit élevé avec une performance du processeur et une utilisation de la mémoire optimaux, et un temps de réponse faible, ce qui permet de réduire le coût de l’hébergement.

## Plateformes prises en charge {#supported-platforms}

La bibliothèque de transcodage d’images est disponible uniquement pour les distributions RHEL 7 et CentOS 7.

>[!NOTE]
>
>Les systèmes Mac OS et autres distributions de type *nix (par exemple, Debian et Ubuntu) ne sont pas pris en charge.

## Utilisation {#usage}

Les arguments de ligne de commande de la bibliothèque ITL peuvent inclure les éléments suivants :

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Vous pouvez configurer les options suivantes pour le paramètre `-resize` :

* `X`: Fonctionne de la même manière que  [!DNL Experience Manager]. Par exemple, -resize 319.
* `WxH`: Le rapport L/H n’est pas conservé, par exemple  `-resize 319x319`.
* `Wx` : définit la largeur et calcule la hauteur en conservant le rapport d’aspect. Par exemple, `-resize 319x`.
* `xH` : définit la hauteur et calcule la largeur en conservant le rapport d’aspect. Par exemple, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configuration de la bibliothèque ITL {#configuring-imaging-transcoding-library}

Pour configurer le traitement ITL, créez un fichier de configuration et mettez à jour le processus pour l’exécuter.

### Créer un fichier de configuration pour le lot extrait {#create-conf-file}

Pour configurer la bibliothèque, créez un fichier CONF pour indiquer les bibliothèques à l’aide des étapes suivantes. Vous avez besoin d’autorisations d’administrateur ou de root.

1. Téléchargez le [package de la bibliothèque de transcodage d’images à partir de Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) et installez-le à l’aide de Package Manager. Le package est compatible avec [!DNL Experience Manager] 6.5.

1. Pour connaître un ID de lot pour `com.day.cq.dam.cq-dam-switchengine`, connectez-vous à la console Web et cliquez sur **[!UICONTROL OSGi]** > **[!UICONTROL Bundles]**. Vous pouvez également ouvrir la console des lots en accédant à l’URL `https://[aem_server:[port]/system/console/bundles/`. Localisez le lot `com.day.cq.dam.cq-dam-switchengine` et son ID.

1. Assurez-vous que toutes les bibliothèques requises sont extraites en vérifiant le dossier à l’aide de la commande `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, où le nom du dossier est créé à l’aide de l’ID d’assemblage. Par exemple, la commande est `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si l’ID d’assemblage est `588`.

1. Créez le fichier `SWitchEngineLibs.conf` à lier à la bibliothèque.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Ajoutez `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` chemin d’accès au fichier conf à l’aide de la commande `cat SWitchEngineLibs.conf`.

1. Exécutez la commande `ldconfig` pour créer les liens et le cache nécessaires.

1. Dans le compte utilisé pour début [!DNL Experience Manager], modifiez le fichier `.bash_profile`. Ajoutez `LD_LIBRARY_PATH` en ajoutant ce qui suit.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Pour vous assurer que la valeur du chemin d’accès est définie sur `.`, utilisez la commande `echo $LD_LIBRARY_PATH`. La sortie doit simplement être `.`. Si la valeur n&#39;est pas définie sur `.`, redémarrez la session.

### Configurer [!UICONTROL le flux de travail {#configure-dam-asset-update-workflow} DAM Update Asset]

Mettez à jour le flux de travail [!UICONTROL DAM Update Asset] pour utiliser la bibliothèque pour le traitement des images.

1. Dans l&#39;interface utilisateur [!DNL Experience Manager], sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.

1. Dans la page **[!UICONTROL Modèles de flux de travaux]**, ouvrez le modèle de flux de travaux **[!UICONTROL DAM Update Asset]** en mode d’édition.

1. Ouvrez l’étape de processus **[!UICONTROL Traiter les miniatures]**. Dans l’onglet **[!UICONTROL Miniatures]**, ajoutez les types MIME pour lesquels vous souhaitez ignorer le processus de génération de miniatures par défaut dans la liste **[!UICONTROL Ignorer les types MIME]**.
Par exemple, si vous souhaitez créer des miniatures pour une image TIFF à l’aide de la bibliothèque de transcodage d’images, spécifiez `image/tiff` dans le champ **[!UICONTROL Ignorer les types MIME]**.

1. Dans l’onglet **[!UICONTROL Image Web]**, ajoutez les types MIME pour lesquels vous souhaitez ignorer le processus de génération de rendu web par défaut dans **[!UICONTROL Liste à ignorer]**. Par exemple, si vous avez ignoré le type MIME `image/tiff` à l’étape ci-dessus, ajoutez `image/tiff` à la liste de saut.

1. Ouvrez l’étape **[!UICONTROL Miniatures EPS (optimisées par ImageMagick)]**, accédez à l’onglet **[!UICONTROL Arguments]**. Dans la liste **[!UICONTROL Mime Types]**, ajoutez les types MIME que la bibliothèque de transcodage d’images doit traiter. Par exemple, si vous avez ignoré le type MIME `image/tiff` à l’étape ci-dessus, ajoutez `image/jpeg` à la liste **[!UICONTROL Types MIME]**.

1. Supprimez les commandes par défaut, le cas échéant.

1. Active/désactive le panneau latéral et ajoute le **[!UICONTROL gestionnaire SWitchEngine]** à la liste des étapes.

1. Ajoutez les commandes au [!UICONTROL Gestionnaire SwitchEngine] en fonction de vos besoins personnalisés. Réglez les paramètres des commandes que vous spécifiez pour répondre à vos besoins. Par exemple, si vous souhaitez préserver le profil colorimétrique de votre image JPEG, ajoutez les commandes suivantes à la liste **[!UICONTROL Commandes]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![limage](assets/chlimage_1-199.png)

1. (Facultatif) Générez des miniatures à partir d’un rendu intermédiaire à l’aide d’une seule commande. Le rendu intermédiaire sert de source pour générer des rendus statiques et des rendus web. Cette méthode est plus rapide que la méthode précédente. Toutefois, vous ne pouvez pas appliquer de paramètres personnalisés aux miniatures à l’aide de cette méthode.

   ![limage](assets/chlimage_1-200.png)

1. Pour générer des rendus Web, configurez les paramètres dans l&#39;onglet **[!UICONTROL Image Web-Enabled]**.

1. Synchronisez le modèle de flux de travaux [!UICONTROL DAM Update Asset] mis à jour. Enregistrez le workflow.

Le programme vérifie la configuration, télécharge une image TIFF et surveille le fichier error.log. Vous remarquerez les messages `INFO` avec les mentions de `SwitchEngineHandlingProcess execute: executing command line`. Les journaux mentionnent les rendus générés. Une fois le processus terminé, vous pouvez vue les nouveaux rendus dans [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Article de types MIME pris en charge](assets-formats.md#supported-image-transcoding-library)

