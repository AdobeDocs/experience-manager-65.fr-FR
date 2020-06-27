---
title: A propos des ressources d'Adobe Experience Manager
description: Découvrez ce que sont la gestion des ressources numériques, ses cas d’utilisation et l’offre d’actifs Experience Manager Adobe
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 48%

---


# Administration des fichiers {#administering-assets}

Assets est un outil de gestion des actifs numériques (DAM) entièrement intégré à la plate-forme Experience Manager et qui permet à votre entreprise de partager et de distribuer des actifs numériques. Les utilisateurs au sein d’une organisation peuvent gérer, stocker et accéder à des images, des vidéos, des documents, des clips audio et des fichiers multimédias enrichis, tels que des fichiers Flash, en vue de les utiliser sur le web, les imprimer et effectuer une distribution numérique.

## What is Digital Asset Management? {#what-is-digital-asset-management}

Les ressources permettent le partage et la distribution des ressources numériques principales d’une organisation dans toute l’entreprise. Les utilisateurs d’une organisation peuvent stocker, gérer et accéder à des ressources numériques telles que des images, des graphiques, de l’audio, de la vidéo et des documents via une interface Web (ou un dossier CIFS ou WebDAV).

Bien intégrée dans le Experience Manager, la fonctionnalité Ressources vous permet d’effectuer les opérations suivantes :

* Ajouter et partager des images, des documents, ainsi que des fichiers audio et vidéo dans divers formats.
* Gérez les ressources en les regroupant par balises, cadre lumineux ou étoiles (vos favoris). Annoter les ressources.
* Rechercher des ressources en recherchant des noms de fichier, le texte intégral des documents et en recherchant les dates, le type de document et les balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources. Les métadonnées sont automatiquement versionnées avec la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exercer des fonctions de retouche d’images, telles que la mise à l’échelle et l’ajout de filtres d’image. Importer et exporter simultanément des ressources numériques multiples à l’aide d’un dossier WebDAV ou CIFS.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources.

### Les ressources du Experience Manager sont intégrées aux sites Experience Manager {#aem-assets-fully-integrated-in-cq-wcm}

Les ressources sont entièrement intégrées aux sites et toutes les fonctionnalités sont disponibles en toute transparence. Les ressources numériques gérées dans le référentiel Assets peuvent ensuite être accessibles via l’outil de recherche de contenu lors de la création de pages Web.

L&#39;interface utilisateur de base est la même que celle des sites. Voir [Présentation des sites](/help/sites-authoring/page-authoring.md) pour en savoir plus.

### Digital Asset Management versus image component {#digital-asset-management-versus-image-component}

Lorsque vous décidez de placer une image dans le référentiel DAM ou d’utiliser le composant d’image, tenez compte du cycle de vie des images :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image.
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu web, utilisez Assets.

## What are digital assets? {#what-are-digital-assets}

Un fichier est un document numérique, une image, une vidéo ou de l’audio (ou une partie de celui-ci) qui peut comporter plusieurs rendus et des sous-ressources (par exemple, des calques dans un fichier Photoshop, des diapositives dans un fichier PowerPoint, des pages dans un PDF, des fichiers dans un ZIP).

Une ressource se compose principalement de données binaires + métadonnées + rendus + sous-ressources. Consultez le [Guide de performance DAM](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le téléchargement et/ou la modification d’un volume important de ressources (en particulier des images) peut avoir un impact sur les performances de votre instance de Experience Manager.

### Terminologie des ressources Experience Manager {#aem-assets-terminology}

Lorsque vous utilisez des ressources numériques en Experience Manager, vous devez comprendre la terminologie suivante :

* **Collection** Collection de ressources, basée sur l’emplacement physique (dossier), les propriétés communes (dossier de recherche enregistré) ou la sélection d’utilisateurs (dossiers de cadre lumineux).

* **Les ressources de métadonnées** comportent des métadonnées ; par exemple, auteur, date d’expiration, informations DRM (Digital Rights Management), etc. Les métadonnées sont sous contrôle d’accès.  Assets prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : notamment l’auteur, la description, la date, l’objet, etc.
   * IPTC : notamment l’événement, le modèle, l’emplacement, etc.
   * WCM : y compris les propriétés de la page, [!UICONTROL Heure] de début et Heure [!UICONTROL de]fin, etc.

* **Le balisage** des ressources peut être balisé et classifié. Voir Utilisation des balises et Administration des balises.

* **Rendus** Un rendu est la représentation binaire d’une ressource. Une ressource possède toujours une représentation principale, à savoir celle du fichier téléchargé. Elle peut en avoir d’autres qui sont créées par des étapes de workflow personnalisées ou lors du téléchargement de la ressource, par exemple. Les rendus peuvent avoir différentes tailles, différentes résolutions et un filigrane ou d’autres caractéristiques modifiées.

* **Versions** Versioning crée un instantané des ressources numériques à un moment précis. Vous pouvez restaurer la version précédente des ressources. See [versioning in Assets](managing-assets-touch-ui.md#asset-versioning).

* **Sous-ressources** Les sous-ressources sont des ressources qui constituent un élément, par exemple, des calques d’un fichier Adobe Photoshop ou des pages d’un fichier PDF. Dans Assets, vous pouvez gérer les sous-ressources comme les ressources.

### How to work with assets {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (téléchargement, suppression, mise à jour, enregistrement de sous-ressources) déclenchent des workflows préconfigurés. Ils sont automatiquement activés dans Assets et sont décrits en détail dans les gestionnaires de médias Assets.

tâches que vous pouvez exécuter avec ces workflows préconfigurés :

* Enregistrer la ressource dans le référentiel ou la supprimer.
* Extraire et enregistrer des métadonnées pour la ressource ; les différents éléments de métadonnées sont enregistrés au format XMP.
* Générer des rendus et des vignettes pour la ressource ; notamment le redimensionnement et le recadrage automatiques si nécessaire.
* Transcoder la ressource si nécessaire. Par exemple, la vidéo destinée aux utilisateurs mobiles et Web est transcodée avec 24 images par seconde, la vidéo téléchargée avec 30 images par seconde. Un fichier audio pour utilisation sur appareils mobiles et sur le web est transcodé avec 128 Kbits/s et téléchargé avec 192 Kbits/s.

Vous pouvez bien sûr aussi appliquer des workflows manuellement. Voir [Gestionnaires de médias Assets](/help/assets/media-handlers.md) pour obtenir une liste des workflows par défaut.

## Ressources du Experience Manager et MediaLibrary {#cq-dam-vs-cq-medialibrary}

Voir [Ressources et MediaLibrary](/help/assets/medialibrary.md) pour en savoir plus sur les différences.
