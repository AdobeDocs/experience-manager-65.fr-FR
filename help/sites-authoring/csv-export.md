---
title: Exporter au format CSV
seo-title: Export to CSV
description: Exporter des informations sur vos pages dans un fichier CSV sur votre système local
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 83%

---

# Exporter au format CSV{#export-to-csv}

L’option **Créer une exportation CSV** vous permet d’exporter les informations relatives à vos pages vers un fichier CSV situé sur votre système local.

* Le fichier téléchargé est nommé `export.csv`.
* Le contenu dépend des propriétés que vous sélectionnez.
* Vous pouvez définir le chemin, ainsi que la profondeur de l’exportation.

>[!NOTE]
>
>La fonction de téléchargement et la destination par défaut du navigateur sont utilisées.

La variable **Créer une exportation CSV** vous permet de sélectionner :

* Propriétés à exporter
   * Métadonnées
      * Nom
      * Modifié
      * Publié
      * Modèle
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

La création **Rapport CSV** est disponible lors de la navigation dans la **Sites** console (en mode Liste) : il s’agit d’une option de la **Créer** menu déroulant :

![etc-02](assets/etc-02.png)

Pour créer une exportation CSV :

1. Ouvrez la console **Sites**, puis, le cas échéant, accédez à l’emplacement requis.
1. Dans la barre d’outils, sélectionnez **Créer** puis **Rapport CSV** pour ouvrir l’assistant :

   ![etc-03](assets/etc-03.png)

1. Sélectionnez les propriétés à exporter.
1. Sélectionnez **Créer**.
