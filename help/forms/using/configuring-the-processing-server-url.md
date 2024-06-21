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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 100%

---

# Configuration des paramètres AEM DS{#configuring-aem-ds-settings}

Cet article décrit comment configurer le **Service de paramètres AEM DS**. Ce paramètre peut être utilisé dans plusieurs scénarios, par exemple :

* Dans Correspondence Management

   * Pour configurer AEM Forms Workflow
   * Lors de l’utilisation du portail Formulaires pour l’enregistrement à distance des brouillons/envois

* Dans les formulaires adaptatifs, par exemple lorsqu’un formulaire adaptatif est envoyé à partir de l’instance de publication

Vous trouverez ci-dessous les étapes de configuration des **[!UICONTROL Paramètres AEM DS]** :

1. Ouvrez Configuration Manager sur l’instance de publication à l’aide de l’URL :\
   *https://localhost:port/system/console/configMgr*.

   ![Configuration de la console web AEM](assets/web_configuration_console_new.png)

1. Dans la fenêtre **[!UICONTROL Configuration de la console web Adobe Experience Manager]**, recherchez et cliquez sur l’option **[!UICONTROL Paramètres AEM DS]**.

   ![Paramètres DS](assets/ds_settings_new.png)

1. La fenêtre **[!UICONTROL Service Paramètres AEM DS]** affiche les paramètres de configuration communs pour les composants AEM DS.

   ![Service Paramètres DS](assets/ds_settings_service_new.png)

1. Ajoutez les informations suivantes dans les champs respectifs :

   **[!UICONTROL URL du serveur de traitement]** : le serveur de traitement est le serveur sur lequel les formulaires ou le workflow AEM doivent être déclenchés. Elle peut être identique à l’URL de l’instance de création AEM ou de l’autre URL du serveur (à savoir https://localhost:port/).

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
