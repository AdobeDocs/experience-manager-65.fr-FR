---
title: Utilisation de la bibliothèque multimédia pour la gestion des ressources numériques de base
description: '[!DNL Experience Manager Assets] et la bibliothèque multimédia pour la gestion des fichiers.'
contentOwner: AG
role: Architecte, Leader
feature: Gestion des ressources
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 2%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Utiliser la bibliothèque multimédia pour la gestion de base des ressources {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] offre différentes fonctionnalités de gestion des ressources. La bibliothèque de supports permet aux utilisateurs de télécharger un petit nombre de ressources vers le référentiel, de les rechercher et de les utiliser dans les pages Web et d’accomplir des tâches simples de gestion des ressources sur les ressources.

Media Library est une solution légère de gestion des actifs numériques (DAM) qui est gratuite avec la licence [!DNL Adobe Experience Manager Sites]. [!DNL Sites] est une offre de Gestion de contenu Web (WCM). Media Library fonctionne avec toutes les fonctionnalités du Experience Manager.

[!DNL Adobe Experience Manager Assets] est disponible séparément pour l’achat. [!DNL Experience Manager Assets] permet une gestion robuste des ressources au moyen de cas d’utilisation en entreprise, de personnalisations des métadonnées, des schémas, de la recherche et de l’interface utilisateur, ainsi que de nombreuses autres fonctionnalités au-delà de ce que fournit Media Library.

## Exigences de licence {#avail-media-library-license}

Les clients disposant d’une licence [!DNL Sites] sont autorisés à utiliser la bibliothèque de médias. Il fonctionne avec tous les composants de [!DNL Experience Manager].

La bibliothèque de médias est installée dans le cadre de Sites. Aucune licence ou package supplémentaire n’est requise au-delà de la licence et de l’installation de Sites.

## [!DNL Assets] versus Media Library  {#assets-and-media-library}

Experience Manager Assets fournit une fonctionnalité de gestion des actifs numériques de niveau entreprise. La fonctionnalité Ressources est fournie avec [!DNL Experience Manager] dans un seul package. Toutefois, les utilisateurs qui n’ont pas acheté de licence Ressources ne sont pas autorisés à utiliser les fonctionnalités avancées de gestion des actifs numériques. Sans licence Ressources, seules les [fonctions de la bibliothèque de médias](#use-media-library) sont disponibles.

Si vous souhaitez empêcher l&#39;utilisation involontaire des fonctionnalités [!DNL Assets] que vous n&#39;avez pas sous licence, supprimez tous les workflows, composants, taxonomies, options spécifiques à [!DNL Assets] et l&#39;administrateur [!DNL Assets] de [!DNL Experience Manager]. Cela empêche vos utilisateurs d&#39;utiliser accidentellement des fonctionnalités [!DNL Assets] que vous n&#39;aviez pas sous licence.

## Utiliser la bibliothèque de médias {#use-media-library}

La bibliothèque de médias couvre en général les cas d’utilisation suivants :

* Fournissez des fonctions de gestion des actifs numériques de base pour les pages Web créées à l&#39;aide de [!DNL Adobe Experience Manager Sites].
* Formulaires et communications adaptatifs créés à l&#39;aide de [!DNL Adobe Experience Manager Forms].
* Expériences d’écran numérique créées à l’aide de [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API REST HTTP pour les opérations sans en-tête.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

Pour utiliser la fonctionnalité Bibliothèque de médias, vous pouvez utiliser l’interface utilisateur [!DNL Experience Manager] par défaut. Media Library fait partie de l&#39;installation de [!DNL Experience Manager Sites] et aucune interface ou module complémentaire distinct n&#39;est nécessaire. Grâce à l’interface existante, les utilisateurs de la bibliothèque de médias sont autorisés à effectuer les tâches suivantes :

* Créez des dossiers pour organiser les fichiers.
* Chargement des ressources.
* Publication des ressources.
* Modifiez, déplacez et copiez des ressources.
* Parcourir, filtrer et rechercher (y compris la recherche par analogie) les fichiers.
* Ajoutez et modifiez par défaut les valeurs des champs de métadonnées, à l’exception du champ Balises dynamiques, disponibles dans l’onglet [!UICONTROL Basic] de la page [!UICONTROL Propriétés] d’un fichier.
* Ajoutez et supprimez des rendus statiques.
* Téléchargez des dossiers, des fichiers et des rendus de fichier.
* Créez des versions de fichier.
* Créez et exécutez des tâches de révision sur les ressources.
* Annotez les ressources.
* Ajoutez des ressources sur des pages [!DNL Sites] par l’intermédiaire de l’outil de recherche de contenu.
* Utilisation [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>De nombreux cas d&#39;utilisation avancés de la gestion des actifs numériques sont traités par [!DNL Experience Manager Assets]. La licence de la bibliothèque de médias vous permet de ne traiter que les cas d’utilisation répertoriés à l’aide de la bibliothèque de médias. Si un cas d’utilisation n’est pas répertorié, ne l’utilisez pas avec la licence de la bibliothèque de médias. Si vous avez des requêtes, contactez le service à la clientèle Adobe.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Fonctionnalités de DAM dans [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=fr)
>* [[!DNL Experience Manager] 6.5 Description du produit Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Description du produit sur site](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

