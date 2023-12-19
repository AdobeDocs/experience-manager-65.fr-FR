---
title: Présentation d’ [!DNL Adobe Experience Manager Assets]
description: Découvrez ce qu’est la gestion des ressources numériques, ses cas d’utilisation et l’offre d’ [!DNL Adobe Experience Manager Asset] .
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 97%

---

# A propos d’[!DNL Adobe Experience Manager Assets] en tant que solution de gestion des ressources numériques (DAM) {#administering-assets}

AEM [!DNL Assets] est un outil de gestion des ressources numériques (DAM) qui fait partie de la plateforme [!DNL Experience Manager] et qui permet à votre entreprise de gérer et de diffuser des ressources numériques. Les utilisateurs d’une entreprise peuvent gérer, stocker et accéder à de nombreux types de ressources numériques, tels que des images, des vidéos, des documents, des clips audio, des fichiers 3D et des médias riches, en vue de les utiliser sur le Web, sur papier et pour la distribution numérique.

## Qu’est-ce que la gestion des ressources numériques (DAM) ? {#what-is-digital-asset-management}

[!DNL Assets] permet le partage et la diffusion des principales ressources numériques d’une organisation dans toute l’entreprise. Les utilisateurs d’une organisation peuvent archiver des ressources numériques (images, graphiques, audio, vidéos et documents, notamment), les gérer et y accéder au moyen d’une interface Web (ou d’un dossier CIFS ou WebDAV).

Les fonctionnalités d’[!DNL Assets] d’[!DNL Experience Manager] vous permettent d’effectuer les opérations suivantes :

* Ajouter et partager des images, des documents, ainsi que des fichiers audio et vidéo dans divers formats.
* Gérer les ressources en les regroupant par balise, lightbox ou étoiles (vos favoris) Ajouter des annotations aux ressources.
* Trouver des ressources en recherchant les noms de fichiers, le texte intégral des documents et en recherchant des dates, un type de document et des balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources Le contrôle de version des métadonnées se fait automatiquement en fonction de la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exécuter des fonctions d’édition d’images, telles que la mise à l’échelle et l’ajout de filtres d’images. Importer et exporter simultanément plusieurs ressources numériques à l’aide d’un dossier WebDAV ou CIFS.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources

### [!DNL Experience Manager Assets] est intégré à [!DNL Experience Manager Sites]. {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] s’intègre entièrement à [!DNL Sites] et fonctionne de manière transparente pour tous les cas d’utilisation. Par exemple, lors de la création de pages Web, les auteurs [!DNL Sites] peuvent rechercher et utiliser les ressources numériques via l’outil de recherche de contenu. L’interface utilisateur d’[!DNL Assets] est identique à celle de [!DNL Sites]. Consultez [Présentation de Sites](/help/sites-authoring/page-authoring.md) pour plus d’informations.

L’interface utilisateur de base est la même que celle de [!DNL Sites]. Consultez [Présentation de Sites](/help/sites-authoring/page-authoring.md) pour plus d’informations.

### Comparaison entre gestion des ressources numériques et composant de l’image {#digital-asset-management-versus-image-component}

Pour déterminer s’il est nécessaire de mettre une image dans le référentiel de gestion des ressources numériques ou d’utiliser un composant image, tenez compte du cycle de vie de l’image :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image.
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu Web, utilisez [!DNL Assets].

## Qu’est-ce qu’une ressource numérique ? {#what-are-digital-assets}

Une ressource est un document numérique, une image, une vidéo ou de l’audio (ou une partie) qui peut comporter plusieurs rendus. Elle peut également comporter des sous-ressources, par exemple, des calques dans un fichier Photoshop, des diapositives dans un fichier PowerPoint, des pages dans un PDF, des fichiers dans un ZIP.

