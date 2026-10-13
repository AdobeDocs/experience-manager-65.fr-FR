---
title: Publier des ressources sur Brand Portal
description: Découvrez comment publier ou dépublier des ressources sur Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
subfeature_v2:
  - id: e00c7c12-7035-41fe-ad76-1ec82c8c3f01
    internal-label: Brand Portal
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%
---
# Publication de ressources sur Brand Portal {#publish-assets-to-brand-portal}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquer ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=fr) |
| AEM 6.5 | Cet article |

En tant qu’administrateur ou administratrice d’Adobe Experience Manager (AEM) Assets, vous pouvez publier des ressources et des dossiers sur l’instance AEM Assets Brand Portal (ou planifier le workflow de publication à une date/heure ultérieure) pour votre organisation. Cependant, vous devez d’abord configurer AEM Assets avec Brand Portal. Pour plus de détails, voir [Configuration d’AEM Assets avec Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Une fois la réplication réussie, vous pouvez publier des ressources, des dossiers et des collections sur Brand Portal. Pour publier des ressources sur Brand Portal, procédez comme suit :

>[!NOTE]
>
>Adobe recommande la publication décalée, de préférence en dehors des heures de pointe, de sorte que l’auteur AEM n’utilise pas une quantité excessive de ressources.

1. Dans la console Assets, sélectionnez les dossiers/ressources à publier, puis cliquez sur l’option **[!UICONTROL Publication rapide]** dans la barre d’outils.

   Vous pouvez également sélectionner les ressources que vous voulez publier sur Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Pour publier les ressources dans Brand Portal, deux options sont disponibles :
   * [Publication immédiate des ressources](#publish-to-bp-now)
   * [Publication immédiate des ressources](#publish-to-bp-now)

## Publication immédiate des ressources {#publish-to-bp-now}

Pour publier les ressources sélectionnées sur Brand Portal, effectuez l’une des opérations suivantes :

* Dans la barre d’outils, sélectionnez **[!UICONTROL Publication rapide]**. Ensuite, sélectionnez **[!UICONTROL Publier sur Brand Portal]** dans le menu.

* Dans la barre d’outils, sélectionnez **[!UICONTROL Gérer la publication]**.

  1. Ensuite, dans **[!UICONTROL Action]**, sélectionnez **[!UICONTROL Publier sur Brand Portal]** et dans **[!UICONTROL Planification]**, sélectionnez **[!UICONTROL Maintenant]**. Cliquez sur **[!UICONTROL Suivant]**.

  2. Dans **[!UICONTROL Portée]**, confirmez votre sélection et cliquez sur **[!UICONTROL Publier sur Brand Portal]**.

Un message indique que les ressources ont été placées en file d’attente pour publication sur Brand Portal. Connectez-vous à l’interface Brand Portal pour voir les ressources publiées.

## Publication ultérieure des ressources {#publish-to-bp-later}

Pour planifier la publication des ressources sur Brand Portal à une date ou une heure ultérieure :

1. Une fois que vous avez sélectionné les ressources/dossiers à publier, sélectionnez **[!UICONTROL Gérer la publication]** dans la barre d’outils supérieure.

1. Sur la page **[!UICONTROL Gérer la publication]**, sélectionnez **[!UICONTROL Publier sur Brand Portal]** dans **[!UICONTROL Action]** et sélectionnez **[!UICONTROL Plus tard]** à partir de **[!UICONTROL Planification]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Sélectionnez une **[!UICONTROL Date d’activation]** et spécifiez l’heure. Cliquez sur **[!UICONTROL Suivant]**.

1. Sélectionnez une **Date d’activation** et spécifiez l’heure. Cliquez sur **Suivant**.

1. Spécifiez un **[!UICONTROL Titre de workflow]** sous **[!UICONTROL Processus]**. Cliquez sur **[!UICONTROL Publier ultérieurement]**.

   ![publishworkflow](assets/publishworkflow.png)

Désormais, connectez-vous à Brand Portal pour voir si les ressources publiées sont disponibles dans l’interface de Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)

## Afficher le fichier ou le dossier publié dans Brand Portal {#view-published-file-folder}

1. Connectez-vous à l’interface Brand Portal pour afficher les ressources publiées (selon la date ou l’heure planifiée).

   ![bp_landingpage](assets/bp_landingpage.png)

1. Passez en mode Liste ![Mode Liste](assets/list-view.svg) pour afficher le statut de publication actuel de la ressource.

<!--2. On the [Asset Reports page](#https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/admin/asset-reports), you can see the current state of the report job, for example, Success, Failed, Queued, or Scheduled.-->

![Statut du rapport généré](assets/report-status.JPG)
