---
title: Formats de fichiers et types MIME pris en charge
description: Formats de fichiers et types MIME pris en charge par  [!DNL Assets]  et  [!DNL Dynamic Media] , et les fonctionnalités prises en charge pour chaque format.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0d491be4fb2605220b1558c8c877151ab4405978
workflow-type: ht
source-wordcount: '1872'
ht-degree: 100%

---

# Formats pris en charge dans [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] prend en charge un large éventail de formats de fichier. Chaque fonctionnalité prend en charge différents types MIME. Pour intégrer [!DNL Assets] à d’autres solutions de gestion des ressources numériques (DAM) et logiciels de bureau conformes aux normes, utilisez la plateforme [!DNL Extensible Metadata Platform] (XMP) d’Adobe.

Reportez-vous à la légende pour comprendre le niveau de prise en charge.

| Niveau de prise en charge | Description |
| :-----------: | ------------------------------ |
| ✓ | Pris en charge |
| &#42; | Prise en charge avec des fonctionnalités de composant additionnel |
| − | Non applicable |

## Formats d’image matricielle pris en charge dans [!DNL Experience Manager] {#supported-raster-image-formats}

Les formats d’image matricielle pris en charge dans [!DNL Assets] sont les suivants :

| Format | Stockage | Gestion des métadonnées | Extraction de métadonnées | Génération de miniatures | Modification | Écriture différée des métadonnées | Insights |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡ L’image fusionnée est extraite du fichier PSD. Il s’agit d’une image générée par Adobe Photoshop et incluse dans le fichier PSD. Selon les paramètres, l’image fusionnée peut constituer ou non l’image réelle.

Outre les informations ci-dessus, tenez compte des points suivants :

