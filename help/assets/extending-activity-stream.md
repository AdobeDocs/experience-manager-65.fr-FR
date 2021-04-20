---
title: Intégrer [!DNL Assets] avec le flux d’activité
description: Décrit les capacités d'enregistrement de  [!DNL Experience Manager] et comment le configurer pour enregistrer des événements spécifiques.
contentOwner: AG
role: Developer
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 53%

---


# Intégrer [!DNL Assets] au flux d’activité {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] les utilisateurs effectuent de nombreuses actions, telles que la création, le téléchargement et la suppression de fichiers. Ces actions peuvent être enregistrées de manière à fournir un historique de toutes actions réalisées par un utilisateur. Cette section décrit les capacités d&#39;enregistrement de [!DNL Experience Manager] et comment configurer [!DNL Experience Manager] pour enregistrer des événements spécifiques.

## Performances et comportement par défaut {#performance-considerations-and-default-behavior}

Cette intégration peut solliciter une puissance de processeur et un espace disque conséquents, par exemple lors d’opérations d’importation en bloc. Pour ces raisons, l&#39;intégration de [!DNL Assets] au flux d&#39;Activité est désactivée par défaut.

## Événements d’action pris en charge {#supported-action-events}

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

## Configurer [!DNL Assets] l&#39;enregistrement des événements {#configuring-aem-assets-events-recording}

La [console Web](/help/sites-deploying/configuring-osgi.md) permet d&#39;accéder au réglage de l&#39;enregistreur du Événement des ressources. Pour configurer l’enregistreur de Événement des ressources, procédez comme suit :

1. Accédez à la **[!UICONTROL console Web]**

1. Cliquez sur **[!UICONTROL Configuration]**.

1. Double-cliquez sur **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]**. 

1. Cochez **[!UICONTROL Activer ce service]**.

1. Vérifiez les **[!UICONTROL types d’événement]** que vous souhaitez enregistrer dans le flux d’activités de l’utilisateur. 

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Lire les événements enregistrés {#reading-recorded-events}

Les événements enregistrés sont stockés en tant qu’activités. Vous pouvez les lire par programmation à l’aide de l’[API ActivityManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
