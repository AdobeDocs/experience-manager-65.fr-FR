---
title: Notes de mise à jour d’AEM Content and Commerce 2022
description: Notes de mise à jour d’Adobe Experience Manager Content and Commerce 2021
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 100%

---

# Vue d’ensemble de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Adobe Commerce 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : septembre 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.09.20.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| Composants principaux CIF | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| Site de référence CIF Venia | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Nouveautés {#what-is-new-september}

* Les auteurs et autrices peuvent enrichir dynamiquement des listes de produits avec des fragments d’expérience (par exemple : placer une bannière entre les listes de produits).
* Le composant Liste prend en charge les pages de produit/catégorie associées pour afficher dynamiquement les pages associées.
* Prise en charge des composants Peregrine 12.5
* Prise en charge du chargement des prix côté client dans le teaser de produit et le carrousel

## Date de publication : juillet 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.08.02.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Nouveautés {#what-is-new-july}

* Association des pages AEM aux produits et aux catégories à l’aide des propriétés de page AEM et aperçu dans le cockpit de produits
  ![Association de page du cockpit de produits](/help/assets/CIF/product_cockpit_page_association.png)

## Date de publication : juin 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.07.05.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Composants principaux CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Site de référence CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Nouveautés {#what-is-new-june}

* L’enrichissement du catalogue de produits prend désormais en charge les pages AEM, ce qui permet aux créateurs et aux créatrices de gérer l’association page-produit.

* Diverses améliorations du composant principal CIF

### Correctifs {#bug-fixes-june}

* Ajouter un jeton de connexion à la récupération des prix côté client

* Composant de page incorrect dans la couche de données.

## Date de publication : mai 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.05.31.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| Composants principaux CIF | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| Site de référence CIF Venia | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Nouveautés {#what-is-new-may}

* Nouvelle page des propriétés du cockpit du produit pour simplifier et améliorer l’aperçu

![Présentation des propriétés du cockpit du produit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Amélioration de la compatibilité et de la robustesse pour les connecteurs tiers sur I/O Runtime

* Amélioration de la prise en charge des remplacements de la configuration du client GQL (par exemple, pour définir le comportement de mise en cache personnalisée)

### Correctifs {#bug-fixes-may}

* Le champ de sélecteur de produits à plusieurs valeurs affiche le deuxième produit et les produits supplémentaires comme non valides.

* Le sélecteur de produit est parfois masqué derrière les composants.

## Date de publication : avril 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.04.28.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| Composants principaux CIF | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| Site de référence CIF Venia | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Nouveautés {#what-is-new-april}

* Accès rapide au cockpit du produit : accédez facilement à des informations détaillées sur les produits en un seul clic dans l’éditeur de Sites.

  ![Activation de la liste de souhaits](/help/assets/CIF/enable-wishlist.png)

* Prise en charge de composants commerciaux marketing supplémentaires : les composants peuvent être configurés pour afficher un appel à l’action de type « Ajouter au panier » et « Ajouter à une liste de souhaits ».

  ![Raccourci de l’éditeur de Sites vers le cockpit du produit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Date de publication : février 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.02.24.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Composants principaux CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Site de référence CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Nouveautés {#what-is-new-march}

* Version bêta : le composant principal de Recherche CIF AEM prend en charge Commerce LiveSearch.
* Optimisation du référencement pour les scénarios multi-magasin : les formats d’URL pour PDP/PLP peuvent désormais être configurés au niveau du magasin via les propriétés de configuration cloud CIF.
* Le sélecteur de produit prend en charge les produits intermédiaires par le biais de la nouvelle option de filtre de l’interface utilisateur. Il permet aux personnes spécialistes du contenu de préparer la gestion de contenu de produit pour les lancements de produits à venir.
* Simplification de la gestion de la configuration et de la gestion des erreurs CIF à l’aide du nom de configuration cloud CIF au lieu de l’URL du proxy de configuration.
* Sélection manuelle de catégories pour la liste de produits et les composants de carrousel. Elle permet aux personnes spécialistes du contenu d’utiliser ces composants sur les pages de contenu, en dehors du catalogue.

## Date de publication : janvier 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.01.20.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| Composants principaux CIF | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| Site de référence CIF Venia | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Nouveautés {#what-is-new-january}

* Amélioration des composants myAccount
* Le composant de recommandation de produit prend en charge d’autres types de page (page d’accueil, panier, confirmation de commande).
* **Liste de souhaits**
   * Les visiteurs connectés peuvent ajouter des produits à une liste de souhaits.
   * La gestion de la liste des souhaits et de ses produits est possible via Mon compte.
   * Le bouton « Ajouter à la liste de souhaits » peut être activé/désactivé au niveau des composants par une politique (par exemple un teaser de produit ou les informations de produit).
   * Disponible en tant que composant principal et dans AEM Venia Storefront

![Liste de souhaits](/help/assets/CIF/wishlist.png)
