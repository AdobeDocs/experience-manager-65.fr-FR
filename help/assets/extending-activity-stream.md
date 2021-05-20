---
title: Intégrer [!DNL Assets] avec le flux d’activité
description: Décrit les fonctionnalités d’enregistrement de  [!DNL Experience Manager] et comment le configurer pour enregistrer des événements spécifiques.
contentOwner: AG
role: Developer
feature: Gestion des ressources
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 53%

---

# Intégrer [!DNL Assets] au flux d’activité {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] Les utilisateurs effectuent de nombreuses opérations, telles que la création, le chargement et la suppression d’actifs. Ces actions peuvent être enregistrées de manière à fournir un historique de toutes actions réalisées par un utilisateur. Cette section décrit les fonctionnalités d’enregistrement de [!DNL Experience Manager] et comment configurer [!DNL Experience Manager] afin d’enregistrer des événements spécifiques.

## Considérations de performance et comportement par défaut {#performance-considerations-and-default-behavior}

Cette intégration peut solliciter une puissance de processeur et un espace disque conséquents, par exemple lors d’opérations d’importation en bloc. Pour ces raisons, l’intégration de [!DNL Assets] au flux d’activités est désactivée par défaut.

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

## Configurer [!DNL Assets] l’enregistrement des événements {#configuring-aem-assets-events-recording}

La [console web](/help/sites-deploying/configuring-osgi.md) permet d’accéder au réglage de l’enregistreur d’événements de ressources. Pour configurer l’enregistreur d’événements de ressources, procédez comme suit :

1. Accédez à la **[!UICONTROL console web]**

1. Cliquez sur **[!UICONTROL Configuration]**.

1. Double-cliquez sur **[!UICONTROL Enregistreur d’événements de la gestion des actifs numériques Day CQ]**. 

1. Cochez **[!UICONTROL Activer ce service]**.

1. Vérifiez les **[!UICONTROL types d’événement]** que vous souhaitez enregistrer dans le flux d’activités de l’utilisateur. 

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Lire les événements enregistrés {#reading-recorded-events}

Les événements enregistrés sont stockés en tant qu’activités. Vous pouvez les lire par programmation à l’aide de l’[API ActivityManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
