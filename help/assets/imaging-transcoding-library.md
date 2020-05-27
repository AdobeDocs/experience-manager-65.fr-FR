---
title: Bibliothèque ITL
description: Apprenez à configurer et à utiliser la bibliothèque de transcodage de l’imagerie (ou ITL, de l’anglais Imaging Transcoding Library) d’Adobe, une solution de traitement des images qui peut réaliser des fonctions essentielles de manipulation graphique, y compris le codage, le transcodage, le rééchantillonnage et le redimensionnement des images.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 37%

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
* **Débit élevé :** Le temps de réponse est inférieur et le débit est constamment supérieur à ImageMagick. Par conséquent, la bibliothèque de transcodage d’images doit réduire le temps d’attente des utilisateurs et le coût de l’hébergement.
* **Optimiser l&#39;évolutivité avec la charge simultanée :** La bibliothèque de transcodage d’images fonctionne de manière optimale dans des conditions de chargement simultanées. La bibliothèque offre un débit élevé avec une performance du processeur et une utilisation de la mémoire optimaux, et un temps de réponse faible, ce qui permet de réduire le coût de l’hébergement.

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

You can configure the following options for the `-resize` parameter:

* `X`: Fonctionne de la même manière qu’Experience Manager. Par exemple, -resize 319.
* `WxH`: Le rapport L/H n’est pas conservé, par exemple `-resize 319x319`.
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

Pour configurer la bibliothèque, créez un fichier .conf pour indiquer les bibliothèques à l’aide des étapes suivantes. Vous avez besoin d’autorisations d’administrateur ou de root.

1. Download the [Imaging Transcoding Library package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) and install it using the Package Manager. Le package est compatible avec Experience Manager 6.5.

1. Pour connaître un ID d&#39;assemblage pour `com.day.cq.dam.cq-dam-switchengine`, connectez-vous à la console Web et cliquez sur **[!UICONTROL OSGi > Bundles]**. Vous pouvez également ouvrir la console des lots en utilisant l’ `https://[aem_server:[port]/system/console/bundles/` URL d’accès. Localisez le `com.day.cq.dam.cq-dam-switchengine` lot et son ID.

1. Assurez-vous que toutes les bibliothèques requises sont extraites en vérifiant le dossier à l’aide de la commande `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, où le nom de dossier est créé à l’aide de l’ID d’assemblage. Par exemple, la commande est `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si l’ID d’assemblage est `588`défini.

1. Créez un `SWitchEngineLibs.conf` fichier à lier à la bibliothèque.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Ajouter chemin d’accès au fichier conf à l’aide de la `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` `cat SWitchEngineLibs.conf` commande.

1. Exécutez `ldconfig` la commande pour créer les liens et le cache nécessaires.

1. Dans le compte utilisé pour début d’Experience Manager, modifiez le `.bash_profile` fichier. Ajouter `LD_LIBRARY_PATH` en ajoutant ce qui suit.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Pour vous assurer que la valeur du chemin d’accès est définie sur `.`, utilisez `echo $LD_LIBRARY_PATH` la commande. La production ne devrait être que `.`. Si la valeur n&#39;est pas définie sur `.`, redémarrez la session.

### Configurer le processus de mise à jour des ressources  DAM {#configure-dam-asset-update-workflow}

Mettez à jour le processus de mise à jour des actifs  DAM pour utiliser la bibliothèque pour le traitement des images.

1. Dans l’interface utilisateur d’Experience Manager, sélectionnez **[!UICONTROL Outils > Processus > Modèles]**.

1. From the **[!UICONTROL Workflow Models]** page, open the **[!UICONTROL DAM Update Asset]** workflow model in edit mode.

1. Open the **[!UICONTROL Process Thumbnails]** workflow process step. In the **[!UICONTROL Thumbnails]** tab, add the MIME types for which you want to skip the default thumbnail generation process in the **[!UICONTROL Skip Mime Types]** list.
For example, if you want to create thumbnails for a TIFF image using Imaging Transcoding Library, specify `image/tiff` in the **[!UICONTROL Skip Mime Types]** field.

1. Dans l’onglet **[!UICONTROL Image Web]**, ajoutez les types MIME pour lesquels vous souhaitez ignorer le processus de génération de rendu web par défaut dans **[!UICONTROL Liste à ignorer]**. For example, if you skipped MIME type `image/tiff` in the above step, add `image/tiff` to the skip list.

1. Open the **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** step, navigate to the **[!UICONTROL Arguments]** tab. In the **[!UICONTROL Mime Types]** list, add the MIME types you want Imaging Transcoding Library to process. For example, if you skipped the MIME type `image/tiff` in the above step, add `image/jpeg` to the **[!UICONTROL Mime Types]** list.

1. Supprimez les commandes par défaut, le cas échéant.

1. Active/désactive le panneau latéral et ajoute le **[!UICONTROL gestionnaire SWitchEngine]** à la liste des étapes.

1. Ajouter des commandes au gestionnaire  SwitchEngine en fonction de vos besoins personnalisés. Réglez les paramètres des commandes que vous spécifiez pour répondre à vos besoins. Par exemple, si vous souhaitez préserver le profil colorimétrique de votre image JPEG, ajoutez les commandes suivantes à la liste **[!UICONTROL Commandes]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![limage](assets/chlimage_1-199.png)

1. (Facultatif) Générez des miniatures à partir d’un rendu intermédiaire à l’aide d’une seule commande. Le rendu intermédiaire sert de source pour générer des rendus statiques et des rendus web. Cette méthode est plus rapide que la méthode précédente. Toutefois, vous ne pouvez pas appliquer de paramètres personnalisés aux miniatures à l’aide de cette méthode.

   ![limage](assets/chlimage_1-200.png)

1. Pour générer des rendus Web, configurez les paramètres dans l’onglet Image **[!UICONTROL compatible]** Web.

1. Synchronisez le modèle mis à jour du processus de mise à jour des actifs  DAM. Enregistrez le workflow.

Le programme vérifie la configuration, télécharge une image TIFF et surveille le fichier error.log. Vous remarquerez `INFO` les messages avec des mentions de `SwitchEngineHandlingProcess execute: executing command line`. Les journaux mentionnent les rendus générés. Une fois le processus terminé, vous pouvez vue les nouveaux rendus dans Experience Manager.

>[!MORELIKETHIS]
>
>* [Article de types MIME pris en charge](assets-formats.md#supported-image-transcoding-library)

