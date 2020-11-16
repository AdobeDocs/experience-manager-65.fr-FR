---
title: Utilisation des balises
seo-title: Utilisation des balises
description: Les balises sont un moyen simple et rapide de classer le contenu de votre site web. Les balises sont en quelque sorte des mots-clés ou des libellés qu’il est possible d’associer à une page, à une ressource ou à tout autre type de contenu, pour permettre aux fonctions de recherche de retrouver le contenu en question et son contenu associé.
seo-description: Les balises sont un moyen simple et rapide de classer le contenu de votre site web. Les balises sont en quelque sorte des mots-clés ou des libellés qu’il est possible d’associer à une page, à une ressource ou à tout autre type de contenu, pour permettre aux fonctions de recherche de retrouver le contenu en question et son contenu associé.
uuid: 9799131f-4043-4022-a401-af8be93a1bf6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: c117b9d1-e4ae-403f-8619-6e48d424a761
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 78%

---


# Utilisation des balises{#using-tags}

Les balises sont un moyen simple et rapide de classer le contenu de votre site web. Les balises sont en quelque sorte des mots-clés ou des libellés qu’il est possible d’associer à une page, à une ressource ou à tout autre type de contenu, pour permettre aux fonctions de recherche de retrouver le contenu en question et son contenu associé.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Dix raisons d’utiliser les balises {#ten-reasons-to-use-tagging}

1. Organisation du contenu : le balisage simplifie les activités des développeurs qui peuvent rapidement organiser le contenu presque sans effort.
1. Organisation des balises : si les balises permettent d’organiser le contenu, les taxonomies/espaces de noms hiérarchiques permettent d’organiser les balises.
1. Organisation avancée des balises : dans la mesure où il est possible de créer des balises et des sous-balises, vous pouvez formuler des systèmes taxonomiques complets, couvrant des termes, des sous-termes, ainsi que leurs relations. Cela vous permet de créer une deuxième (ou une troisième) hiérarchie de contenu, parallèlement à la hiérarchie officielle.
1. Balisage contrôlé : le balisage peut être contrôlé en appliquant des autorisations aux balises et/ou aux espaces de noms pour contrôler la création et l’application de balises.
1. Balisage flexible : les balises se présentent sous de nombreuses formes et portent différents noms (tags, termes de taxonomie, catégories, libellés, etc.). Ils se distinguent par une grande souplesse au niveau de leur modèle de contenu et de leur mode d’exploitation ; par exemple, lors de la description des données démographiques cibles, de la classification et de l’évaluation du contenu, ou encore de la création d’une hiérarchie de contenu secondaire.
1. Amélioration de la recherche : dans AEM, le composant de recherche par défaut inclut les balises créées et les balises appliquées auxquelles des filtres peuvent être appliqués pour que seuls les résultats pertinents soient renvoyés.
1. Optimisation pour les moteurs de recherche : les balises appliquées sous forme de propriétés de page s’affichent automatiquement dans les métabalises de la page pour que les moteurs de recherche puissent les identifier.
1. Utilisation simple : les balises se créent facilement à partir d’un mot et en cliquant sur un bouton. Ensuite, un titre, une description et un nombre illimité de libellés peuvent être utilisés pour associer plus de termes à la balise.
1. Cohérence : le système de balisage est un composant central d’AEM. Il est utilisé par toutes les applications AEM pour catégoriser le contenu. En outre, l’API de balisage est mise à la disposition des développeurs pour leur permettre de créer des applications prenant en charge le balisage avec un accès aux mêmes taxonomies.
1. Structuration et souplesse : AEM est idéal pour travailler avec des informations structurées, grâce à l’imbrication des pages et des chemins d’accès. Il s’avère tout aussi puissant pour le traitement des informations non structurées grâce à sa fonctionnalité intégrée de recherche en texte intégral. Le balisage combine les avantages liés à la structuration et à la souplesse.

Lors de la conception de la structure du contenu d’un site et du schéma de métadonnées des ressources, pensez à l’approche légère et accessible qu’offre le balisage.

## Application de balises   {#applying-tags}

Dans l’environnement de développement de contenu, les auteurs peuvent appliquer des balises en accédant aux propriétés de la page et en entrant une ou plusieurs balises dans le champ **Balises/Mots-clés**.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the `Tags/Keywords` field pull-down to select from the list of tags permitted for the page. Tthe **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Publication de balises {#publishing-tags}

Comme c’est le cas avec les pages, vous pouvez effectuer les opérations suivantes sur les tags et espaces de noms :

**Activer**

* Activez individuellement des balises.

   A l’instar des pages, les nouvelles balises doivent être activées avant d’être disponibles dans l’environnement de publication.

>[!NOTE]
>
>Lorsque vous activez une page, une boîte de dialogue s’ouvre automatiquement et vous permet d’activer les balises non activées appartenant à la page.

**Désactiver**

* Désactivez les tags sélectionnés.

## Nuages de tags {#tag-clouds}

Les nuages de balises affichent un nuage de balises, soit pour la page active, soit pour l’ensemble du site Web, soit pour les pages les plus consultées. Les nuages de balises permettent de mettre en évidence les problèmes qui intéressent (ont été) l’utilisateur. La taille du texte utilisé pour afficher la balise varie en termes d’utilisation.

Le composant [Nuage de tags](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) (groupe de composants Général) sert à ajouter un nuage de tags à une page.

## Recherche sur des balises {#searching-on-tags}

Vous pouvez rechercher des tags dans les environnements de création et de publication.

### Utilisation d’un composant de recherche {#using-search-component}

Adding a [Search component](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) to a page provides a search capability which includes tags and can be used in both the author and publish environments.

![chlimage_1-3](assets/chlimage_1-3a.png)

