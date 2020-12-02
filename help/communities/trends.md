---
title: Tendances d’activité
seo-title: Tendances d’activité
description: Ajouter un composant Liste d'Activité communautaire à une page
seo-description: Ajouter un composant Liste d'Activité communautaire à une page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 29%

---


# Tendances d’activité {#activity-trends}

## Présentation {#introduction}

Le composant `Community Activity List` permet d’ajouter des informations de tendance concernant les publications et les vues des membres, ainsi que les publications et les vues de contenu.

Le document décrit :

* Ajouter le composant `Community Activity List` à un [site communautaire](/help/communities/overview.md#community-sites).

* Paramètres de configuration du composant `Community Activity List`.

### Condition requise {#requirement}

Les données de `Community Activity List` ne sont disponibles que lorsque Adobe Analytics est sous licence et configuré pour le site communautaire.

Voir [Configuration d’Analytics pour les fonctionnalités des communautés](/help/communities/analytics.md).

### Ajouter une Liste d&#39;Activité communautaire à une page {#adding-a-community-activity-list-to-a-page}

Pour ajouter un composant `Community Activity List` à une page en mode création, recherchez le composant.

* `Communities / Community Activity List`

et faites-le glisser sur la page.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![activité communautaire](assets/community-activity.png)

### Configuration de la Liste d&#39;Activité de la communauté {#configuring-community-activity-list}

Sélectionnez le composant `Community Activity List` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Dans l’onglet **Commentaires**, indiquez si et comment les commentaires pour les fichiers transférés apparaissent :

![propriétés](assets/activity-list-properties.png)

* **Type**

   Indiquez si les données relatives aux membres de la communauté ou au contenu généré par l’utilisateur doivent être affichées.

   Faites un choix parmi 

   * `Members`
   * `Content`

   La valeur par défaut est `Members`.

* **Titre affiché**

   Titre descriptif à afficher au-dessus des données, tel que `Trending Content`.
Par défaut, il n’existe aucun titre.

* **Nombre d’affichages**

   Nombre d&#39;éléments à liste.
La valeur par défaut est 10.

* **Type d’activité**

   Sélectionnez l&#39;une des options suivantes :

   * `Views`(visites de page)
   * `Posts`(création d’UGC)
   * `Follows`
   * `Likes`

   La valeur par défaut est Vues.

* **Période**

   Sélectionnez l&#39;une des options suivantes :

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

   Si cette option est désactivée, seules les publications de niveau supérieur sont comptabilisées. Par exemple, si le contexte est la page racine (par défaut), un `Activity Type` de `Posts` n’affichera jamais aucune activité, car il n’est pas possible de publier du contenu sur la page racine. Lorsque cette option est cochée, les nombres sur toutes les pages descendantes sont inclus.
Cette option est cochée par défaut.

### Exemple de page avec 4 composants {#example-page-with-components}

**Principaux visiteurs** config : Type = Membres, Type d’activité = Vues

**Top** Contributorsconfig : Type = Membres, type d’Activité = Publications

**Top** Contentconfig : Type = Contenu, type d&#39;Activité = Vues,

**Trending** Contentconfig : Type = Contenu, type d’Activité = Publications

![composants](assets/activity-list-components.png)

