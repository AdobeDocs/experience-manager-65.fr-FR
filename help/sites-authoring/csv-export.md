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
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
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
