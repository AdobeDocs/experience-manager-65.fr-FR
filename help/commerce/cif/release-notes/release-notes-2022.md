---
title: Notes de mise à jour d’AEM Content and Commerce 2022
description: Notes de mise à jour d’AEM Content and Commerce 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 0fdff88695646603cec120d25f156f8c918686df
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 48%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Magento 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Septembre 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.09.20.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| Composants principaux CIF | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| Site de référence CIF Venia | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Nouveautés {#what-is-new-september}

* Les auteurs peuvent enrichir dynamiquement des listes de produits avec des fragments d’expérience (par exemple : Placer une bannière entre les listes de produits)
* Le composant Liste prend en charge les pages de produit/catégorie associées pour afficher dynamiquement les pages associées.
* Prise en charge des composants Peregrine 12.5
* Prise en charge du chargement des prix côté client dans le teaser de produit et le carrousel

## Date de publication : Juillet 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.08.02.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Nouveautés {#what-is-new-july}

* Association des pages d’AEM aux produits et aux catégories via AEM propriétés de page plus aperçu dans le cockpit du produit
   ![association de page du cockpit du produit](/help/assets/CIF/product_cockpit_page_association.png)

## Date de publication : Juin 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.07.05.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Composants principaux CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Site de référence CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Nouveautés {#what-is-new-june}

* L’enrichissement du catalogue de produits prend désormais en charge AEM pages. Cela permet aux auteurs de gérer l’association page - produit.

* Diverses améliorations du composant principal CIF

### Correctifs {#bug-fixes-june}

* Ajout d’un jeton de connexion à la récupération de prix côté client

* Composant de page incorrect dans le lecteur de données

## Date de publication : Mai 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.05.31.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Composants principaux CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Site de référence CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Nouveautés {#what-is-new-may}

* Nouvelle page des propriétés du cockpit du produit pour un aperçu meilleur et simplifié

![Présentation des propriétés du cockpit du produit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Amélioration de la compatibilité et de la robustesse pour les connecteurs tiers sur I/O Runtime

* Amélioration de la prise en charge des remplacements de la configuration du client GQL (par exemple, définir le comportement de mise en cache personnalisée)

### Correctifs {#bug-fixes-may}

* Le champ de sélecteur de produits à plusieurs valeurs affiche le deuxième et les produits supplémentaires comme non valides

* Le sélecteur de produit est parfois masqué derrière les composants.

## Date de publication : Avril 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.04.28.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Composants principaux CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Site de référence CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Nouveautés {#what-is-new-april}

* Accès rapide au cockpit du produit : accédez facilement à des informations détaillées sur les produits en un seul clic dans l’éditeur de sites.

   ![Activer la liste de souhaits](/help/assets/CIF/enable-wishlist.png)

* Prise en charge de composants commerciaux marketing supplémentaires : les composants peuvent être configurés pour afficher un appel à l’action de type « ajouter au panier » et « ajouter à une liste de souhaits ».

   ![Raccourci de l’éditeur de sites vers le cockpit du produit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Date de publication : Février 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.02.24.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Composants principaux CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Site de référence CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Nouveautés {#what-is-new-march}

* Version bêta : AEM le composant principal Recherche CIF prend en charge Commerce LiveSearch
* Optimisation du référencement pour les scénarios multi-magasin : les formats d’URL pour les pages d’information ou de recensement produit peuvent désormais être configurés au niveau du magasin grâce aux propriétés de configuration cloud CIF.
* Le sélecteur de produits prend en charge les produits intermédiaires par le biais d’une nouvelle option de filtre dans l’interface utilisateur. Il permet aux spécialistes du contenu de préparer la gestion de contenu de produit pour les lancements de produits à venir.
* Simplification de la gestion de la configuration et des erreurs CIF à l’aide du nom de configuration cloud CIF au lieu de l’URL du proxy de configuration
* Sélection manuelle de la catégorie de composant de Liste de produits et de Carrousel. Elle permet aux spécialistes du contenu d’utiliser ces composants sur les pages de contenu, en dehors du catalogue..

## Date de publication : Janvier 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.01.20.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Composants principaux CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Site de référence CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Nouveautés {#what-is-new-january}

* Amélioration des composants myAccount
* Le composant de recommandation de produit prend en charge d’autres types de page (page d’accueil, panier, confirmation de commande).
* **Liste de souhaits**
   * Les visiteurs connectés peuvent ajouter des produits à une liste de souhaits.
   * La gestion de la liste des souhaits et de ses produits est possible via myAccount
   * Le bouton « Ajouter à la liste de souhaits » peut être activé/désactivé au niveau des composants par une stratégie (par exemple un teaser de produit ou les informations de produit).
   * Disponible en tant que composant principal et dans AEM Venia Storefront

![Liste de souhaits](/help/assets/CIF/wishlist.png)
