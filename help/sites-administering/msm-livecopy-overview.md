---
title: Console Aperçu de Live Copy
seo-title: Live Copy Overview Console
description: Découvrez les principes de base de la console Aperçu de la Live Copy.
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 60%

---

# Console Aperçu de Live Copy{#live-copy-overview-console}

La variable **Présentation de la Live Copy** permet d’effectuer les opérations suivantes :

* Afficher/gérer l’héritage sur un site :

   * Afficher l’arborescence du plan directeur et la structure de Live Copy correspondante, ainsi que leur état d’héritage
   * Modifier l’état d’héritage ; par exemple, suspendre, reprendre
   * Affichage des propriétés de plan directeur et de Live Copy

* d’exécuter des actions de déploiement

## Ouverture de l’aperçu de la Live Copy {#opening-the-live-copy-overview}

Vous pouvez ouvrir l’aperçu de la Live Copy via :

* [Panneau latéral de références d’une page de plan directeur (console Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Propriétés d’une page de plan directeur](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Ouverture de l’aperçu de la Live Copy - Références pour une page de plan directeur {#opening-live-copy-overview-references-for-a-blueprint-page}

L’**aperçu de la Live Copy** peut être ouvert via le panneau latéral **Références** de la console **Sites** :

1. Dans la console **Sites**, [accédez à la page de plan directeur et sélectionnez-la](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Ouvrez le panneau **[Références](/help/sites-authoring/basic-handling.md#references)** et sélectionnez **Live Copies**.

   ![Panneau Références - Live Copies](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >Vous pouvez également ouvrir d’abord Références , puis sélectionner le plan directeur.

1. Sélectionner **Présentation de la Live Copy** pour afficher et utiliser l’aperçu de toutes les Live Copies liées au plan directeur sélectionné.
1. Utilisez **Fermer** pour fermer l’aperçu et retourner à la console **Sites**.

### Ouverture de l’aperçu de la Live Copy - Propriétés d’une page de plan directeur {#opening-live-copy-overview-properties-of-a-blueprint-page}

L’**Aperçu de Live Copy** peut être ouvert lors de l’affichage des propriétés d’une page de plan directeur :

1. Ouvrez les **propriétés** pour la page de plan directeur appropriée.
1. Ouvrez l’onglet **Plan directeur**, l’option **Aperçu de Live Copy** s’affiche dans la barre d’outils supérieure :

   ![Onglet Plan directeur - Aperçu de la Live Copy](assets/chlimage_1-360.png)

1. Sélectionnez **Aperçu de la Live Copy** pour afficher et utiliser l’aperçu de toutes les Live Copies associées au plan directeur actuel.

   >[!NOTE]
   >
   >Pour plus de détails, consultez également l’article [Livecopy status message - Up-to-date/Green/In Sync](https://helpx.adobe.com/fr/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html) (Message d’état de la Live Copy - À jour/Vert/Synchronisé) de la base de connaissances.

1. Utilisez **Fermer** pour fermer l’aperçu et retourner à la console **Sites**.

## Utilisation de l’aperçu de la Live Copy {#using-the-live-copy-overview}

La variable **Présentation de la Live Copy** peut également être utilisé pour exécuter des actions sur la Live Copy :

1. Ouvrez l’**aperçu de la Live Copy**.
1. Sélectionnez la page de plan directeur ou de Live Copy requise. La barre d’outils est mise à jour pour afficher les actions disponibles. La variable [actions](/help/sites-administering/msm.md#terms-used) disponible selon que vous sélectionnez une [plan directeur](#actions-for-a-blueprint-page) ou [Live Copy](#actions-for-a-live-copy-page) page :

### Actions d’une page de plan directeur {#actions-for-a-blueprint-page}

Lorsque vous sélectionnez une page de plan directeur, les actions suivantes sont disponibles :

![Plan directeur sélectionné : actions disponibles](assets/chlimage_1-361.png)

* Modification

   * Ouvrez la page de plan directeur pour la modifier.

* [Déploiement](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Effectuez un déploiement pour transmettre les modifications de la source à la Live Copy.

### Actions pour une page de Live Copy {#actions-for-a-live-copy-page}

Lorsque vous sélectionnez une page Live Copy, les actions suivantes sont disponibles :

![Page Live Copy sélectionnée - actions disponibles](assets/chlimage_1-362.png)

* Modifier

   * Ouvrez la page Live Copy pour la modifier.

* [Statut de la relation](#relationship-status)

   * Affichez des informations sur le statut et l’héritage.

* [Synchronisation](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Synchronisez une Live Copy pour extraire des modifications de la source vers la Live Copy.

* [Réinitialisation](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Réinitialisez une page de Live Copy pour supprimer toutes les annulations d’héritage et restaurer la page au même état que la page source.

* [Suspension](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Désactivez temporairement les relations en direct entre une Live Copy et sa page de plan directeur.

* [Reprise](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * Reprendre vous permet de rétablir une relation suspendue.

* [Désolidariser](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Supprime de façon permanente la relation en direct entre une Live Copy et sa page de plan directeur.

## Statut de la relation {#relationship-status}

La console **Statut de la relation** comporte deux onglets fournissant de nombreuses fonctionnalités :

* [Informations sur le statut de la relation](#relationship-status-information)
* [Informations sur la Live Copy](#live-copy-information)

### Informations sur le statut de la relation {#relationship-status-information}

Cet onglet fournit des informations détaillées sur l’état de la relation entre le plan directeur et la Live Copy :

![Informations sur l’état de la relation](assets/chlimage_1-363.png)

### Informations sur la Live Copy {#live-copy-information}

Cet onglet vous permet d’afficher et de modifier la configuration de la Live Copy :

![Informations sur la Live Copy](assets/chlimage_1-364.png)
