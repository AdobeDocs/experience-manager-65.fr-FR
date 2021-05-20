---
title: FFmpeg pour les communautés
seo-title: FFmpeg pour les communautés
description: Installation et configuration de FFmpeg pour Communities
seo-description: Installation et configuration de FFmpeg pour Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Administrator
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 1%

---

# FFmpeg pour Communities {#ffmpeg-for-communities}

## Présentation {#overview}

FFmpeg est une solution pour la conversion et la diffusion en continu d’audio et de vidéo. Lorsqu’elle est installée, elle est utilisée pour le transcodage correct des [ressources vidéo](../../help/sites-authoring/default-components-foundation.md#video) ainsi que pour la fonction d’activation des communautés AEM.

FFmpeg est utilisé dans l’environnement de création pour obtenir des métadonnées pour les ressources d’activation chargées, ainsi que pour générer une miniature à afficher lors de la mise en liste de la ressource d’activation.

## Installation de FFmpeg {#installing-ffmpeg}

FFmpeg doit être installé sur le ou les serveurs hébergeant la ou les instances *author* AEM.

1. Accédez à [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Téléchargez la dernière version de FFmpeg pour votre environnement spécifique (Macintosh, Windows ou Linux).

   * Il est important de maintenir FFmpeg à jour en raison de vulnérabilités de sécurité dans les anciennes versions.

1. Installez FFmpeg en suivant les instructions pour le système d’exploitation.

1. Assurez-vous que le fichier exécutable FFmpeg est défini dans le chemin d’accès de votre système.

   Vous devriez être en mesure d’exécuter FFmpeg à partir de n’importe quel répertoire de votre système.

   * Par exemple, `ffmpeg -version`.

## Configuration du service de transcodage FFmpeg {#configure-ffmpeg-transcoding-service}

Par défaut, lorsque FFmpeg est installé, plusieurs rendus sont configurés (transcodages) conformément à la définition de workflow [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] .

Comme les transcodages consomment beaucoup d’unité centrale, il est recommandé de modifier la liste des rendus cibles. Dans la plupart des cas, le transcodage n’est pas nécessaire.

Pour modifier le workflow [!UICONTROL Ressource de mise à jour de gestion des actifs numériques] et, dans cet exemple, désactiver le transcodage :

* Connectez-vous à l’instance d’auteur avec les droits d’administrateur.
* Dans la navigation globale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]**.
* Recherchez **[!UICONTROL Ressource de mise à jour de gestion des actifs numériques]**.
* Double-cliquez pour ouvrir le workflow à modifier dans l’interface utilisateur classique.

   Emplacement obtenu : [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Double-cliquez sur l’étape **[!UICONTROL Transcodage FFmpeg]** pour accéder à la boîte de dialogue Propriétés des étapes .
* Sous l’onglet **[!UICONTROL Processus]** :

   * **[!UICONTROL Arugments]** : Effacer toutes les entrées pour désactiver le transcodage Valeurs par défaut :  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Sélectionnez **[!UICONTROL OK]** pour fermer la boîte de dialogue `Step Properties`.

* Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le workflow `DAM Update Asset`.
