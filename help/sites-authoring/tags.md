---
title: Utilisation des balises
seo-title: Utilisation des balises
description: Les balises sont un moyen simple et rapide de classer le contenu de votre site web.
seo-description: Les balises sont un moyen simple et rapide de classer le contenu de votre site web.
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Utilisation des balises{#using-tags}

Les balises sont un moyen simple et rapide de classer le contenu de votre site web. Les balises sont en quelque sorte des mots-clés ou des libellés qu’il est possible d’associer à une page, à une ressource ou à tout autre type de contenu, pour permettre aux fonctions de recherche de retrouver le contenu en question et son contenu associé.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Dix raisons d’utiliser les balises {#ten-reasons-to-use-tagging}

1. **Organisation du contenu** - Le balisage simplifie la vie des auteurs, qui peuvent rapidement organiser le contenu sans effort.
1. **Organisation des balises** - Tandis que les balises organisent le contenu, les taxonomies/espaces de noms hiérarchiques organisent les balises.
1. **Balises** fortement organisées - Avec la possibilité de créer des balises et des sous-balises, il devient possible d&#39;exprimer des systèmes taxonomiques entiers, couvrant des termes, des sous-termes et leurs relations. Cela vous permet de créer une deuxième (ou une troisième) hiérarchie de contenu, parallèlement à la hiérarchie officielle.
1. **Balisage** contrôlé : le balisage peut être contrôlé en appliquant des autorisations aux balises et/ou aux espaces de noms pour contrôler la création et l’application des balises.
1. **Balisage** flexible : les balises ont de nombreux noms et visages : balises, termes de taxonomie, catégories, étiquettes et bien d’autres choses encore. Ils se distinguent par une grande souplesse au niveau de leur modèle de contenu et de leur mode d’exploitation ; par exemple, lors de la description des données démographiques cibles, de la classification et de l’évaluation du contenu, ou encore de la création d’une hiérarchie de contenu secondaire.
1. **Amélioration de la recherche** : le composant de recherche par défaut d’AEM inclut en général les balises créées et les balises appliquées auxquelles des filtres peuvent être appliqués pour restreindre les résultats aux balises pertinentes.
1. **Activation** du référencement : les balises appliquées en tant que propriétés de page s’affichent automatiquement dans les métadonnées de la page afin de les rendre visibles aux moteurs de recherche.
1. **Sophistication** simple - Les balises peuvent simplement être créées à partir d&#39;un mot et d&#39;un bouton. Ensuite, un titre, une description et un nombre illimité de libellés peuvent être utilisés pour associer plus de termes à la balise.
1. **Cohérence** principale - Le système de balisage est un composant principal d’AEM et est utilisé par toutes les fonctionnalités d’AEM pour classer le contenu par catégorie. En outre, l’API de balisage est mise à la disposition des développeurs pour leur permettre de créer des applications prenant en charge le balisage avec un accès aux mêmes taxonomies.
1. **Combine la structure et la flexibilité** : AEM est idéal pour travailler avec des informations structurées, en raison de l’imbrication de pages et de chemins. Il s’avère tout aussi puissant pour le traitement des informations non structurées grâce à sa fonctionnalité intégrée de recherche en texte intégral. Le balisage combine les avantages liés à la structuration et à la souplesse.

Lors de la conception de la structure du contenu d’un site et du schéma de métadonnées des ressources, pensez à l’approche légère et accessible qu’offre le balisage.

## Application de balises {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window. The **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-41](assets/chlimage_1-41.png)

### Publication de balises {#publishing-tags}

Comme c’est le cas avec les pages, vous pouvez effectuer les opérations suivantes sur les tags et espaces de noms :

**Activer**

* Activez des tags individuels.

   A l’instar des pages, les nouveaux tags doivent être activés avant d’être disponibles dans l’environnement de publication.

>[!NOTE]
>
>Lorsque vous activez une page, une boîte de dialogue s’ouvre automatiquement et vous permet d’activer les balises non activées appartenant à la page.

**Désactiver**

* Désactivez les tags sélectionnés.
