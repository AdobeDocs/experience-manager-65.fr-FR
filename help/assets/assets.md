---
title: Présentation de  [!DNL Adobe Experience Manager Assets]
description: Découvrez ce qu’est la gestion des actifs numériques, ses cas d’utilisation et  [!DNL Adobe Experience Manager Asset] l’offre.
contentOwner: AG
feature: Asset Management
role: Leader, Architect, Business Practitioner
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 29%

---


# À propos de [!DNL Adobe Experience Manager Assets] en tant que solution DAM {#administering-assets}

[!DNL Assets] est un outil de gestion des actifs numériques (DAM) qui fait partie intégrante de la  [!DNL Experience Manager] plate-forme et permet à votre entreprise de gérer et de distribuer des actifs numériques. Les utilisateurs d’une organisation peuvent gérer, stocker et accéder à de nombreux types de ressources numériques, tels que des images, des vidéos, des documents, des clips audio, des fichiers 3D et des médias enrichis, qui peuvent être utilisés sur le Web, sur papier et pour la distribution numérique.

## Qu’est-ce que la gestion des ressources numériques ? {#what-is-digital-asset-management}

[!DNL Assets] permet le partage et la distribution à l’échelle de l’entreprise des principaux actifs numériques d’une organisation. Les utilisateurs d’une organisation peuvent stocker, gérer et accéder à des ressources numériques telles que des images, des graphiques, de l’audio, de la vidéo et des documents via une interface Web (ou un dossier CIFS ou WebDAV).

[!DNL Assets] permet d’ [!DNL Experience Manager] effectuer les opérations suivantes :

* Ajouter et partager des images, des documents, ainsi que des fichiers audio et vidéo dans divers formats.
* Gérez les ressources en les regroupant par balises, cadre lumineux ou étoiles (vos favoris). Annoter les ressources.
* Rechercher des ressources en recherchant des noms de fichier, le texte intégral des documents et en recherchant les dates, le type de document et les balises.
* Ajouter ou modifier des informations sur les métadonnées pour les ressources. Les métadonnées sont automatiquement versionnées avec la ressource correspondante. Vous pouvez importer ou exporter des métadonnées de ressources.
* Exercer des fonctions de retouche d’images, telles que la mise à l’échelle et l’ajout de filtres d’image. Importer et exporter simultanément des ressources numériques multiples à l’aide d’un dossier WebDAV ou CIFS.
* Utiliser les workflows et les notifications pour permettre le traitement et le téléchargement communs de n’importe quel groupe de ressources et gérer les droits d’accès aux ressources.

### [!DNL Experience Manager Assets] est intégré à  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] s&#39;intègre complètement avec  [!DNL Sites] et fonctionne de façon transparente pour tous les cas d&#39;utilisation. Par exemple, lors de la création de pages Web, les auteurs [!DNL Sites] peuvent rechercher et utiliser les ressources numériques via l’outil de recherche de contenu. L&#39;interface utilisateur de [!DNL Assets] est identique à celle de [!DNL Sites]. Voir [présentation des sites](/help/sites-authoring/page-authoring.md) pour plus de détails.

L’interface utilisateur de base est identique à celle de [!DNL Sites]. Voir [Présentation des sites](/help/sites-authoring/page-authoring.md) pour plus de détails.

### Gestion des ressources numériques par rapport au composant d’image {#digital-asset-management-versus-image-component}

Pour déterminer si une image doit être placée dans le référentiel DAM ou utiliser le composant d’image, tenez compte du cycle de vie des images :

* Si l’image a le même cycle de vie que la page, utilisez le composant Image.
* Si l’image a un cycle de vie distinct, par exemple, si vous utilisez l’image deux fois ou en dehors de la gestion de contenu web, utilisez [!DNL Assets].

## Que sont les ressources numériques ? {#what-are-digital-assets}

Un fichier est un document numérique, une image, une vidéo ou de l’audio (ou une partie de celui-ci) qui peut comporter plusieurs rendus et des sous-ressources (par exemple, des calques dans un fichier Photoshop, des diapositives dans un fichier PowerPoint, des pages dans un PDF, des fichiers dans un ZIP).

