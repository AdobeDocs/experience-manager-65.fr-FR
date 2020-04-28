---
title: Comparaison des ressources AEM et de l’offre de la bibliothèque de médias AEM
description: Comparez les ressources AEM et les offres de la bibliothèque de médias AEM et connaissez les différences.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 476a8acbca2f498472225fe1df220f63eafe61e5

---


# Ressources AEM par rapport à la bibliothèque de médias AEM {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager (AEM) Assets fait partie intégrante de la plateforme AEM. Cette intégration parfaite est vue comme un avantage important d’AEM et garantit une homogénéité de gestion de contenu et de productivité élevée pour les auteurs de contenu. 

## Forum aux questions {#frequently-asked-questions}

### Qu’est-ce qu’AEM Assets ?{#what-is-aem-assets}

AEM Assets est une application de la plateforme AEM qui permet à nos clients de gérer leurs ressources numériques (images, documents, vidéos et clips audio) dans un référentiel basé sur le web. AEM Assets comprend la prise en charge des métadonnées, les rendus, l’outil de recherche de la gestion des actifs numériques et l’interface utilisateur d’administration d’AEM Assets.

### Qu’est-ce que la bibliothèque multimédia AEM ?{#what-is-the-aem-media-library}

La bibliothèque multimédia AEM est un élément désigné du référentiel de contenu de la gestion de contenu web d’AEM où les images et d’autres ressources partagées sont enregistrées. La bibliothèque multimédia utilise les fonctionnalités de gestion des actifs numériques de la gestion de contenu web d’AEM.

### Que m’offre AEM Assets qui ne soit pas déjà inclus dans la gestion de contenu web d’AEM ?   {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Les fonctionnalités uniques disponibles uniquement pour les clients AEM Assets sont : 

* La possibilité d’extraire et de modifier des métadonnées autres que le titre, les balises et la description
* Admin AEM Assets, disponible dans l’écran de bienvenue en sélectionnant le deuxième bouton en regard de l’administrateur du site.
* toutes les étapes du flux de travail liées à la gestion des ressources numériques, à savoir la gestion des ressources AEM, la suppression des ressources AEM, la gestion des sous-ressources AEM Assets, les métadonnées  AEM Assets .
* Les bibliothèques, y compris « dam » dans l’espace de modules

L’utilisation de ces fonctions nécessite une licence AEM Assets valide.

### AEM Assets est-il disponible en tant que module distinct ?   {#is-aem-assets-available-as-a-separate-package}

Non. Pour faciliter l’installation et le déploiement, toutes les applications et modules complémentaires d’AEM sont fournis dans un module unique dans lequel toutes les fonctionnalités sont incluses. Cela ne signifie pas que vous avez le droit d’utiliser toutes les fonctionnalités incluses dans le module.

### Je souhaite modifier les métadonnées des ressources numériques. Ai-je besoin d’AEM Assets ?   {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si vous prévoyez de modifier les métadonnées autres que le titre, la description et les balises, vous aurez besoin d’une licence AEM Assets. 

### Je souhaite utiliser le prédicat de catégorie sur mon site web. Ai-je besoin d’AEM Assets ?   {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Oui, le prédicat du  fait partie des ressources AEM et nécessite une licence AEM Assets.

### Je souhaite redimensionner automatiquement les images lors de l’importation. Ai-je besoin d’AEM Assets ?   {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Non. Le redimensionnement et la transformation automatique des images statiques pilotée par workflow, de même que la capacité de gérer les rendus sont inclus dans la bibliothèque multimédia AEM. Ces fonctionnalités ne nécessitent pas de licence AEM Assets.

### Je souhaite redimensionner des images à l’aide d’un composant image personnalisé. Ai-je besoin d’AEM Assets ?   {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Le composant image fait partie de la gestion du contenu web d’AEM. La bibliothèque d’images utilisée par le composant image (et par AEM Assets) fait partie de la plateforme AEM et ne nécessite de licence AEM Assets. 

### Comment puis-je empêcher mes utilisateurs d’utiliser AEM Assets si je ne dispose pas d’une licence AEM Assets ?{#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Vous pouvez supprimer tous les workflows, composants, taxonomies et options d’AEM Assets, ainsi que l’administrateur AEM Assets à partir d’AEM. Cela empêche vos utilisateurs d’utiliser accidentellement les fonctionnalités AEM Assets que vous n’avez pas sous licence.

### Je souhaite ajouter des images à une page et recadrer ou redimensionner ces images. Ai-je besoin d’AEM Assets ?   {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Pour ce cas d’utilisation, il n’est pas nécessaire d’acheter AEM Assets. Il n’est même pas nécessaire d’utiliser la bibliothèque multimédia pour les images d’un site web, car le composant d’image dynamique permet de transférer des images directement dans la page.

### A detailed list of features available in AEM Assets vs Media Library {#listoffeatures}

**AEM Assets**

* Collections et Lightbox
* Propriétés et gestion avancées des métadonnées
* Adobe Asset Link (connexion à Creative Cloud abonnement Entreprise)
* Application de bureau AEM
* Profils de traitement
* Intégration du serveur InDesign
* Modèles de ressources et infrastructure de producteur de catalogue
* Ressources liées Adobe Photoshop, Illustrator et InDesign
* Gestion des ressources multilingues
* Intégration PIM
* Gestion des droits
* Prise en charge de Camera RAW
* Gestion et configuration des facettes de recherche
* Workflows DAM préconfigurés (par exemple, séance photo)
* Rapports et analyses des ressources : statistiques sur les ressources
* Gestion des ressources 3D
* Ressources connectées
* Brand Portal
* Accès en libre-service
* Parcourir, rechercher et télécharger
* Partage de collections et de dossiers
* Outils d’administration
* Balises intelligentes
* Recherche visuelle
* Interface utilisateur d’administration Assets

**Media Library**

* Propriétés des métadonnées de base
* Gestion des balises
* Gestion de version
* Rendus statiques
* Projets, tâches, création de workflows
* Flux d’activités (chronologie)
* Query Builder (API)
* Intégration de Marketing Cloud
* Personnalisation et extension de l’interface utilisateur
* Commentaires et annotations
