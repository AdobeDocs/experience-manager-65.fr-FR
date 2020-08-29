---
title: Utilisation des points de départ
seo-title: Utilisation des points de départ
description: Travailler avec un processus AEM Forms défini dans Workbench depuis votre périphérique mobile.
seo-description: Travailler avec un processus AEM Forms défini dans Workbench depuis votre périphérique mobile.
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 81%

---


# Utilisation des points de départ{#working-with-startpoints}

Un point de départ appelle un processus créé dans Workbench. Il est associé à un formulaire qui appelle le processus lors de l’envoi du formulaire.

>[!NOTE]
>
>Les termes « points de départ », « processus de démarrage » et « formulaire » sont indifféremment utilisés pour désigner ce concept.

To initiate a process from the AEM Forms app, you need to have a startpoint of type **Workspace** in your process. En outre, vous devez sélectionner l’option **[!UICONTROL Visible dans Mobile Workspace]** pour le point de départ.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Démarrage d’un processus défini dans Workbench**

1. Pour afficher les points de départ disponibles dans l’application AEM Forms, accédez à l’écran [Accueil](../../forms/using/home-screen.md).
1. On the **[!UICONTROL Home]** screen, by default, the **[!UICONTROL All Forms]** list is displayed.

   Le point de départ est associé à un formulaire. Appuyez sur le formulaire associé au point de départ dans la liste pour l’ouvrir.

   Le formulaire associé au point de départ s’ouvre.

1. Saisissez les informations dans le **[!UICONTROL formulaire]** Point de départ.

   Vous pouvez ajouter des annotations à cette tâche à l’aide du bouton de la [pièce jointe](../../forms/using/add-attachments.md).

1. Une fois que vous avez remplir le formulaire, appuyez sur le bouton **[!UICONTROL Envoyer.]**

Si l’application est hors ligne, le formulaire et ses données sont enregistrés dans le dossier de boîte d’envoi.

Si l’application est en ligne, la tâche est synchronisée avec le serveur AEM Forms et assignée à l’utilisateur spécifié dans le processus.

Pour effectuer la tâche présente dans la liste des tâches, consultez la section [Ouverture d’une tâche](/help/forms/using/open-task.md).
