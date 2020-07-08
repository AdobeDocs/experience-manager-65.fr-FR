---
title: Recommandations relatives au traitement des différents formats de fichier pris en charge à l’aide [!DNL Adobe Experience Manager Assets]de.
description: Meilleures pratiques pour traiter les différents types de fichiers pris en charge à l’aide [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 46%

---


# Meilleures pratiques relatives au format de fichier des ressources {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] prend en charge de nombreuses bibliothèques de formats de fichiers propriétaires et tierces pour gérer les divers besoins des utilisateurs en matière de prise en charge des fichiers. The supported Adobe libraries include, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer, and [!DNL Adobe InDesign Server]. In addition, [!DNL Experience Manager Assets] supports third-party libraries, including [!DNL ImageMagick], [!DNL TwelveMonkeys], and so on.

Pour les formats de fichiers pris en charge, voir [Formats pris en charge par AEM Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>If you are using [!DNL Experience Manager] on Adobe Managed Services (AMS), reach out to Adobe Customer Care if you plan to process lots of large PSD or PSB files. Collaborez avec le représentant du service à la clientèle Adobe pour mettre en oeuvre ces meilleures pratiques pour votre déploiement AMS et pour choisir les meilleurs outils et modèles possibles pour les formats propriétaires Adobe. [!DNL Experience Manager] peut ne pas traiter de fichiers PSB très haute résolution de plus de 3 000 x 2 3 000 pixels.

## [!DNL Adobe Camera Raw] bibliothèque {#adobe-camera-raw-library}

Pour des performances optimales, Adobe recommande d’utiliser [!DNL Adobe Camera Raw] la bibliothèque pour les fichiers RAW et DNG.

[!DNL Adobe Camera Raw] prend en charge le profil de couleurs CMJN en tant qu’entrée. Cependant, elle génère la sortie dans l’espace colorimétrique RVB et ne la prend en charge qu’au format JPEG. Elle ne conserve pas l’espace colorimétrique du fichier source (CMJN, par exemple) dans les miniatures.

Pour plus d’informations, voir Prise en charge [de](/help/assets/camera-raw.md)Camera Raw.

## Bibliothèque Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Pour des résultats optimaux, Adobe recommande d’utiliser la bibliothèque Adobe PDF Rasterizer pour les fichiers suivants :

* Fichiers PDF lourds ayant un contenu dense
* Fichiers AI avec des miniatures qui ne sont pas générées à l’avance
* Pour les fichiers AI avec des couleurs SPOT (PMS)

Les miniatures et les aperçus générés à l’aide de l’interpréteur de PDF sont de qualité supérieure par rapport à la sortie de trame prête à l’emploi. La bibliothèque Adobe PDF Rasterizer ne prend en charge aucune conversion d’espace colorimétrique. Indépendamment de l’espace colorimétrique du fichier PDF source, Adobe PDF Rasterizer génère uniquement une sortie RVB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe recommends that you use [!DNL Adobe InDesign Server] to extract [!DNL Adobe InDesign]-specific renditions, such as IDML and HTML. For more information, see [Adding Experience Manager assets as references in Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] génère et diffuse plusieurs variations de contenu riche en temps réel via son réseau mondial, extensible et optimisé pour garantir de bonnes performances. Il diffuse des expériences d’affichage interactif et simplifie le processus de gestion des campagnes numériques. For details around enabling [!DNL Dynamic Media], see [Configuring Dynamic Media](/help/assets/config-dynamic.md).

Currently, [!DNL Dynamic Media] can support videos up to 15 GB of content per file.

## Bibliothèque ImageMagick {#imagemagick-library}

Adobe recommande d’utiliser la bibliothèque ImageMagick dans les cas suivants :

* Pour générer des rendus de miniatures pour les fichiers EPS.
* Pour conserver les informations sur les profils d’image.
* Pour conserver la transparence.
* Pour traiter des fichiers PSD et PSB.

To know how to set up the [!DNL ImageMagick] library in [!DNL Experience Manager], see [Using ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Pour une utilisation optimale, voir [Bonnes pratiques pour configurer ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bibliothèque de transcodage d’imagerie (ITL) {#image-transcoding-library}

La bibliothèque de transcodage d’images Adobe est une solution de traitement d’images qui exécute des fonctions essentielles de gestion d’images, notamment le codage d’images, le transcodage, le rééchantillonnage, le redimensionnement, etc.

La bibliothèque de transcodage d’imagerie (ITL) prend en charge les types MIME suivants :

* JPG/JPEG
* PNG (8 et 16 bits)
* GIF
* BMP
* TIFF/TIFF compressé (hormis pour les images Tiff et PTiff 32 bits).
* ICO
* ICN

For details, see [Imaging Transcoding Library](/help/assets/imaging-transcoding-library.md).
