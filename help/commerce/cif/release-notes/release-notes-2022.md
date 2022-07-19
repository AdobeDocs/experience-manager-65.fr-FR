---
title: Notes de mise à jour d’AEM Content and Commerce 2022
description: Notes de mise à jour d’AEM Content and Commerce 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 600a836ff7ae0be9fde107ff2828bb41e8eed98f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 29%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Magento 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Juin 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.06.xx.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| Composants principaux CIF | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| Site de référence CIF Venia | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Nouveautés {#what-is-new-june}

* Le nom du modèle est maintenant visible dans l’éditeur de sites lors de la création d’un modèle de catalogue de produits.

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

* Accès rapide au cockpit du produit : Accédez facilement à des informations détaillées sur les produits en un seul clic dans l’éditeur de sites.

   ![Activer la liste bloquée](/help/assets/CIF/enable-wishlist.png)

* Prise en charge de composants commerciaux marketing supplémentaires : Les composants peuvent être configurés pour afficher un appel à l’action de type &quot;ajouter au panier&quot; et &quot;ajouter à une liste de souhaits&quot;.

   ![Raccourci de l’éditeur de sites vers le cockpit du produit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Date de publication : Février 2022

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2022.02.24.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| Composants principaux CIF | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| Site de référence CIF Venia | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Nouveautés {#what-is-new-march}

* Version bêta : AEM le composant principal Recherche CIF prend en charge Commerce LiveSearch
* Optimisation du référencement pour les scénarios multi-magasin : Les formats d’URL pour PDP/PLP peuvent désormais être configurés au niveau du magasin via les propriétés de configuration du cloud CIF.
* Le sélecteur de produits prend en charge les produits intermédiaires par le biais d’une nouvelle option de filtre dans l’interface utilisateur.  Cela permet aux spécialistes du contenu de préparer la gestion de contenu de produit pour les lancements de produits à venir.
* Simplification de la gestion de la configuration et de la gestion des erreurs CIF à l’aide du nom de configuration du cloud CIF au lieu de l’URL du proxy de configuration
* Sélection manuelle de catégories pour la liste de produits et les composants de carrousel. Cela permet aux spécialistes du contenu d’utiliser ces composants sur les pages de contenu, en dehors de l’expérience de catalogue.

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
