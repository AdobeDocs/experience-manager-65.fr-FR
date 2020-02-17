---
title: Intégration des ressources au flux d’activité
description: Décrit les fonctionnalités d’enregistrement d’AEM ainsi que la procédure de configuration d’AEM pour enregistrer des événements spécifiques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Integrate Assets with activity stream {#integrating-assets-with-activity-stream}

Les utilisateurs d’Adobe Experience Manager (AEM) Assets exécutent de nombreuses actions, telles que la création, le téléchargement et la suppression de ressources. Ces actions peuvent être enregistrées de manière à fournir un historique de toutes actions réalisées par un utilisateur. Cette section décrit les fonctionnalités d’enregistrement d’AEM ainsi que la procédure de configuration d’AEM pour enregistrer des événements spécifiques.

## Performance considerations and default behavior {#performance-considerations-and-default-behavior}

Cette intégration peut solliciter une puissance de processeur et un espace disque conséquents, par exemple lors d’opérations d’importation en bloc. C’est pourquoi l’intégration des ressources AEM au flux d’activités est désactivée par défaut.

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

## Configure AEM Assets events recording {#configuring-aem-assets-events-recording}

The [Web console](/help/sites-deploying/configuring-osgi.md) provides access to the AEM Assets Event Recorder tuning. Pour configurer l’enregistreur d’événements AEM Assets, procédez comme suit :

1. Navigate to the **[!UICONTROL Web Console]**

1. Cliquez sur **[!UICONTROL Configuration]**.

1. Double-cliquez sur **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]**. 

1. Cochez **[!UICONTROL Activer ce service]**.

1. Vérifiez les **[!UICONTROL types d’événement]** que vous souhaitez enregistrer dans le flux d’activités de l’utilisateur. 

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Evénements enregistrés en lecture {#reading-recorded-events}

Les événements enregistrés sont stockés en tant qu’activités. You can read them programmatically using the [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
