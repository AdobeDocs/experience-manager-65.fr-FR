---
title: Console Aperçu de Live Copy
description: Découvrez les principes de base de la console Vue d’ensemble de Live Copy.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 100%

---

# Console Aperçu de Live Copy{#live-copy-overview-console}

La **vue d’ensemble de Live Copy** vous permet :

* d’afficher ou de gérer l’héritage sur un site :

   * d’afficher l’arborescence de plan directeur de la structure de Live Copy correspondante, ainsi que le statut d’héritage ;
   * modifier le statut d’héritage ; par exemple, suspendre, reprendre ;
   * d’afficher les propriétés de plan directeur et de Live Copy ;

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
   >Vous pouvez également ouvrir le panneau des références en premier, puis sélectionner le plan directeur.

1. Sélectionnez **Vue d’ensemble de Live Copy** pour afficher et utiliser la vue d’ensemble de toutes les Live Copies associées au plan directeur sélectionné.
1. Utilisez **Fermer** pour fermer l’aperçu et retourner à la console **Sites**.

### Ouverture de la vue d’ensemble de la Live Copy - Propriétés d’une page de plan directeur {#opening-live-copy-overview-properties-of-a-blueprint-page}

La **vue d’ensemble de Live Copy** peut être ouverte lors de l’affichage des propriétés d’une page de plan directeur :

1. Ouvrez les **propriétés** pour la page de plan directeur appropriée.
1. Ouvrez l’onglet **Plan directeur**, l’option **Aperçu de Live Copy** s’affiche dans la barre d’outils supérieure :

   ![Onglet Plan directeur - Vue d’ensemble de la Live Copy](assets/chlimage_1-360.png)

1. Sélectionnez **Aperçu de la Live Copy** pour afficher et utiliser l’aperçu de toutes les Live Copies associées au plan directeur actuel.

   >[!NOTE]
   >
   >Pour plus de détails, consultez également l’article [Livecopy status message - Up-to-date/Green/In Sync](https://helpx.adobe.com/fr/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html) (Message d’état de la Live Copy - À jour/Vert/Synchronisé) de la base de connaissances.

1. Utilisez **Fermer** pour fermer l’aperçu et retourner à la console **Sites**.

## Utilisation de l’aperçu de la Live Copy {#using-the-live-copy-overview}

La **vue d’ensemble de Live Copy** peut également être utilisée pour effectuer des actions sur la Live Copy :

1. Ouvrez l’**aperçu de la Live Copy**.
1. Sélectionnez la page de plan directeur ou de Live Copy requise. La barre d’outils est mise à jour pour afficher les actions disponibles. Les [actions](/help/sites-administering/msm.md#terms-used) disponibles varient selon que vous sélectionnez une page de [plan directeur](#actions-for-a-blueprint-page) ou de [Live Copy](#actions-for-a-live-copy-page) :

### Actions d’une page de plan directeur {#actions-for-a-blueprint-page}

Lorsque vous sélectionnez une page de plan directeur, les actions suivantes sont disponibles :

![Plan directeur sélectionné - Actions disponibles](assets/chlimage_1-361.png)

* Modification

   * Ouvrez la page de plan directeur pour la modifier.

* [Déploiement](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Effectuez un déploiement pour envoyer les modifications de la source vers la Live Copy.

### Actions pour une page de Live Copy {#actions-for-a-live-copy-page}

Lorsque vous sélectionnez une page de Live Copy, les actions suivantes sont disponibles :

![Page de Live Copy sélectionnée - Actions disponibles](assets/chlimage_1-362.png)

* Modifier

   * Ouvrez la page de la Live Copy pour la modifier.

* [Statut de la relation](#relationship-status)

   * Affichez des informations sur le statut et l’héritage.

* [Synchronisation](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Synchronisez une Live Copy pour extraire des modifications de la source vers la Live Copy.

* [Réinitialisation](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Réinitialisez une page de Live Copy pour supprimer toutes les annulations d’héritage et restaurer la page au même état que la page source.

* [Suspension](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Désactivez temporairement les relations en direct entre une Live Copy et sa page de plan directeur.

* [Reprise](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * La reprise vous permet de rétablir une relation suspendue.

* [Désolidariser](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Supprime de façon permanente la relation en direct entre une Live Copy et sa page de plan directeur.

## Statut de la relation {#relationship-status}

La console **Statut de la relation** comporte deux onglets fournissant de nombreuses fonctionnalités :

* [Informations sur le statut de la relation](#relationship-status-information)
* [Informations sur la Live Copy](#live-copy-information)

### Informations sur le statut de la relation {#relationship-status-information}

Cet onglet fournit des informations détaillées sur le statut de la relation entre le plan directeur et la Live Copy :

![Informations sur le statut de la relation](assets/chlimage_1-363.png)

### Informations sur la Live Copy {#live-copy-information}

Cet onglet vous permet d’afficher et de modifier la configuration de la Live Copy :

![Informations sur la Live Copy](assets/chlimage_1-364.png)
