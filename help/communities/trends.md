---
title: Tendances d’activité
seo-title: Activity Trends
description: Ajout d’un composant Liste d’activités de la communauté à une page
seo-description: Adding a Community Activity List component to a page
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 30%

---

# Tendances d’activité {#activity-trends}

## Présentation  {#introduction}

Le `Community Activity List` offre la possibilité d’ajouter des informations de tendance concernant les publications et les vues par les membres, ainsi que les publications et les vues de contenu.

Le document décrit :

* Ajouter le `Community Activity List` en un composant [site communautaire](/help/communities/overview.md#community-sites).

* Paramètres de configuration de la variable `Community Activity List` composant.

### Condition requise {#requirement}

Données pour la variable `Community Activity List` n’est disponible que si Adobe Analytics est sous licence et configuré pour le site de la communauté.

Voir [Configuration d’Analytics pour les fonctionnalités des communautés](/help/communities/analytics.md).

### Ajout d’une liste d’activités de la communauté à une page {#adding-a-community-activity-list-to-a-page}

Pour ajouter une `Community Activity List` à une page en mode création, recherchez le composant.

* `Communities / Community Activity List`

et faites-le glisser sur la page.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](/help/communities/basics.md).

Placé pour la première fois sur une page d’un site de communauté, voici à quoi ressemble le composant :

![communauté-activité](assets/community-activity.png)

### Configuration de la liste des activités de la communauté  {#configuring-community-activity-list}

Sélectionnez le `Community Activity List` pour accéder au composant et le sélectionner. `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Dans l’onglet **Commentaires**, indiquez si et comment les commentaires pour les fichiers transférés apparaissent :

![propriétés](assets/activity-list-properties.png)

* **Type**

   Indiquez s’il faut afficher les données concernant les membres de la communauté ou le contenu généré par l’utilisateur.

   Faites un choix parmi 

   * `Members`
   * `Content`

   La valeur par défaut est `Members`.

* **Titre affiché**

   Titre descriptif à afficher au-dessus des données, tel que `Trending Content`.
Par défaut, il n’existe aucun titre.

* **Nombre d’affichages**

   Nombre d’éléments à répertorier.
La valeur par défaut est 10.

* **Type d’activité**

   Sélectionnez l’une des options suivantes :

   * `Views`(visites de page)
   * `Posts`(création du contenu généré par l’utilisateur)
   * `Follows`
   * `Likes`

   La valeur par défaut est Vues.

* **Période**

   Sélectionnez l’une des options suivantes :

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

   Si cette option est désélectionnée (désactivée), seules les publications de niveau supérieur sont comptabilisées. Par exemple, si le contexte est la page racine (valeur par défaut), une `Activity Type` de `Posts` n’affichera jamais d’activité, car il n’est pas possible de publier du contenu sur la page racine. Lorsque cette option est cochée, les nombres sur toutes les pages descendantes sont inclus.
Cette option est cochée par défaut.

### Exemple de page avec 4 composants {#example-page-with-components}

**Principaux visiteurs** config : Type = Membres, Type d’activité = Vues

**Principaux contributeurs** config : Type = Membres, Type d’activité = Publications

**Contenu principal** config : Type = Contenu, Type d’activité = Vues,

**Contenu de tendance** config : Type = Contenu, Type d’activité = Publications

![components](assets/activity-list-components.png)
