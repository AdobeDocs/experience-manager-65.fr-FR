---
title: Modification de lancements
description: Une fois un lancement créé pour une page (ou un ensemble de pages), vous pouvez modifier le contenu dans la copie de lancement des pages.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 76%

---

# Modification de lancements{#editing-launches}

## Modification de pages de lancement {#editing-launch-pages}

Une fois un lancement créé pour une page (ou un ensemble de pages), vous pouvez modifier le contenu dans la copie de lancement des pages.

1. Ouvrez la page pour modification.
1. Dans le sidekick, sélectionnez l’onglet **Contrôle de version**, puis développez le groupe **Lancements**. Le titre du lancement en cours de modification utilise une police en gras.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Sélectionnez le lancement sur lequel vous souhaitez travailler, puis cliquez sur **Basculer**.
1. Commencez la modification.

   >[!NOTE]
   >
   >Vous pouvez utiliser la variable **Page** de sidekick pour effectuer des actions telles que **Créer une page enfant**, entre autres.

## Modification d’une configuration de lancement {#editing-a-launch-configuration}

Après avoir créé un lancement, vous pouvez en modifier le nom et la date. Vous pouvez également spécifier une image à associer au lancement.

1. Ouvrez la page d’administration des lancements ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Sélectionnez le lancement requis, puis cliquez sur **Modifier** pour ouvrir la boîte de dialogue :

   * Dans l’onglet **Général**, vous pouvez modifier les éléments suivants :

      * **Titre**
      * **Date de mise en service** : équivaut à la date de lancement.
      * **Prêt pour l’exploitation**

     Voir [Lancements - Ordre des événements](/help/sites-authoring/launches.md#launches-the-order-of-events) pour plus d’informations sur l’objectif et l’interaction de ces champs.

   * Dans l’onglet **Image**, vous pouvez télécharger un fichier image.

1. Cliquez sur **Enregistrer**.

## Identification du statut de lancement d’une page {#discovering-the-launch-status-of-a-page}

Lorsque vous modifiez le lancement d’une page, les informations sur le lancement s’affichent au bas de l’onglet **Contrôle de version** du sidekick :

* Nom du lancement.
* Temps écoulé depuis la dernière modification.
* Personne ayant effectué la dernière modification.
* Le statut de l’indicateur **Prêt pour l’exploitation** (orange=non défini ; vert=défini).

![chlimage_1-186](assets/chlimage_1-186.png)
