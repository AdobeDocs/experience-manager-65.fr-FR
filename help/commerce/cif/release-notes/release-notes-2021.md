---
title: Notes de mise à jour d’Adobe Experience Manager Content and Commerce 2021
description: Notes de mise à jour de Adobe Experience Manager Content and Commerce 2021.
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 99%

---

# Vue d’ensemble de la version GitHub de Commerce Integration Framework

## Présentation de la configuration système requise

Passez en revue la configuration système minimale requise dans le tableau ci-dessous pour la version CIF que vous utilisez actuellement ou que vous prévoyez d’utiliser à l’avenir.

| Composant | Configuration requise |
|:-------|:-----:|
| Module complémentaire CIF | Minimum : Adobe Experience Manager (AEM) 6.5.7, schémas GraphQL Adobe Commerce 2.3.5 |
| Composants principaux CIF | [Configuration requise](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| Archétype de projet AEM | [Configuration requise](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Date de publication : novembre 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.11.18.00 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| Composants principaux CIF | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| Site de référence CIF Venia | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Nouveautés {#what-is-new-november}

* Extension des composants myAccount, basés sur les composants extensibles Peregrine de Commerce

![Extension des composants myAccount](/help/assets/CIF/extended-myAccount-components.png)

* Les auteurs peuvent créer des recommandations de produits Commerce ad hoc à l’aide de types de recommandations supplémentaires.

* Prise en charge des cartes-cadeaux dans la vitrine AEM

## Date de publication : octobre 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.10.20.02 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| Composants principaux CIF | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| Site de référence CIF Venia | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Nouveautés {#what-is-new-october}

* Le module complémentaire CIF prend en charge la dernière version de Commerce v2.4.3 avec de nouveaux schémas et API GraphQL.

* Les auteurs peuvent ajouter des liens vers les pages de produits et de catalogues dans les champs de texte à l’aide de l’éditeur de texte enrichi (RTE). Une icône CIF a été ajoutée à la barre d’outils RTE pour ouvrir les sélecteurs afin de rechercher et sélectionner rapidement le produit ou la catégorie sans quitter le contexte.

* Les fenêtres pop-up de panier et de passage en caisse existantes ont été remplacées par des pages de panier et de passage en caisse AEM dédiées. Les composants de ces pages sont créés à l’aide des composants Peregrine extensibles d’Adobe Commerce.

* Les commerces peuvent masquer certaines catégories de catalogues de produits lors de la navigation à l’aide du serveur principal de Commerce. Le composant principal de navigation CIF respecte la configuration du serveur principal de Commerce « inclure dans le menu » pour afficher/masquer les catégories dans la navigation.

* Le storefront Venia d’AEM renvoie une erreur HTTP 404 si la catégorie ou page produit est introuvable.

## Date de publication : septembre 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.09.27 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| Composants principaux CIF | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| Site de référence CIF Venia | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Nouveautés {#what-is-new-september}

* Le nouvel onglet « Contenu commercial associé » dans l’éditeur de sites améliore l’efficacité de la création en permettant d’accéder rapidement au contenu produit AEM approprié pour le contexte actuel.

  ![Contenu commercial associé](/help/assets/CIF/associated-commerce-content.png)

* Amélioration de l’interface utilisateur du sélecteur de produits pour une meilleure expérience client, et optimisation de l’efficacité et de la prise en charge du catalogue de produits complexe

  ![Nouveau sélecteur de produits](/help/assets/CIF/product-picker.png)

* Respect de la propriété « include_in_menu » dans le composant de navigation

### Correctifs {#bug-fixes-september}

* La purge du cache du menu ne fonctionne pas comme prévu.

* Erreurs JS lors de l’étape de déploiement d’AEM CS et lorsque vous n’utilisez pas les composants côté client.

* Impossible de créer une configuration cloud CIF dans les dossiers comportant un nœud sling:configs

## Date de publication : août 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.09.02 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| Composants principaux CIF | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| Site de référence CIF Venia | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Nouveautés {#what-is-new-august}

* Nouvelle interface utilisateur du sélecteur de catégorie pour une meilleure expérience client, une efficacité améliorée et une meilleure prise en charge du catalogue de produits complexe

  ![Nouveau sélecteur de catégorie](/help/assets/CIF/category-picker.png)

* Meilleure prise en charge d’A11Y pour les composants principaux CIF

### Correctifs {#bug-fixes-august}

* Impossible de fermer l’accordéon Filtre de catégorie une fois ouvert

* Propriété « Texte de l’appel à l’action » rompue dans le Teaser de produit

* Erreurs JS CIF lors de l’étape de déploiement CS AEM

* Correction de l’accès aux produits bruts pour les éléments de liste de produits mappés

## Date de publication : juillet 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.07.21 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| Composants principaux CIF | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| Site de référence CIF Venia | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Nouveautés {#what-is-new-july}

* Composants principaux CIF v2
   * Simplification et amélioration des configurations pour URL PDP/PLP et SEO
   * Indicateur visuel pour les données de produits évaluées en mode création pour une meilleure visibilité des modifications à venir
   * Nouveau composant sitemap pour pages de contenu et de commerce

* Prise en charge de la [recommandation de produit Adobe Commerce Sensei, optimisée par Adobe Sensei](https://business.adobe.com/fr/products/magento/product-recommendations.html) dans le storefront AEM à l’aide de recommandations prédéfinies ou créées à la volée

## Date de publication : juin 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.06.18 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| Composants principaux CIF | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| Site de référence CIF Venia | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Nouveautés {#what-is-new-june}

* Nouveaux types de données de référence de catégorie et de produit CIF pour les fragments de contenu (y compris prise en charge de l’interface utilisateur du sélecteur de produits/catégories)
* Nouveau composant principal de fragment de contenu Commerce
* Recherche commerciale en texte intégral prise en charge dans AEM serveur principal
* Les composants principaux de Commerce prennent en charge la collecte de données de recommandations Adobe Commerce
* Amélioration des URL compatibles avec les moteurs de recherche pour les pages de catégorie
* Prise en charge des en-têtes HTTP personnalisés par site/configuration

## Date de publication : mai 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.05.26 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| Composants principaux CIF | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| Site de référence CIF Venia | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Nouveautés {#what-is-new-may}

* Prise en charge de la pagination pour le contenu associé dans les propriétés de la console de produit

### Correctifs {#bug-fixes-may}

* Miniatures des ressources non affichées dans l’onglet Ressource des propriétés du produit

* Le chemin de navigation réinitialise les données d’aperçu dans la console de produit

## Date de publication : avril 2021

| Composant | Version | Détails |
|:-------|:-----:|---------------------:|
| Module complémentaire CIF | 2021.04.22 | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| Composants principaux CIF | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-april}

* Prise en charge de l’UID de catégorie – Cette option ouvre les intégrations commerciales tierces pour les systèmes qui utilisent des chaînes pour les ID de catégorie.

* Extension AEM pour PWA Studio, avec un exemple d’intégration

* Nouveau composant principal de navigation CIF qui étend le composant principal de navigation WCM

### Correctifs {#bug-fixes-april}

* Le champ de catégorie racine n’était pas affiché sous l’onglet Commerce dans les propriétés de page des pages de catégorie.

## Date de publication : mars 2021 {#what-is-new-march}

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.9.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.03.25 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés

* Prise en charge d’Adobe Commerce 2.4.2

### Améliorations

* Amélioration de la réutilisation du composant Détails du produit pour les pages pilotées par le contenu

* Amélioration de la mise en cache et diminution des appels d’arrière-plan pour les PDP

* Plusieurs correctifs de bogues.

## Date de publication : février 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.8.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.24 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-february}

* Gestion de l’expérience des produits : enrichissez les pages du catalogue de produits individuellement grâce aux fragments d’expérience.

* Propriétés étendues de la console de produits pour afficher les ressources liées et les fragments d’expérience, y compris les actions permettant d’accéder rapidement au contenu associé.

### Améliorations  {#what-is-improved-february}

* Amélioration de la couche de données côté client avec l’URL de l’image du produit et les informations sur les catégories.

* Plusieurs correctifs de bogues.

## Date de publication : janvier 2021

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 1.7.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Site de référence CIF Venia | 2021.02.02 | [Notes de mise à jour](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nouveautés {#what-is-new-january}

* Gestion de l’expérience des produits : nouvel onglet de propriétés Commerce pour les ressources et les fragments d’expérience. Cet onglet vous permet de lier les ressources et les fragments d’expérience aux produits et catégories. L’onglet affiche également des données en temps réel pour les objets Commerce liés ainsi qu’un lien permettant d’afficher des détails dans la console du produit.

### Améliorations  {#what-is-improved-january}

* Envoyez les données utilisateur après l’authentification à la couche de données client Adobe.

* Plusieurs correctifs de bogues.