* La prise en charge des fichiers EPS s’applique uniquement aux images matricielles. Par exemple, la génération de miniatures pour les images vectorielles EPS n’est pas prise en charge par défaut. Pour ajouter une prise en charge, [configurez ImageMagick](best-practices-for-imagemagick.md). Pour intégrer des outils tiers afin d’activer des fonctionnalités supplémentaires, consultez [Gestionnaire de médias en ligne de commande](media-handlers.md#command-line-based-media-handler).

* L’écriture différée des métadonnées fonctionne pour le format PSB lorsqu’elle est ajoutée au gestionnaire `NComm`.

* Concernant les fichiers EPS, l’écriture différée des métadonnées est prise en charge dans PostScript Document Structuring Convention (PS-Adobe) version 3.0 ou supérieure.

## Formats 3D pris en charge {#support-3d-formats}

Les formats 3D de la liste suivante sont pris en charge.

Voir [Utilisation de ressources 3D dans Dynamic Media.](/help/assets/assets-3d.md)

| Format | Stockage | Contrôle de version | Workflow | Publication | Contrôle d’accès | Aperçu de miniature | Aperçu 3D | Diffusion Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## Bibliothèque PDF Rasterizer prise en charge {#supported-pdf-rasterizer-library}

La bibliothèque Adobe PDF Rasterizer génère des miniatures de haute qualité et des aperçus pour les fichiers [!DNL Adobe Illustrator] et PDF de grande taille et riches en contenu. Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Les fichiers AI/PDF à fort contenu dont le traitement nécessite un nombre important de ressources
* Fichiers AI/PDF pour lesquels les miniatures ne sont pas générées par défaut.
* Fichiers AI contenant des couleurs PMS (Pantone Matching System)

Consultez [Utilisation de PDF Rasterizer](aem-pdf-rasterizer.md).

## Bibliothèque de transcodage d’images prise en charge {#supported-image-transcoding-library}

La bibliothèque de transcodage d’imagerie Adobe est une solution de traitement d’images exécutant des fonctions essentielles de manipulation graphique, telles que le codage, le transcodage, le ré-échantillonnage, le redimensionnement, etc.

La bibliothèque de transcodage d’imagerie prend en charge les types MIME JPG/JPEG, PNG (8 et 16 bits), GIF, BMP, TIFF/TIFF compressé (sauf les fichiers TIFF 32 bits et les fichiers PTIFF), ICO et ICN.

Consultez [Configuration de la bibliothèque ITL](imaging-transcoding-library.md).

## Prise en charge de Camera Raw {#supported-camera-raw}

La bibliothèque [!DNL Adobe Camera Raw] permet à [!DNL Assets] d’importer des images brutes. Consultez [Prise en charge de Camera Raw](camera-raw.md).

## Formats de documents [!DNL Assets] pris en charge {#supported-document-formats}

Les formats de documents pris en charge pour les fonctionnalités de gestion des ressources sont les suivants :

| Format | Stockage | [Gestion des métadonnées](metadata.md) | Extraction de texte intégral <br> | [Extraction de métadonnées](metadata.md) | Génération de miniatures<br> | [Extraction de sous-ressource](managing-linked-subassets.md) | [Écriture différée des métadonnées](xmp-writeback.md) | [Ressources connectées](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| EPUB | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## Formats multimédias pris en charge {#supported-multimedia-formats}

| | Stockage | Gestion des métadonnées | Extraction de métadonnées | Génération de miniatures | Transcodage FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## Formats d’archives pris en charge {#supported-archive-formats}

Le tableau suivant présente les formats d’archive pris en charge et l’applicabilité des workflows de gestion des ressources numériques courants.

| Formats | Stockage | Contrôle de version | Workflow | Publication | Contrôle d’accès | Diffusion Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Autres formats pris en charge {#other-supported-formats}

L’applicabilité des fonctionnalités de gestion des ressources numériques habituelles pour quelques formats de fichiers spécifiques est décrite ci-dessous.

| Formats | Stockage | Contrôle de version | Workflow | Publication | Contrôle d’accès | Diffusion Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (lorsque configuré avec son propre domaine de diffusion) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>Il se peut que le téléchargement et la distribution de fichiers JavaScript puissent présenter des failles de sécurité. Si nécessaire, vous pouvez utiliser des recouvrements pour empêcher les utilisateurs de télécharger des fichiers JS.

## Types MIME pris en charge {#supported-mime-types}

Par défaut, [!DNL Experience Manager] détecte le type de fichier à l’aide de l’extension de fichier. [!DNL Experience Manager] peut le détecter à partir du contenu des fichiers. Pour plus d’informations, sélectionnez l’option [!UICONTROL Détecter le MIME du contenu] du [!UICONTROL service de type MIME de gestion des ressources numériques Day CQ] dans la console Web [!DNL Experience Manager].

Une liste des types MIME pris en charge est disponible dans CRXDE Lite à l’adresse `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extension de fichier | Type MIME/type de support Internet | Valeur de jobParam par défaut | Valeur de jobParam autorisée |
|---|---|---|---|
| Image | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | La valeur de jobParam par défaut s’applique à toutes les ressources de type MIME image.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html?lang=fr)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html?lang=fr)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html?lang=fr)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html?lang=fr)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html?lang=fr)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html?lang=fr)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html?lang=fr)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html?lang=fr)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html?lang=fr)</li></ul> |
| 3G2 | video/3gpp2 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| 3GP | video/3gpp | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=fr)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=fr)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| BMP | image/bmp | | |
| CSS | text/css | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| M4V | video/x-m4v | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| MOV | video/quicktime | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| MPEG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| MPG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| OTF | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html?lang=fr) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=fr)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=fr</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html?lang=fr)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html?lang=fr)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF/TIFF | image/tiff | | |
| TTC | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | video/dvd | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls.html?lang=fr) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media : formats vidéo d’entrée pris en charge pour le transcodage {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extension de fichier vidéo | Conteneur | Codecs vidéo recommandés | Codecs vidéo non pris en charge |
|---|---|---|---|
| AVI | A/V Interleave | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (fichiers d’animation vectorielle) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 et HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| MP4 | MPEG-4 | H264/AVC (tous les profils) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft® Screen (MSS2), Microsoft® Photo Story (WVP2) |

‡ Ce format vidéo n’est pas encore pris en charge pour une utilisation avec les vidéos interactives dans Dynamic Media ou avec lʼannotation dans Experience Manager Assets.

## Dynamic Media - Formats de document pris en charge {#supported-document-formats-dynamic-media}

| Format | Charger<br> (format d’entrée) | Créer un <br>paramètre prédéfini <br>d’image<br> (format de sortie) | Prévisualiser un rendu <br>dynamique<br> | Diffuser un rendu <br>dynamique<br> | Télécharger un rendu <br>dynamique<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (Voir la remarque ci-dessous) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Pour les PDF sécurisés, seul le téléchargement est pris en charge.

Outre les fonctionnalités ci-dessus, tenez compte des points suivants :

* Pour utiliser Dynamic Media de sorte à générer des rendus dynamiques pour des fichiers PDF, voir [Adobe Illustrator (AI), Postscript (EPS) et formats de fichier PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Pour utiliser Dynamic Media afin de prévisualiser et de générer des rendus dynamiques pour les fichiers AI, voir [les formats de fichiers Adobe Illustrator (AI), Postscript (EPS) et PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Pour utiliser Dynamic Media afin de générer des rendus dynamiques pour les fichiers INDD, consultez [Format de fichier InDesign (INDD)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - Formats d’images pixellisées prises en charge {#supported-raster-image-formats-dynamic-media}

| Format | Charger (format d’entrée) | Créer un paramètre prédéfini d’image (format de sortie) | Prévisualiser un rendu dynamique | Diffuser un rendu dynamique | Télécharger un rendu dynamique | Types de visionneuses qui prennent en charge ce format |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Image](/help/assets/image-sets.md), [Supports variés](/help/assets/mixed-media-sets.md) et [360°](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Image](/help/assets/image-sets.md), [Supports variés](/help/assets/mixed-media-sets.md) et [360°](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Image](/help/assets/image-sets.md), [Supports variés](/help/assets/mixed-media-sets.md) et [360°](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Image](/help/assets/image-sets.md), [Supports variés](/help/assets/mixed-media-sets.md) et [360°](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ L’image fusionnée est extraite du fichier PSD. Il s’agit d’une image générée par Adobe Photoshop et incluse dans le fichier PSD. Selon les paramètres, l’image fusionnée peut constituer ou non l’image réelle.

* La prise en charge des fichiers EPS s’applique uniquement aux images matricielles. Par exemple, la génération de miniatures pour les images vectorielles EPS n’est pas prise en charge par défaut. Pour ajouter une prise en charge, [configurez ImageMagick](best-practices-for-imagemagick.md). Pour intégrer des outils tiers afin d’activer des fonctionnalités supplémentaires, consultez [Gestionnaire de médias en ligne de commande](media-handlers.md#command-line-based-media-handler).

* Pour utiliser [!DNL Dynamic Media] pour prévisualiser et générer des rendus dynamiques pour les fichiers EPS, consultez [Adobe Illustrator (AI), Postscript (EPS) et les formats de fichier PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Concernant les fichiers EPS, l’écriture différée des métadonnées est prise en charge dans PostScript Document Structuring Convention (PS-Adobe) version 3.0 ou supérieure.

## Dynamic Media - Formats d’images matricielles non prises en charge {#unsupported-image-formats-dynamic-media}

La liste suivante décrit les sous-types de formats de fichiers d’images matricielles *non* pris en charge dans Dynamic Media.

Consultez aussi l’article [Détecter les formats de fichiers non pris en charge pour Dynamic Media](https://helpx.adobe.com/fr/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) de la base de connaissances.

* Fichiers PNG dont la taille de bloc IDAT est supérieure à 100 Mo.
* Fichiers PSB.
* Les fichiers PSD avec un espace colorimétrique autre que CMJN, RVB, niveaux de gris ou bitmap ne sont pas pris en charge. Les espaces colorimétriques DuoTone, Lab et indexé ne sont pas pris en charge.
* Fichiers PSD ayant une résolution binaire supérieure à 16.
* Fichiers TIFF contenant des données à virgule flottante.
* Fichiers TIFF dotés d’un espace colorimétrique Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media - Formats 3D pris en charge {#supported-three-d-file-formats-in-dm}

Dynamic Media prend en charge les formats de 3D suivants :

Consultez [Utilisation de ressources 3D dans Dynamic Media](/help/assets/assets-3d.md).

| Extension de fichier 3D | Format de fichier | Type MIME | Remarques |
|---|---|---|---|
| GLB | Transmission GL binaire | model/gltf-binary | Inclut les matières et les textures dans une seule ressource. |
| OBJ | Fichier d’objet 3D WaveFront | application/x-tgif |  |
| STL | Stéréolithographie | application/vnd.ms-pki.stl |  |
| USDZ | Fichier zip de description de scène universelle | model/vnd.usdz+zip | *Prise en charge de l’ingestion uniquement ; aucun affichage ni interaction n’est disponible.* USDZ est un format 3D propriétaire qui peut être visualisé en mode natif à l’aide d’appareils Safari ou iOS. |

>[!MORELIKETHIS]
>
>* [Activez la prise en charge des paramètres de tâche de téléchargement Assets et Dynamic Media Classic basés sur le type MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configurez la prise en charge des paramètres de tâche de téléchargement basés sur le type MIME](config-dynamic.md).
