---
title: Notes de mise à jour d’AEM Content and Commerce 2021
description: Notes de mise à jour d’AEM Content and Commerce 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: b6703f519295eef728d5504360d99de69438064c
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 22%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

**Avec la version d’avril, nous avons remplacé le connecteur CIF de GitHub par le module complémentaire CIF** disponible sur la distribution de logiciels  [Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Le passage au module complémentaire présente de nombreux avantages pour les projets :

* La plupart des nouvelles fonctionnalités seront immédiatement disponibles dans AEM 6.5 (plus d’attente pour le port latéral de la fonctionnalité).
* Mise à niveau aisée vers de nouvelles versions de module complémentaire
* Prêt pour Cloud Service

L’ancien connecteur CIF AEM passe en mode de maintenance et ne doit plus être utilisé. Remplacez le connecteur CIF par le nouveau module complémentaire CIF. Un simple remplacement de package doit être possible pour la plupart des projets.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : AEM 6.5.7, schémas GraphQL Magento 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : Août 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.08.20 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.08.20.zip) |
| Composants principaux CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Site de référence CIF Venia | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Nouveautés {#what-is-new-august}

* Nouvelle interface utilisateur du sélecteur de catégorie pour une meilleure expérience utilisateur, une efficacité accrue et une meilleure prise en charge d’un catalogue de produits complexe

   ![Nouveau sélecteur de catégorie](/help/assets/CIF/category-picker.png)

* Meilleure prise en charge d’A11Y pour les composants principaux CIF

### Correctifs {#bug-fixes-august}

* Impossible de fermer l’accordéon Filtre de catégorie une fois ouvert

* Propriété &quot;Texte de l’appel à l’action&quot; rompue dans le teaser de produit.

* Erreurs JS CIF lors de l’étape de déploiement AEM CS

* Correction de l’accès aux produits bruts pour les éléments de liste de produits mappés

## Date de publication : Juillet 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.07.21 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Composants principaux CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Site de référence CIF Venia | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Nouveautés {#what-is-new-july}

* Composants principaux CIF v2
   * Simplification et amélioration des configurations pour l’URL PDP/PLP et l’optimisation du référencement
   * Indicateur visuel pour les données de produits intermédiaires en mode création pour une meilleure visibilité des modifications à venir
   * Nouveau composant sitemap pour les pages de contenu et de commerce

* Prise en charge de la [recommandation de produit Adobe Commerce Sensei, optimisée par Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) dans AEM Storefront à l’aide de recommandations prédéfinies ou créées à la volée

## Date de publication : Juin 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.06.18 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Composants principaux CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Site de référence CIF Venia | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Nouveautés {#what-is-new-june}

* Nouveaux types de données de référence de catégorie et de produit CIF pour les fragments de contenu (Incl. prise en charge de l’interface utilisateur du sélecteur de produits/catégories)
* Nouveau composant principal de fragment de contenu commercial
* Recherche commerciale en texte intégral prise en charge dans AEM serveur principal
* Les composants principaux de Commerce prennent en charge la collecte de données Adobe Commerce Sensei Recs
* Amélioration des URL compatibles avec l’optimisation pour les moteurs de recherche pour les pages de catégorie
* Prise en charge des en-têtes HTTP personnalisés par site/configuration

## Date de publication : Mai 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.05.26 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Composants principaux CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Site de référence CIF Venia | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Nouveautés {#what-is-new-may}

* Prise en charge de la pagination pour le contenu associé dans les propriétés de la console de produit

### Correctifs {#bug-fixes-may}

* Miniatures des ressources non affichées dans l’onglet Ressource des propriétés du produit

* Le chemin de navigation réinitialise les données d’aperçu dans la console de produit.

## Date de publication : Avril 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.04.22 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Composants principaux CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-april}

* Prise en charge de l’UID de catégorie : libère les intégrations commerciales tierces pour les systèmes qui utilisent des chaînes pour les ID de catégorie.

* Extension AEM pour PWA Studio, avec un exemple d’intégration

* Nouveau composant principal de navigation CIF qui étend le composant principal de navigation WCM

### Correctifs {#bug-fixes-april}

* Le champ de catégorie racine n’était pas affiché sous l’onglet Commerce dans les propriétés de page des pages de catégorie.

## Date de publication : Mars 2021 {#what-is-new-march}

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.03.25 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés

* Prise en charge de Magento 2.4.2

### Nouveautés

* Amélioration de la réutilisation du composant Détails du produit pour les pages pilotées par le contenu

* Amélioration de la mise en cache et diminution des appels d’arrière-plan pour les PDP

* Plusieurs correctifs.

## Date de publication : Février 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.24 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-february}

* Gestion de l’expérience des produits : enrichissez les pages du catalogue de produits individuellement grâce aux fragments d’expérience.

* Étendez les propriétés de la console de produit pour afficher les ressources liées et les fragments d’expérience, y compris l’action permettant d’accéder rapidement au contenu associé.

### Nouveautés  {#what-is-improved-february}

* Amélioration de la couche de données côté client avec l’URL de l’image du produit et les informations sur les catégories.

* Plusieurs correctifs.

## Date de publication : Janvier 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.02 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-january}

* Gestion de l’expérience du produit : Nouvel onglet de propriété &quot;Commerce&quot; pour les ressources et les fragments d’expérience. Cet onglet vous permet de lier les ressources et les fragments d’expérience aux produits et catégories. L’onglet affiche également des données en temps réel pour les objets de commerce liés et un lien pour afficher les détails dans la console du produit.

### Nouveautés  {#what-is-improved-january}

* Envoyez les données utilisateur après l’authentification pour Adobe de la couche de données client.

* Plusieurs correctifs.
