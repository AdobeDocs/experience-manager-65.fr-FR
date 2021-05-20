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
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 20%

---

# Fonctionnalité du tableau de classement {#leaderboard-feature}

## Présentation {#introduction}

Le composant `Leaderboard` permet d’obtenir une idée de la façon dont les membres interagissent au sein de la communauté en classant les membres en fonction des points gagnés (notation de base) ou de leur expertise (notation avancée).

Avant d’inclure le composant de classement sur une page, il est nécessaire de configurer [Notation et badges des communautés](/help/communities/implementing-scoring.md).

Cette section de la documentation décrit:

* Ajout du composant `Leaderboard` à un [site communautaire](/help/communities/overview.md#community-sites).
* Paramètres de configuration du composant `Leaderboard`.

### Ajout d’un tableau de classement à une page {#adding-a-leaderboard-to-a-page}

Pour ajouter un composant `Leaderboard` à une page en mode création, localisez le composant .

* `Communities / Leaderboard`

et faites-le glisser sur la page.

Pour plus d’informations, voir [Principes de base des composants des communautés](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![tableau de classement](assets/leaderboard.png)

### Configuration de Leaderboard {#configuring-leaderboard}

Sélectionnez le composant `Leaderboard` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![configure-lead-board](assets/configure-leaderboard.png)

#### Onglet Settings {#settings-tab}

Sous l’onglet **[!UICONTROL Paramètres]** , indiquez les informations relatives au membre qui s’affichent :

* **Nom d’affichage**

   Nom descriptif à afficher pour le panorama, reflétant les règles sélectionnées pour l’affichage des badges et des scores.
La valeur par défaut est `Leaderboard`, si rien n’est renseigné.

* **Badge**

   Si cette case est cochée, une colonne pour les icônes de badge est incluse dans le tableau de classement.
Cette option n’est pas cochée par défaut.

* **Nom du badge**

   Si cette case est cochée, une colonne correspondant au nom du badge est incluse dans le tableau de classement.
Cette option n’est pas cochée par défaut.

* **Utiliser l’avatar**

   Si cette case est cochée, l’avatar du membre est inclus dans le tableau de classement, en regard du lien de son nom vers son profil de membre.
Cette option n’est pas cochée par défaut.

#### Onglet Règles {#rules-tab}

Sous l’onglet **Règles**, le site de la communauté et ses règles de notation et de badge

* **Emplacement des règles**

   (Obligatoire) Emplacement où la règle de notation/attribution de badges est configurée.

* **Règle de notation**

   (Obligatoire) Règle spécifique générant les scores à afficher.

* **Règle d’attribution des badges**

   (Obligatoire) Règle spécifique générant le badge à afficher.

* **Limite d’affichage**

   Nombre de membres à afficher par page. La valeur par défaut est 10.

### Exemple : Tableau de bord des participants {#example-participants-leaderboard}

Ce tableau de classement indique les résultats de l’application de règles de notation de base.

Configuration des composants de classement :

* Onglet Settings:

   * Nom d’affichage = `Participation Board`
   * `checked` :

      * Badge
      * Nom du badge
      * Utiliser l’avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/forums-scoring`
   * Règle d’attribution des badges = `/libs/settings/community/badging/rules//reference-badging`
   * Limite d’affichage = `10`

![participant-leader](assets/participants-leaderboard.png)

### Exemple : Tableau de bord des experts {#example-experts-leaderboard}

Ce tableau de classement indique les résultats de l’application de règles de notation avancées.

Configuration des composants de classement :

* Onglet Settings:

   * Nom d’affichage = `Expertise Board`
   * `checked` :

      * Badge
      * Utiliser l’avatar

* Onglet Règles :

   * Emplacement des règles = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Règle d’attribution des badges = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite d’affichage = `10`

![Experts-Lead board](assets/experts-leaderboard.png)

### Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur le tableau de classement](/help/communities/leaderboard.md) pour les développeurs.

Les instructions de création de règles sont fournies sur la page [Notation et badges communautaires](/help/communities/implementing-scoring.md) pour les administrateurs.
