---
title: Affichage des données d’analyse de page
seo-title: Affichage des données d’analyse de page
description: Utilisez les données d’analyse de page pour mesurer l’efficacité de leur contenu de page
seo-description: Utilisez les données d’analyse de page pour mesurer l’efficacité de leur contenu de page
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 93%

---


# Affichage des données d’analyse de page{#seeing-page-analytics-data}

Utilisez les données d’analyse de page pour mesurer l’efficacité du contenu de page.

## Les données d’analyse sont visibles à partir de la console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Les données d’analyse de page s’affichent en [mode Liste](/help/sites-authoring/basic-handling.md#list-view) dans la console Sites. Lorsque les pages sont affichées sous forme de liste, les colonnes suivantes sont disponibles par défaut :

* Pages vues
* Visiteurs uniques
* Temps sur la page

Chaque colonne indique une valeur pour la période de création de rapports actuelle et indique également si la valeur a augmenté ou diminué depuis la période de création de rapports précédente. Les données affichées sont mises à jour toutes les 12 heures.

>[!NOTE]
>
>Pour modifier la période de mise à jour, [configurez l’intervalle d’importation](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Ouvrez la console **Sites** (par exemple, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. À l’extrême droite de la barre d’outils (dans le coin supérieur droit), appuyez ou cliquez sur l’icône pour sélectionner **Mode Liste** (l’icône affichée dépendra du [mode actuel](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. À nouveau à l’extrême droite de la barre d’outils (dans le coin supérieur droit), cliquez ou appuyez sur l’icône, puis sélectionnez **Paramètres**. La boîte de dialogue **Configurer les colonnes** s’ouvre. Apportez les modifications requises et confirmez-les avec la commande **Mettre à jour**.

   ![aa-04](assets/aa-04.png)

### Sélection de la période de création de rapports {#selecting-the-reporting-period}

Sélectionnez la période de création de rapports pour laquelle les données d’analyse s’affichent sur la console Sites :

* Données  Données
* Données des 90 derniers jours
* Données de cette année

La période de création de rapports actuelle apparaît sur la barre d’outils de la console Sites (à droite dans la barre d’outils supérieure). Utilisez le menu déroulant pour sélectionner la période de création de rapports requise. ![aa-05](assets/aa-05.png)

### Configuration des colonnes Données disponibles {#configuring-available-data-columns}

Les membres du groupe d’utilisateurs administrateurs d’analyse peuvent configurer la console Sites pour permettre aux auteurs de voir des colonnes Analyses supplémentaires.

>[!NOTE]
>
>Lorsqu’une arborescence de pages contient des enfants associés à différentes configurations de cloud d’Adobe Analytics, vous ne pouvez pas configurer les colonnes de données disponibles pour les pages.

1. Dans Liste Vue, utilisez les sélecteurs de vue (à droite de la barre d’outils), sélectionnez **Paramètres de Vue**, puis **Ajouter les données Analytics personnalisées**.

   ![aa-15](assets/aa-15.png)

1. Sélectionnez les mesures à présenter aux auteurs dans la console Sites, puis cliquez sur **Ajouter**.

   Les colonnes affichées sont obtenues à partir d’Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Ouverture de Content Insights à partir de la console Sites {#opening-content-insights-from-sites}

Ouvrez [Content Insight](/help/sites-authoring/content-insights.md) à partir de la console Sites pour en savoir plus sur l&#39;efficacité des pages.

1. Dans la console Sites, sélectionnez la page pour laquelle vous souhaitez voir Content Insight.
1. Sur la barre d’outils, cliquez sur l’icône Analyses et recommandations.

   ![](do-not-localize/chlimage_1-16a.png)

## Les données d’analyse sont visibles dans l’éditeur de page (carte d’activité)  {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Elles s&#39;affichent si la [carte d’activité a été configurée ](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map)pour votre site Web.

>[!NOTE]
>
>Les données de la carte d’activité proviennent d’Adobe Analytics.

Si votre site web a été [configuré pour Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), vous pouvez utiliser le [mode Activité](/help/sites-authoring/author-environment-tools.md#page-modes) de l’activité pour afficher les données pertinentes. Par exemple :

![aa-07](assets/aa-07.png)

### Accès à Activity Map {#accessing-the-activity-map}

Après avoir sélectionné le mode [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes), vous devrez saisir vos données d’identification Adobe Analytics.

![aa-03](assets/aa-03.png)

La barre d’outils flottante d’**Analytics** s’affiche et vous permet d’effectuer les opérations suivantes :

* Modification du format de la barre d’outils à l’aide des doubles flèches (**>>**)
* Activation/Désactivation des détails de la page (icône représentant un œil)
* Configuration des paramètres d’Activity Map (icône représentant un engrenage)
* Sélection des analyses à afficher (plusieurs sélecteurs de liste déroulante)
* Fermeture d’Activity Map et de la barre d’outils (x)

![aa-09](assets/aa-09.png)

### Sélection des analyses à afficher {#selecting-the-analytics-to-show}

Vous pouvez sélectionner les données analytiques à afficher et leur affichage, à l’aide des critères suivants :

* **Standard**/**En direct**

* Type d&#39;événement
* Groupe d&#39;utilisateurs
* **Bulles**/**Dégradé**/**Gagnants et perdants**/**Fermé**

* Période à afficher

![aa-13](assets/aa-13.png)

### Configuration d’Activity Map {#configuring-the-activity-map}

Utilisez l’icône **Afficher les paramètres** pour ouvrir la boîte de dialogue **Paramètres** d’Activity Map.

![aa-04-1](assets/aa-04-1.png)

La boîte de dialogue **Paramètres de l’Activity Map** propose plusieurs options, sur trois onglets :

![aa-06](assets/aa-06.png)

* Général

   * Suite de rapports
   * Nom de page
   * Langue
   * Étiqueter les superpositions avec
   * Taille de police de l’étiquette
   * Couleur du dégradé
   * Couleur de la bulle
   * Couleur du dégradé basée sur
   * Transparence du dégradé

* Standard

   * Afficher (type et nombre de liens)
   * Masquer les superpositions pour les liens qui n’ont reçu aucune visite

* En direct

   * Afficher en haut (Gagnants ou perdants)
   * Exclure le bas %
   * Mise à jour automatique (données et point)

