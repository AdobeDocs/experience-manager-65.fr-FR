---
title: Création de lancements
seo-title: Création de lancements
description: Créez un lancement pour permettre la mise à jour d’une nouvelle version des pages web existantes en vue d’une activation future. Lors de la création d’un lancement, vous devez spécifier un titre et la page source.
seo-description: Créez un lancement pour permettre la mise à jour d’une nouvelle version des pages web existantes en vue d’une activation future. Lors de la création d’un lancement, vous devez spécifier un titre et la page source.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 96%

---


# Création de lancements{#creating-launches}

Créez un lancement pour permettre la mise à jour d’une nouvelle version des pages web existantes en vue d’une activation future. Lors de la création d’un lancement, vous devez spécifier un titre et la page source :

* The title appears in the **Sidekick**, from where authors can access them to work on them.
* Les pages enfants de la page source sont incluses, par défaut, dans le lancement. Si vous le souhaitez, vous pouvez n’utiliser que la page source.
* Par défaut, [Live Copy](/help/sites-administering/msm.md) met automatiquement à jour les pages de lancement à mesure que les pages source changent. Vous pouvez spécifier qu’une copie statique soit créée afin d’empêcher les modifications automatiques.

Vous pouvez éventuellement indiquer la **date de lancement** (et l’heure) pour définir le moment auquel les pages de lancement doivent être promues et activées. Toutefois, la **date de lancement** fonctionne uniquement en conjonction avec l’indicateur **Prêt pour la production** (voir [Modification d’une configuration de lancement](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)). Pour que les actions se produisent automatiquement, les deux doivent être définis.

## Création d’un lancement {#creating-a-launch}

La procédure suivante crée un lancement.

1. Ouvrez la page d’administration de site web ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Cliquez sur **Nouveau…**, puis sur **Nouveau lancement…**.
1. Définissez des valeurs pour les propriétés suivantes dans la boîte de dialogue **Créer un lancement** :

   * **Titre du lancement **: nom du lancement. Ce nom doit être explicite pour les auteurs.
   * **Page source** : chemin d’accès à la page pour laquelle vous souhaitez créer le lancement. Par défaut, toutes les pages enfants sont incluses.
   * **Exclure les sous-pages** : sélectionnez cette option pour ne créer le lancement que pour la page source (et non pour les pages enfants). Par défaut, cette option n’est pas sélectionnée.
   * **** Garder synchronisé : sélectionnez cette option pour mettre à jour automatiquement le contenu des pages de lancement lors de la modification des pages source. Cette option transforme le lancement en [Live Copy](/help/sites-administering/msm.md).
   * **Date de lancement** : date et heure d’activation de la copie de lancement (selon l’indicateur **Prêt pour la production**. Voir [Lancements - Ordre des événements](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Cliquez sur **Créer**.

## Suppression d’un lancement {#deleting-a-launch}

Vous pouvez également supprimer un lancement. 

1. Sélectionnez le lancement souhaité dans la [console des lancements](/help/sites-classic-ui-authoring/classic-launches.md).
1. Cliquez sur **Supprimer**. Une confirmation est demandée : 

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Lorsque vous supprimez des lancements imbriqués, vous devriez supprimer d’abord les niveaux inférieurs.

