---
title: Console Rapports
seo-title: Reports Console
description: Découvrez comment accéder aux rapports
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# Console Rapports {#reports-console}

## Présentation {#overview}

Pour AEM Communities, plusieurs rapports sont accessibles de plusieurs manières à partir de l’environnement de création.

En général, les différents rapports sont les suivants :

* [Rapport des vues](#views-report)

   Fournit un tableau des vues du contenu par les membres de la communauté et les visiteurs du site pour n’importe quel site de la communauté.

* [Rapport des publications](#posts-report)

   Fournit un graphique des différents types de publications par membres de la communauté sur n’importe quel site de la communauté.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Consoles de création de rapports {#reporting-consoles}

### Rapports pour les sites de la communauté {#reports-for-community-sites}

* À partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** >  **[!UICONTROL Rapports]**

* Choisissez parmi :

   * **[!UICONTROL Rapport des affectations]**

      * Générez un rapport pour le site, l’utilisateur ou le groupe de la communauté sélectionné et l’affectation.
   * **[!UICONTROL Rapport des publications]**

      * Générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.
   * **[!UICONTROL Rapport des vues]**

      * générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.



![rapports](assets/reports1.png)

## Rapport des vues {#views-report}

La console Vues permet de générer des rapports sur les pages vues par fonction(s) de la communauté pendant une période donnée.

![view-report](assets/view-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site de la communauté.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir l’option Tout contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionner **[!UICONTROL Générer]** pour créer le rapport.

![generate-views](assets/generate-views.png)

## Rapport des publications {#posts-report}

La console Publications permet de générer des rapports sur le nombre de publications pour les fonctionnalités de la communauté pendant une période donnée.

![post-report](assets/posts-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site de la communauté.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir l’option Tout contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionner **[!UICONTROL Générer]** pour créer le rapport.

![generate-report](assets/generate-posts-report.png)

## Résolution des problèmes {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de communauté n’est répertorié, vérifiez qu’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que la fonction des affectations se trouve dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans l’instance AEM Author {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance d’auteur AEM, vérifiez les personnalisations, comme le mappage des URL sur l’instance de publication. Si le mappage des URL n’est effectué que sur l’instance AEM Publish du site des communautés, assurez-vous que la même opération a été configurée dans l’instance AEM Author dans **Rapport de tendances du site Fabrique de composants sociaux** configuration.

![Mappage des URL sur l’auteur AEM](assets/sitetrend.png)
