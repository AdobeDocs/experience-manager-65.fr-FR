---
title: Console Rapports
description: Découvrez comment utiliser différents rapports auxquels vous pouvez accéder de plusieurs manières à partir de l’environnement de création Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# Console Rapports {#reports-console}

## Vue d’ensemble {#overview}

Pour AEM Communities, plusieurs rapports sont accessibles de plusieurs manières à partir de l’environnement de création.

En général, les différents rapports sont :

* [Rapport Vues](#views-report)

  Fournit un tableau des vues du contenu par les membres de la communauté et les visiteurs du site pour n’importe quel site de la communauté.

* [Rapport Publications](#posts-report)

  Fournit un graphique des différents types de publications par membres de la communauté sur n’importe quel site de la communauté.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Consoles de création de rapports {#reporting-consoles}

### Rapports pour les sites de la communauté {#reports-for-community-sites}

* À partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Rapports]**

* Choisissez parmi :

   * **[!UICONTROL Rapport d’affectations]**

      * Générez un rapport pour le site, l’utilisateur ou le groupe de la communauté sélectionné et l’affectation.

   * **[!UICONTROL Rapport Publications]**

      * Générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.

   * **[!UICONTROL Rapport Vues]**

      * générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.

![reports](assets/reports1.png)

## Rapport des vues {#views-report}

La console Vues permet de générer des rapports sur les pages vues par les fonctionnalités de la communauté pendant une période donnée.

![view-report](assets/view-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

  Sélectionnez un site de la communauté.

* **[!UICONTROL Type de contenu]**

  Vous pouvez choisir l’option Tout contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

  Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L’année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![generate-views](assets/generate-views.png)

## Rapport des publications {#posts-report}

La console Publications permet de générer des rapports sur le nombre de publications aux fonctions de la communauté pour une période donnée.

![post-report](assets/posts-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

  Sélectionnez un site de la communauté.

* **[!UICONTROL Type de contenu]**

  Vous pouvez choisir l’option Tout contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

  Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L’année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![generate-report](assets/generate-posts-report.png)

## Résolution des problèmes {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de communauté n’est répertorié, vérifiez qu’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que les affectations fonctionnent dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans AEM instance d’auteur {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance d’auteur AEM, vérifiez les personnalisations, comme le mappage des URL sur l’instance Publish. Si le mappage des URL n’est effectué que sur l’instance Publish AEM du site Communities, assurez-vous que le même a été configuré dans l’instance AEM Author dans la configuration **Site Trend Report Social Component Factory** .

![Mappage d’URL sur AEM Auteur](assets/sitetrend.png)
