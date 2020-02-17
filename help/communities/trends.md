---
title: Tendances d’activité
seo-title: Tendances d’activité
description: Ajout d’un composant Liste d’activités de la communauté à une page
seo-description: Ajout d’un composant Liste d’activités de la communauté à une page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Tendances d’activité{#activity-trends}

## Présentation {#introduction}

The `Community Activity List` component provides the ability to add trending information regarding posts and views by members as well as posts and views of content.

Le document décrit :

* ajout du `Community Activity List` composant à un site [communautaire](/help/communities/overview.md#community-sites)

* les paramètres de configuration du composant `Community Activity List`.

### Condition requise {#requirement}

Les données du `Community Activity List` module ne sont disponibles que si Adobe Analytics est sous licence et configuré pour le site de la communauté.

Voir Configuration [Analytics pour les fonctionnalités](/help/communities/analytics.md)des communautés.

### Adding a Community Activity List to a Page {#adding-a-community-activity-list-to-a-page}

To add a `Community Activity List` component to a page in author mode, locate the component

* `Communities / Community Activity List`

et faites-le glisser sur la page.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![chlimage_1-54](assets/chlimage_1-54.png)

### Configuration de la liste des activités de la communauté {#configuring-community-activity-list}

Select the placed `Community Activity List` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-55](assets/chlimage_1-55.png)

Sous l’onglet **Commentaires **, indiquez si et comment les commentaires des fichiers téléchargés apparaissent :

![chlimage_1-56](assets/chlimage_1-56.png)

* **Type**

   Indiquez s’il faut afficher les données concernant les membres de la communauté ou le contenu généré par l’utilisateur.

   Sélectionner parmi

   * `Members`
   * `Content`
   La valeur par défaut est `Members`.

* **Titre affiché**

   Titre descriptif à afficher au-dessus des données, par exemple `Trending Content`.
Par défaut, il n’existe aucun titre.

* **Nombre d’affichages**

   Nombre d’éléments à répertorier.
La valeur par défaut est 10.

* **Type d’activité**

   Sélectionnez l’un des

   * `Views`(visites de page)
   * `Posts`(création d’UGC)
   * `Follows`
   * `Likes`
   La valeur par défaut est Vues.

* **Période**

   Sélectionnez l’un des

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`
   La valeur par défaut est `Total`.

* **Chemin d’accès au contexte**

   Permet d’étendre l’activité à un sous-ensemble du site, tel qu’un blog spécifique.
La valeur par défaut est le site de la communauté entier.

* **Agrégation du nombre de membres**

   Si cette option est désactivée, seules les publications de niveau supérieur sont comptabilisées. For example, if the context is the root page (the default), then an `Activity Type`of `Posts`will never show any activity as there is no ability to post content to the root page. Lorsque cette option est cochée, les nombres sur toutes les pages descendantes sont inclus.
Cette option est cochée par défaut.

### Exemple de page avec 4 composants {#example-page-with-components}

**Principaux visiteurs** config : Type = Membres, Type d’activité = Vues

**Configuration des principaux contributeurs** : Type = Membres, Type d’activité = Publications

**Configuration du contenu** principal : Type = Contenu, Type d’activité = Vues,

**Configuration du contenu** de tendance : Type = Contenu, Type d’activité = Publications

![chlimage_1-57](assets/chlimage_1-57.png)

