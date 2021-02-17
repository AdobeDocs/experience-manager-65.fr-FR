---
title: Recommandations relatives au traitement des formats de fichier pris en charge
description: Recommandations relatives au traitement des différents types de fichiers pris en charge à l’aide de  [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 47%

---


# Meilleures pratiques relatives au format de fichier des ressources {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] prend en charge de nombreuses bibliothèques de formats de fichiers propriétaires et tierces pour gérer les divers besoins des utilisateurs en matière de prise en charge des fichiers. Les bibliothèques d&#39;Adobes prises en charge sont [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer et [!DNL Adobe InDesign Server]. En outre, [!DNL Experience Manager Assets] prend en charge les bibliothèques tierces, notamment [!DNL ImageMagick], [!DNL TwelveMonkeys], etc.

Pour les formats de fichiers pris en charge, voir [Formats pris en charge par AEM Assets](/help/assets/assets-formats.md).

>[!TIP]
>
>Si vous utilisez [!DNL Experience Manager] sur Adobe Managed Services (AMS), contactez le service à la clientèle d’Adobe si vous prévoyez de traiter de nombreux fichiers PSD ou PSB volumineux. Collaborez avec le service à la clientèle d’Adobe pour mettre en oeuvre ces meilleures pratiques pour votre déploiement AMS et choisir les meilleurs outils et modèles possibles pour les formats propriétaires des Adobes. [!DNL Experience Manager] peut ne pas traiter de fichiers PSB très haute résolution de plus de 3 000 x 2 3 000 pixels.

## [!DNL Adobe Camera Raw] bibliothèque  {#adobe-camera-raw-library}

Pour des performances optimales, l’Adobe recommande d’utiliser la bibliothèque [!DNL Adobe Camera Raw] pour les fichiers RAW et DNG.

[!DNL Adobe Camera Raw] prend en charge le profil de couleurs CMJN en tant qu’entrée. Cependant, elle génère la sortie dans l’espace colorimétrique RVB et ne la prend en charge qu’au format JPEG. Elle ne conserve pas l’espace colorimétrique du fichier source (CMJN, par exemple) dans les miniatures.

Pour plus d’informations, voir [Prise en charge Camera Raw](/help/assets/camera-raw.md).

## Bibliothèque Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Pour des résultats optimaux, Adobe recommande d’utiliser la bibliothèque Adobe PDF Rasterizer pour les fichiers suivants :

* Fichiers PDF lourds ayant un contenu dense
* Fichiers AI avec des miniatures qui ne sont pas générées à l’avance
* Pour les fichiers AI avec des couleurs SPOT (PMS)

Les miniatures et les aperçus générés à l’aide de l’interpréteur de PDF sont de qualité supérieure par rapport à la sortie de trame prête à l’emploi. La bibliothèque Adobe PDF Rasterizer ne prend en charge aucune conversion d’espace colorimétrique. Indépendamment de l’espace colorimétrique du fichier PDF source, Adobe PDF Rasterizer génère uniquement une sortie RVB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe vous recommande d’utiliser [!DNL Adobe InDesign Server] pour extraire des rendus spécifiques à [!DNL Adobe InDesign], tels que IDML et HTML. Pour plus d’informations, voir [Ajouter des ressources Experience Manager en tant que références dans Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

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

La bibliothèque de transcodage d’images d’Adobe est une solution de traitement d’images qui exécute des fonctions de gestion d’images de base, notamment le codage d’images, le transcodage, le ré-échantillonnage, le redimensionnement, etc.

La bibliothèque de transcodage d’imagerie (ITL) prend en charge les types MIME suivants :

* JPG/JPEG
* PNG (8 et 16 bits)
* GIF
* BMP
* TIFF/TIFF compressé (hormis pour les images Tiff et PTiff 32 bits).
* ICO
* ICN

Pour plus d’informations, voir [Bibliothèque de transcodage d’images](/help/assets/imaging-transcoding-library.md).
