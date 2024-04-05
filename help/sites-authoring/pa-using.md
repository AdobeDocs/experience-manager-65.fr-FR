---
title: Afficher des données d’analyse de page pour évaluer l’efficacité du contenu de la page
description: Utilisez les données d’analyse de page pour évaluer l’efficacité de leur contenu de page.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 100%

---

# Affichage des données d’analyse de page{#seeing-page-analytics-data}

Utilisez les données d’analyse de page pour évaluer l’efficacité du contenu de page.

## Analyse visible à partir de la console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Les données d’analyse de page s’affichent dans la [vue liste](/help/sites-authoring/basic-handling.md#list-view) de la console Sites. Lorsque les pages sont affichées au format liste, les colonnes suivantes sont disponibles par défaut :

* Pages vues
* Visiteurs uniques
* Temps sur la page

Chaque colonne indique une valeur pour la période de création de rapports actuelle et indique également si la valeur a augmenté ou diminué depuis la période de création de rapports précédente. Les données affichées sont mises à jour toutes les 12 heures.

>[!NOTE]
>
>Pour modifier la période de mise à jour, [configurez l’intervalle d’importation](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Ouvrez la console **Sites** (par exemple, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. À l’extrême droite de la barre d’outils (dans le coin supérieur droit), cliquez sur l’icône pour sélectionner **Vue Liste** (l’icône affichée dépend de la [vue actuelle](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. À l’extrémité droite de la barre d’outils (coin supérieur droit), cliquez à nouveau sur l’icône, puis sélectionnez **Paramètres d’affichage**. La boîte de dialogue **Configurer les colonnes** s’ouvre. Apportez les modifications requises et confirmez-les avec la commande **Mettre à jour**.

   ![aa-04](assets/aa-04.png)

### Sélectionner la période de création de rapports {#selecting-the-reporting-period}

Sélectionnez la période de création de rapports pour laquelle les données Analytics apparaissent sur la console Sites :

* Données des 30 derniers jours
* Données des 90 derniers jours
* Données de cette année

La période de création de rapports actuelle apparaît sur la barre d’outils de la console Sites (à droite dans la barre d’outils supérieure). Utilisez le menu déroulant pour sélectionner la période de création de rapports requise.
![aa-05](assets/aa-05.png)

### Configurer les colonnes de données disponibles {#configuring-available-data-columns}

Les membres du groupe d’utilisateurs et d’utilisatrices d’administration d’Analytics peuvent configurer la console Sites pour permettre aux auteurs et aux autrices d’afficher des colonnes Analytics supplémentaires.

>[!NOTE]
>
>Lorsqu’une arborescence de pages contient des enfants associés à différentes configurations d’Adobe Analytics Cloud, vous ne pouvez pas configurer les colonnes de données disponibles pour les pages.

1. Dans la vue Liste, utilisez les sélecteurs de vue (à droite de la barre d’outils), sélectionnez **Afficher les paramètres**, puis **Ajouter des données d’analyse personnalisées**.

   ![aa-15](assets/aa-15.png)

1. Sélectionnez les mesures à présenter aux auteurs dans la console Sites, puis cliquez sur **Ajouter**.

   Les colonnes affichées sont obtenues à partir d’Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Ouverture de Content Insights à partir de la console Sites {#opening-content-insights-from-sites}

Ouvrez [Content Insight](/help/sites-authoring/content-insights.md) à partir de la console Sites pour continuer à évaluer en détail l’efficacité des pages.

1. Dans la console Sites, sélectionnez la page pour laquelle vous souhaitez afficher des Insights sur le contenu.
1. Dans la barre d’outils, cliquez sur l’icône Analytics et Recommendations.

   ![Icône Analytics et Recommendations](do-not-localize/chlimage_1-16a.png)

## Analytics visible dans l’éditeur de page (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>S’affiche si [Activity Map a été configuré](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) pour votre site Web.

>[!NOTE]
>
>Les données de l’Activity Map proviennent d’Adobe Analytics.

Si votre site web a été [configuré pour Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), vous pouvez utiliser le [mode Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) pour afficher les données pertinentes. Par exemple :

![aa-07](assets/aa-07.png)

### Accès à l’Activity Map {#accessing-the-activity-map}

Après avoir sélectionné le mode [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes), vous devrez saisir vos données d’identification Adobe Analytics.

![aa-03](assets/aa-03.png)

La barre d’outils flottante **Analytics** s’affiche et permet les actions suivantes :

* Modification du format de la barre d’outils à l’aide des deux flèches (**>>**)
* Activation ou désactivation des détails de la page (icône représentant un œil)
* Configuration des paramètres d’Activity Map (icône représentant un engrenage)
* Sélection des analyses à afficher (plusieurs sélecteurs de liste déroulante)
* Fermeture d’Activity Map et de la barre d’outils (x)

![aa-09](assets/aa-09.png)

### Sélectionner les analyses à afficher {#selecting-the-analytics-to-show}

Vous pouvez sélectionner les données analytiques à afficher ainsi que leur mode d’affichage, selon différents critères :

* **Standard**/**En direct**

* type d’événement
* Groupe d’utilisateurs
* **Bulles**/**Dégradé**/**Gagnants et perdants**/**Désactivé**

* période à afficher

![aa-13](assets/aa-13.png)

### Configurer l’Activity Map {#configuring-the-activity-map}

Utilisez l’icône **Afficher les paramètres** pour ouvrir la boîte de dialogue **Paramètres d’Activity Map**.

![aa-04-1](assets/aa-04-1.png)

La boîte de dialogue **Paramètres de l’Activity Map** propose plusieurs options, sur trois onglets :

![aa-06](assets/aa-06.png)

* Général

   * Suite de rapports
   * Nom de page
   * Langue
   * Recouvrements de libellés avec
   * Taille de police du libellé
   * Couleur de dégradé
   * Couleur de bulle
   * Couleur de dégradé basée sur
   * Transparence de dégradé

* Standard

   * Affichage (type et nombre de liens)
   * Masquer les recouvrements pour les liens qui n’ont reçu aucune visite

* En direct

   * Affichage en haut (gagnants ou perdants)
   * Exclure le % inférieur
   * Mise à jour automatique (données et période)
