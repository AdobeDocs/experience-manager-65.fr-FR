---
title: Notes de mise à jour d’AEM Content and Commerce 2021
description: Notes de mise à jour d’AEM Content and Commerce 2021
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 8%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Date de publication : Novembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0,7.1 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.6.2 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-november}

* Les auteurs peuvent prévisualiser les pages de détails du produit et de la liste de produits avec des produits/catégories avec une nouvelle option &quot;Afficher avec produit/catégorie&quot; dans l’éditeur de sites.

* Les auteurs peuvent baliser des ressources par SKU de produit et rechercher des ressources spécifiques à un produit par SKU.

* Ajout/suppression de la prise en charge des bons dans le panier.

* Ajout d’un soutien de paiement Braintree à AEM devant le magasin Venia.

### Nouveautés {#what-is-improved-november}

* Les sélecteurs de catégorie/produit ont été améliorés pour respecter la vue de magasin de Magento spécifiée dans une configuration multi-magasin.

* Composants basés sur React disponibles sous la forme d’un package npm. Cela permet aux développeurs d’utiliser le package Composants React comme dépendance pour un nouveau projet React afin de permettre la personnalisation des composants existants ou le développement de nouveaux composants React.

* Personnalisation simplifiée des requêtes GraphQL. Cela permet aux développeurs de personnaliser les composants principaux CIF avec moins de code.

## Date de publication : Octobre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0,5.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0,5.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-october}

* Modèles entièrement modifiables pour la page des détails du produit et la page de liste des produits. Les auteurs peuvent maintenant créer des modèles et faire glisser et déposer des composants de liste de produits et de détails de produits sur ces modèles. En plus d’ajouter d’autres composants, les auteurs peuvent désormais modifier la mise en page de ces modèles, leur donnant ainsi une liberté illimitée pour créer des expériences incroyables combinant du contenu marketing et commercial.

* Tous les composants principaux CIF compatibles avec l’auteur ont été améliorés pour prendre en charge [AEM système de style](https://helpx.adobe.com/fr/experience-manager/6-5/sites/authoring/using/style-system.html). Des exemples de styles ont été fournis pour le composant de liste de produits.

* Composants côté client basés sur React pour la gestion de compte. Cette version prend en charge les fonctionnalités suivantes : Connectez-vous, Mot de passe oublié et Créer un compte.

### Nouveautés {#what-is-improved-october}

* Les composants Détails du produit et Liste de produits ont été améliorés pour afficher des données factices afin de fournir aux auteurs un aperçu de la mise en page lorsque ces composants sont placés sur un modèle/une page.

* Les composants Minicart et Checkout utilisent désormais les hooks React pour une meilleure extensibilité.

## Date de publication : Septembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0,5.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-september}

* Fonction multi-modèles permettant aux auteurs d’enrichir une page de détails de produit ou une page de liste de produits spécifique. Les auteurs peuvent facilement créer une page de détails de produit ou une page de liste de produits personnalisée et utiliser le sélecteur de produit ou de catégorie pour affecter la page personnalisée à un ou plusieurs produits ou catégories spécifiques.

* Liaison multi-catalogue pour permettre aux auteurs de lier plusieurs catalogues dans la console de produit AEM. Les auteurs peuvent également modifier et afficher les propriétés de liaison du catalogue après la création de la liaison.

* Achat et panier côté client basé sur React à l’aide de GraphQL pour prendre en charge un parcours d’achat de base complet.

* Le composant Passage en caisse comprend les formulaires d’adresse, la sélection des paiements et la sélection du mode de livraison.

### Nouveautés {#what-is-improved-september}

* Les composants Teaser de produit et Carrousel de produit prennent en charge les variantes de produit.

## Date de publication : Août 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0,3.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0,3.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-august}

* L’incorporation de CIF Connector dans CIF Archetype est devenue facultative pour offrir plus de flexibilité aux développeurs.

* Composants CIF découplés de la mise en forme CSS spécifique à Venia pour permettre aux développeurs d’appliquer le style CSS de leur choix.

* Fonctionnalité multi-magasin/site pour permettre l’utilisation des composants principaux CIF sur plusieurs structures de site AEM et permettre à l’implémentation du client GraphQL sous-jacent de se connecter à différentes vues de magasin/magasin du Magento.

* Mise en cache GraphQL activée pour certaines requêtes GraphQL via le GET HTTP afin de réduire le temps de réponse.

* Vue de description du produit activée dans AEM console Produits.

* Commerce Teaser étend le composant WCM Teaser pour permettre aux auteurs d’ajouter également des champs CTA à une page de détails de produit ou à une page de liste de produits.

* Bouton permettant aux auteurs de placer sur une page AEM et de créer un lien vers une page AEM, une page des détails du produit, une page de liste de produits ou un lien externe.

### Nouveautés {#what-is-improved-august}

* La configuration de la boutique de Magento a été déplacée d’OSGi vers AEM console de produit afin de rendre la configuration de l’intégration plus conviviale en termes de création.

## Date de publication : Juillet 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0,3.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0,2.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0,2.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-july}

* Premier archétype CIF à fournir aux développeurs plusieurs options de déploiement : 1. Déployez AEM storefront Venia 2. Déployer un modèle automatique pour un nouveau projet 3. Utilisation d’éléments CIF dans un projet existant

* Navigation catalogue à plusieurs niveaux pour prendre en charge la navigation au travers des catégories et sous-catégories.

* Pagination sur les pages de catégorie pour un meilleur UX.

* Rendu côté client de l’attribut de prix dans les composants Détails du produit et Liste de produits pour prendre en charge le rendu des attributs dynamiques.

* Carrousel de produits côté serveur pour afficher la liste des produits présentés dans un style de carrousel.

* Liste des catégories proposées côté serveur pour afficher la liste des catégories sur une page AEM.

### Nouveautés {#what-is-improved-july}

* La prise en charge de Magento 2.3.2 et les correctifs liés aux propriétés du produit s’affichent dans la console du produit.

## Date de publication : Juin 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0,2.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0,1.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |

### Nouveautés {#what-is-new-june}

* AEM vitrine B2C avec style CSS Venia pour mobile en premier, page d’entrée, navigation dynamique dans les catalogues via les pages de produits et de catégories, page de recherche de produits et fonctionnalités de panier pour lancer et accélérer les projets commerciaux.

* Connecteur CIF et outils de création (console de produits, sélecteur de produits et sélecteur de catégorie) pour permettre aux auteurs de créer des expériences dans AEM avec du contenu commercial.

* Première version des composants principaux CIF compatible avec Magento 2.3.1 :
   * Détails du produit
   * Liste des produits
   * Teaser de produit
   * Navigation
   * Recherche de produit
   * Panier (REST)

