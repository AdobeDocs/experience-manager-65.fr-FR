---
title: Configuration des statistiques sur les ressources
description: Configuration des informations sur les ressources dans les ressources AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Configuration des statistiques sur les ressources {#configure-asset-insights}

Adobe Experience Manager (AEM) Assets récupère les données d’utilisation des ressources AEM utilisées par les sites web tiers à partir d’Adobe Analytics. Pour permettre à la fonction Statistiques sur les ressources de récupérer ces données et de générer des informations, commencez par la configurer afin qu’elle s’intègre à Adobe Analytics.

>[!NOTE]
>
>Les statistiques sont uniquement prises en charge et fournies pour les images.

1. Dans AEM, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Cliquez sur la carte **[!UICONTROL Configuration des statistiques]**.
1. Dans l’assistant, sélectionnez un centre de données et fournissez vos informations d’identification, notamment le nom de votre société, votre nom d’utilisateur et votre secret partagé.

   ![Configuration d’Adobe Analytics pour les statistiques sur les ressources dans AEM](assets/insights_config2.png)

   *Figure : Configuration d’Adobe Analytics pour Assets Insights dans AEM*

1. Cliquez/appuyez sur **[!UICONTROL S’authentifier]**.
1. Une fois qu’AEM authentifie vos informations d’identification, dans la liste **[!UICONTROL Suite de rapports]**, sélectionnez une suite de rapports Adobe Analytics à partir de laquelle la fonction Statistiques sur les ressources doit récupérer les données. Cliquez sur **[!UICONTROL Ajouter]**.
1. Une fois qu’AEM configure votre suite de rapports, appuyez/cliquez sur **[!UICONTROL Terminé]**.

## Page tracker {#page-tracker}

Une fois votre compte Adobe Analytics configuré, le code de suivi de page est généré à votre place. Pour permettre à la fonction Statistiques sur les ressources de surveiller les ressources AEM utilisées sur les sites web tiers, incluez le code de suivi de page dans le code du site web. Utilisez l’utilitaire de suivi de page d’AEM Assets pour générer le code de suivi de page. For more information on how to include your Page Tracker code in third-party web pages, see [Use page tracker and embed code in web pages](/help/assets/touch-ui-using-page-tracker.md).

1. Dans AEM, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Dans la page **[!UICONTROL Navigation]**, cliquez sur la carte **[!UICONTROL Dispositif de suivi de la page de statistiques]**.
1. Click **[!UICONTROL Download]** to download the page tracker code.
