---
title: Fonctionnalité du tableau de classement
description: Découvrez comment le composant Tableau de classement vous permet de voir comment les membres interagissent au sein de la communauté en classant les membres en fonction des points gagnés et de l’expertise.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---

# Fonctionnalité du tableau de classement {#leaderboard-feature}

## Présentation {#introduction}

La variable `Leaderboard` vous aide à comprendre comment les membres interagissent au sein de la communauté en classant les membres en fonction des points gagnés (notation de base) ou de leur expertise (notation avancée).

Avant d’inclure le composant de classement sur une page, vous devez configurer [Notation et badges des communautés](/help/communities/implementing-scoring.md).

Cette section de la documentation décrit :

* Ajouter le `Leaderboard` en un composant [site communautaire](/help/communities/overview.md#community-sites).
* Paramètres de configuration de la variable `Leaderboard` composant.

### Ajout d’un panneau de classement à une page {#adding-a-leaderboard-to-a-page}

Pour ajouter une `Leaderboard` à une page en mode création, recherchez le composant.

* `Communities / Leaderboard`

Et faites-le glisser sur la page.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Lorsqu’il est placé pour la première fois sur une page d’un site de communauté, voici comment le composant apparaît :

![tableau de classement](assets/leaderboard.png)

### Configuration du tableau de classement {#configuring-leaderboard}

Sélectionnez le `Leaderboard` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

![configure-lead-board](assets/configure-leaderboard.png)

#### Onglet Paramètres {#settings-tab}

Sous , **[!UICONTROL Paramètres]** , indiquez les informations relatives au membre qui s’affichent :

* **Nom d’affichage**

  Nom descriptif à afficher pour le panorama, reflétant les règles sélectionnées pour l’affichage des badges et des scores.
Par défaut : `Leaderboard` si rien n’est renseigné.

* **Badge**

  Si cette case est cochée, une colonne pour les icônes de badge est incluse dans le tableau de classement.
La case par défaut est décochée.

* **Nom du badge**

  Si cette case est cochée, une colonne correspondant au nom du badge est incluse dans le tableau de classement.
La case par défaut est décochée.

* **Utiliser l’avatar**

  Si cette case est cochée, l’avatar du membre est inclus dans le tableau de classement, en regard du lien de son nom vers son profil de membre.
La case par défaut est décochée.

#### Onglet Règles {#rules-tab}

Sous , **Règles** , le site de la communauté et ses règles de notation et de badge

* **Emplacement des règles**

  (Obligatoire) Emplacement où la règle de notation/attribution de badges est configurée.

* **Règle de notation**

  (Obligatoire) Règle spécifique générant les scores à afficher.

* **Règle de badge**

  (Obligatoire) Règle spécifique générant le badge à afficher.

* **Limite d’affichage**

  Nombre de membres à afficher par page. La valeur par défaut est 10.

### Exemple : Tableau de bord des participants {#example-participants-leaderboard}

Ce tableau de classement indique les résultats de l’application de règles de notation de base.

Configuration des composants de classement :

* Onglet Paramètres :

   * Nom d’affichage = `Participation Board`
   * `checked` :

      * Badge
      * Nom du badge
      * Utiliser l’avatar

* Onglet Règles :

   * Emplacement de la règle = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/forums-scoring`
   * Règle de badge = `/libs/settings/community/badging/rules//reference-badging`
   * Limite d’affichage = `10`

![participant-leader](assets/participants-leaderboard.png)

### Exemple : Experts Leaderboard {#example-experts-leaderboard}

Ce tableau de classement indique les résultats de l’application de règles de notation avancées.

Configuration des composants de classement :

* Onglet Paramètres :

   * Nom d’affichage = `Expertise Board`
   * `checked` :

      * Badge
      * Utiliser l’avatar

* Onglet Règles :

   * Emplacement de la règle = `/content/sites/<site name>/jcr:content`
   * Règle de notation = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Règle de badge = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite d’affichage = `10`

![Experts-Lead board](assets/experts-leaderboard.png)

### Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales relatives au tableau de bord](/help/communities/leaderboard.md) pour les développeurs.

Les instructions de création de règles sont fournies sur la page [Notation et badges des communautés](/help/communities/implementing-scoring.md) pour les administrateurs.
