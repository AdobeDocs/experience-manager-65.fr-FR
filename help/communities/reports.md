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
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 8%

---


# Console Rapports{#reports-console} 

## Présentation {#overview}

Pour AEM Communities, divers rapports peuvent être consultés de plusieurs manières depuis l’environnement auteur.

En général, les différents rapports sont les suivants :

* [Rapport des affectations](#assignments-report)

   Pour une communauté [d’](/help/communities/overview.md#enablement-community)activation, fournit une vue d’ensemble des progrès des apprenants sur leurs tâches, y compris un score associé si la mise en oeuvre de la norme SCORM est mise en oeuvre.

* [Rapport des vues](#views-report)

   Fournit un tableau des vues de contenu par les membres de la communauté et les visiteurs du site pour tout site communautaire.

* [Rapport des publications](#posts-report)

   Fournit un graphique des différents types de publications par les membres de la communauté sur n’importe quel site de la communauté.

Lorsque [Adobe Analytics est activé](/help/communities/sites-console.md#analytics), les rapports incluent le nombre de vues, de lectures, de commentaires et d’évaluations pour chaque ressource d’activation au fil du temps.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Consoles de rapports {#reporting-consoles}

### Rapports pour les sites communautaires {#reports-for-community-sites}

* A partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Rapports]**

* Choisissez parmi :

   * **[!UICONTROL Rapport des affectations]**

      * Générez un rapport pour le site de la communauté, l’utilisateur ou le groupe sélectionné et l’affectation.
   * **[!UICONTROL Rapport des publications]**

      * Générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.
   * **[!UICONTROL Rapport des vues]**

      * générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.



![rapports](assets/reports1.png)

### Rapports sur les ressources d’activation et les chemins d’apprentissage {#reports-for-enablement-resources-and-learning-paths}

* A partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Ressources]**

* Sélectionnez un site communautaire d&#39;activation existant :

   * Sélectionnez l&#39;icône **Rapport** pour générer des rapports qui couvrent toutes les ressources d&#39;activation.
   * Sélectionnez un chemin d’apprentissage d’activation.
   * Sélectionnez l&#39;icône **Rapport** pour générer des rapports pour :

      * Les ressources d’activation incluses.
      * Les apprenants affectés au chemin d’apprentissage.

* Ces rapports fournissent :

   * Données de tableau, téléchargeables au format CSV :

      * Identification de l’apprenant
      * Leur statut
      * Affecté ou accessible via le catalogue
      * Nombre de commentaires formulés
      * Évaluation par étoiles donnée

Pour plus d&#39;informations, reportez-vous à la section [](/help/communities/resources.md#report) Rapports de la console Ressources.

## Rapport des affectations {#assignments-report}

La console Affectations permet de filtrer les rapports par site, utilisateurs ou groupes de la communauté d&#39;activation et par affectation.

Le rapport fournit des renseignements sur leurs progrès ainsi que sur les commentaires ou évaluations qui ont été fournis.

![rapport d&#39;affectation](assets/assignment-report.png)

Sélectionnez les critères du rapport :

* **Site**

   Sélectionnez un site de la communauté d&#39;activation.

* **Utilisateur ou groupe**
   * Sélectionnez Utilisateur pour générer un rapport pour un seul stagiaire.
   * Sélectionnez Groupe pour générer un rapport pour un groupe d’apprenants.

   Le service tunnel accède aux membres et aux groupes de membres à partir de l&#39;environnement de publication.

* **Affectation**

   Faites votre choix parmi les ressources d&#39;activation attribuées aux apprenants sélectionnés.

Sélectionnez **Générer** pour créer le rapport :

![generate-report](assets/generate-assignment-report.png)

## Rapport des vues {#views-report}

La console Vues permet de générer des rapports sur les vues de page par fonction(s) de la communauté pendant une période donnée.

![vue-rapport](assets/view-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site communautaire.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir tout le contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l&#39;une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![generate-vues](assets/generate-views.png)

## Rapport des publications {#posts-report}

La console Publications permet de générer des rapports sur le nombre de publications pour les fonctionnalités de la communauté pendant une période donnée.

![post-report](assets/posts-report.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site communautaire.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir tout le contenu ou sélectionner l’une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l&#39;une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![generate-report](assets/generate-posts-report.png)

## Résolution des incidents {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de la communauté n’est répertorié, vérifiez que l’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que la fonction des affectations est dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans l’instance Auteur AEM {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance Auteur AEM, recherchez les personnalisations, telles que le mappage des URL sur l’instance Publication. Si le mappage des URL est effectué uniquement sur l’instance de publication AEM du site des communautés, assurez-vous que la même instance a été configurée dans l’instance d’auteur AEM dans la configuration de l’usine **de composants sociaux du rapport de tendances du** site.

![Mappage d’URL sur l’auteur AEM](assets/sitetrend.png)