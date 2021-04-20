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
feature: Brand Portal
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 61%

---


# Publication de ressources sur Brand Portal {#publish-assets-to-brand-portal}

En tant qu’administrateur d’Adobe Experience Manager (AEM) Assets, vous pouvez publier des ressources et des dossiers sur l’instance AEM Assets Brand Portal (ou planifier le workflow de planification à une date/heure ultérieure) pour votre organisation. Cependant, vous devez d’abord configurer AEM Assets avec Brand Portal. Pour plus de détails, voir [Configuration d’AEM Assets avec Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Une fois la réplication réussie, vous pouvez publier des ressources, des dossiers et des collections sur Brand Portal. Pour publier des ressources sur Brand Portal, procédez comme suit :

>[!NOTE]
>
>Adobe recommande la publication décalée, de préférence en dehors des heures de pointe, de sorte que l’auteur AEM n’utilise pas une quantité excessive de ressources.

1. Dans la console Ressources, sélectionnez les ressources/le dossier à publier, puis cliquez sur **[!UICONTROL Publication rapide]** dans la barre d’outils.

   Vous pouvez également sélectionner les ressources que vous voulez publier sur Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Pour publier les fichiers sur le portail des marques, deux options sont disponibles :
   * [Publication immédiate des fichiers](#publish-to-bp-now)
   * [Publication ultérieure des ressources](#publish-to-bp-now)

## Publication immédiate des ressources {#publish-to-bp-now}

Pour publier les ressources sélectionnées sur Brand Portal, effectuez l’une des opérations suivantes :

* Dans la barre d’outils, sélectionnez **[!UICONTROL Publication rapide]**. Ensuite, dans le menu, sélectionnez **[!UICONTROL Publier sur le portail de marque]**.

* Dans la barre d’outils, sélectionnez **[!UICONTROL Gérer la publication]**.

   1. Ensuite, à partir de **[!UICONTROL Action]** sélectionnez **[!UICONTROL Publier sur le portail de la marque]**, et dans **[!UICONTROL Planification]** sélectionnez **[!UICONTROL Maintenant]**. Cliquez sur **[!UICONTROL Next]** (Suivant).

   2. Dans **[!UICONTROL Scope]**, confirmez votre sélection et cliquez sur **[!UICONTROL Publier sur le portail de la marque]**.

Un message indique que les ressources ont été placées en file d’attente pour publication sur Brand Portal. Connectez-vous à l’interface Brand Portal pour voir les ressources publiées.

## Publication ultérieure des ressources {#publish-to-bp-later}

Pour planifier la publication des ressources sur Brand Portal à une date ou une heure ultérieure :

1. Une fois que vous avez sélectionné les fichiers/dossiers à publier, sélectionnez **[!UICONTROL Gérer la publication]** dans la barre d’outils située en haut de l’écran.

1. Sur la **[!UICONTROL page Gérer la publication]**, sélectionnez **[!UICONTROL Publier sur le portail de la marque]** dans **[!UICONTROL Action]** et **[!UICONTROL Plus tard]** dans **[!UICONTROL Planification]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Sélectionnez une **[!UICONTROL Date d’activation]** et spécifiez l’heure. Cliquez sur **[!UICONTROL Suivant]**.

1. Sélectionnez une **Date d’activation** et spécifiez l’heure. Cliquez sur **Suivant**.

1. Spécifiez un **[!UICONTROL Titre de workflow]** sous **[!UICONTROL Processus]**. Cliquez sur **[!UICONTROL Publier ultérieurement]**.

   ![publishworkflow](assets/publishworkflow.png)

Désormais, connectez-vous au portail Marques pour savoir si les fichiers publiés sont disponibles dans l’interface du portail Marque.

![bp_landing_page](assets/bp_landing_page.png)

