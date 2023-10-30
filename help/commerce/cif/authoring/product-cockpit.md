---
title: Console du produit
description: Utiliser le cockpit de produits qui offre une vue d’ensemble unifiée des catalogues de produits liés et du contenu associé.
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 93%

---

# Console du produit {#product-cockpit}

## Vue d’ensemble {#overview}

Le cockpit de produits fournit une vue d’ensemble unifiée des catalogues de produits liés et du contenu associé. Tous les contenus associés comportent des liens pour y accéder rapidement à partir du cockpit.

Les données des produits intermédiaires incluent toute mutation future telle que de nouvelles catégories, de nouveaux produits ou des propriétés mises à jour.

>[!NOTE]
>
>Le terme catalogue de produits est interchangeable avec magasin Commerce, vue de magasin et autres expressions similaires.

## Configuration {#configuration}

Les catalogues de produits doivent être configurés dans AEM. Pour plus d’informations, consultez la section [Configurer un magasin et des catalogues](/help/commerce/cif/getting-started.md#catalog).

L’activation des fonctionnalités de catalogue intermédiaire nécessite une authentification. Pour plus d’informations, consultez la section [Prise en main](/help/commerce/cif/getting-started.md).

>[!NOTE]
>
>Les fonctionnalités de catalogue intermédiaire ne sont disponibles qu’avec Adobe Commerce et les connecteurs tiers qui prennent en charge l’authentification basée sur les jetons.

## Ouvrir le cockpit de produits {#opening-product-cockpit}

Le moyen le plus simple d’accéder au Cockpit de produit est d’utiliser le menu &quot;Commerce&quot; dans AEM menu principal. Il est également possible d’utiliser l’omni-recherche (pour rechercher Commerce) ou d’ouvrir `https://<yourAEMInstance>/commerce.html`.

![Menu AEM](/help/commerce/cif/assets/aem-menu.png)

## Naviguer dans les catalogues de produits {#browsing-product-catalogs}

Le cockpit de produits est organisé de manière hiérarchique selon la structure du catalogue de produits. Le premier niveau affiche le niveau racine du catalogue de tous les catalogues de produits configurés, y compris les métadonnées du serveur principal de Commerce.

![Catalogues configurés](/help/commerce/cif/assets/catalog-overview.png)

Cliquez sur une catégorie pour charger les enfants de la catégorie sur laquelle vous avez cliqué.

![Enfants de catégorie](/help/commerce/cif/assets/catalog-category-children.png)

Cliquez sur un produit pour charger les variations du produit si elles sont disponibles.

![Variations de produit](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>Les données du catalogue de produits dans AEM sont des données récupérées en temps réel via le point d’entrée de commerce configuré. Aucune donnée de catalogue de produits n’est stockée dans AEM.

## Effectuer une recherche dans les catalogues de produits {#searching-product-catalog}

Une recherche en texte intégral sur le catalogue de produits complet est proposée dans l’onglet de filtre de gauche pour rechercher rapidement des produits.

![recherche](/help/commerce/cif/assets/search-cockpit.png)

## Naviguer dans le catalogue de produits intermédiaires {#staged-product-catalogs}

Par défaut, le cockpit de produits affiche les données du catalogue de produits actives. L’utilisation de l’option « CATALOGUE INTERMÉDIAIRE » dans l’onglet de filtre de gauche charge le catalogue de produits pour toute date sélectionnée.

![catalogue intermédiaire](/help/commerce/cif/assets/staged-cockpit.png)

## Propriétés du catalogue de produits {#catalog-properties}

Cliquez sur l’icône des propriétés d’un produit ou d’une catégorie pour ouvrir l’affichage des propriétés de l’objet sélectionné. Ouvrir les propriétés d’une variante de produit revient à ouvrir les propriétés du produit principal.

### Onglets Commerce {#tabs}

Les onglets Général et Variante affichent les propriétés commerciales prédéfinies provenant du serveur principal de Commerce. Ces données (y compris les variantes) est en lecture seule dans AEM, car le système d’enregistrement est le serveur principal de Commerce. L’onglet Variante ne s’affiche que pour les produits comportant des variantes et présente une liste de toutes les variantes.

![propriétés de catalogue](/help/commerce/cif/assets/catalog-properties.png)

### Onglets AEM Content {#content-tabs}

Ces onglets, regroupés par type de contenu AEM (Fragments d’expérience, Fragments de contenu, Ressources associées), affichent le contenu AEM associé à l’objet commercial. L’action « Afficher les détails » ouvre un nouvel onglet de navigateur avec le contenu sélectionné.

![propriétés de contenu](/help/commerce/cif/assets/content-properties.png)
