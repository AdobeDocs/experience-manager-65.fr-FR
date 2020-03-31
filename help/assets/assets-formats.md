---
title: Formats pris en charge par Assets
description: de formats de fichier pris en charge par les ressources AEM et par les médias dynamiques et fonctionnalités prises en charge pour chaque format.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 593c1e1954a1c8e0355ede9889caed05ff72f3f9

---


# Formats Ressources pris en charge {#assets-supported-formats}

AEM Assets prend en charge un large éventail de formats de fichier. Chaque fonctionnalité prend en charge différents types MIME.

Pour intégrer AEM Assets à d’autres solutions de gestion des actifs numériques (DAM) et logiciels de bureau conformes aux normes, utilisez la plateforme XMP (Extensible Metadata Platform) d’Adobe.

Reportez-vous à la légende pour comprendre le niveau de prise en charge.

| Niveau de prise en charge | Description |
|:---:|---|
| ✓ | Pris en charge |
| * | Prise en charge avec des fonctionnalités de composant additionnel |
| − | Non applicable |

## Formats d’image pixellisée pris en charge dans AEM Assets {#supported-raster-image-formats}

| Format | Stockage | Gestion des métadonnées | Extraction de métadonnées | Génération de miniature | Modification interactive | Écriture différée des métadonnées | Statistiques |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

‡ L’image fusionnée est extraite du fichier PSD. Il s’agit d’une image générée par Adobe Photoshop et incluse dans le fichier PSD. Selon les paramètres, l’image fusionnée peut constituer ou non l’image réelle.

## Formats d’image pixellisée pris en charge dans les médias dynamiques (#supported-raster-image-formats-dynamic-media)

| Format | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **‡** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**‡** L’image fusionnée est extraite du fichier PSD. Il s’agit d’une image générée par Adobe Photoshop et incluse dans le fichier PSD. Selon les paramètres, l’image fusionnée peut constituer ou non l’image réelle.

Outre les informations ci-dessus, tenez compte des points suivants :

