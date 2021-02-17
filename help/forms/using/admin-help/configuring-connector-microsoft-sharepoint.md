---
title: Configuration de Connector for Microsoft SharePoint
seo-title: Configuration de Connector for Microsoft SharePoint
description: Configurez le connecteur pour Microsoft SharePoint pour permettre la communication entre AEM forms et Microsoft SharePoint.
seo-description: Configurez le connecteur pour Microsoft SharePoint pour permettre la communication entre AEM forms et Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 63%

---


# Configuration de Connector for Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Le connecteur pour Microsoft SharePoint permet la communication entre AEM forms et Microsoft SharePoint. Pour plus d’informations, voir Connectors for ECM, dans le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_63).

1. Dans Administration Console, cliquez sur Services > Connector for Microsoft SharePoint.
1. Spécifiez les paramètres suivants pour votre serveur SharePoint :

   **Nom d’hôte SharePoint Server :** numéro de port du nom d’hôte de l’application Web sur le serveur SharePoint, au format  `[hostname]:'port'`.

   **Nom d’utilisateur :** compte d’utilisateur utilisé pour la connexion au serveur SharePoint.

   **Mot de passe :** mot de passe du compte utilisateur utilisé pour la connexion au serveur SharePoint.

   **Nom de domaine :** domaine où se trouve le serveur SharePoint.

1. Cliquez sur Enregistrer.

## Service de configuration Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Le service de configuration Microsoft SharePoint `(MSSharePointConfigService)` vous permet de spécifier les informations d’identification de l’utilisateur de formulaires AEM qui dispose d’autorisations d’emprunt d’identité. Pour plus d’informations sur les droits d’emprunt d’identité, consultez [Configuration du connecteur pour Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Suivez les étapes suivantes pour définir les paramètres de `MSSharePointConfigService` :

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Parcourez la liste des services et cliquez sur `MSSharePointConfigService`.
1. Spécifiez les paramètres suivants sur la page Configuration :

   * Nom d’utilisateur pour un utilisateur disposant de droits d’emprunt d’identité
   * Mot de passe pour le même utilisateur

1. Cliquez sur Enregistrer.

