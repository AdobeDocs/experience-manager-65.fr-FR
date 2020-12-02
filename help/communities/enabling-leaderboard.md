---
title: Fonctionnalité du tableau de bord
seo-title: Fonctionnalité du tableau de bord
description: Ajouter un composant de tableau de bord à une page
seo-description: Ajouter un composant de tableau de bord à une page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: 6720d5a0fdf1facc0b10011ec306dffbb31f4ac5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 22%

---


# Fonctionnalité du tableau de bord {#leaderboard-feature}

## Présentation {#introduction}

Le composant `Leaderboard` permet d&#39;obtenir une idée de la façon dont les membres interagissent au sein de la communauté en classant les membres en fonction des points gagnés (note de base) ou de leur expertise (note avancée).

Avant d’inclure le composant Leadboard sur une page, il est nécessaire de configurer [le score des communautés et les badges](/help/communities/implementing-scoring.md).

Cette section de la documentation décrit:

* Ajouter le composant `Leaderboard` à un [site communautaire](/help/communities/overview.md#community-sites).
* Paramètres de configuration du composant `Leaderboard`.

### Ajouter un tableau de bord à une page {#adding-a-leaderboard-to-a-page}

Pour ajouter un composant `Leaderboard` à une page en mode création, recherchez le composant.

* `Communities / Leaderboard`

et faites-le glisser sur la page.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![chlimage_1-8](assets/chlimage_1-8.png)

### Configuration de Leaderboard {#configuring-leaderboard}

Sélectionnez le composant `Leaderboard` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![chlimage_1-9](assets/chlimage_1-9.png)

![chlimage_1-10](assets/chlimage_1-10.png)

#### Onglet Settings {#settings-tab}

Sous l&#39;onglet **[!UICONTROL Paramètres]**, indiquez les informations relatives au membre qui s&#39;affichent :

* **Nom d’affichage**

   Nom descriptif à afficher pour le panorama, reflétant les règles sélectionnées pour l’affichage des badges et des scores.
La valeur par défaut est `Leaderboard`, si rien n’est saisi.

* **Badge**

   Si cette case est cochée, une colonne pour les icônes de badge est incluse dans le tableau de bord.
Cette option n’est pas cochée par défaut.

* **Nom du badge**

   Si cette case est cochée, une colonne correspondant au nom du badge est incluse dans le tableau de bord.
Cette option n’est pas cochée par défaut.

* **Utiliser un avatar**

   Si cette case est cochée, l&#39;avatar du membre est inclus dans le tableau de bord, à côté du lien de son nom vers son profil membre.
Cette option n’est pas cochée par défaut.

#### Onglet Règles {#rules-tab}

Sous l&#39;onglet **Règles**, le site communautaire et ses règles de notation et de badge

* **Emplacement des règles**

   (Obligatoire) Emplacement où la règle Scoring / Badging est configurée.

* **Règle de notation**

   (Obligatoire) Règle spécifique générant les scores à afficher.

* **Règle d’attribution des badges**

   (Obligatoire) Règle spécifique générant le badge à afficher.

* **Limite d’affichage**

   Nombre de membres à afficher par page.La valeur par défaut est 10.

### Exemple : Tableau de bord des participants {#example-participants-leaderboard}

Ce tableau de bord indique les résultats de l’application des règles de notation de base.

Configuration du composant de tableau de bord :

* Onglet Settings:

   * Nom d’affichage = `Participation Board`
   * `checked` :

      * Badge
      * Nom du badge
      * Utiliser un avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/forums-scoring`
   * Règle d’attribution des badges = `/libs/settings/community/badging/rules//reference-badging`
   * Limite d’affichage = `10`

![chlimage_1-11](assets/chlimage_1-11.png)

### Exemple : Tableau de bord des experts {#example-experts-leaderboard}

Ce tableau de bord indique les résultats de l’application de règles de notation avancées.

Configuration du composant de tableau de bord :

* Onglet Settings:

   * Nom d’affichage = `Expertise Board`
   * `checked` :

      * Badge
      * Utiliser un avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Règle d’attribution des badges = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite d’affichage = `10`

![chlimage_1-12](assets/chlimage_1-12.png)

### Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Leaderboard Essentials](/help/communities/leaderboard.md) destinée aux développeurs.

Les instructions de création de règles sont fournies sur la page [Scores et badges des communautés](/help/communities/implementing-scoring.md) à l’intention des administrateurs.