Une ressource est essentiellement un fichier binaire avec des métadonnées, des rendus et des sous-ressources. Voir [Guide de performances de la gestion des ressources numériques](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le chargement et la modification d’une grande quantité de ressources (en particulier des images) peuvent avoir une incidence sur les performances de votre déploiement [!DNL Experience Manager].

### Terminologie d’[!DNL Experience Manager Assets] {#aem-assets-terminology}

Lorsque vous utilisez des ressources numériques dans [!DNL Experience Manager], il est utile de comprendre la terminologie suivante :

* **Collection** : collection de ressources basée sur un emplacement physique (dossier), des propriétés communes (dossier de recherche enregistrée) ou une sélection de l’utilisateur ou de l’utilisatrice (dossiers de lightbox).

* **Métadonnées** : les ressources [!DNL Assets] ont des métadonnées ; par exemple, l’auteur ou l’autrice, la date d’expiration et les informations DRM (Digital Rights Management). Les métadonnées sont sous contrôle d’accès. [!DNL Assets] prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : auteur ou autrice, description, date, objet, etc.
   * IPTC : comprenant l’événement, le modèle, l’emplacement, etc.
   * Gestion de contenu web : notamment les propriétés de page, l’[!UICONTROL Heure d’activation] et l’[!UICONTROL Heure de désactivation], etc.

* **Balisage** : les ressources [!DNL Assets] peuvent être balisées et classifiées. Consultez [Organisation des ressources](/help/assets/organize-assets.md).

* **Rendus** : un rendu est une représentation binaire d’une ressource. Les ressources [!DNL Assets] possèdent une représentation principale, à savoir celle du fichier chargé. Il peut y avoir un certain nombre de représentations supplémentaires qui sont créées, par exemple, par des étapes de workflow personnalisées ou lorsqu’une ressource est chargée. Les rendus peuvent avoir une taille différente, une résolution différente, un filigrane ajouté ou une autre caractéristique modifiée.

* **Versions** : le contrôle de version permet de créer un instantané des ressources numériques à un moment donné. Vous pouvez restaurer la version précédente des ressources. Consultez [Contrôle de version dans  [!DNL Assets]](manage-assets.md#asset-versioning).

* **Sous-ressources** : les sous-ressources sont des ressources qui composent une ressource (comme les calques d’un fichier [!DNL Adobe Photoshop] ou les pages d’un fichier PDF). Dans [!DNL Assets], vous pouvez gérer les sous-ressources comme vous le feriez pour les ressources.

### Travailler avec des ressources numériques {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (chargement, suppression, mise à jour, enregistrement des sous-ressources) déclenchent des workflows préconfigurés. Ils sont automatiquement activés dans [!DNL Assets] et sont décrits en détail dans les gestionnaires de médias [!DNL Assets].

Les tâches que vous pouvez réaliser avec ces workflows préconfigurés sont les suivantes :

* Enregistrer la ressource dans le référentiel ou la supprimer
* Extraire et enregistrer des métadonnées pour la ressource, avec les différents éléments de métadonnées enregistrés au format XMP
* Générer des rendus et des vignettes pour la ressource, notamment le redimensionnement et le recadrage automatiques si nécessaire
* Transcoder la ressource si nécessaire Par exemple, une vidéo pour utilisation sur appareils mobiles et sur le Web est transcodée avec 24 images par seconde et téléchargée avec 30 images par seconde. Un fichier audio pour utilisation sur appareils mobiles et sur le Web est transcodé à 128 Kbits/s et téléchargé à 192 Kbits/s.

Vous pouvez aussi appliquer des workflows manuellement. Consultez [Gestionnaires de médias Assets](media-handlers.md) pour obtenir une liste des workflows par défaut.

## [!DNL Experience Manager Assets] et [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consultez la [Bibliothèque de médias et de ressources](medialibrary.md) pour plus d’informations sur ces différences.

>[!MORELIKETHIS]
>
>* [Présentation vidéo - Experience Manager Assets en tant qu’outil de gestion des ressources numériques moderne](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Présentation des concepts de métadonnées](/help/assets/metadata-concepts.md)
