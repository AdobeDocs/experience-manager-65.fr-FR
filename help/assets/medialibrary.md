---
title: Utilisation de Media Library pour la gestion de base des ressources numériques
description: '[!DNL Experience Manager Assets] et Media Library pour la gestion des ressources.'
contentOwner: AG
role: Architect, Leader
feature: Gestion des ressources
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Utilisez Media Library pour la gestion des ressources de base {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platform offre différentes fonctionnalités de gestion des ressources. Media Library permet aux utilisateurs de charger un petit nombre de ressources dans le référentiel, de les rechercher et de les utiliser dans les pages web et d’accomplir des tâches de gestion des ressources simples sur les ressources.

Media Library est une solution légère de gestion des actifs numériques (DAM) qui complète la licence [!DNL Adobe Experience Manager Sites]. [!DNL Sites] est une offre de gestion de contenu web (WCM). Media Library fonctionne avec toutes les fonctionnalités de Experience Manager.

[!DNL Adobe Experience Manager Assets] La licence est disponible séparément pour achat. [!DNL Experience Manager Assets] permet une gestion robuste des ressources au moyen de cas d’utilisation d’entreprise, de personnalisations pour les métadonnées, les schémas, la recherche et l’interface utilisateur, et de nombreuses autres fonctionnalités au-delà de ce que Media Library fournit.

## Exigences de licence {#avail-media-library-license}

Les clients qui disposent d’une licence [!DNL Sites] ont le droit d’utiliser Media Library. Il fonctionne avec tous les composants de [!DNL Experience Manager].

Media Library est installé dans le cadre de Sites. Aucune licence ou package supplémentaire n’est nécessaire au-delà de la licence et de l’installation de Sites.

## [!DNL Assets] versus Media Library  {#assets-and-media-library}

Experience Manager Assets offre des fonctionnalités de gestion des actifs numériques d’entreprise. La fonctionnalité Assets est fournie avec [!DNL Experience Manager] dans un seul module. Toutefois, les utilisateurs qui n’ont pas acheté de licence Assets ne sont pas autorisés à utiliser les fonctionnalités avancées de gestion des actifs numériques. Sans licence Assets, seules les [fonctions Media Library](#use-media-library) sont disponibles.

Si vous souhaitez empêcher l’utilisation involontaire des fonctionnalités [!DNL Assets] que vous n’avez pas sous licence, supprimez tous les workflows, composants, taxonomies, options spécifiques à [!DNL Assets] et l’administrateur [!DNL Assets] de [!DNL Experience Manager]. Cela empêche vos utilisateurs d’utiliser accidentellement des fonctionnalités [!DNL Assets] que vous n’avez pas sous licence.

## Utiliser Media Library {#use-media-library}

Media Library couvre globalement les cas d’utilisation suivants :

* Fournissez des fonctions de gestion des actifs numériques de base pour les pages web créées à l’aide de [!DNL Adobe Experience Manager Sites].
* Formulaires adaptatifs et communications créés à l’aide de [!DNL Adobe Experience Manager Forms].
* Expériences d’écran numérique créées à l’aide de [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API HTTP REST pour les opérations sans interface utilisateur.

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

Pour utiliser la fonctionnalité Media Library, vous pouvez utiliser l’interface utilisateur par défaut [!DNL Experience Manager]. Media Library fait partie de l’installation de [!DNL Experience Manager Sites] et aucune interface distincte ni module complémentaire n’est requise. Grâce à l’interface existante, les utilisateurs de Media Library ont le droit d’accomplir les tâches suivantes :

* Créez des dossiers pour organiser les ressources.
* Chargement des ressources.
* Publication des ressources.
* Modifier, déplacer et copier des ressources.
* Parcourir, filtrer et rechercher (inclut la recherche par analogie) des ressources.
* Ajoutez des valeurs aux champs de métadonnées et modifiez-les, à l’exception du champ Balises intelligentes , disponibles par défaut dans l’onglet [!UICONTROL De base] de la page [!UICONTROL Propriétés] d’une ressource.
* Ajoutez et supprimez des rendus statiques.
* Téléchargez des dossiers, des ressources et des rendus de ressources.
* Création de versions de ressources.
* Créez et effectuez des tâches de révision sur les ressources.
* Annotation de ressources.
* Ajoutez des ressources aux pages [!DNL Sites] via l’outil de recherche de contenu.
* Utilisation [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>De nombreux cas d’utilisation avancés de la gestion des actifs numériques sont remplis par [!DNL Experience Manager Assets]. La licence Media Library vous permet de ne remplir que les cas d’utilisation répertoriés à l’aide de Media Library. Si un cas pratique n’est pas répertorié, ne l’utilisez pas avec la licence Media Library. Si vous avez des questions, contactez l’Assistance clientèle d’Adobe.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Fonctionnalités de gestion des actifs numériques dans [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=fr)
>* [[!DNL Experience Manager] 6.5 Description du produit Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Description du produit on-premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

