---
title: Exporter au format CSV
description: Exporter des informations sur vos pages dans un fichier CSV sur votre système local
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 100%

---

# Exporter au format CSV{#export-to-csv}

L’option **Créer une exportation CSV** vous permet d’exporter les informations relatives à vos pages vers un fichier CSV situé sur votre système local.

* Le fichier téléchargé est nommé `export.csv`.
* Le contenu dépend des propriétés que vous sélectionnez.
* Vous pouvez définir le chemin, ainsi que la profondeur de l’exportation.

>[!NOTE]
>
>La fonction de téléchargement et la destination par défaut du navigateur sont utilisées.

L’assistant **Créer un export CSV** vous permet de sélectionner les éléments suivants :

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

L’option **Créer une exportation CSV** est disponible lorsque vous naviguez sur la console **Sites** (dans la vue Liste) : il s’agit d’une option du menu déroulant **Créer** :

![etc-02](assets/etc-02.png)

Pour créer une exportation CSV :

1. Ouvrez la console **Sites**, puis, le cas échéant, accédez à l’emplacement requis.
1. Dans la barre d’outils, sélectionnez **Créer** puis **Rapport CSV** pour ouvrir l’assistant :

   ![etc-03](assets/etc-03.png)

1. Sélectionnez les propriétés requises à exporter.
1. Sélectionnez **Créer**.
