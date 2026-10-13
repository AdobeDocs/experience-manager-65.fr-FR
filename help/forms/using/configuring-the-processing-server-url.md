---
title: Configuration des paramètres AEM DS
description: Découvrez comment spécifier l’URL du serveur de traitement avant d’envoyer un formulaire.
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 88%
---
# Configuration des paramètres AEM DS{#configuring-aem-ds-settings}

Cet article décrit comment configurer le **Service de paramètres AEM DS**. Ce paramètre peut être utilisé dans plusieurs scénarios, par exemple :

* Dans Correspondence Management

  * Pour configurer AEM Forms Workflow
  * Lors de l’utilisation du portail Formulaires pour l’enregistrement à distance des brouillons/envois

* Dans les formulaires adaptatifs, par exemple lorsqu’un formulaire adaptatif est envoyé à partir de l’instance de publication

Vous trouverez ci-dessous les étapes de configuration des **[!UICONTROL Paramètres AEM DS]** :

1. Ouvrez Configuration Manager sur l’instance de publication à l’aide de l’URL :\
   *:port/system/console/configMgr*.

   ![Configuration de la console web AEM](assets/web_configuration_console_new.png)

1. Dans la fenêtre **[!UICONTROL Configuration de la console web Adobe Experience Manager]**, recherchez et cliquez sur l’option **[!UICONTROL Paramètres AEM DS]**.

   ![Paramètres DS](assets/ds_settings_new.png)

1. La fenêtre **[!UICONTROL Service Paramètres AEM DS]** affiche les paramètres de configuration communs pour les composants AEM DS.

   ![Service Paramètres DS](assets/ds_settings_service_new.png)

1. Ajoutez les informations suivantes dans les champs respectifs :

   **[!UICONTROL URL du serveur de traitement]** : le serveur de traitement est le serveur sur lequel les formulaires ou le workflow AEM doivent être déclenchés. Il peut s’agir de l’URL de l’instance d’auteur AEM ou de l’autre URL du serveur (c’est-à-dire https://localhost:port/).

   **[!UICONTROL Nom d’utilisateur du serveur de traitement]** : nom d’utilisateur de l’utilisateur du workflow [basé sur l’URL du serveur utilisé].

   **[!UICONTROL Mot de passe du serveur de traitement]** : mot de passe de l’utilisateur ou de l’utilisatrice du workflow

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Lors de l’utilisation de workflows Forms ou AEM, avant de soumettre un envoi à partir du serveur de publication, il est nécessaire de configurer le service de paramètres DS. Sinon, l’envoi du formulaire échouera.
   >    
   >
