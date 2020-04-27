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
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Console Rapports{#reports-console} 

## Présentation {#overview}

Pour les communautés AEM, plusieurs rapports peuvent être accessibles de plusieurs manières à partir de l’auteur   de l’.

En général, les différents rapports sont les suivants :

* [Rapport des affectations](#assignments-report)

   Dans le cas d’une communauté [d’](/help/communities/overview.md#enablement-community)activation, fournit un aperçu des progrès des apprenants sur leurs affectations, y compris un score associé lors de la mise en oeuvre de la norme SCORM.

* [Rapport des vues](#views-report)

   Fournit un tableau des  de contenu par les membres de la communauté et les du site pour tout site communautaire.

* [Rapport des publications](#posts-report)

   Fournit un tableau des différents types de publications par les membres de la communauté sur n’importe quel site de la communauté.

Lorsque [Adobe Analytics est activé](/help/communities/sites-console.md#analytics), les rapports incluent le nombre de , de lectures, de commentaires et d’évaluations pour chaque ressource d’activation au fil du temps.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Consoles {#reporting-consoles}

### Rapports pour les sites communautaires {#reports-for-community-sites}

* A partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Rapports]**

* Choisissez parmi :

   * **[!UICONTROL Rapport des affectations]**

      * Générez un rapport pour le site, l’utilisateur ou le groupe de la communauté sélectionné et l’affectation.
   * **[!UICONTROL Rapport des publications]**

      * Générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.
   * **[!UICONTROL Rapport des vues]**

      * générez un rapport pour le site de la communauté, le type de contenu et la période sélectionnés.



![chlimage_1-236](assets/chlimage_1-236.png)

### Rapports sur les ressources d’activation et les chemins d’apprentissage {#reports-for-enablement-resources-and-learning-paths}

* A partir de la navigation globale : **[!UICONTROL Navigation]** > **[!UICONTROL Communautés]** > **[!UICONTROL Ressources]**

* Sélectionnez un site communautaire d&#39;activation existant :

   * Sélectionnez l’icône **Rapport** pour générer des rapports qui couvrent toutes les ressources d’activation.
   * Sélectionnez un chemin d’apprentissage d’activation.
   * Sélectionnez l&#39;icône **Rapport** pour laquelle générer des rapports pour :

      * Ressources d’activation incluses.
      * Les apprenants affectés au chemin d’apprentissage.

* Ces rapports fournissent :

   * Données de tableau, téléchargeables au format CSV :

      * Identification de l’apprenant
      * Leur statut
      * Affecté ou accessible via le catalogue
      * Nombre de commentaires
      * Note d&#39;étoiles donnée

Pour plus d&#39;informations, reportez-vous à la section [](/help/communities/resources.md#report) Rapports de la console Ressources.

## Rapport des affectations {#assignments-report}

La console Affectations permet de filtrer les rapports par site, utilisateurs ou groupes de la communauté d’activation et par affectation.

Le rapport fournit des informations sur les progrès accomplis ainsi que sur les commentaires ou les évaluations fournis.

![chlimage_1-237](assets/chlimage_1-237.png)

Sélectionnez les critères du rapport :

* **Site**

   Sélectionnez un site de la communauté d&#39;activation.

* **Utilisateur ou groupe**
   * Sélectionnez Utilisateur pour générer un rapport pour un seul stagiaire.
   * Sélectionnez Groupe pour générer un rapport pour un groupe d’apprenants.
   Le service tunnel accède aux membres et aux groupes de membres à partir du  de publication .

* **Affectation**

   Faites votre choix parmi les ressources d’activation affectées aux apprenants sélectionnés.

Sélectionnez **Générer** pour créer le rapport :

![chlimage_1-238](assets/chlimage_1-238.png)

## Rapport des vues {#views-report}

La console  permet de générer des rapports sur les de page  par fonction(s) de la communauté pendant une période donnée.

![chlimage_1-239](assets/chlimage_1-239.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site communautaire.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir Tout le contenu ou sélectionner l&#39;une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![chlimage_1-240](assets/chlimage_1-240.png)

## Rapport des publications {#posts-report}

La console Publications permet de générer des rapports sur le nombre de publications pour les fonctionnalités de la communauté pendant une période donnée.

![chlimage_1-241](assets/chlimage_1-241.png)

Sélectionnez les critères du rapport :

* **[!UICONTROL Site]**

   Sélectionnez un site communautaire.

* **[!UICONTROL Type de contenu]**

   Vous pouvez choisir Tout le contenu ou sélectionner l&#39;une des fonctionnalités présentes sur le site.

* **[!UICONTROL Période]**

   Sélectionnez l’une des options suivantes :

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **[!UICONTROL Générer]** pour créer le rapport.

![chlimage_1-242](assets/chlimage_1-242.png)

## Résolution des incidents {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de la communauté n’est répertorié, vérifiez qu’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que la fonction des affectations est dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans l’instance d’auteur AEM {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance Auteur AEM, vérifiez les personnalisations, comme le mappage des URL sur l’instance Publication. Si le mappage des URL est effectué uniquement sur l’instance de publication AEM du site des communautés, assurez-vous que la même opération a été configurée dans l’instance d’auteur AEM dans la configuration des composants sociaux en usine **des rapports de tendances** du site.

![Mappage d’URL sur AEM Author](assets/sitetrend.png)