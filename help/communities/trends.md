---
title: Tendances des activités
description: Ajout d’un composant Liste des activités de la communauté à une page
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%
---
# Tendances des activités {#activity-trends}

## Présentation {#introduction}

Le composant `Community Activity List` vous permet d’ajouter des informations de tendance concernant les publications et les vues par les membres, ainsi que les publications et les vues de contenu.

Le document décrit :

* Ajout du composant `Community Activity List` à un [site communautaire](/help/communities/overview.md#community-sites).

* Paramètres de configuration du composant `Community Activity List`.

### Condition requise {#requirement}

Les données du `Community Activity List` ne sont disponibles que lorsqu’Adobe Analytics dispose d’une licence et est configuré pour le site de la communauté.

Voir [Configuration d’Analytics pour les fonctionnalités de Communities](/help/communities/analytics.md).

### Ajout d’une liste d’activités de la communauté à une page {#adding-a-community-activity-list-to-a-page}

Pour ajouter un composant `Community Activity List` à une page en mode création, localisez-le `Communities / Community Activity List` et faites-le glisser sur une page.

Pour plus d’informations, consultez [Principes de base des composants de communautés](/help/communities/basics.md).

Lorsque vous placez le composant sur une page d’un site communautaire pour la première fois, voici comment il s’affiche :

![community-activity](assets/community-activity.png)

### Configuration de la liste des activités de la communauté  {#configuring-community-activity-list}

Sélectionnez le composant de `Community Activity List` placé, puis sélectionnez l’icône `Configure` pour ouvrir la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Sous l’onglet **Commentaires**, indiquez si et comment les commentaires des fichiers chargés s’affichent :

![propriétés](assets/activity-list-properties.png)

* **Type**

  Indiquez s’il faut afficher les données concernant les membres de la communauté ou le contenu créé par l’utilisateur.

  Faites un choix parmi les éléments suivants :

  * `Members`
  * `Content`

  La valeur par défaut est `Members`.

* **Afficher le titre**

  Titre descriptif à afficher au-dessus des données, tel que `Trending Content`.
  La valeur par défaut est aucun titre.

* **Afficher le nombre**

  Nombre d’éléments à répertorier.
  La valeur par défaut est 10.

* **Type d’activité**

  Sélectionnez l’une des options suivantes :

  * `Views` (visites de page)
  * `Posts`(création du contenu créé par l’utilisateur)
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

  Vous pouvez ainsi étendre l’activité à un sous-ensemble du site, tel qu’un blog spécifique.
  La valeur par défaut est l’ensemble du site de la communauté.

* **Agrégation des nombres de membres**

  Lorsque cette option est désélectionnée (désactivée), seules les publications de niveau supérieur sont comptabilisées. Par exemple, si le contexte est la page racine (valeur par défaut), une `Activity Type` de `Posts` n’affiche jamais d’activité, car il n’est pas possible de publier du contenu sur la page racine. Lorsque cette case est cochée, les nombres de toutes les pages descendantes sont inclus.
  La valeur par défaut est cochée.

### Exemple de page avec quatre composants {#example-page-with-components}

**Principaux visiteurs** configuration : Type = Membres, Type d’activité = Vues

**Principaux contributeurs** configuration : Type = Membres, Type d’activité = Publications

**Contenu principal** configuration : Type = Contenu, Type d’activité = Vues,

**Contenu en tendance** configuration : Type = Contenu, Type d’activité = Publications

![composants](assets/activity-list-components.png)
