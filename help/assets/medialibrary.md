---
title: ' [!DNL Assets] Comparaison des offres de la bibliothèque de supports'
description: Comparaison [!DNL Experience Manager Assets] des offres de la bibliothèque de médias et connaissance des différences.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 24%

---


# [!DNL Experience Manager Assets] versus [!DNL Experience Manager] Media Library {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] fait partie intégrante de la [!DNL Experience Manager] plateforme. This smooth integration is seen as a major advantage of [!DNL Experience Manager] and ensures consistency in content management and high productivity for content authors.

## Forum aux questions {#frequently-asked-questions}

### What is [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] est une fonctionnalité de [!DNL Experience Manager] qui permet aux utilisateurs de gérer leurs ressources numériques (images, vidéos, documents et clips audio) dans un référentiel Web. [!DNL Assets] inclut la prise en charge des métadonnées, les rendus, l’outil de recherche et l’interface d’administration.

### What is the [!DNL Experience Manager] Media Library? {#what-is-the-aem-media-library}

The [!DNL Experience Manager] Media Library is a designated part of the [!DNL Experience Manager] WCM content repository where images and other shared resources are stored. La bibliothèque de supports fournit des fonctionnalités de base de gestion des ressources numériques à WCM.

### What do I get from [!DNL Assets] that is not part of WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Unique features that are only available to customers of [!DNL Assets] are:

* La possibilité d’extraire et de modifier des métadonnées autres que le titre, les balises et la description
* l’ [!DNL Assets] administrateur, disponible à partir de l’écran de bienvenue.
* toutes les étapes du processus liées à Digital Asset Management, telles que l’assimilation, la suppression de ressources, la gestion des sous-ressources, l’extraction des métadonnées.
* bibliothèques, y compris `dam` dans l’espace du package.

Using these features requires a valid license of [!DNL Assets].

### Is [!DNL Assets] available as a separate Package? {#is-aem-assets-available-as-a-separate-package}

Non. To ease installation and deployment, all [!DNL Experience Manager] applications and add-ons are delivered in one single package with all functionality included. Cela ne signifie pas que vous avez le droit d’utiliser toutes les fonctionnalités incluses dans le module.

### Je souhaite modifier les métadonnées des ressources numériques. Ai-je besoin [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si vous prévoyez de modifier les métadonnées autres que le titre, la description et les balises, vous aurez besoin d’une licence [!DNL Assets].

### Je souhaite utiliser le prédicat de catégorie sur mon site web. Ai-je besoin [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Oui, le prédicat de la catégorie fait partie de [!DNL Assets] et nécessite une [!DNL Assets] licence.

### Je souhaite redimensionner automatiquement les images lors de l’importation. Ai-je besoin [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Non. Resizing and automatic workflow-driven transformation of static images as well as the ability to manage renditions are part of [!DNL Experience Manager] Media Library. These features do not require an [!DNL Assets] license.

### Je souhaite redimensionner des images à l’aide d’un composant image personnalisé. Ai-je besoin [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Le composant d’image fait partie de WCM. The graphics library that is being used by the image component (but also by [!DNL Assets]) is part of the [!DNL Experience Manager] platform and does not require an [!DNL Assets] license.

### How can I prevent my users from using [!DNL Assets] if I did not license [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

You can remove all [!DNL Assets]-specific workflows, components, taxonomies, options and the [!DNL Assets] admin from [!DNL Experience Manager]. Doing so prevents your users from accidentally using [!DNL Assets] features that you did not license.

### Je souhaite ajouter des images à une page et recadrer ou redimensionner ces images. Do I need Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

For this use case it is not required to buy [!DNL Assets], even the use of the Media Library is not required to use images on a website as the smart image component allows uploading images directly into the page.

### A detailed list of features available in [!DNL Assets] vs Media Library {#listoffeatures}

**Experience Manager Assets**

* Collections et Lightbox
* Propriétés et gestion avancées des métadonnées
* Adobe Asset Link (connexion à Creative Cloud abonnement Entreprise)
* [!DNL Experience Manager] application de bureau
* Profils de traitement
* [!DNL Adobe InDesign Server] intégration
* Modèles d’actifs et structure de production de catalogue
* [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]et [!DNL Adobe InDesign] intégration
* Gestion des ressources multilingues
* Intégration PIM
* Gestion des droits
* Prise en charge Camera Raw
* Gestion et configuration des facettes de recherche
* Workflows DAM préconfigurés (par exemple, séance photo)
* Rapports et analyses des ressources appelés statistiques
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
* Intégration Marketing Cloud
* Personnalisation et extension de l’interface utilisateur
* Commentaires et annotation
