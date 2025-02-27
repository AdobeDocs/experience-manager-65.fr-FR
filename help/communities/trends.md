---
title: Tendances des activités
description: Ajout d’un composant Liste d’activités de la communauté à une page
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 4%

---

# Tendances des activités {#activity-trends}

## Présentation {#introduction}

Le composant `Community Activity List` vous permet d’ajouter des informations de tendance concernant les publications et les vues par les membres, les publications et les vues de contenu.

Le document décrit :

* Ajout du composant `Community Activity List` à un [site communautaire](/help/communities/overview.md#community-sites).

* Paramètres de configuration du composant `Community Activity List`.

### Condition requise {#requirement}

Les données pour `Community Activity List` ne sont disponibles que lorsque Adobe Analytics est sous licence et configuré pour le site de la communauté.

Voir [Configuration d’Analytics pour les fonctionnalités de Communities](/help/communities/analytics.md).

### Ajout d’une liste d’activités de la communauté à une page {#adding-a-community-activity-list-to-a-page}

Pour ajouter un composant `Community Activity List` à une page en mode création, recherchez le composant `Communities / Community Activity List` et faites-le glisser sur la page.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](/help/communities/basics.md).

Lorsqu’il est placé pour la première fois sur une page d’un site de communauté, voici comment le composant apparaît :

![community-activity](assets/community-activity.png)

### Configuration de la liste des activités communautaires  {#configuring-community-activity-list}

Sélectionnez le composant `Community Activity List` placé, puis sélectionnez l’icône `Configure` pour ouvrir la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous l’onglet **Comments** , indiquez si et comment les commentaires des fichiers chargés apparaissent :

![propriétés](assets/activity-list-properties.png)

* **Type**

  Indiquez s’il faut afficher les données concernant les membres de la communauté ou le contenu généré par l’utilisateur.

  Faites un choix parmi les éléments suivants :

   * `Members`
   * `Content`

  La valeur par défaut est `Members`.

* **Titre d’affichage**

  Titre descriptif à afficher au-dessus des données, par exemple `Trending Content`.
La valeur par défaut n’est pas le titre.

* **Nombre d’affichages**

  Nombre d’éléments à répertorier.
La valeur par défaut est 10.

* **Type d’activité**

  Sélectionnez l’une des options suivantes :

   * `Views`(visites de page)
   * `Posts`(création de contenu généré par l’utilisateur)
   * `Follows`
   * `Likes`

  La valeur par défaut est Vues.

* **Période**

  Sélectionnez l’une des options suivantes :

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  La valeur par défaut est `Total`.

* **Chemin du contexte**

  Vous pouvez ainsi répartir l’activité sur un sous-ensemble du site, tel qu’un Blog spécifique.
La valeur par défaut est l’ensemble du site de la communauté.

* **Agrégation du nombre de membres**

  Si cette option est désélectionnée (désactivée), seules les publications de niveau supérieur sont comptabilisées. Par exemple, si le contexte est la page racine (valeur par défaut), un `Activity Type` de `Posts` n’affiche aucune activité, car il n’est pas possible de publier du contenu sur la page racine. Lorsque cette case est cochée, les décomptes de toutes les pages descendantes sont inclus.
La valeur par défaut est cochée.

### Exemple de page avec quatre composants {#example-page-with-components}

**Meilleurs visiteurs** config : Type = Membres, Type d’activité = Vues

**Principaux contributeurs** config : Type = Membres, Type d’activité = Publications

**Contenu supérieur** config : Type = Contenu, Type d’activité = Vues,

**Contenu de tendance** config : Type = Contenu, Type d’activité = Publications

![composants](assets/activity-list-components.png)
