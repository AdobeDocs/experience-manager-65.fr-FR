---
title: Notes de mise à jour AEM Content and Commerce 2021
description: Notes de mise à jour AEM Content and Commerce 2021
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 8%

---

# Présentation de la version GitHub de Commerce Integration Framework

## Date de publication : Novembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.7.1 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.6.2 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-november}

* Les auteurs peuvent prévisualisation les détails des produits et les pages de liste des produits avec des produits/catégories avec une nouvelle option &quot;Vue avec produit/catégorie&quot; dans l&#39;éditeur Sites.

* Les auteurs peuvent baliser des ressources par SKU de produit et rechercher des ressources spécifiques à un produit par SKU.

* Ajout de la prise en charge des bons d’Ajoute/suppression dans le panier.

* Un soutien de paiement Braintree a été ajouté au AEM magasin Venia.

### Améliorations {#what-is-improved-november}

* Les sélecteurs de catégories/produits sont améliorés pour respecter la vue de stockage des Magento spécifiée dans une configuration multi-boutique.

* Composants basés sur la réaction disponibles sous la forme d’un package npm. Cela permet aux développeurs d&#39;utiliser le package React Components comme une dépendance pour un nouveau projet React afin de permettre la personnalisation des composants existants ou de développer de nouveaux composants React.

* La personnalisation de la requête GraphQL est simplifiée. Cela permet aux développeurs de personnaliser les composants principaux de CIF avec moins de code.

## Date de publication : Octobre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.6.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-october}

* Modèles entièrement autorisés pour la page des détails du produit et la page de la liste du produit. Les auteurs peuvent désormais créer de nouveaux modèles et faire glisser et déposer des composants de liste de produits et de détail de produits sur ces modèles. En plus d’ajouter d’autres composants, les auteurs peuvent désormais modifier la disposition de ces modèles, ce qui leur donne une liberté illimitée de créer des expériences étonnantes combinant du contenu marketing et commercial.

* Tous les composants de base du FIC conviviaux à l&#39;auteur ont été améliorés pour prendre en charge [AEM Style System](https://helpx.adobe.com/fr/experience-manager/6-5/sites/authoring/using/style-system.html). Des exemples de styles ont été fournis pour le composant de liste de produits.

* Composants côté client basés sur la réaction pour la gestion de compte. Cette version prend en charge les fonctionnalités suivantes : Connectez-vous, Mot de passe oublié et créez un compte.

### Améliorations {#what-is-improved-october}

* Les détails du produit et les composants de la liste du produit ont été améliorés afin d’afficher les données factices afin de fournir aux auteurs une prévisualisation de la mise en page lorsque ces composants sont placés sur un modèle/une page.

* Les composants Minicart et Checkout utilisent désormais des crochets React pour améliorer l&#39;extensibilité.

## Date de publication : Septembre 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.5.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-september}

* Fonctionnalité à modèles multiples qui permet aux auteurs d’enrichir la page des détails d’un produit ou la page de la liste d’un produit. Les auteurs peuvent facilement créer une page de détails de produit ou de liste de produit personnalisée et utiliser le sélecteur de produits ou de catégories pour affecter la page personnalisée à un ou plusieurs produits ou catégories spécifiques.

* Liaison à catalogue multiple pour permettre aux auteurs de lier plusieurs catalogues dans la console de produits AEM. Les auteurs peuvent également modifier et vue les propriétés de liaison de catalogue après avoir créé la liaison.

* Réagissez en fonction du passage en caisse et du mini-panier côté client à l&#39;aide de GraphQL pour prendre en charge un parcours d&#39;achat de base complet.

* Le composant Passage en caisse comprend les formulaires d&#39;adresse, la sélection des paiements et la sélection des modes de livraison.

### Améliorations {#what-is-improved-september}

* Les composants Teaser et Carrousel de produit prennent en charge les variantes de produit.

## Date de publication : Août 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.4.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-august}

* L’intégration de CIF Connector dans CIF Archetype est devenue facultative pour offrir aux développeurs plus de flexibilité.

* Composants CIF découplés du style CSS spécifique à &quot;Venia&quot; pour permettre aux développeurs d’appliquer le style CSS de leur choix.

* Fonctionnalité multi-magasin/site permettant l&#39;utilisation des composants principaux CIF sur plusieurs structures de site AEM et permettant à l&#39;implémentation sous-jacente du client GraphQL de se connecter à différentes vues de magasin/magasin Magento.

* Mise en cache de GraphQL activée pour certaines requêtes GraphQL via le GET HTTP afin de réduire le temps de réponse.

* Vue de description de produit activée dans AEM Console Produits.

* Commerce Teaser étend le composant WCM Teaser pour permettre aux auteurs d&#39;ajouter également des champs CTA à une page de détails de produit ou à une page de liste de produit.

* Bouton permettant aux auteurs de placer un lien sur une page d’AEM et de créer un lien vers une page d’AEM, une page des détails du produit, une page de liste du produit ou un lien externe.

### Améliorations {#what-is-improved-august}

* La configuration de la boutique de Magento a été déplacée d’OSGi vers AEM Console de produit pour rendre la configuration de l’intégration plus conviviale en termes de création.

## Date de publication : Juillet 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.3.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |
| Archétype CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nouveautés {#what-is-new-july}

* Premier archétype CIF à fournir aux développeurs plusieurs options de déploiement : 1.Déployer AEM vitrine Venia 2. Déployer l&#39;échafaudage pour un nouveau projet 3. Utiliser des éléments CIF dans un projet existant

* Navigation catalogue à plusieurs niveaux pour prendre en charge la navigation dans les catégories et sous-catégories.

* Pagination sur les pages de catégorie pour un UX amélioré.

* Rendu côté client de l’attribut de prix dans les composants Détails du produit et Liste de produit pour prendre en charge le rendu des attributs dynamiques.

* Carrousel de produits côté serveur pour afficher la liste des produits présentés dans un style de carrousel.

* Liste de Catégories personnalisées côté serveur pour afficher la liste des catégories sur une page AEM.

### Améliorations {#what-is-improved-july}

* La prise en charge de Magento 2.3.2 et les correctifs liés aux propriétés du produit s’affichent dans la console du produit.

## Date de publication : Juin 2019

| GitHub | Version | Notes de mise à jour détaillées |
|:-------|:-----:|---------------------:|
| Connecteur CIF | 0.2.0 | [Notes de mise à jour](https://github.com/adobe/commerce-cif-connector/releases) |
| Composants principaux CIF | 0.1.0 | [Notes de mise à jour](https://github.com/adobe/aem-core-cif-components/releases) |

### Nouveautés {#what-is-new-june}

* AEM vitrine B2C avec style CSS Venia pour mobile en premier, landing page, navigation dynamique dans les catalogues via les pages de produits et de catégories, la page de recherche de produits et les fonctionnalités de panier pour lancer et accélérer les projets commerciaux.

* CIF Connector et outils de création (Console de produit, Sélecteur de produits et Sélecteur de Catégories) pour permettre aux auteurs de créer des expériences dans AEM avec du contenu commercial.

* Première version de CIF Core Components compatible avec Magento 2.3.1 :
   * Détails du produit
   * Liste des produits
   * Produit Teaser
   * Navigation
   * Recherche de produit
   * Panier (REST)

