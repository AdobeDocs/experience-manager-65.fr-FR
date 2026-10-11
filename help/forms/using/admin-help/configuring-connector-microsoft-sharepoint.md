---
title: Configuration de Connector for Microsoft SharePoint
description: Configurez Connector for Microsoft SharePoint pour activer la communication entre AEM forms et Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 100%
---

# Configuration de Connector for Microsoft SharePoint

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Le connecteur pour Microsoft SharePoint permet la communication entre AEM Forms et Microsoft SharePoint. Pour plus d’informations, voir Connecteurs pour ECM, dans le [Guide de référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

1. Dans la console d’administration, cliquez sur Services > Connecteur pour Microsoft SharePoint.
2. Spécifiez les paramètres suivants pour votre serveur SharePoint :

   **Nom d’hôte du serveur SharePoint :** numéro de port du nom d’hôte de l’application web sur le serveur SharePoint, au format `[hostname]:'port'`.

   **Nom d’utilisateur** : compte d’utilisateur servant à la connexion au serveur SharePoint.

   **Mot de passe** : mot de passe du compte d’utilisateur servant à la connexion au serveur SharePoint.

   **Nom de domaine :** domaine où se trouve le serveur SharePoint.

3. Cliquez sur Enregistrer.

## Service de configuration Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Le service de configuration Microsoft SharePoint `(MSSharePointConfigService)` vous permet de spécifier les informations d’identification de l’utilisateur AEM Forms disposant des droits d’emprunt d’identité. Pour plus d’informations sur les droits d’emprunt d’identité, consultez [Configuration du connecteur pour Microsoft SharePoint](https://help.adobe.com/fr/AEMForms/6.1/SharePointConfig/index.html). Suivez les étapes suivantes pour définir les paramètres de `MSSharePointConfigService` :

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Parcourez la liste des services et cliquez sur `MSSharePointConfigService`.
1. Spécifiez les paramètres suivants sur la page Configuration :

   * Nom d’utilisateur ou d’utilisatrice pour un utilisateur ou une utilisatrice disposant de droits d’emprunt d’identité
   * Mot de passe pour ce même utilisateur ou cette même utilisatrice

1. Cliquez sur Enregistrer.
