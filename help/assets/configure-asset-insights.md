---
title: Configurez Asset Insights pour obtenir des analyses.
description: Configurez Asset Insights dans  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 35%

---


# Configuration des statistiques sur les ressources {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] récupère les données d’utilisation des ressources numériques utilisées par des sites Web tiers à partir de  [!DNL Adobe Analytics]. Pour permettre à la fonction Statistiques sur les ressources de récupérer ces données et de générer des informations, commencez par la configurer afin qu’elle s’intègre à Adobe Analytics.

>[!NOTE]
>
>Les statistiques sont uniquement prises en charge et fournies pour les images.

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Cliquez sur la carte **[!UICONTROL Configuration des statistiques]**.
1. Dans l’assistant, sélectionnez un centre de données et fournissez vos informations d’identification, notamment le nom de votre société, votre nom d’utilisateur et votre secret partagé.

   ![Configuration d’Adobe Analytics pour Assets Insights dans le Experience Manager](assets/insights_config2.png)

   *Figure : Configurez  [!DNL Adobe Analytics] pour Assets Insights dans  [!DNL Experience Manager].*

1. Cliquez sur **[!UICONTROL Authentifier]**.
1. Une fois que [!DNL Experience Manager] a authentifié vos informations d’identification, dans la liste **[!UICONTROL Report Suite]**, choisissez une suite de rapports [!DNL Adobe Analytics] à partir de laquelle vous souhaitez que Asset Insights récupère les données. Cliquez sur **[!UICONTROL Ajouter]**.
1. Une fois [!DNL Experience Manager] configuré votre suite de rapports, cliquez sur **[!UICONTROL Terminé]**.

## Suivi de page {#page-tracker}

Une fois votre compte [!DNL Adobe Analytics] configuré, le code de suivi de page est généré pour vous. Pour permettre à Assets Insights d’effectuer le suivi des [!DNL Experience Manager] fichiers utilisés dans les sites Web tiers, incluez le code de suivi de page dans le code du site Web. Utilisez l&#39;utilitaire [!UICONTROL Suivi de page] dans [!DNL Experience Manager Assets] pour générer le code du suivi de page. Pour plus d&#39;informations sur la manière d&#39;inclure votre code de suivi de page dans des pages Web tierces, voir [Utilisation du suivi de page et du code incorporé dans les pages Web](/help/assets/use-page-tracker.md).

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Sur la page **[!UICONTROL Navigation]**, cliquez sur la carte **[!UICONTROL Dispositif de suivi de la page de statistiques]**.
1. Cliquez sur **[!UICONTROL Télécharger]** pour télécharger le code de suivi de page.
