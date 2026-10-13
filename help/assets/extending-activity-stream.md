---
title: Intégration d’[!DNL Assets] avec flux d’activité
description: Décrit les fonctionnalités d’enregistrement de [!DNL Experience Manager] et comment les configurer pour enregistrer des événements spécifiques.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 88%
---
# Intégration d’[!DNL Assets] avec flux d’activité {#integrating-assets-with-activity-stream}

Les utilisateurs et utilisatrices [!DNL Adobe Experience Manager Assets] effectuent de nombreuses opérations, telles que la création, le chargement et la suppression de ressources. Ces actions peuvent être enregistrées de manière à fournir un historique de toutes les actions réalisées par un utilisateur ou une utilisatrice. Cette section décrit les fonctionnalités d’enregistrement d’[!DNL Experience Manager] ainsi que la procédure de configuration d’[!DNL Experience Manager] pour enregistrer des événements spécifiques.

## Considérations concernant les performances et comportement par défaut {#performance-considerations-and-default-behavior}

Cette intégration peut solliciter une puissance de processeur et un espace disque conséquents, par exemple lors d’opérations d’import en bloc. Pour ces raisons, l’intégration d’[!DNL Assets] au flux d’activités est désactivée par défaut.

## Événements d’actions pris en charge {#supported-action-events}

Vous pouvez configurer les événements suivants pour qu’ils soient enregistrés :

* Licence acceptée (ACCEPTED)
* Ressource créée (ASSET_CREATED)
* Ressource déplacée (ASSET_MOVED)
* Ressource supprimée (ASSET_REMOVED)
* Licence refusée (REJECTED)
* Ressource téléchargée (DOWNLOADED)
* Ressource versionnée (VERSIONED)
* Version de la ressource restaurée (RESTORED)
* Métadonnées de ressource mises à jour (METADATA_UPDATED)
* Ressource publiée sur un système externe (PUBLISHED_EXTERNAL)
* Originale de la ressource mis à jour (ORIGINAL_UPDATED)
* Rendu de la ressource mis à jour (RENDITION_UPDATED)
* Rendu de la ressource supprimé (RENDITION_REMOVED)
* Sous-ressource mise à jour (SUBASSET_UPDATED)
* Sous-ressource supprimée (SUBASSET_REMOVED)

## Configuration d’un enregistrement d’événements [!DNL Assets] {#configuring-aem-assets-events-recording}

La [console Web](/help/sites-deploying/configuring-osgi.md) permet d’accéder aux réglages de l’enregistreur d’événements d’Assets. Pour configurer l’enregistreur d’événements d’Assets, procédez comme suit :

1. Accédez à la **[!UICONTROL console Web]**.

1. Cliquez sur **[!UICONTROL Configuration]**.

1. Double-cliquez **[!UICONTROL Enregistreur d’événements DAM Day CQ]**.

1. Cochez **[!UICONTROL Activer ce service]**.

1. Vérifiez les **[!UICONTROL types d’événement]** que vous souhaitez enregistrer dans le flux d’activités de l’utilisateur ou l’utilisatrice.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

## Lecture d’événements enregistrés {#reading-recorded-events}

Les événements enregistrés sont stockés en tant qu’activités. Vous pouvez les consulter par programmation en utilisant [l’API ActivityManager](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
