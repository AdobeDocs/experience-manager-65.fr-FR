---
title: Comparaison des ressources d’Adobe Experience Manager et de l’offre de la bibliothèque de médias.
description: Comparez les ressources d’Experience Manager et les offres de la bibliothèque de supports et connaissez les différences.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 35%

---


# Fichiers Experience Manager versus Bibliothèque multimédia Experience Manager {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager Assets fait partie intégrante de la plate-forme Experience Manager. Cette intégration fluide est considérée comme un avantage majeur d’Experience Manager et garantit la cohérence de la gestion de contenu et une productivité élevée pour les auteurs de contenu.

## Forum aux questions {#frequently-asked-questions}

### What is Assets? {#what-is-aem-assets}

Les ressources sont une fonctionnalité d’Experience Manager qui permet aux utilisateurs de gérer leurs ressources numériques (images, vidéos, documents et clips audio) dans un référentiel Web. Les ressources comprennent la prise en charge des métadonnées, les rendus, l’outil de recherche et l’interface d’administration.

### Qu’est-ce que la bibliothèque de supports Experience Manager ? {#what-is-the-aem-media-library}

La bibliothèque de supports Experience Manager fait partie du référentiel de contenu WCM d’Experience Manager où sont stockées les images et les autres ressources partagées. La bibliothèque de supports fournit des fonctionnalités de base de gestion des ressources numériques à WCM.

### What do I get from Assets that is not part of WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Les fonctionnalités uniques disponibles uniquement pour les clients  Assets sont : 

* La possibilité d’extraire et de modifier des métadonnées autres que le titre, les balises et la description
* l’administrateur Ressources, disponible dans l’écran de bienvenue.
* toutes les étapes du processus liées à Digital Asset Management, telles que l’assimilation, la suppression de ressources, la gestion des sous-ressources, l’extraction des métadonnées.
* bibliothèques, y compris `dam` dans l’espace du package.

L’utilisation de ces fonctions nécessite une licence  Assets valide.

### Is Assets available as a separate Package? {#is-aem-assets-available-as-a-separate-package}

Non. Pour faciliter l’installation et le déploiement, toutes les applications et modules complémentaires d’Experience Manager sont fournis dans un seul pack avec toutes les fonctionnalités incluses. Cela ne signifie pas que vous avez le droit d’utiliser toutes les fonctionnalités incluses dans le module.

### Je souhaite modifier les métadonnées des ressources numériques. Do I need Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si vous prévoyez de modifier les métadonnées autres que le titre, la description et les balises, vous aurez besoin d’une licence  Assets. 

### Je souhaite utiliser le prédicat de catégorie sur mon site web. Do I need Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Oui, le prédicat de catégorie fait partie des ressources et nécessite une licence Ressources.

### Je souhaite redimensionner automatiquement les images lors de l’importation. Do I need Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Non. Le redimensionnement et la transformation automatique des images statiques, pilotées par le flux de travail, ainsi que la capacité de gérer les rendus font partie de la bibliothèque multimédia d’Experience Manager. Ces fonctionnalités ne nécessitent pas de licence  Assets.

### Je souhaite redimensionner des images à l’aide d’un composant image personnalisé. Do I need Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Le composant d’image fait partie de WCM. La bibliothèque graphique utilisée par le composant d’image (mais également par les ressources) fait partie de la plate-forme Experience Manager et ne nécessite pas de licence Ressources.

### Comment puis-je empêcher mes utilisateurs d’utiliser  Assets si je ne dispose pas d’une licence  Assets ?{#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Vous pouvez supprimer tous les workflows, composants, taxonomies, options et l’administrateur Ressources spécifiques à Assets d’Experience Manager. Cela évite aux utilisateurs d’utiliser accidentellement des fonctions de ressources que vous n’aviez pas sous licence.

### Je souhaite ajouter des images à une page et recadrer ou redimensionner ces images. Do I need Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Pour ce cas d’utilisation, il n’est pas nécessaire d’acheter  Assets. Il n’est même pas nécessaire d’utiliser la bibliothèque multimédia pour les images d’un site web, car le composant d’image dynamique permet de transférer des images directement dans la page.

### A detailed list of features available in Assets vs Media Library {#listoffeatures}

**Experience Manager Assets**

* Collections et Lightbox
* Propriétés et gestion avancées des métadonnées
* Adobe Asset Link (connexion à Creative Cloud abonnement Entreprise)
* Appli de bureau Experience Manager
* Profils de traitement
* [!DNL Adobe InDesign Server] intégration
* Modèles d’actifs et structure de production de catalogue
* [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]et [!DNL Adobe InDesign] intégration
* Gestion des ressources multilingues
* Intégration PIM
* Gestion des droits
* Prise en charge de Camera RAW
* Gestion et configuration des facettes de recherche
* Workflows DAM préconfigurés (par exemple, séance photo)
* rapports et analyses des ressources appelés statistiques
* Gestion des ressources 3D
* Ressources connectées
* Brand Portal
* Accès en libre-service
* Parcourir, rechercher et télécharger
* Collections et partage de dossiers
* Outils d’administration et interface
* Balisage intelligent
* Recherche visuelle

**Media Library**

* Propriétés de métadonnées de base
* Gestion des balises
* Contrôle de version
* Rendus statiques
* Projets, tâches, création de processus
* Flux d’Activité (chronologie)
* Query Builder (API)
* Intégration de Marketing Cloud
* Personnalisation et extension de l’interface utilisateur
* Commentaires et annotation
