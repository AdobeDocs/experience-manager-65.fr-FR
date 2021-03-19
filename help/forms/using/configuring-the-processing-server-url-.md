---
title: Configuration des paramètres AEM DS
seo-title: Configuration des paramètres AEM DS
description: Vous devez spécifier l’URL du serveur de traitement avant d’envoyer un formulaire.
seo-description: Vous devez spécifier l’URL du serveur de traitement avant d’envoyer un formulaire.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 61%

---


# Configuration des paramètres AEM DS{#configuring-aem-ds-settings}

Cet article explique comment configurer le **service de paramètres AEM DS**. Ce paramètre peut être utilisé dans plusieurs cas de figure, par exemple :

* Dans Correspondence Management

   * Pour configurer les processus AEM Forms
   * En utilisant le portail des formulaires pour enregistrer à distance un brouillon/un envoi

* Dans les formulaires adaptatifs pour les cas où le formulaire adaptatif est envoyé à partir d’une instance de publication

Voici les étapes pour configurer les **[!UICONTROL paramètres AEM DS]** :

1. Ouvrez Configuration Manager sur l’instance de publication à l’aide de l’URL :\
   *https://localhost:port/system/console/configMgr*.

   ![Configuration de la console Web AEM](assets/web_configuration_console_new.png)

1. Dans la fenêtre **[!UICONTROL Configuration de la console Web de Adobe Experience Manager]**, recherchez **[!UICONTROL AEM Paramètres DS]** et cliquez dessus.

   ![Paramètres DS](assets/ds_settings_new.png)

1. La fenêtre **[!UICONTROL Service Paramètres AEM DS]** affiche les paramètres de configuration communs pour les composants AEM DS.

   ![Service des paramètres DS](assets/ds_settings_service_new.png)

1. Ajoutez les informations suivantes dans les champs respectifs :

   **[!UICONTROL URL]** du serveur de traitement : Le serveur de traitement est le serveur sur lequel le flux de travail Forms ou AEM doit être déclenché. Il peut s’agir de l’URL de l’instance d’auteur AEM ou de l’autre URL de serveur (https://localhost:port/).

   **[!UICONTROL Nom]** d’utilisateur du serveur de traitement : Nom d’utilisateur de l’utilisateur de Workflow  [en fonction de l’URL du serveur utilisé]

   **[!UICONTROL Mot de passe du serveur de traitement]** : mot de passe de l’utilisateur du processus

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Lorsque vous utilisez des processus AEM ou des formulaires, vous devez configurer le service de paramètres DS avant tout envoi depuis le serveur de publication. Dans le cas contraire, l’envoi du formulaire échouera.


