---
title: Utilisation de Media Library pour la gestion de base des ressources numériques
description: "[!DNL Experience Manager Assets] et Media Library pour la gestion des ressources."
contentOwner: AG
role: Architect, Leader
feature: Asset Management
exl-id: e10d632d-1d90-4f28-8617-95ee41602997
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '555'
ht-degree: 100%

---


# Utilisation de Media Library pour la gestion de base des ressources {#manage-assets-using-media-library}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=fr) |
| AEM 6.5 | Cet article |

La plateforme [!DNL Adobe Experience Manager] offre différentes fonctionnalités de gestion des ressources. Media Library permet aux utilisateurs de charger un petit nombre de ressources dans le référentiel, de les rechercher et de les utiliser dans les pages web et de réaliser des tâches de gestion simples des ressources.

Media Library est une solution légère de gestion des actifs numériques (DAM) qui complète la licence [!DNL Adobe Experience Manager Sites]. [!DNL Sites] est une offre de gestion de contenu web (WCM). Media Library fonctionne avec toutes les fonctionnalités d’Experience Manager.

La licence [!DNL Adobe Experience Manager Assets] est disponible séparément à l’achat. [!DNL Experience Manager Assets] permet une gestion robuste des ressources au moyen de cas d’utilisation d’entreprise, de personnalisations des métadonnées, de schémas, de recherches et d’une interface utilisateur, ainsi que de nombreuses autres fonctionnalités supplémentaires au-delà de celles de Media Library.

## Exigences de licence {#avail-media-library-license}

Les clients qui disposent d’une licence [!DNL Sites] ont le droit d’utiliser Media Library. La fonctionnalité coopère avec tous les composants d’[!DNL Experience Manager].

Media Library est installé dans le cadre de Sites. Aucune licence ou package supplémentaire n’est nécessaire au-delà de la licence et de l’installation de Sites.

## [!DNL Assets] face à Media Library {#assets-and-media-library}

Experience Manager Assets offre des fonctionnalités de gestion des actifs numériques d’entreprise. La fonctionnalité Assets est fournie avec [!DNL Experience Manager] dans un seul package. Toutefois, les utilisateurs qui n’ont pas acheté de licence Assets ne sont pas autorisés à utiliser les fonctionnalités avancées de gestion des actifs numériques. Sans licence Assets, seules les [fonctions Media Library](#use-media-library) sont disponibles.

Si vous souhaitez empêcher l’utilisation involontaire des fonctionnalités [!DNL Assets] qui ne font pas partie de la licence, supprimez tous les workflows, composants, taxonomies, options spécifiques à [!DNL Assets] et l’administrateur [!DNL Assets] d’[!DNL Experience Manager]. Cela empêche vos utilisateurs d’utiliser accidentellement des fonctionnalités d’[!DNL Assets] pour lesquelles vous ne disposez pas de licence.

## Utilisation de Media Library {#use-media-library}

Media Library fournit des fonctions de gestion des ressources numériques de base pour les cas d’utilisation suivants :

* Pages web créées à l’aide d’[!DNL Adobe Experience Manager Sites].
* Formulaires adaptatifs et communications créés à l’aide d’[!DNL Adobe Experience Manager Forms].
* Expériences d’écran numérique créées à l’aide d’[!DNL Adobe Experience Manager Screens].
* API HTTP REST [!DNL Assets] pour les opérations en mode découplé.

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Pour utiliser la fonctionnalité Media Library, vous pouvez utiliser l’interface utilisateur par défaut d’[!DNL Experience Manager]. Media Library fait partie de l’installation d’[!DNL Experience Manager Sites] et aucune interface distincte ni module complémentaire ne sont requis. Grâce à l’interface existante, les utilisateurs de Media Library ont le droit d’accomplir les tâches suivantes :

* Créer des dossiers pour organiser les ressources.
* Charger des ressources.
* Publier des ressources.
* Modifier, déplacer et copier des ressources.
* Parcourir, filtrer et rechercher (inclut la recherche par analogie) des ressources.
* Ajouter des valeurs aux champs de métadonnées et les modifier, à l’exception du champ Balises intelligentes, disponibles par défaut dans l’onglet [!UICONTROL De base] de la page [!UICONTROL Propriétés] d’une ressource.
* Ajouter et supprimer des rendus statiques.
* Télécharger des dossiers, des ressources et des rendus de ressources.
* Créer des versions de ressources.
* Créer et effectuer des tâches de révision sur les ressources.
* Appliquer des annotations à des ressources.
* Ajouter des ressources aux pages [!DNL Sites] via l’outil de recherche de contenu.
* Utilisation [!DNL Content Fragments].
* Utilisation des API HTTP REST et GraphQL pour les [!DNL Content Fragments] et les ressources multimédias référencées, sous licence Sites.
* Intégration d’Experience Cloud.
* Personnalisez et étendez l’interface utilisateur de gestion des ressources.
* Accédez à Query Builder (API) pour étendre la fonctionnalité de recherche.
* Créez des balises statiques.
* Créez des projets et des tâches.
* Flux d’activités (journal).
* Commentaires et annotations.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>De nombreux cas d’utilisation avancés de la gestion des actifs numériques sont remplis par [!DNL Experience Manager Assets]. La licence Media Library vous permet de ne répondre qu’aux cas d’utilisation répertoriés à l’aide de Media Library. Si un cas pratique n’est pas répertorié, ne l’utilisez pas avec la licence Media Library. Si vous avez des questions, contactez l’Assistance clientèle d’Adobe.

Notez que vous ne pouvez pas utiliser de balises intelligentes, de lien [!DNL Asset], de sélecteur [!DNL Asset], de balisage en masse, des workflows de modification des ressources ou l’interface utilisateur standard [!DNL Adobe Experience Manager] pour accéder à Media Library sans licence [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [Fonctionnalités de gestion des ressources numériques dans  [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/home.html?lang=fr)
>* Description du produit [[!DNL Experience Manager]  6.5 Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* Description du produit [[!DNL Experience Manager]  6.5 on-premise](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-on-premise.html)
