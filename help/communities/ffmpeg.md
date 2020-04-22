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
source-git-commit: bb523ecf97ea18d8e8d5afa238fdf9e95fa58ab4

---


# FFmpeg pour les communautés {#ffmpeg-for-communities}

## Présentation {#overview}

FFmpeg est une solution de conversion et de diffusion audio et vidéo en flux continu. Une fois installée, elle est utilisée pour le transcodage correct des ressources [](../../help/sites-authoring/default-components-foundation.md#video) vidéo ainsi que pour la fonctionnalité d’activation des communautés AEM.

Le fichier mpeg est utilisé dans le de l’auteur  pour obtenir des métadonnées pour les ressources d’activation téléchargées et générer une miniature à afficher lors de la liste de la ressource d’activation.

## Installation de FFmpeg {#installing-ffmpeg}

FFmpeg doit être installé sur le ou les serveurs hébergeant les instances d’ *auteur* AEM.

1. Go to [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Téléchargez la dernière version de FFmpeg pour votre  de  spécifique (Macintosh, Windows ou Linux).

   * Il est important de maintenir FFmpeg à jour en raison de vulnérabilités de sécurité dans les versions antérieures.

1. Installez FFmpeg en suivant les instructions du système d’exploitation.

1. Assurez-vous que l&#39;exécutable FFmpeg est défini dans le chemin d&#39;accès du système.

   Vous devez pouvoir exécuter FFmpeg à partir de n&#39;importe quel répertoire de votre système.

   * Par exemple, `ffmpeg -version`.

## Configuration du service de transcodage FFmpeg {#configure-ffmpeg-transcoding-service}

Par défaut, lorsque FFmpeg est installé, plusieurs rendus sont configurés (transcodages) conformément à la définition du flux de travail [!UICONTROL DAM Update Asset] .

Comme les transcodages consomment beaucoup d’UC, il est recommandé de modifier le  des rendus de . Dans la plupart des cas, le transcodage n’est pas nécessaire.

Pour modifier le flux de travail [!UICONTROL DAM Update Asset] et, dans cet exemple, désactiver le transcodage :

* Connectez-vous à l’instance d’auteur avec des privilèges d’administration.
* Dans la navigation globale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]**.
* Locate **[!UICONTROL DAM Update Asset]**.
* Cliquez sur  pour ouvrir le flux de travail en vue de le modifier dans l’interface utilisateur de Classic.

   Emplacement résultant : [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* -cliquez sur l’étape de transcodage **** FFmpeg pour accéder à la boîte de dialogue Propriétés de l’étape.
* Under the **[!UICONTROL Process]** tab:

   * **[!UICONTROL Arugments]**: Effacer toutes les entrées pour désactiver le transcodage Valeurs par défaut : `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Select **[!UICONTROL OK]** to close the `Step Properties` dialog.

* Select **[!UICONTROL Save]** to save the `DAM Update Asset` workflow.



