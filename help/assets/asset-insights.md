---
title: Assets Insights
description: Découvrez comment la fonction Assets Insights permet d’effectuer le suivi des évaluations des utilisateurs et des statistiques d’utilisation des images utilisées dans les sites Web tiers, les campagnes marketing et les solutions de création d’Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 89%

---

# Assets Insights {#asset-insights}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=fr) |
| AEM 6.5 | Cet article |

La fonction Assets Insights vous permet d’effectuer le suivi des évaluations des utilisateurs et des statistiques d’utilisation des images utilisées dans les sites Web tiers, les campagnes marketing et les solutions de création d’Adobe. Elle permet d’extraire les statistiques sur leurs performances et leur popularité.

[!DNL Assets] Insights capture les détails de l’activité des utilisateurs, comme le nombre de fois où une image est évaluée et a fait l’objet d’un clic, ainsi que le nombre d’impressions (nombre de fois où une image est chargée sur le site Web). Elle attribue des scores aux images en fonction de ces statistiques. Vous pouvez utiliser les scores et les statistiques de performances pour sélectionner les images populaires à inclure dans les catalogues, les campagnes marketing et ainsi de suite. Vous pouvez même formuler des stratégies de renouvellement de licence et d’archivage en fonction de ces statistiques.

Pour que la fonction [!DNL Assets] Insights puisse capturer les statistiques d’utilisation des images à partir d’un site Web, vous devez inclure le code intégré de l’image dans celui du site Web.

Pour permettre à Assets Insights d’afficher les statistiques d’utilisation des ressources, commencez par configurer la fonction afin qu’elle récupère les données de rapports d’Adobe Analytics. Pour plus d’informations, consultez [Configuration d’Assets Insights](/help/assets/configure-asset-insights.md). Pour utiliser cette fonctionnalité dans une installation on-premise, achetez le licence [!DNL Adobe Analytics] séparément. Les clients [!DNL Managed Services] reçoivent une licence [!DNL Analytics] groupée avec [!DNL Experience Manager]. Consultez [Description du produit Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insights n’est pris en charge et fourni que pour les images.

## Affichage des statistiques pour une image {#viewing-statistics-for-an-image}

Vous pouvez afficher les scores de statistiques sur les ressources à partir de la page des métadonnées.

1. Dans l’interface utilisateur d’[!DNL Assets], sélectionnez l’image, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.
1. Sur la page Propriétés, cliquez sur le **[!UICONTROL Insights]** .
1. Consultez les détails d’utilisation de la ressource dans l’onglet **[!UICONTROL Statistiques]**. La section **[!UICONTROL Score]** indique les scores totaux d’utilisation et de performances d’une ressource.

   Le score d’utilisation indique le nombre de fois que la ressource est utilisée dans diverses solutions.

   Le **[!UICONTROL Impressions]** score correspond au nombre de fois où la ressource est chargée sur le site web. Le nombre affiché sous **[!UICONTROL Clics]** correspond au nombre de clics sur la ressource.

1. Passez en revue la section **[!UICONTROL Statistiques d’utilisation]** pour savoir de quelles entités la ressource faisait partie et dans quelles solutions de création elle a récemment été utilisée. Plus l’utilisation est élevée, plus la ressource a de chances d’être populaire auprès des utilisateurs. Les données d’utilisation s’affichent sous les sections suivantes :

   * **Ressource** : nombre de fois où la ressource faisait partie d’une collection ou d’une ressource composite
   * **Web et mobile** : nombre de fois où la ressource faisait partie de sites web et d’applications
   * **Social** : nombre de fois où la ressource a été utilisée dans des solutions, comme Adobe Social et Adobe Campaign
   * **E-mail** : nombre de fois où la ressource a été utilisée dans des campagnes par e-mail

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Parce que la fonction Assets Insights récupère les données de solutions d’Adobe Analytics de manière périodique, la section Solutions peut ne pas afficher les données les plus récentes. La période pendant laquelle les données sont affichées dépend de la planification de l’opération de récupération que la fonction Statistiques sur les ressources exécute pour récupérer les données d’Analytics.

1. Pour afficher les statistiques de performances de l’actif sous forme graphique sur une période donnée, sélectionnez une période dans la section **[!UICONTROL Statistiques de performances]**. Les détails, y compris les clics et les impressions, sont affichés sous forme de lignes de tendance dans un graphique.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Contrairement à la section Solutions, la section Statistiques de performances affiche les données les plus récentes.

1. Pour obtenir le code intégré de la ressource que vous incluez sur les sites Web afin d’obtenir les données de performances, cliquez sur **[!UICONTROL Obtenir le code intégré]** au-dessous de la miniature de la ressource. Pour plus d’informations sur la manière d’inclure votre code intégré sur des pages Web tierces, reportez-vous à la section [Utilisation du dispositif de suivi de page et du code intégré sur les pages Web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Affichage des statistiques générales pour les images {#viewing-aggregate-statistics-for-images}

Vous pouvez afficher les scores de toutes les ressources d’un dossier simultanément à l’aide du **[!UICONTROL mode Statistiques]**.

1. Dans l’interface utilisateur d’[!DNL Assets], accédez au dossier contenant les ressources dont vous souhaitez consulter les statistiques.
1. Cliquez sur Mise en page dans la barre d’outils, puis sélectionnez **[!UICONTROL Mode Insights]**.
1. La page affiche les scores d’utilisation des ressources. Comparez les évaluations des différentes ressources et tirez-en des conclusions.

## Planification d’une tâche en arrière-plan {#scheduling-background-job}

La fonction Assets Insights extrait les données d’utilisation des ressources à partir de suites de rapports Adobe Analytics de manière périodique. Par défaut, la fonction Assets Insights exécute une tâche en arrière-plan toutes les 24 heures, à 2 heures du matin, pour récupérer les données. Cependant, vous pouvez modifier la fréquence et l’heure en configurant le service de **[!UICONTROL tâche de synchronisation de rapport de performances de ressource de gestion des ressources numériques Adobe CQ]** via la console Web.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
1. Ouvrez la configuration de service **[!UICONTROL Tâche de synchronisation des rapports sur les performances des ressources de la gestion des actifs numériques Adobe CQ]**.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Spécifiez la fréquence du planificateur et l’heure de début de la tâche dans l’expression du planificateur de propriété. Enregistrez les modifications.
