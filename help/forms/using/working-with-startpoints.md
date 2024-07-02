---
title: Utilisation des points de départ
description: Étapes à suivre pour utiliser un processus Adobe Experience Manager Forms de votre appareil mobile défini dans Workbench.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: dd8748cee7a4b3ba91795a51928bd8590c47ef27
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---


# Utilisation des points de départ{#working-with-startpoints}

Un point de départ appelle un processus créé dans Workbench. Il est associé à un formulaire qui appelle le processus lors de l’envoi du formulaire.

>[!NOTE]
>
>Les termes « points de départ », « processus de démarrage » et « formulaire » sont indifféremment utilisés pour désigner ce concept.

Pour lancer un processus à partir de l’application Adobe Experience Manager (AEM) Forms, vous devez disposer d’un point de départ de type **Espace de travail** dans votre processus. En outre, vous devez sélectionner l’option **[!UICONTROL Visible dans Mobile Workspace]** pour le point de départ.

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Pour démarrer un processus défini dans Workbench**

1. Pour afficher les points de départ disponibles dans l’application AEM Forms, accédez à [Écran d’accueil](../../forms/using/home-screen.md).
1. Sur l’écran d’**[!UICONTROL Accueil]**, la liste **[!UICONTROL Tous les formulaires]** s’affiche par défaut.

   Le point de départ est associé à un formulaire. Sélectionnez le formulaire associé au point de départ dans la liste pour l’ouvrir.

   Le formulaire associé au point de départ s’ouvre.

1. Saisissez les informations dans le **[!UICONTROL formulaire]** Point de départ.

   Vous pouvez ajouter des annotations à cette tâche à l’aide du bouton de la [pièce jointe](../../forms/using/add-attachments.md).

1. Une fois que vous avez rempli le formulaire, cliquez sur le bouton **[!UICONTROL Envoyer]**.

Si l’application est hors ligne, le formulaire et ses données sont enregistrés dans le dossier de boîte d’envoi.

Si l’application est en ligne, la tâche est synchronisée avec le serveur AEM Forms et affectée à l’utilisateur ou l’utilisatrice spécifié dans le processus.

Pour utiliser la tâche dans votre liste de tâches, voir [Ouvrir une tâche](/help/forms/using/open-task.md).
