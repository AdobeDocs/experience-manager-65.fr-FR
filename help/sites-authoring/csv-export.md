---
title: 'Exporter au format CSV  '
seo-title: 'Exporter au format CSV  '
description: Exportez les informations relatives à vos pages vers un fichier CSV situé sur votre système local
seo-description: Exportez les informations relatives à vos pages vers un fichier CSV situé sur votre système local
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 317093bce043ff2aaa5b5ceb8499f057fa9fa24b
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 86%

---


# Exporter au format CSV  {#export-to-csv}

L’option **Créer une exportation CSV** vous permet d’exporter les informations relatives à vos pages vers un fichier CSV situé sur votre système local.

* Le fichier téléchargé est nommé `export.csv`.
* Le contenu dépend des propriétés que vous sélectionnez.
* Vous pouvez définir le chemin, ainsi que la profondeur de l’exportation.

>[!NOTE]
>
>La fonction de téléchargement et la destination par défaut du navigateur sont utilisées.

L’assistant **Créer une exportation CSV** vous permet de sélectionner les éléments suivants :

* Propriétés à exporter
   * Métadonnées  
      * Nom
      * Modifié
      * Publié
      * Template
      * Workflow
   * Traduction
      * Traduit
   * Analyses
      * Pages vues
      * Visiteurs uniques
      * Temps sur la page
* Profondeur
   * Chemin d’accès parent
   * Enfants directs uniquement
   * Niveaux supplémentaires d’enfants
   * Niveaux

Vous pouvez ouvrir le fichier `export.csv` obtenu dans Excel (ou toute autre application compatible).

![etc-01](assets/etc-01.png)

L’option Créer un rapport **CSV** est disponible lorsque vous parcourez la console **Sites** (dans la vue de Liste) : il s’agit d’une option du menu déroulant **Créer** :

![etc-02](assets/etc-02.png)

Pour créer une exportation CSV :

1. Ouvrez la console **Sites**, puis, le cas échéant, accédez à l’emplacement requis.
1. Dans la barre d’outils, sélectionnez **Créer** puis **Rapport CSV** pour ouvrir l’assistant :

   ![etc-03](assets/etc-03.png)

1. Sélectionnez les propriétés requises à exporter.
1. Sélectionnez **Créer**.
