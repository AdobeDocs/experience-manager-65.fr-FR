---
title: Publication de ressources sur Brand Portal
seo-title: Publication de ressources sur Brand Portal
description: Découvrez comment publier et annuler la publication de fichiers sur le portail des marques.
seo-description: Découvrez comment publier et annuler la publication de fichiers sur le portail des marques.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 4c00385984a0ac315a60c768cb517832ab4289b4
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 61%

---


# Publication de ressources sur Brand Portal {#publish-assets-to-brand-portal}

En tant qu’administrateur d’Adobe Experience Manager (AEM) Assets, vous pouvez publier des ressources et des dossiers sur l’instance AEM Assets Brand Portal (ou planifier le workflow de planification à une date/heure ultérieure) pour votre organisation. Cependant, vous devez d’abord configurer AEM Assets avec Brand Portal. Pour plus de détails, voir [Configuration d’AEM Assets avec Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Une fois la réplication réussie, vous pouvez publier des ressources, des dossiers et des collections sur Brand Portal. Pour publier des ressources sur Brand Portal, procédez comme suit :

>[!NOTE]
>
>Adobe recommande la publication décalée, de préférence en dehors des heures de pointe, de sorte que l’auteur AEM n’utilise pas une quantité excessive de ressources.

1. From the Assets console, select the assets/folder that you want to publish and click **[!UICONTROL Quick Publish]** option from the toolbar.

   Vous pouvez également sélectionner les ressources que vous voulez publier sur Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Pour publier les fichiers sur le portail des marques, deux options sont disponibles :
   * [Publication immédiate des fichiers](#publish-to-bp-now)
   * [Publication ultérieure des ressources](#publish-to-bp-now)

## Publication immédiate des ressources {#publish-to-bp-now}

Pour publier les ressources sélectionnées sur Brand Portal, effectuez l’une des opérations suivantes :

* Dans la barre d’outils, sélectionnez **[!UICONTROL Publication rapide]**. Then from the menu, select **[!UICONTROL Publish to Brand Portal]**.

* Dans la barre d’outils, sélectionnez **[!UICONTROL Gérer la publication]**.

   1. Then from the **[!UICONTROL Action]** select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]** select **[!UICONTROL Now]**. Cliquez sur **[!UICONTROL Suivant]**.

   2. Within **[!UICONTROL Scope]**, confirm your selection and click **[!UICONTROL Publish to Brand Portal]**.

Un message indique que les ressources ont été placées en file d’attente pour publication sur Brand Portal. Connectez-vous à l’interface Brand Portal pour voir les ressources publiées.

## Publication ultérieure des ressources {#publish-to-bp-later}

Pour planifier la publication des ressources sur Brand Portal à une date ou une heure ultérieure :

1. Once you have selected assets/ folders to publish, select **[!UICONTROL Manage Publication]** from the tool bar at the top.

1. On **[!UICONTROL Manage Publication]** page, select **[!UICONTROL Publish to Brand Portal]** from **[!UICONTROL Action]** and select **[!UICONTROL Later]** from **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Sélectionnez une **[!UICONTROL Date d’activation]** et spécifiez l’heure. Cliquez sur **[!UICONTROL Suivant]**.

1. Sélectionnez une **Date d’activation** et spécifiez l’heure. Cliquez sur **Suivant**.

1. Spécifiez un **[!UICONTROL Titre de workflow]** sous **[!UICONTROL Processus]**. Cliquez sur **[!UICONTROL Publier ultérieurement]**.

   ![publishworkflow](assets/publishworkflow.png)

Désormais, connectez-vous au portail Marques pour savoir si les fichiers publiés sont disponibles dans l’interface du portail Marque.

![bp_landing_page](assets/bp_landing_page.png)

