---
title: Bonnes pratiques relatives au traitement des formats de fichiers pris en charge
description: Bonnes pratiques pour traiter les différents types de fichiers pris en charge à l’aide de  [!DNL Experience Manager Assets].
contentOwner: AG
role: Administrator
feature: Gestion des ressources,Outils de développement
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 46%

---

# Meilleures pratiques relatives au format de fichier des ressources {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] prend en charge de nombreuses bibliothèques de formats de fichiers propriétaires et tierces pour gérer les divers besoins des utilisateurs en matière de prise en charge des fichiers. Les bibliothèques d’Adobe prises en charge sont les suivantes : [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer et [!DNL Adobe InDesign Server]. En outre, [!DNL Experience Manager Assets] prend en charge les bibliothèques tierces, notamment [!DNL ImageMagick], [!DNL TwelveMonkeys], etc.

Pour les formats de fichiers pris en charge, voir [Formats pris en charge par AEM Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Si vous utilisez [!DNL Experience Manager] sur Adobe Managed Services (AMS), contactez l’assistance clientèle Adobe si vous prévoyez de traiter de nombreux fichiers PSD ou PSB volumineux. Collaborez avec le représentant de l’assistance clientèle d’Adobe afin de mettre en oeuvre ces bonnes pratiques pour votre déploiement AMS et de choisir les meilleurs outils et modèles possibles pour les formats propriétaires de l’Adobe. [!DNL Experience Manager] peut ne pas traiter des fichiers PSB à très haute résolution de plus de 3 000 x 2 3 000 pixels.

## [!DNL Adobe Camera Raw] bibliothèque  {#adobe-camera-raw-library}

Pour des performances optimales, Adobe recommande d’utiliser la bibliothèque [!DNL Adobe Camera Raw] pour les fichiers RAW et DNG.

[!DNL Adobe Camera Raw] prend en charge le profil colorimétrique CMJN en tant qu’entrée. Cependant, elle génère la sortie dans l’espace colorimétrique RVB et ne la prend en charge qu’au format JPEG. Elle ne conserve pas l’espace colorimétrique du fichier source (CMJN, par exemple) dans les miniatures.

Pour plus d’informations, voir [Prise en charge Camera Raw](/help/assets/camera-raw.md).

## Bibliothèque Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Pour des résultats optimaux, Adobe recommande d’utiliser la bibliothèque Adobe PDF Rasterizer pour les fichiers suivants :

* Fichiers PDF lourds ayant un contenu dense
* Fichiers AI avec des miniatures qui ne sont pas générées à l’avance
* Pour les fichiers AI avec des couleurs SPOT (PMS)

Les miniatures et les aperçus générés à l’aide de l’interpréteur de PDF sont de qualité supérieure par rapport à la sortie de trame prête à l’emploi. La bibliothèque Adobe PDF Rasterizer ne prend en charge aucune conversion d’espace colorimétrique. Indépendamment de l’espace colorimétrique du fichier PDF source, Adobe PDF Rasterizer génère uniquement une sortie RVB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe vous recommande d’utiliser [!DNL Adobe InDesign Server] pour extraire des rendus spécifiques à [!DNL Adobe InDesign], tels que IDML et HTML. Pour plus d’informations, voir [Ajout de ressources de Experience Manager comme références dans Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] génère et diffuse plusieurs variations de contenu riche en temps réel via son réseau mondial, extensible et optimisé pour garantir de bonnes performances. Il diffuse des expériences d’affichage interactif et simplifie le processus de gestion des campagnes numériques. Pour plus d’informations sur l’activation de [!DNL Dynamic Media], voir [Configuration de Dynamic Media](/help/assets/config-dynamic.md).

Actuellement, [!DNL Dynamic Media] peut prendre en charge les vidéos jusqu’à 15 Go de contenu par fichier.

## Bibliothèque ImageMagick {#imagemagick-library}

Adobe recommande d’utiliser la bibliothèque ImageMagick dans les cas suivants :

* Pour générer des rendus de miniatures pour les fichiers EPS.
* Pour conserver les informations sur les profils d’image.
* Pour conserver la transparence.
* Pour traiter des fichiers PSD et PSB.

Pour savoir comment configurer la bibliothèque [!DNL ImageMagick] dans [!DNL Experience Manager], voir [Utilisation d’ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Pour une utilisation optimale, voir [Bonnes pratiques pour configurer ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bibliothèque de transcodage d’imagerie (ITL) {#image-transcoding-library}

La bibliothèque ITL est une solution de traitement des images qui exécute des fonctions essentielles de gestion des images, notamment le codage, le transcodage, le rééchantillonnage, le redimensionnement des images, etc.

La bibliothèque de transcodage d’imagerie (ITL) prend en charge les types MIME suivants :

* JPG/JPEG
* PNG (8 et 16 bits)
* GIF
* BMP
* TIFF/TIFF compressé (hormis pour les images Tiff et PTiff 32 bits).
* ICO
* ICN

Pour plus d’informations, voir [Bibliothèque de transcodage d’imagerie](/help/assets/imaging-transcoding-library.md).
