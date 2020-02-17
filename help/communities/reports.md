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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Console Rapports{#reports-console} 

## Présentation {#overview}

Pour les communautés AEM, plusieurs rapports peuvent être accessibles de plusieurs manières à partir de l’environnement d’auteur.

En général, les différents rapports sont :

* [Rapport](#assignments-report) sur les affectations - pour une communauté [d’](/help/communities/overview.md#enablement-community)activation, fournit un aperçu des progrès des apprenants sur leurs affectations, y compris un score associé lors de la mise en oeuvre de la norme SCORM
* [Rapport](#views-report) Vues - fournit un graphique des vues du contenu par les membres de la communauté et les visiteurs du site pour tout site communautaire
* [Rapport](#posts-report) Publications - fournit un graphique des différents types de publications des membres de la communauté sur n’importe quel site de la communauté.

Lorsque [Adobe Analytics est activé](/help/communities/sites-console.md#analytics), les rapports incluent le nombre de vues, de lectures, de commentaires et d’évaluations pour chaque ressource d’activation au fil du temps.

Les rapports tabulaires peuvent être exportés au format .csv pour un traitement ultérieur.

## Console de création de rapports {#reporting-consoles}

### Rapports pour les sites communautaires {#reports-for-community-sites}

* de la navigation globale : **Navigation**, **Communautés, Rapports**

* choisir

   * **Rapport des affectations**

      * générer un rapport pour le site communautaire, l’utilisateur ou le groupe sélectionné et l’affectation

      * **Rapport des publications**

         * générer un rapport pour le site communautaire, le type de contenu et la période sélectionnés
      * **Rapport des vues**

         * générer un rapport pour le site communautaire, le type de contenu et la période sélectionnés


![chlimage_1-236](assets/chlimage_1-236.png)

### Rapports sur les ressources d’activation et les chemins d’apprentissage {#reports-for-enablement-resources-and-learning-paths}

* de la navigation globale : **Navigation**, **Communautés, Ressources**

* sélectionner un site de communauté d&#39;activation existant ;

   * sélectionner **L&#39;icône **Rapport pour générer des rapports qui couvrent toutes les ressources d&#39;activation
   * sélectionner un chemin d&#39;apprentissage d&#39;activation
   * sélectionnez **L’icône **Rapport pour générer des rapports pour

      * les ressources d&#39;activation incluses
      * les apprenants affectés au chemin d&#39;apprentissage

* ces rapports fournissent :

   * données tabulaires, téléchargeables au format CSV

      * identification de l’apprenant
      * leur statut
      * attribué ou accessible via le catalogue
      * nombre de commentaires
      * note étoile donnée

Pour plus d&#39;informations, reportez-vous à la section [](/help/communities/resources.md#report) Rapports de la console Ressources.

## Rapport des affectations {#assignments-report}

La console Affectations permet de filtrer les rapports par site, utilisateurs ou groupes de la communauté d’activation et par affectation.

Le rapport fournit des informations sur les progrès accomplis ainsi que sur les commentaires ou les évaluations fournis.

![chlimage_1-237](assets/chlimage_1-237.png)

Sélectionnez les critères du rapport :

* **Site**

   sélectionner un site de la communauté d&#39;activation ;

* **Utilisateur ou groupe**
   * sélectionnez Utilisateur pour générer un rapport pour un seul stagiaire
   * sélectionnez Groupe pour générer un rapport pour un groupe d’apprenants.
   Le service tunnel accède aux membres et aux groupes de membres à partir de l’environnement de publication.

* **Affectation**

   Faites votre choix parmi les ressources d’activation affectées aux apprenants sélectionnés.

Sélectionnez **Générer** pour créer le rapport :

![chlimage_1-238](assets/chlimage_1-238.png)

## Rapport des vues {#views-report}

La console Affichages permet de générer des rapports sur les pages vues par fonction(s) de la communauté pendant une période donnée.

![chlimage_1-239](assets/chlimage_1-239.png)

Sélectionnez les critères du rapport :

* **Site**

   sélectionner un site communautaire ;

* **Type de contenu**

   peut choisir Tout le contenu ou sélectionner l’une des fonctionnalités présentes sur le site

* période

   sélectionnez l’un des

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **Générer** pour créer le rapport :

![chlimage_1-240](assets/chlimage_1-240.png)

## Rapport des publications {#posts-report}

La console Publications permet de générer des rapports sur le nombre de publications pour les fonctionnalités de la communauté pendant une période donnée.

![chlimage_1-241](assets/chlimage_1-241.png)

Sélectionnez les critères du rapport :

* **Site**

   sélectionner un site communautaire ;

* **Type de contenu**

   peut choisir Tout le contenu ou sélectionner l’une des fonctionnalités présentes sur le site

* période

   sélectionnez l’un des

   * 7 derniers jours
   * 30 derniers jours
   * 90 derniers jours
   * L&#39;année dernière

Sélectionnez **Générer** pour créer le rapport :

![chlimage_1-242](assets/chlimage_1-242.png)

## Résolution des incidents {#troubleshooting}

### Aucun site de communauté répertorié {#no-community-sites-listed}

Si aucun site de la communauté n’est répertorié, vérifiez qu’Adobe Analytics a été activé pour un site. Si vous choisissez des rapports sur les affectations, assurez-vous que la fonction des affectations est dans la structure du site de la communauté.

### Les rapports ne s’affichent pas dans l’instance Auteur AEM {#reports-do-not-show-in-aem-author-instance}

Si les rapports ne s’affichent pas dans l’instance Auteur AEM, vérifiez les personnalisations, comme le mappage des URL sur l’instance Publication. Si le mappage des URL est effectué uniquement sur l’instance de publication AEM du site des communautés, assurez-vous que la même opération a été configurée dans l’instance d’auteur AEM dans **Rapport de tendances du site Fabrique de composants sociaux **configuration.

![Mappage d’URL sur AEM Author](assets/sitetrend.png)