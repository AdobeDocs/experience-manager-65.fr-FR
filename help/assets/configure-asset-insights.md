---
title: Configurez Asset Insights pour obtenir des analyses.
description: Configurez les statistiques sur les ressources dans  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Statistiques sur les ressources, rapports sur les ressources
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 47%

---

# Configuration des statistiques sur les ressources {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] récupère les données d’utilisation des ressources numériques utilisées par des sites web tiers à partir de [!DNL Adobe Analytics]. Pour permettre à la fonction Statistiques sur les ressources de récupérer ces données et de générer des informations, commencez par la configurer afin qu’elle s’intègre à [!DNL Adobe Analytics]. Pour utiliser cette fonctionnalité, achetez la licence [!DNL Adobe Analytics] séparément. Les clients sur [!DNL Managed Services] reçoivent la licence [!DNL Analytics] inclue avec [!DNL Experience Manager]. Voir [Description du produit Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Les statistiques sont uniquement prises en charge et fournies pour les images.

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Cliquez sur la carte **[!UICONTROL Configuration des statistiques]**.
1. Dans l’assistant, sélectionnez un centre de données et fournissez vos informations d’identification, notamment le nom de votre société, votre nom d’utilisateur et votre secret partagé.

   ![Configuration d’Adobe Analytics pour Assets Insights dans Experience Manager](assets/insights_config2.png)

   *Figure : Configurez  [!DNL Adobe Analytics] pour les statistiques sur les ressources dans  [!DNL Experience Manager].*

1. Cliquez sur **[!UICONTROL Authentifier]**.
1. Une fois que [!DNL Experience Manager] a authentifié vos identifiants, dans la liste **[!UICONTROL Suite de rapports]**, sélectionnez une suite de rapports à partir de laquelle la fonction Statistiques sur les ressources doit récupérer les données. [!DNL Adobe Analytics] Cliquez sur **[!UICONTROL Ajouter]**.
1. Une fois que [!DNL Experience Manager] a configuré votre suite de rapports, cliquez sur **[!UICONTROL Terminé]**.

## Suivi de page {#page-tracker}

Une fois votre compte [!DNL Adobe Analytics] configuré, le code de suivi de page est généré pour vous. Pour permettre à Assets Insights d’effectuer le suivi des [!DNL Experience Manager] ressources utilisées dans les sites web tiers, insérez le code de suivi de page dans le code du site web. Utilisez l’utilitaire [!UICONTROL Page Tracker] dans [!DNL Experience Manager Assets] pour générer le code de suivi de page. Pour plus d’informations sur la manière d’inclure le code de suivi de page dans les pages web tierces, voir [Utilisation du suivi de page et du code intégré dans les pages web](/help/assets/use-page-tracker.md).

1. Dans [!DNL Experience Manager], cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Ressources]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Sur la page **[!UICONTROL Navigation]**, cliquez sur la carte **[!UICONTROL Dispositif de suivi de la page de statistiques]**.
1. Cliquez sur **[!UICONTROL Télécharger]** pour télécharger le code de suivi de page.
