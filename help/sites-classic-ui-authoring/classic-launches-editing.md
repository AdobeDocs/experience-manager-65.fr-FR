---
title: Modification de lancements
description: Après avoir créé un lancement pour une page (ou un jeu de pages), vous pouvez modifier le contenu dans la copie de lancement correspondante.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 45%

---

# Modification de lancements{#editing-launches}

## Modification de pages de lancement {#editing-launch-pages}

Après avoir créé un lancement pour une page (ou un jeu de pages), vous pouvez modifier le contenu dans la copie de lancement correspondante.

1. Ouvrez la page à modifier.
1. Dans le sidekick, sélectionnez la variable **Contrôle de version** puis développez l’onglet **Lancements** groupe. Le titre du lancement en cours de modification utilise une police en gras.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Sélectionnez le lancement sur lequel vous souhaitez travailler, puis cliquez sur **Basculer**.
1. Commencez la modification.

   >[!NOTE]
   >
   >Vous pouvez utiliser l’onglet **Page** du sidekick pour effectuer des actions telles que **Créer une page enfant**, entre autres. 

## Modification d’une configuration de lancement {#editing-a-launch-configuration}

Après avoir créé un lancement, vous pouvez en modifier le nom et la date. Vous pouvez également spécifier une image à associer au lancement.

1. Ouvrez la page d’administration des lancements ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Sélectionnez le lancement requis, puis cliquez sur **Modifier** pour ouvrir la boîte de dialogue :

   * Dans le **Général** vous pouvez modifier les éléments suivants :

      * **Titre**
      * **Date de mise en service** : équivaut à la date de lancement.
      * **Prêt pour l’exploitation**

      Voir [Lancements - Ordre des événements](/help/sites-authoring/launches.md#launches-the-order-of-events) pour plus d’informations sur l’objectif et l’interaction de ces champs.

   * Dans le **Image** vous pouvez télécharger un fichier image.


1. Cliquez sur **Enregistrer**.

## Identification du statut de lancement d’une page {#discovering-the-launch-status-of-a-page}

Lorsque vous modifiez le lancement d’une page, les informations sur le lancement s’affichent au bas de la **Contrôle de version** de Sidekick :

* Nom du lancement.
* Temps écoulé depuis la dernière modification.
* L’utilisateur qui a effectué la dernière modification.
* Le statut de l’indicateur **Prêt pour l’exploitation** (orange=non défini ; vert=défini).

![chlimage_1-186](assets/chlimage_1-186.png)
