---
title: Recommandations relatives au traitement des différents formats de fichier pris en charge à l’aide d’AEM Assets.
description: Recommandations relatives au traitement des différents types de fichiers pris en charge à l’aide d’AEM Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


# Meilleures pratiques relatives au format de fichier des ressources {#assets-file-format-best-practices}

AEM Assets prend en charge de nombreuses bibliothèques de formats de fichiers propriétaires et tierces pour gérer les divers besoins des utilisateurs en matière de prise en charge des fichiers. Les bibliothèques Adobe prises en charge comprennent Adobe Camera Raw, Gibson, Adobe PDF Rasterizer et Adobe InDesign Server. En outre, AEM Assets prend en charge les bibliothèques tierces, y compris ImageMagick, TwelveMonkeys, etc.

Pour les formats de fichiers pris en charge, voir [Formats pris en charge par AEM Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Si vous utilisez Experience Manager sur Adobe Managed Services (AMS), contactez l’assistance d’Adobe si vous prévoyez de traiter un grand nombre de fichiers PSD ou PSB volumineux. Contactez le représentant du service à la clientèle Adobe pour mettre en oeuvre ces bonnes pratiques pour votre déploiement AMS et choisir les meilleurs outils et modèles possibles pour les formats propriétaires d’Adobe. Experience Manager peut ne pas traiter les fichiers PSB haute résolution de plus de 3 000 x 2 3 000 pixels.

## Bibliothèque Adobe Camera Raw {#adobe-camera-raw-library}

Pour des performances optimales, Adobe recommande d’utiliser la bibliothèque Adobe Camera Raw pour les fichiers RAW et DNG.

La bibliothèque Adobe Camera Raw prend en charge les de couleurs CMJN  en entrée. Cependant, elle génère la sortie dans l’espace colorimétrique RVB et ne la prend en charge qu’au format JPEG. Elle ne conserve pas l’espace colorimétrique du fichier source (CMJN, par exemple) dans les miniatures.

Pour plus d’informations, voir Prise en charge [de](/help/assets/camera-raw.md)Camera Raw.

## Bibliothèque Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Pour des résultats optimaux, Adobe recommande d’utiliser la bibliothèque Adobe PDF Rasterizer pour les fichiers suivants :

* Fichiers PDF lourds ayant un contenu dense
* Fichiers AI avec des miniatures qui ne sont pas générées à l’avance
* Pour les fichiers AI avec des couleurs SPOT (PMS)

Les miniatures et les aperçus générés à l’aide de l’interpréteur de PDF sont de qualité supérieure par rapport à la sortie de trame prête à l’emploi. La bibliothèque Adobe PDF Rasterizer ne prend en charge aucune conversion de l’espace colorimétrique. Quel que soit l’espace colorimétrique du fichier PDF source, Adobe PDF Rasterizer génère uniquement une sortie RVB.

## Adobe InDesign Server {#adobe-indesign-server}

Adobe vous recommande d’utiliser Adobe InDesign Server pour extraire des rendus spécifiques à Adobe InDesign, tels que IDML et HTML. For more information, see [Adding AEM assets as references in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## Dynamic Media  {#dynamic-media}

Dynamic Media génère et diffuse plusieurs variations de contenu riche en temps réel via son réseau mondial, extensible et optimisé pour garantir de bonnes performances. Il diffuse des expériences d’affichage interactif et simplifie le processus de gestion des campagnes numériques. Pour en savoir plus sur l’activation de Dynamic Media, voir [Configuration de Dynamic Media](/help/assets/config-dynamic.md).

Actuellement, Dynamic Media peut prendre en charge jusqu’à 20 Go de contenu vidéo par fichier.

## Bibliothèque ImageMagick {#imagemagick-library}

Adobe recommande d’utiliser la bibliothèque ImageMagick dans les cas suivants :

* Pour générer des rendus de miniatures pour les fichiers EPS
* Pour conserver les informations sur les profils d’image
* Pour conserver la transparence
* Pour traiter des fichiers PSD et PSB

To know how to set up the ImageMagic library in AEM, see [Using ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Pour une utilisation optimale, voir [Bonnes pratiques pour configurer ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bibliothèque de transcodage d’imagerie (ITL) {#image-transcoding-library}

La bibliothèque de transcodage d’images d’Adobe est une solution de traitement d’images qui exécute des fonctions essentielles de gestion des images, notamment le codage d’images, le transcodage, le rééchantillonnage, le redimensionnement, etc.

La bibliothèque de transcodage d’imagerie (ITL) prend en charge les types MIME suivants :

* JPG/JPEG
* PNG (8 et 16 bits)
* GIF
* BMP
* TIFF/TIFF compressé (hormis pour les images Tiff et PTiff 32 bits).
* ICO
* ICN

For details, see [Imaging Transcoding Library](/help/assets/imaging-transcoding-library.md).
