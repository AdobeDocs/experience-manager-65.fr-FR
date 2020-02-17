---
title: Fonctionnalité de classement
seo-title: Fonctionnalité de classement
description: Ajout d’un composant Leaderboard à une page
seo-description: Ajout d’un composant Leaderboard à une page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Fonctionnalité de classement{#leaderboard-feature}

## Présentation {#introduction}

La `Leaderboard` composante permet d&#39;obtenir une idée de la façon dont les membres interagissent au sein de la communauté en classant les membres selon les points gagnés (note de base) ou leur expertise (note de niveau avancé).

Avant d’inclure le composant du tableau de bord dans une page, il est nécessaire de configurer le score [des communautés et les badges](/help/communities/implementing-scoring.md).

Cette section de la documentation décrit :

* ajout du `Leaderboard` composant à un site [communautaire](/help/communities/overview.md#community-sites)
* les paramètres de configuration du composant `Leaderboard`.

### Adding a Leaderboard to a Page {#adding-a-leaderboard-to-a-page}

To add a `Leaderboard` component to a page in author mode, locate the component

* `Communities / Leaderboard`

et faites-le glisser sur la page.

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![chlimage_1-19](assets/chlimage_1-19.png)

### Configuration de Leaderboard {#configuring-leaderboard}

Select the placed `Leaderboard` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-20](assets/chlimage_1-20.png) ![chlimage_1-21](assets/chlimage_1-21.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **Paramètres **, indiquez les informations relatives au membre qui s’affichent :

* **Nom d’affichage**

   Nom descriptif à afficher pour le panorama, reflétant les règles sélectionnées pour l’affichage des badges et des scores.
La valeur par défaut est `Leaderboard`, si rien n’est saisi.

* **Badge**

   Si cette option est cochée, une colonne pour les icônes de badge est incluse dans le tableau de bord.
Cette option n’est pas cochée par défaut.

* **Nom du badge**

   Si cette option est cochée, une colonne correspondant au nom du badge est incluse dans le tableau de bord.
Cette option n’est pas cochée par défaut.

* **Utiliser un avatar**

   Si cette option est cochée, l&#39;avatar du membre est inclus dans le tableau de bord, en regard du lien du nom vers son profil de membre.
Cette option n’est pas cochée par défaut.

#### Onglet Règles {#rules-tab}

Sous l’onglet **Règles** , le site de la communauté et ses règles de notation et de badge

* **Emplacement des règles**

   (obligatoire) Emplacement où la règle Scoring / Badging est configurée.

* **Règle de notation**

   (obligatoire) Règle spécifique générant les scores à afficher.

* **Règle d’attribution des badges**

   (obligatoire) Règle spécifique générant le badge à afficher.

* **Limite d’affichage**

   Nombre de membres à afficher par page.

   La valeur par défaut est 10.

### Exemple : Tableau de bord des participants {#example-participants-leaderboard}

Ce tableau de bord indique comment appliquer les règles de notation de base.

Configuration du composant Leaderboard :

* Onglet Settings:

   * Nom d’affichage = `Participation Board`
   * `checked`:

      * Badge
      * Nom du badge
      * Utiliser un avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/communities/jcr:content`
   * Règle de notation = `/etc/community/scoring/rules/forums-scoring`
   * Règle d’attribution des badges = `/etc/community/badging/rules/reference-badging`
   * Limite d’affichage = `10`

![chlimage_1-22](assets/chlimage_1-22.png)

### Exemple : Tableau de bord des experts {#example-experts-leaderboard}

Ce tableau de bord indique les résultats de l’application de règles de notation avancées.

Configuration du composant Leaderboard :

* Onglet Settings:

   * Nom d’affichage = `Expertise Board`
   * `checked`:

      * Badge
      * Utiliser un avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/communities/jcr:content`
   * Règle de notation = `/etc/community/scoring/rules/adv-forums-scoring`
   * Règle d’attribution des badges = `/etc/community/badging/rules/adv-forums-badging`
   * Limite d’affichage = `10`

![chlimage_1-23](assets/chlimage_1-23.png)

### Informations supplémentaires {#additional-information}

More information may be found on the [Leaderboard Essentials](/help/communities/leaderboard.md) page for developers.

Les instructions de création de règles sont fournies sur la page Scores et badges [des communautés](/help/communities/implementing-scoring.md) pour les administrateurs.
