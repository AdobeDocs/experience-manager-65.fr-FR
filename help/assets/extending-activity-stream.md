---
title: Intégration [!DNL Assets] avec le flux d’activité.
description: Describes the recording capabilities of [!DNL Experience Manager] and how to configure it to record specific events.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 53%

---


# Intégration [!DNL Assets] du flux d’activité {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] les utilisateurs effectuent de nombreuses actions, telles que la création, le téléchargement et la suppression de fichiers. Ces actions peuvent être enregistrées de manière à fournir un historique de toutes actions réalisées par un utilisateur. This section describes the recording capabilities of [!DNL Experience Manager] and how to configure [!DNL Experience Manager] in order to record specific events.

## Performance considerations and default behavior {#performance-considerations-and-default-behavior}

Cette intégration peut solliciter une puissance de processeur et un espace disque conséquents, par exemple lors d’opérations d’importation en bloc. For these reasons the [!DNL Assets] integration with the Activity Stream is disabled by default.

## Supported action events {#supported-action-events}

Il est possible de configurer l’enregistrement des événements suivants : 

* Licence acceptée (ACCEPTED)
* Ressource créée (ASSET_CREATED)
* Ressource déplacée (ASSET_MOVED)
* Ressource supprimée (ASSET_REMOVED)
* Licence rejetée (REJECTED)
* Ressource téléchargée (DOWNLOADED)
* Version de la ressource (VERSIONED)
* Version de la ressource restaurée (RESTORED)
* Métadonnées de la ressource mises à jour (METADATA_UPDATED)
* Ressource publiée dans un système externe (PUBLISHED_EXTERNAL)
* Version originale de la ressource mise à jour (ORIGINAL_UPDATED)
* Rendu de la ressource mis à jour (RENDITION_UPDATED)
* Rendu de la ressource supprimé (RENDITION_REMOVED)
* Sous-ressource mise à jour (SUBASSET_UPDATED)
* Sous-ressource supprimée (SUBASSET_REMOVED)

## Configuration de l’enregistrement des [!DNL Assets] événements {#configuring-aem-assets-events-recording}

The [Web console](/help/sites-deploying/configuring-osgi.md) provides access to the Assets Event Recorder tuning. Pour configurer l’enregistreur de Événement des ressources, procédez comme suit :

1. Navigate to the **[!UICONTROL Web Console]**

1. Cliquez sur **[!UICONTROL Configuration]**.

1. Double-cliquez sur **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]**. 

1. Cochez **[!UICONTROL Activer ce service]**.

1. Vérifiez les **[!UICONTROL types d’événement]** que vous souhaitez enregistrer dans le flux d’activités de l’utilisateur. 

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Lire les événements enregistrés {#reading-recorded-events}

Les événements enregistrés sont stockés en tant qu’activités. You can read them programmatically using the [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
