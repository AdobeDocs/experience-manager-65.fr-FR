---
title: Notes de mise à jour d’AEM Content and Commerce 2019
description: Notes de mise à jour de Adobe Experience Manager Content and Commerce 2019.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 99%

---

# Vue d’ensemble de la version GitHub de Commerce Integration Framework

## Date de publication : novembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.7.1 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.6.2 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-november}

* Les auteurs peuvent prévisualiser les pages de détails du produit et de la liste de produits avec des produits/catégories grâce à une nouvelle option « Afficher avec produit/catégorie » dans l’éditeur de Sites.

* Les auteurs peuvent baliser des ressources par SKU de produit et rechercher des ressources spécifiques à un produit par SKU.

* Ajout/suppression de la prise en charge des bons dans le panier

* Ajout d’une assistance pour le paiement Braintree dans le storefront AEM Venia.

### Améliorations {#what-is-improved-november}

* Les sélecteurs de catégorie/produit ont été améliorés pour respecter la vue spécifiée pour la boutique Adobe Commerce dans une configuration à plusieurs boutiques.

* Les composants basés sur React sont disponibles sous la forme d’un package npm. Cela permet à l’équipe de développement d’utiliser le package Composants React comme dépendance pour un nouveau projet React afin de permettre la personnalisation des composants existants ou le développement de nouveaux composants React.

* La personnalisation des requêtes GraphQL est simplifiée. Cela permet à l’équipe de développement de personnaliser les composants principaux CIF avec moins de code.

## Date de publication : octobre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-october}

* Modèles entièrement modifiables pour la page des détails du produit et la page de liste des produits. Les auteurs et autrices peuvent maintenant créer des modèles et faire glisser et déposer des composants de liste de produits et de détails de produits sur ces modèles. En plus d’ajouter d’autres composants, les auteurs peuvent désormais modifier la mise en page de ces modèles, leur donnant ainsi une liberté illimitée pour créer des expériences incroyables combinant du contenu marketing et commercial.

* Tous les composants principaux CIF compatibles avec l’auteur ont été améliorés pour prendre en charge le [Système de style AEM](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=fr). Des exemples de styles ont été fournis pour le composant de liste de produits.

* Composants côté client basés sur React pour la gestion de compte. Cette version prend en charge les fonctionnalités suivantes : Connexion, Mot de passe oublié et Créer un compte.

### Améliorations {#what-is-improved-october}

* Les composants Détails du produit et Liste de produits ont été améliorés pour afficher des données factices afin de fournir aux auteurs un aperçu de la mise en page lorsque ces composants sont placés sur un modèle ou une page.

* Les composants Minicart et Checkout utilisent désormais les hooks React pour une meilleure extensibilité.

## Date de publication : septembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-september}

* La fonction de modèle multiple permet aux auteurs et aux autrices d’enrichir une page de détails de produits ou une page de liste de produits spécifique. Les auteurs et autrices peuvent facilement créer une page de détails de produits ou une page de liste de produits personnalisée et utiliser le sélecteur de produit ou de catégorie pour attribuer la page personnalisée à un ou plusieurs produits ou catégories spécifiques.

* Liaison multi-catalogue pour permettre aux auteurs de lier plusieurs catalogues dans la console de produit AEM. Les auteurs peuvent également modifier et afficher les propriétés de liaison du catalogue après la création de la liaison.

* Achat et panier côté client basé sur React à l’aide de GraphQL pour prendre en charge un parcours d’achat de base complet.

* Le composant Passage en caisse comprend les formulaires d’adresse, la sélection des paiements et la sélection du mode de livraison.

### Améliorations {#what-is-improved-september}

* Les composants Teaser de produit et Carrousel de produit prennent en charge les variantes de produit.

## Date de publication : août 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-august}

* L’incorporation du connecteur CIF dans l’archétype CIF est devenue facultative pour offrir plus de flexibilité à l’équipe de développement.

* Les composants CIF ont été découplés de la mise en forme CSS spécifique à Venia pour permettre à l’équipe de développement d’appliquer le style CSS de son choix.

* Fonctionnalité multi-magasin multisite pour permettre l’utilisation des composants principaux CIF sur plusieurs structures de site AEM et permettre à l’implémentation du client GraphQL sous-jacent de se connecter à différentes vues de magasin ou magasins Adobe Commerce.

* Le caching GraphQL es activé pour certaines requêtes GraphQL via GET HTTP afin de réduire le temps de réponse.

* La vue de description du produit est activée dans la console Produits d’AEM.

* Le Teaser Commerce étend le composant Teaser de gestion de contenu web pour permettre aux auteurs et autrices d’ajouter également des champs d’appel à l’action à une page de détails de produit ou à une page de liste de produits.

* Bouton pouvant être placé par les auteurs sur une page AEM et permettant de créer un lien vers une page AEM, une page des détails du produit, une page de liste de produits ou un lien externe.

### Améliorations {#what-is-improved-august}

* La configuration du magasin Adobe Commerce a été déplacée d’OSGi vers la console Produit d’AEM afin de rendre la configuration de l’intégration plus conviviale pour la création.

## Date de publication : juillet 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-july}

* Premier archétype CIF à fournir à l’équipe de développement, avec plusieurs options de déploiement : 1. Déployez me storefront AEM Venia. 2. Déployez un modèle automatique pour un nouveau projet. 3. Utilisez des éléments CIF dans un projet existant.

* Navigation catalogue à plusieurs niveaux pour prendre en charge la navigation au travers des catégories et sous-catégories.

* Pagination sur les pages de catégorie pour une meilleure expérience utilisateur.

* Rendu côté client de l’attribut de prix dans les composants Détails du produit et Liste de produits pour prendre en charge le rendu des attributs dynamiques.

* Carrousel de produits côté serveur pour afficher la liste des produits présentés dans un style de carrousel.

* Liste des catégories proposées côté serveur pour afficher la liste des catégories sur une page AEM.

### Améliorations {#what-is-improved-july}

* La prise en charge d’Adobe Commerce 2.3.2 et les correctifs liés aux propriétés du produit s’affichent dans la console du produit.

## Date de publication : juin 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.1.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |

### Nouveautés {#what-is-new-june}

* Storefront B2C AEM avec le premier style CSS Venia destiné aux terminaux mobiles, page de destination, navigation dynamique dans les catalogues via les pages de produits et de catégories, page de recherche de produits et fonctionnalités de panier pour lancer et accélérer les projets commerciaux.

* Connecteur CIF et outils de création (console de produits, sélecteur de produits et sélecteur de catégorie) pour permettre aux auteurs de créer des expériences dans AEM avec du contenu commercial.

* Première version des composants principaux CIF compatible avec Adobe Commerce 2.3.1 :
   * Détails du produit
   * Liste des produits
   * Teaser de produit
   * Navigation
   * Recherche de produit
   * Panier (REST)
