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
ht-degree: 67%

---

# A propos d’[!DNL Adobe Experience Manager Assets] en tant que solution de gestion des ressources numériques (DAM) {#administering-assets}

AEM [!DNL Assets] est un outil de gestion des ressources numériques (DAM) qui fait partie de la [!DNL Experience Manager] et permet à votre entreprise de gérer et de distribuer des ressources numériques. Les utilisateurs d’une entreprise peuvent gérer, stocker et accéder à de nombreux types de ressources numériques, tels que des images, des vidéos, des documents, des clips audio, des fichiers 3D et des médias riches, en vue de les utiliser sur le Web, sur papier et pour la distribution numérique.

## Qu’est-ce que la gestion des ressources numériques (DAM) ? {#what-is-digital-asset-management}

[!DNL Assets] permet le partage et la distribution à l’échelle de l’entreprise des ressources numériques clés d’une entreprise. Les utilisateurs d’une organisation peuvent archiver des ressources numériques (images, graphiques, audio, vidéos et documents, notamment), les gérer et y accéder au moyen d’une interface Web (ou d’un dossier CIFS ou WebDAV).

Les fonctionnalités d’[!DNL Assets] d’[!DNL Experience Manager] vous permettent d’effectuer les opérations suivantes :

* Ajoutez et partagez des images, des documents, des fichiers audio et vidéo dans divers formats de fichier.
* Gérer les ressources en les regroupant par balise, lightbox ou étoiles (vos favoris) Ajoutez des annotations aux ressources.
* Recherchez des ressources en recherchant les noms de fichiers, le texte intégral des documents et en recherchant des dates, un type de document et des balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources Le contrôle de version des métadonnées se fait automatiquement en fonction de la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exécutez des fonctions d’édition d’images, telles que la mise à l’échelle et l’ajout de filtres d’images. Importez et exportez simultanément plusieurs ressources numériques à l’aide d’un dossier WebDAV ou CIF.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources

### [!DNL Experience Manager Assets] est intégré à [!DNL Experience Manager Sites]. {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] s’intègre entièrement à [!DNL Sites] et fonctionne de manière transparente pour tous les cas d’utilisation. Par exemple, lors de la création de pages Web, les auteurs [!DNL Sites] peuvent rechercher et utiliser les ressources numériques via l’outil de recherche de contenu. L’interface utilisateur d’[!DNL Assets] est identique à celle de [!DNL Sites]. Voir [Présentation de Sites](/help/sites-authoring/page-authoring.md) pour plus d’informations.

L’interface utilisateur de base est la même que celle de [!DNL Sites]. Consultez [Présentation de Sites](/help/sites-authoring/page-authoring.md) pour plus d’informations.

### Comparaison entre gestion des ressources numériques et composant de l’image {#digital-asset-management-versus-image-component}

Lorsque vous déterminez si une image doit être placée dans le référentiel DAM ou si vous utilisez un composant d’image, tenez compte du cycle de vie de l’image :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image.
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu Web, utilisez [!DNL Assets].

## Qu’est-ce qu’une ressource numérique ? {#what-are-digital-assets}

Une ressource est un document, une image, une vidéo ou de l’audio numérique (en tout ou en partie) qui peut comporter plusieurs rendus. Il peut également y avoir des sous-ressources, par exemple, des calques dans un fichier Photoshop, des diapositives dans un fichier PowerPoint, des pages dans un pdf, des fichiers dans un ZIP.

Une ressource est essentiellement un fichier binaire avec des métadonnées plus des rendus plus des sous-ressources. Voir [Guide de performance de la gestion des actifs numériques](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le chargement et la modification d’une grande quantité de ressources (en particulier des images) peuvent avoir une incidence sur les performances de votre déploiement [!DNL Experience Manager].

### Terminologie d’[!DNL Experience Manager Assets] {#aem-assets-terminology}

Lorsque vous utilisez des ressources numériques dans [!DNL Experience Manager], cela peut vous aider à comprendre la terminologie suivante :

* **Collection** : une collection de ressources basée sur un emplacement physique (dossier), des propriétés communes (dossier de recherche enregistrée) ou une sélection de l’utilisateur (dossiers de lightbox). 

* **Métadonnées** [!DNL Assets] possèdent des métadonnées ; par exemple, l’auteur, la date d’expiration et les informations DRM (Digital Rights Management). Les métadonnées sont sous contrôle d’accès. [!DNL Assets] prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : auteur, description, date, objet, etc.
   * IPTC : y compris l’événement, le modèle, l’emplacement, etc.
   * Gestion de contenu web : notamment les propriétés de page, l’[!UICONTROL Heure d’activation] et l’[!UICONTROL Heure de désactivation], etc.

* **Balisage** : les ressources [!DNL Assets] peuvent être balisées et classifiées. Consultez [Organisation des ressources](/help/assets/organize-assets.md).

* **Rendus** : un rendu est une représentation binaire d’une ressource. Les ressources [!DNL Assets] possèdent une représentation principale, à savoir celle du fichier chargé. Il peut y avoir un certain nombre de représentations supplémentaires qui sont créées, par exemple, par des étapes de workflow personnalisées ou lorsqu’une ressource est chargée. Les rendus peuvent avoir une taille différente, avec une résolution différente, avec un filigrane ajouté ou une autre caractéristique modifiée.

* **Versions** : le contrôle de version permet de créer un instantané des ressources numériques à un moment donné. Vous pouvez restaurer la version précédente des ressources. Consultez [Contrôle de version dans  [!DNL Assets]](manage-assets.md#asset-versioning).

* **Sous-ressources** : les sous-ressources sont des ressources qui composent une ressource (comme les calques d’un fichier [!DNL Adobe Photoshop] ou les pages d’un fichier PDF). Dans [!DNL Assets], vous pouvez gérer les sous-ressources comme vous le feriez pour les ressources.

### Travailler avec des ressources numériques {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (chargement, suppression, mise à jour, enregistrement des sous-ressources) déclenchent des workflows préconfigurés. Ils sont automatiquement activés dans [!DNL Assets] et sont décrits en détail dans les gestionnaires de médias [!DNL Assets].

Les tâches que vous pouvez réaliser avec ces workflows préconfigurés sont les suivantes :

* Enregistrer la ressource dans le référentiel ou la supprimer
* Extraire et enregistrer des métadonnées pour la ressource, avec les différents éléments de métadonnées enregistrés au format XMP
* Générer des rendus et des vignettes pour la ressource, notamment le redimensionnement et le recadrage automatiques si nécessaire
* Transcoder la ressource si nécessaire Par exemple, une vidéo pour utilisation sur appareils mobiles et sur le Web est transcodée avec 24 images par seconde et téléchargée avec 30 images par seconde. Un fichier audio pour utilisation sur appareils mobiles et sur le Web est transcodé à 128 Kbits/s et téléchargé à 192 Kbits/s.

Vous pouvez également appliquer des workflows manuellement. Consultez [Gestionnaires de médias Assets](media-handlers.md) pour obtenir une liste des workflows par défaut.

## [!DNL Experience Manager Assets] et [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Consultez la [Bibliothèque de médias et de ressources](medialibrary.md) pour plus d’informations sur ces différences.

>[!MORELIKETHIS]
>
>* [Présentation vidéo - Experience Manager Assets en tant qu’outil de gestion des ressources numériques moderne](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Présentation des concepts de métadonnées](/help/assets/metadata-concepts.md)
