---
title: FFmpeg pour les communautés
seo-title: FFmpeg pour les communautés
description: Comment installer et configurer FFmpeg pour les communautés
seo-description: Comment installer et configurer FFmpeg pour les communautés
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# FFmpeg pour les communautés {#ffmpeg-for-communities}

## Présentation {#overview}

FFmpeg est une solution pour la conversion et la diffusion audio et vidéo en flux continu et, lorsqu’elle est installée, elle est utilisée pour le transcodage correct des ressources [](../../help/sites-authoring/default-components-foundation.md#video) vidéo ainsi que pour la fonctionnalité d’activation des communautés AEM.

FFmpeg est utilisé dans l’environnement de création pour obtenir des métadonnées pour les ressources d’activation téléchargées et générer une miniature à afficher lors de la liste de la ressource d’activation.

## Installation de FFmpeg {#installing-ffmpeg}

FFmpeg doit être installé sur le ou les serveurs hébergeant les instances d’ *auteur* AEM.

1. Go to [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. Téléchargez la dernière version de FFmpeg pour votre environnement spécifique (Macintosh, Windows ou Linux)

   * il est important de maintenir FFmpeg à jour en raison de vulnérabilités de sécurité dans les versions antérieures

1. Installez FFmpeg en suivant les instructions du système d’exploitation.

1. Assurez-vous que l&#39;exécutable FFmpeg est défini dans le chemin d&#39;accès du système.

   Vous devez pouvoir exécuter FFmpeg à partir de n&#39;importe quel répertoire de votre système.

   * par exemple, `ffmpeg -version`

## Configuration du service de transcodage FFmpeg {#configure-ffmpeg-transcoding-service}

Par défaut, lorsque FFmpeg est installé, plusieurs rendus sont configurés (transcodages) conformément à la définition du flux de travaux de mise à jour des actifs de gestion des actifs numériques.

Comme les transcodages consomment beaucoup d’UC, il est recommandé de modifier la liste des rendus cible. Dans la plupart des cas, le transcodage n’est pas nécessaire.

Pour modifier le processus de mise à jour des actifs de gestion des actifs numériques et, dans cet exemple, désactiver le transcodage :

* Connectez-vous à l’instance d’auteur avec des privilèges d’administration
* A partir de la navigation globale : **[!UICONTROL Outils > Processus > Modèles]**
* Locate **[!UICONTROL DAM Update Asset]**
* Double-cliquez pour ouvrir le processus de modification dans l’interface utilisateur classique.

   Emplacement résultant : [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Cliquez deux fois sur l’étape de transcodage **** FFmpeg pour accéder à la boîte de dialogue Propriétés de l’étape.
* Under the **[!UICONTROL Process]** tab:

   * **[!UICONTROL Arugments]**: Effacer toutes les entrées pour désactiver le transcodage Valeurs par défaut : `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Select **[!UICONTROL OK]** to close the `Step Properties` dialog

* Select **[!UICONTROL Save]** to save the `DAM Update Asset` workflow

   (coin supérieur gauche)