* La prise en charge des fichiers EPS s’applique uniquement aux images pixellisées. Par exemple, la génération de vignettes pour les images vectorielles EPS n’est pas prise en charge par défaut. Pour ajouter une prise en charge, [configurez ImageMagick](best-practices-for-imagemagick.md). Pour intégrer des outils tiers afin d’activer des fonctionnalités supplémentaires, voir Gestionnaire de médias basé sur la ligne de [commande](media-handlers.md#command-line-based-media-handler).

* Metadata writeback works for PSB file format when it is added to the `NComm` handler.

* Pour utiliser Dynamic Media pour prévisualiser et générer des rendus dynamiques pour les fichiers EPS, voir [Adobe Illustrator (AI), Postscript (EPS) et les formats de fichier PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Concernant les fichiers EPS, l’écriture différée des métadonnées est prise en charge dans PostScript Document Structuring Convention (PS-Adobe) version 3.0 ou supérieure.

## Formats d’image pixellisée non pris en charge dans les médias dynamiques (#unsupported-image-formats-dynamic-media)

Le tableau suivant décrit les sous-types de formats d’image pixellisés *non* pris en charge dans Contenu multimédia dynamique. Le tableau décrit également les méthodes suggérées que vous pouvez utiliser pour détecter ces fichiers.

| Format | Qu’est-ce qui n’est pas pris en charge ? | Méthode de détection suggérée |
|---|---|---|
| JPEG | Fichiers dont les trois octets initiaux sont incorrects. | Pour identifier un fichier JPEF, ses trois octets initiaux doivent être `ff d8 ff`. S’il s’agit d’autres éléments, il n’est pas classé au format JPEG.<br>・ Il n&#39;existe aucun outil logiciel qui puisse aider à résoudre ce problème.<br>・ Un petit C++/java qui lit les trois octets initiaux d&#39;un fichier devrait être capable de détecter ces types de fichiers.<br>・ Il serait peut-être préférable de suivre la source de ces fichiers et de regarder l&#39;outil qui génère le fichier. |
| PNG | Fichiers dont la taille du bloc IDAT est supérieure à 100 Mo. | Vous pouvez détecter ce problème à l’aide de [libpng](http://www.libpng.org/pub/png/libpng.html) dans C++. |
| PSB |  | Utilisez exiftool si le type de fichier est PSB.<br>Exemple dans un journal ExifTool:<br>1. Type de fichier: `PSB` |
| PSD | Les fichiers avec un espace colorimétrique autre que CMJN, RVB, Niveaux de gris ou Bitmap ne sont pas pris en charge.<br>Les espaces colorimétriques DuoTone, Lab et Indexé ne sont pas pris en charge. | Utilisez ExifTool si le mode Couleur est Bichromie.<br>Exemple dans un journal ExifTool:<br>1. Mode Couleur : `Duotone` |
|  | Fichiers dont la fin est brusque. | Adobe n’est pas en mesure de détecter cette condition. En outre, ces fichiers ne peuvent pas être ouverts avec Adobe PhotoShop. Adobe vous conseille d’examiner l’outil utilisé pour créer un tel fichier et de résoudre les problèmes à la source. |
|  | Fichiers dont la profondeur est supérieure à 16 bits. | Utilisez ExifTool si la profondeur de bit est supérieure à 16.<br>Exemple dans un journal ExifTool:<br>1. Profondeur du bit : `32` |
|  | Fichier avec espace colorimétrique Lab. | Utilisez exiftool si le mode colorimétrique est Lab.<br>Exemple dans un journal ExifTool:<br>1. Mode Couleur : `Lab` |
| TIFF | Fichiers contenant des données à virgule flottante. En d’autres termes, un fichier TIFF avec une profondeur de 32 bits n’est pas pris en charge. | Utilisez ExifTool si le type MIME est `image/tiff` et que SampleFormat a `Float` sa valeur. Exemple dans un journal ExifTool:<br>1. Type MIME : Format `image/tiff`<br>d’exemple : `Float #`<br>2. Type MIME : Format `image/tiff`<br>d’exemple : `Float; Float; Float; Float` |
|  | Fichiers dotés d’un espace colorimétrique Lab. | Utilisez ExifTool si le mode colorimétrique est Lab.<br>Exemple dans un journal ExifTool:<br>1. Mode Couleur : `Lab` |

## Bibliothèque PDF Rasterizer prise en charge {#supported-pdf-rasterizer-library}

La bibliothèque Adobe PDF Rasterizer génère des miniatures de haute qualité et des aperçus pour les fichiers Adobe Illustrator et PDF de grande taille et riches en contenu. Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Fichiers AI/PDF gourmands en contenu qui nécessitent beaucoup de ressources pour être traités.
* Fichiers AI/PDF pour lesquels les miniatures ne sont pas générées par défaut.
* Fichiers AI contenant des couleurs PMS (Pantone Matching System).

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## Supported Image Transcoding library {#supported-image-transcoding-library}

La bibliothèque Adobe Imaging Transcoding est une solution de traitement d’images qui exécute des fonctions essentielles de gestion des images, telles que le codage, le transcodage, le rééchantillonnage et le redimensionnement.

La bibliothèque de transcodage d’imagerie prend en charge les types MIME JPG/JPEG, PNG (8 et 16 bits), GIF, BMP, TIFF/TIFF compressé (sauf les fichiers TIFF 32 bits et les fichiers PTIFF), ICO et ICN.

See [Imaging Transcoding Library](imaging-transcoding-library.md).

## Supported camera raw {#supported-camera-raw}

La bibliothèque Adobe Camera Raw permet à AEM Assets d’importer des images brutes. Voir Prise en charge [de](camera-raw.md)Camera Raw.

## Formats de Ressources pris en charge {#supported-document-formats}

Les formats de  pris en charge pour les fonctionnalités de gestion des ressources sont les suivants :

| Format | Stockage | Metadata<br> management | Metadata<br> extraction | Thumbnail<br> generation | Interactive<br> editing | Metadata<br> writeback | [Statistiques](touch-ui-asset-insights.md) | [Ressources connectées](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## Formats de  pris en charge dans les médias dynamiques (#supported--formats-dynamic-media)

| Format | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

Outre les fonctionnalités ci-dessus, tenez compte des points suivants :

* Pour utiliser Dynamic Media de sorte à générer des rendus dynamiques pour des fichiers PDF, voir [ Adobe Illustrator (AI), Postscript (EPS) et formats de fichier PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Pour utiliser Dynamic Media de sorte à prévisualiser et générer des rendus dynamiques pour des fichiers AI, voir [Adobe Illustrator (AI), Postscript (EPS) et les formats de fichier PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* To use Dynamic Media to generate dynamic renditions for INDD files, see [InDesign (INDD) file format](../assets/managing-image-presets.md#indesign-indd-file-format).

## Formats multimédias pris en charge {#supported-multimedia-formats}

|  | Stockage | Gestion des métadonnées | Extraction de métadonnées | Génération de miniature | Transcodage FFMPEG |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | * |
| MIDI | ✓ | ✓ |  | − | * |
| 3GP | ✓ | ✓ |  | − | * |
| MP3 | ✓ | ✓ | ✓ | − | * |
| MPG | ✓ | ✓ |  | − | * |
| OGA | ✓ | ✓ |  | − | * |
| OGG | ✓ | ✓ |  | − | * |
| RA | ✓ | ✓ |  | − | * |
| WAV | ✓ | ✓ |  | − | * |
| WMA | ✓ | ✓ |  | − | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Supported input video formats in Dynamic Media for transcoding {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extension de fichier vidéo | Conteneur | Codecs vidéo recommandés | Codecs vidéo non pris en charge |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (tous les profils) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 et HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (fichiers d’animation vectorielle) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Red Raw Video | MJPEG 2000 |  |
| RAM, RM | RealVideo | Non pris en charge | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Native Flac | FLAC (Free Lossless Audio Codec) |  |
| MJ2 | Motion JPEG2000 | Codec Motion JPEG 2000 |  |

## Formats d’archives pris en charge {#supported-archive-formats}

Les formats d’archives pris en charge et l’applicabilité des flux de travail DAM courants sont traités dans le tableau suivant.

| Formats | Stockage | Création de versions | Workflow | Publication | Contrôle d’accès | Livraison Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Autres formats pris en charge {#other-supported-formats}

Le tableau ci-dessous décrit l’applicabilité des processus de gestion des actifs numériques courants pour d’autres formats de fichier. La fonctionnalité de gestion des actifs numériques habituelle, telle que  la gestion des , des versions, des listes de contrôle d’accès, des flux de travaux, de la publication et des métadonnées, à l’exception des de médias dynamiques, est prise en charge pour tous les fichiers.

| Formats | Stockage | Création de versions | Workflow | Publication | Contrôle d’accès | Livraison Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (lorsque configuré avec son propre domaine de diffusion) |  |  |  |  |  | ✓ |

## Pris en charge Types MIME {#supported-mime-types}

Par défaut, AEM détecte le type de fichier à l’aide de l’extension de fichier. AEM peut le détecter à partir du contenu des fichiers. For latter, select [!UICONTROL Detect MIME from content] option in [!UICONTROL Day CQ DAM Mime Type Service] in the AEM Web Console.

Un de types MIME pris en charge est disponible dans CRXDE Lite à `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

Voir [Configuration de MIME en fonction du type pour la prise en charge des paramètres de tâche de téléchargement](config-dynamic.md).

See also [Enabling MIME type-based Assets/Scene7 upload job parameter support](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

| Extension de fichier | Type MIME/type de support Internet | Valeur de jobParam par défaut | Valeur de jobParam autorisée |
|---|---|---|---|
| Image | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | La valeur de jobParam par défaut s’applique à toutes les ressources de type image MIME.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Activation de la prise en charge du paramètre de tâche de téléchargement Assets/Scene7 basé sur le type MIME](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

