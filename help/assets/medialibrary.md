---
title: Comparaison [!DNL Assets] des offres de la bibliothèque multimédia
description: Comparez  [!DNL Experience Manager Assets] les fonctionnalités de la bibliothèque multimédia et connaissez les différences.
contentOwner: AG
role: Architecte, Leader
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 21%

---


# [!DNL Experience Manager Assets] versus  [!DNL Experience Manager] Media Library  {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] fait partie intégrante de la  [!DNL Experience Manager] plateforme. Cette intégration harmonieuse est considérée comme un avantage majeur de [!DNL Experience Manager] et garantit la cohérence de la gestion de contenu et une productivité élevée pour les auteurs de contenu.

## Qu&#39;est-ce que [!DNL Assets] ? {#what-is-aem-assets}

[!DNL Assets] est une fonctionnalité  [!DNL Experience Manager] qui vous permet de gérer des ressources numériques (images, vidéos, documents, clips audio, etc.) dans un référentiel Web. [!DNL Assets] inclut la prise en charge des métadonnées, les rendus, l’outil de recherche de ressources et l’interface d’administration.

## Qu&#39;est-ce que la [!DNL Experience Manager] bibliothèque de médias ? {#what-is-the-aem-media-library}

La [!DNL Experience Manager] bibliothèque de médias est une partie désignée du référentiel de contenu WCM [!DNL Experience Manager] dans lequel les images et les autres ressources partagées sont stockées. La bibliothèque de supports fournit des fonctionnalités de base de gestion des ressources numériques à WCM.

## Qu&#39;est-ce que je reçois de [!DNL Assets] qui ne fait pas partie de WCM ? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Les fonctionnalités uniques disponibles uniquement pour les clients de [!DNL Assets] sont les suivantes :

* Possibilité d’extraire et de modifier des métadonnées autres que le titre, les balises et la description.
* [!DNL Assets] Admin, disponible à partir de l’écran de bienvenue.
* Toutes les étapes de processus liées à la gestion des ressources numériques, telles que le transfert et l’assimilation, la suppression, la gestion des sous-ressources, la gestion des métadonnées et les profils de traitement.
* Bibliothèques incluant `dam` dans l’espace du package.

L&#39;utilisation de ces fonctionnalités requiert une licence valide de [!DNL Assets].

## [!DNL Assets] est-il disponible en tant que package distinct ? {#is-aem-assets-available-as-a-separate-package}

Non. Pour faciliter l&#39;installation et le déploiement, toutes les applications [!DNL Experience Manager] et les modules complémentaires sont fournis dans un seul pack avec toutes les fonctionnalités incluses. Cela ne signifie pas que vous avez le droit d’utiliser toutes les fonctionnalités incluses dans le module.

## Je souhaite modifier les métadonnées des ressources numériques. Ai-je besoin de [!DNL Assets] ? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si vous prévoyez de modifier les métadonnées autres que le titre, la description et les balises, vous aurez besoin d’une licence [!DNL Assets].

## Je souhaite utiliser le prédicat de catégorie sur mon site web. Ai-je besoin de [!DNL Assets] ? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Oui, le prédicat de catégorie fait partie de [!DNL Assets] et nécessite une licence [!DNL Assets].

## Je souhaite redimensionner automatiquement les images lors de l’importation. Ai-je besoin de [!DNL Assets] ? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Non. Le redimensionnement et la transformation automatique des images statiques, pilotées par le flux de travail, ainsi que la capacité de gérer les rendus font partie de [!DNL Experience Manager] Media Library. Ces fonctionnalités ne nécessitent pas de licence [!DNL Assets].

## Je souhaite redimensionner des images à l’aide d’un composant image personnalisé. Ai-je besoin de [!DNL Assets] ? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Le composant d’image fait partie de WCM. La bibliothèque graphique utilisée par le composant d&#39;image (mais également par [!DNL Assets]) fait partie de la plate-forme [!DNL Experience Manager] et ne nécessite pas de licence [!DNL Assets].

## Comment puis-je empêcher mes utilisateurs d’utiliser [!DNL Assets] si je n’avais pas de licence [!DNL Assets] ? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Vous pouvez supprimer tous les workflows, composants, taxonomies, options spécifiques à [!DNL Assets] et l&#39;administrateur [!DNL Assets] de [!DNL Experience Manager]. Cela empêche vos utilisateurs d&#39;utiliser accidentellement des fonctionnalités [!DNL Assets] que vous n&#39;aviez pas sous licence.

## Je souhaite ajouter des images à une page et recadrer ou redimensionner ces images. Ai-je besoin de [!DNL Assets] ? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Dans ce cas d’utilisation, il n’est pas nécessaire d’acheter [!DNL Assets], même l’utilisation de la bibliothèque de médias n’est pas nécessaire pour utiliser des images sur un site Web car le composant d’image dynamique permet de télécharger directement des images dans la page.

## Liste détaillée des fonctionnalités disponibles dans [!DNL Assets] par rapport à la bibliothèque de médias {#listoffeatures}

[!DNL Experience Manager Assets]

* Collections et Lightbox
* Propriétés et gestion avancées des métadonnées
* Adobe Asset Link (connexion à Creative Cloud abonnement Entreprise)
* Appli de bureau [!DNL Experience Manager]
* Profils de traitement
* [!DNL Adobe InDesign Server] intégration
* Modèles d’actifs et structure de production de catalogue
* [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]et  [!DNL Adobe InDesign] intégration
* Gestion des ressources multilingues
* Intégration PIM
* Gestion des droits
* Prise en charge Camera Raw
* Gestion et configuration des facettes de recherche
* Workflows DAM préconfigurés (par exemple, séance photo)
* Rapports et analyses des ressources appelés statistiques
* Gestion des ressources 3D
* Ressources connectées
* Brand Portal
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

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Description du produit Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Description du produit sur site](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

