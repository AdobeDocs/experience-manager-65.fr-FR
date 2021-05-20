---
title: Introduction à [!DNL Adobe Experience Manager Assets]
description: Découvrez ce qu’est la gestion des ressources numériques, ses cas d’utilisation et l’offre  [!DNL Adobe Experience Manager Asset] .
contentOwner: AG
feature: Gestion des ressources
role: Leader, Architect, Business Practitioner
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 29%

---

# À propos de [!DNL Adobe Experience Manager Assets] en tant que solution de gestion des actifs numériques {#administering-assets}

[!DNL Assets] est un outil de gestion des ressources numériques (DAM) qui fait partie intégrante de la  [!DNL Experience Manager] plateforme et permet à votre entreprise de gérer et de distribuer des ressources numériques. Les utilisateurs d’une entreprise peuvent gérer, stocker et accéder à de nombreux types de ressources numériques, tels que des images, des vidéos, des documents, des clips audio, des fichiers 3D et des médias riches, en vue de les utiliser sur le web, sur papier et pour la distribution numérique.

## Qu’est-ce que la gestion des ressources numériques ? {#what-is-digital-asset-management}

[!DNL Assets] permet le partage et la distribution à l’échelle de l’entreprise des ressources numériques clés d’une entreprise. Les utilisateurs d’une entreprise peuvent stocker, gérer et accéder à des ressources numériques telles que des images, des graphiques, de l’audio, de la vidéo et des documents par le biais d’une interface web (ou d’un dossier CIFS ou WebDAV).

[!DNL Assets] La fonctionnalité de vous  [!DNL Experience Manager] permet d’effectuer les opérations suivantes :

* Ajouter et partager des images, des documents, ainsi que des fichiers audio et vidéo dans divers formats.
* Gérez les ressources en les regroupant par balises, Lightbox ou étoiles (vos favoris). Annoter les ressources.
* Rechercher des ressources en recherchant des noms de fichier, le texte intégral des documents et en recherchant les dates, le type de document et les balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources. Les métadonnées sont automatiquement versionnées avec la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exercer des fonctions de retouche d’images, telles que la mise à l’échelle et l’ajout de filtres d’image. Importer et exporter simultanément des ressources numériques multiples à l’aide d’un dossier WebDAV ou CIFS.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources.

### [!DNL Experience Manager Assets] est intégré à  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] s’intègre entièrement à  [!DNL Sites] et fonctionne de manière transparente pour tous les cas d’utilisation. Par exemple, lors de la création de pages web, les auteurs [!DNL Sites] peuvent rechercher et utiliser les ressources numériques via l’outil de recherche de contenu. L’interface utilisateur de [!DNL Assets] est la même que celle de [!DNL Sites]. Voir [Présentation de Sites](/help/sites-authoring/page-authoring.md) pour plus de détails.

L’interface utilisateur de base est la même que celle de [!DNL Sites]. Voir [Présentation des sites](/help/sites-authoring/page-authoring.md) pour plus de détails.

### Gestion des ressources numériques et composant d’image {#digital-asset-management-versus-image-component}

Lorsque vous déterminez si vous souhaitez placer une image dans le référentiel DAM ou utiliser le composant image, tenez compte du cycle de vie de l’image :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image .
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu web, utilisez [!DNL Assets].

## Que sont les ressources numériques ? {#what-are-digital-assets}

Une ressource est un document, une image, une vidéo ou de l’audio numérique (en tout ou en partie) qui peut comporter plusieurs rendus et des sous-ressources (par exemple, les calques d’un fichier photoshop, les diapositives d’un fichier PowerPoint, les pages d’un pdf, les fichiers d’un ZIP).

Une ressource se compose principalement de données binaires + métadonnées + rendus + sous-ressources. Consultez le [Guide de performance DAM](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le chargement et/ou la modification d’un grand volume de ressources (en particulier des images) peut avoir un impact sur les performances de votre déploiement [!DNL Experience Manager].

### [!DNL Experience Manager Assets] terminologie  {#aem-assets-terminology}

Lorsque vous utilisez des ressources numériques dans [!DNL Experience Manager], vous devez connaître la terminologie suivante :

* **Collection** : Collection de ressources basée sur l’emplacement physique (dossier), les propriétés communes (dossier de recherche enregistré) ou la sélection d’utilisateurs (dossiers Lightbox).

* **** [!DNL Assets] Les métadonnées comportent des métadonnées ; par exemple, l’auteur, la date d’expiration, les informations DRM (Digital Rights Management), etc. Les métadonnées sont sous contrôle d’accès. [!DNL Assets] prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : notamment l’auteur, la description, la date, l’objet, etc.
   * IPTC : notamment l’événement, le modèle, l’emplacement, etc.
   * WCM : y compris les propriétés de page, [!UICONTROL Heure d’activation] et [!UICONTROL Heure de désactivation], etc.

* **Balisage** :  [!DNL Assets] peuvent être balisées et classées. Voir [organisation des ressources](/help/assets/organize-assets.md).

* **Rendus** : Un rendu est la représentation binaire d’une ressource. [!DNL Assets] ont toujours une Principale représentation : celle du fichier chargé. Elle peut en avoir d’autres qui sont créées par des étapes de workflow personnalisées ou lors du téléchargement de la ressource, par exemple. Les rendus peuvent avoir différentes tailles, différentes résolutions et un filigrane ou d’autres caractéristiques modifiées.

* **Versions** : Le contrôle de version crée un instantané des ressources numériques à un moment donné. Vous pouvez restaurer la version précédente des ressources. Voir [contrôle de version dans [!DNL Assets]](manage-assets.md#asset-versioning).

* **Sous-ressources** : Les sous-ressources sont des ressources qui constituent une ressource, par exemple, des calques dans un  [!DNL Adobe Photoshop] fichier ou des pages dans un fichier PDF. Dans [!DNL Assets], vous pouvez gérer les sous-ressources comme vous le feriez pour les ressources.

### Utilisation des ressources numériques {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (chargement, suppression, mise à jour, enregistrement des sous-ressources) déclenchent des workflows préconfigurés. Ils sont automatiquement activés dans [!DNL Assets] et sont décrits en détail dans les gestionnaires de médias [!DNL Assets].

Les tâches que vous pouvez effectuer avec ces workflows préconfigurés sont les suivantes :

* Enregistrez la ressource dans le référentiel ou supprimez-la.
* Extraire et enregistrer les métadonnées de la ressource ; les éléments de métadonnées individuels sont enregistrés en tant que XMP.
* Générer des rendus et des miniatures pour la ressource ; y compris le redimensionnement et le recadrage automatiques, le cas échéant.
* Transcodez la ressource si nécessaire. Par exemple, la vidéo pour l’utilisation mobile et web est transcodée avec 24 images par seconde, téléchargez la vidéo avec 30 images par seconde. L’audio pour l’utilisation mobile et web est transcodé avec 128 Kbit/s, l’audio pour téléchargement avec 192 Kbit/s.

Vous pouvez bien sûr aussi appliquer des workflows manuellement. Voir [Gestionnaires de médias Assets](media-handlers.md) pour obtenir une liste des workflows par défaut.

## [!DNL Experience Manager Assets] et [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Voir [Ressources et Media Library](medialibrary.md) pour plus d’informations sur les différences.

>[!MORELIKETHIS]
>
>* [Présentation vidéo - Ressources Experience Manager en tant que gestion des ressources numériques moderne](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Présentation des concepts de métadonnées](/help/assets/metadata-concepts.md)

