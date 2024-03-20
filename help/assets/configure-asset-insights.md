---
title: Configurez les Statistiques sur les ressources pour obtenir des analyses.
description: Configurez les Statistiques sur les ressources dans  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 91%

---

# Configuration des statistiques sur les ressources {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] récupère les données d’utilisation des ressources numériques utilisées par des sites web tiers à partir de [!DNL Adobe Analytics]. Pour permettre à la fonction Statistiques sur les ressources de récupérer ces données et de générer des informations, commencez par la configurer afin qu’elle s’intègre à [!DNL Adobe Analytics]. Pour utiliser cette fonctionnalité dans une installation on-premise, achetez la licence [!DNL Adobe Analytics] séparément. Les clients [!DNL Managed Services] reçoivent une licence [!DNL Analytics] groupée avec [!DNL Experience Manager]. Consultez [Description du produit Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insights n’est pris en charge et fourni que pour les images.

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Cliquez sur la carte **[!UICONTROL Configuration d’Insights]**.
1. Dans l’assistant, sélectionnez un centre de données et fournissez vos informations d’identification, notamment le nom de votre organisation, le nom d’utilisateur et le secret partagé.

   ![Configuration d’Adobe Analytics pour les Statistiques sur les ressources dans Experience Manager](assets/insights_config2.png)

   *Image : configuration d’[!DNL Adobe Analytics] pour les Statistiques sur les ressources dans [!DNL Experience Manager].*

1. Cliquez sur **[!UICONTROL Authentifier]**.
1. Une fois qu’[!DNL Experience Manager] a authentifié vos identifiants, dans la liste **[!UICONTROL Suite de rapports]**, sélectionnez une suite de rapports [!DNL Adobe Analytics] à partir de laquelle la fonction Statistiques sur les ressources doit récupérer les données. Cliquez sur **[!UICONTROL Ajouter]**.
1. Une fois qu’[!DNL Experience Manager] a configuré votre suite de rapports, appuyez sur **[!UICONTROL Terminé]**.

## Suivi de page {#page-tracker}

Une fois que vous avez configuré votre compte [!DNL Adobe Analytics], le code de suivi de page est généré pour vous. Pour permettre à la fonction Statistiques sur les ressources de surveiller les ressources [!DNL Experience Manager] utilisées sur les sites Web tiers, incluez le code de suivi de page dans le code du site Web. Utilisez l’utilitaire de [!UICONTROL suivi de page] dans [!DNL Experience Manager Assets] pour générer le code de suivi de page. Pour plus d’informations sur la manière d’inclure votre code de suivi de page sur des pages Web tierces, reportez-vous à la section [Utilisation du dispositif de suivi de page et du code intégré sur les pages Web](/help/assets/use-page-tracker.md).

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Sur la page **[!UICONTROL Navigation]**, cliquez sur la carte **[!UICONTROL Dispositif de suivi de la page d’informations]**.
1. Cliquez sur **[!UICONTROL Télécharger]** pour télécharger le code de suivi de page.
