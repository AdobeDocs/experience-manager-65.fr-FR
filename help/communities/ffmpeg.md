---
title: FFmpeg pour les communautés
seo-title: FFmpeg for Communities
description: Installation et configuration de FFmpeg pour Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# FFmpeg pour les communautés {#ffmpeg-for-communities}

## Présentation {#overview}

FFmpeg est une solution pour la conversion et la diffusion en continu d’audio et de vidéo. Lorsqu’elle est installée, elle est utilisée pour le transcodage correct de [ressources vidéo](../../help/sites-authoring/default-components-foundation.md#video).

## Installation de FFmpeg {#installing-ffmpeg}

FFmpeg doit être installé sur le ou les serveurs hébergeant l’AEM *author* instances.

1. Accédez à [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Téléchargez la dernière version de FFmpeg pour votre environnement spécifique (Macintosh, Windows ou Linux).

   * Il est important de maintenir FFmpeg à jour en raison de vulnérabilités de sécurité dans les anciennes versions.

1. Installez FFmpeg en suivant les instructions pour le système d’exploitation.

1. Assurez-vous que le fichier exécutable FFmpeg est défini dans le chemin d’accès de votre système.

   Vous devriez être en mesure d’exécuter FFmpeg à partir de n’importe quel répertoire de votre système.

   * Par exemple, `ffmpeg -version`.

## Configuration du service de transcodage FFmpeg {#configure-ffmpeg-transcoding-service}

Par défaut, lorsque FFmpeg est installé, plusieurs rendus sont configurés (transcodages) selon la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] définition de workflow.

Comme les transcodages consomment beaucoup d’unité centrale, il est recommandé de modifier la liste des rendus cibles. Dans la plupart des cas, le transcodage n’est pas nécessaire.

Pour modifier la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow, et dans cet exemple, pour désactiver le transcodage :

* Connectez-vous à l’instance d’auteur avec les droits d’administrateur.
* Dans la navigation globale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
* Localiser **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]**.
* Double-cliquez pour ouvrir le workflow à modifier dans l’interface utilisateur classique.

   Emplacement obtenu : [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Double-cliquez sur le **[!UICONTROL Transcodage FFmpeg]** pour accéder à la boîte de dialogue Propriétés des étapes .
* Sous , **[!UICONTROL Processus]** tab :

   * **[!UICONTROL Arugments]**: Effacer toutes les entrées pour désactiver le transcodage Valeurs par défaut : `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Sélectionner **[!UICONTROL OK]** pour fermer la `Step Properties` boîte de dialogue.

* Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer le `DAM Update Asset` workflow.