Une ressource se compose principalement de données binaires + métadonnées + rendus + sous-ressources. Consultez le [Guide de performance DAM](/help/sites-deploying/assets-performance-sizing.md) pour plus d’informations.

>[!CAUTION]
>
>Le téléchargement et/ou la modification d’un volume important de ressources (en particulier des images) peut avoir un impact sur les performances de votre déploiement [!DNL Experience Manager].

### [!DNL Experience Manager Assets] terminologie  {#aem-assets-terminology}

Lorsque vous utilisez des ressources numériques dans [!DNL Experience Manager], vous devez comprendre la terminologie suivante :

* **Collection** : Collection de ressources, basée sur l’emplacement physique (dossier), les propriétés courantes (dossier de recherche enregistré) ou la sélection d’utilisateurs (dossiers de cadre lumineux).

* **** [!DNL Assets] les métadonnées ont des métadonnées ; par exemple, auteur, date d’expiration, informations DRM (Digital Rights Management), etc. Les métadonnées sont sous contrôle d’accès. [!DNL Assets] prend en charge les schémas de métadonnées communs suivants :

   * Dublin Core : notamment l’auteur, la description, la date, l’objet, etc.
   * IPTC : notamment l’événement, le modèle, l’emplacement, etc.
   * WCM : y compris les propriétés de page, [!UICONTROL Heure d’activation] et [!UICONTROL Heure d’activation], etc.

* **Balisage** :  [!DNL Assets] peuvent être balisés et classifiés. Voir [organisation des ressources](/help/assets/organize-assets.md).

* **Rendus** : Un rendu est la représentation binaire d’une ressource. [!DNL Assets] toujours avoir une Principale représentation - celle du fichier téléchargé. Elle peut en avoir d’autres qui sont créées par des étapes de workflow personnalisées ou lors du téléchargement de la ressource, par exemple. Les rendus peuvent avoir différentes tailles, différentes résolutions et un filigrane ou d’autres caractéristiques modifiées.

* **Versions** : Le contrôle de version crée un instantané des ressources numériques à un moment donné. Vous pouvez restaurer la version précédente des ressources. Voir [versioning dans [!DNL Assets]](manage-assets.md#asset-versioning).

* **Sous-ressources** : Les sous-ressources sont des ressources qui constituent un actif, par exemple, les calques d’un  [!DNL Adobe Photoshop] fichier ou les pages d’un fichier PDF. Dans [!DNL Assets], vous pouvez gérer les sous-ressources comme vous le feriez pour les ressources.

### Utilisation des ressources numériques {#how-to-work-with-assets}

Vous effectuez une action sur une ressource ou une collection. Les actions peuvent créer ou modifier des ressources, des collections et des rendus. La plupart des actions de base que vous effectuez sur les ressources (téléchargement, suppression, mise à jour, enregistrement de sous-ressources) déclenchent des workflows préconfigurés. Ils sont automatiquement activés dans [!DNL Assets] et sont décrits en détail dans les gestionnaires de médias [!DNL Assets].

Tâches que vous pouvez exécuter avec ces workflows préconfigurés :

* Enregistrez la ressource dans le référentiel ou supprimez-la.
* Extraire et enregistrer les métadonnées de la ressource ; les éléments de métadonnées individuels sont enregistrés en tant que XMP.
* Générer des rendus et des miniatures pour la ressource ; y compris le redimensionnement et le recadrage automatiques si nécessaire.
* Transcodez le fichier si nécessaire. Par exemple, la vidéo destinée aux utilisateurs mobiles et Web est transcodée avec 24 images par seconde, la vidéo téléchargée avec 30 images par seconde. L’audio pour l’utilisation mobile et Web est transcodé avec 128 Kbits/s, l’audio pour le téléchargement avec 192 Kbits/s.

Vous pouvez bien sûr aussi appliquer des workflows manuellement. Voir [Gestionnaires de médias Assets](media-handlers.md) pour obtenir une liste des workflows par défaut.

## [!DNL Experience Manager Assets] et [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

Voir [Ressources et bibliothèque de médias](medialibrary.md) pour plus d’informations sur les différences.

>[!MORELIKETHIS]
>
>* [Présentation vidéo - Actifs Experience Manager en tant que gestion des actifs numériques moderne](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [Comprendre les concepts de métadonnées](/help/assets/metadata-concepts.md)

