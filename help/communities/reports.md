---
title: 'Console Rapports '
seo-title: 'Console Rapports '
description: Découvrez comment accéder aux rapports
seo-description: Découvrez comment accéder aux rapports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Administrator
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 8%

---

# Console Rapports{#reports-console} 

## Présentation {#overview}

Pour AEM Communities, plusieurs rapports sont accessibles de plusieurs manières à partir de l’environnement de création.

En général, les différents rapports sont les suivants :

* [Rapport des affectations](#assignments-report)

   Pour une [communauté d’activation](/help/communities/overview.md#enablement-community), fournit un aperçu de l’avancement des apprenants sur leurs affectations, y compris un score associé lors de la mise en oeuvre de la norme SCORM.

* [Rapport des vues](#views-report)

   Fournit un tableau des vues du contenu par les membres de la communauté et les visiteurs du site pour n’importe quel site de la communauté.

* [Rapport des publications](#posts-report)

   Fournit un graphique des différents types de publications par membres de la communauté sur n’importe quel site de la communauté.

Lorsque [Adobe Analytics est activé](/help/communities/sites-console.md#analytics), les rapports comprennent le nombre de vues, lectures, commentaires et évaluations pour chaque ressource d’activation au fil du temps.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Consoles de création de rapports {#reporting-consoles}

### Rapports pour les sites communautaires {#reports-for-community-sites}

* À partir de la navigation globale : **[!UICONTROL Navigation]** **[!UICONTROL Communautés]** > **[!UICONTROL Rapports]**

* Choisissez parmi :

   * **[!UICONTROL Rapport des affectations]**

      * Générez un rapport pour le site, l’utilisateur ou le groupe de la communauté sélectionné et l’affectation.
   * **[!UICONTROL Rapport des publications]**

      * Générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.
   * **[!UICONTROL Rapport des vues]**

      * générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.



![rapports](assets/reports1.png)

### Rapports pour les ressources d’activation et les chemins d’apprentissage {#reports-for-enablement-resources-and-learning-paths}

* À partir de la navigation globale : **[!UICONTROL Navigation]** **[!UICONTROL Communautés]** > **[!UICONTROL Ressources]**

* Sélectionnez un site de la communauté d’activation existant :

   * Sélectionnez l’icône **Rapport** pour générer des rapports qui couvrent toutes les ressources d’activation.
   * Sélectionnez un chemin d’apprentissage d’activation.
   * Sélectionnez l’icône **Rapport** pour générer des rapports pour :

      * Ressources d’activation incluses.
      * Les apprenants affectés au chemin d’apprentissage.

* Ces rapports fournissent les éléments suivants :

   * Données de tableau, téléchargeables au format CSV :

      * Identification de l’apprenant
      * Leur statut
      * Attribué ou accessible par le biais du catalogue
      * Nombre de commentaires effectués
      * Note de l&#39;étoile donnée

Pour plus d’informations, voir [Section Rapports](/help/communities/resources.md#report) de la console Ressources.

## Rapport des affectations {#assignments-report}

La console Affectations permet de filtrer les rapports par site de communauté d’activation, utilisateurs ou groupes, et par affectation.

Le rapport fournit des informations sur leurs progrès ainsi que sur les commentaires ou évaluations fournis.

![assignment-report](assets/assignment-report.png)

Sélectionnez les critères du rapport :

* **Site**

   Sélectionnez un site de la communauté d’activation.

* **Utilisateur ou groupe**
   * Sélectionnez Utilisateur pour générer un rapport destiné à un apprenant.
   * Sélectionnez Groupe pour générer un rapport pour un groupe d’apprenants.

   Le service tunnel accède aux membres et aux groupes de membres à partir de l’environnement de publication.

* **Affectation**

   Faites votre choix parmi les ressources d’activation affectées aux apprenants sélectionnés.

Sélectionnez **Générer** pour créer le rapport :

![generate-report](assets/generate-assignment-report.png)

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

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

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

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![generate-report](assets/generate-posts-report.png)

## Résolution des problèmes {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de communauté n’est répertorié, vérifiez qu’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que la fonction des affectations se trouve dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans l’instance d’auteur AEM {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance d’auteur AEM, vérifiez les personnalisations, comme le mappage des URL sur l’instance de publication. Si le mappage des URL n’est effectué que sur l’instance AEM Publish du site Communities, assurez-vous que la même configuration a été configurée dans l’instance AEM Author dans la configuration **Composant Social du rapport de tendance du site** .

![Mappage des URL sur l’auteur AEM](assets/sitetrend.png)
