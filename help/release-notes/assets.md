---
title: Notes de mise à jour des ressources Adobe Experience Manager
description: Nouvelles fonctionnalités et améliorations apportées à Adobe Experience Manager 6.5 Assets.
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 44%

---


# Notes de mise à jour des ressources Adobe Experience Manager {#aem-assets-release-notes}

Voici les principales fonctionnalités et les principaux points saillants de la version des ressources de l’Adobe Experience Manager 6.5.

## Integration with [!DNL Adobe Creative Cloud] and creative workflows {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] propose différentes manières de s’intégrer à et de partager des ressources à utiliser dans des workflows, où les équipes créatives et marketing ou les équipes d’entreprise collaborent étroitement.[!DNL Adobe Creative Cloud] [!DNL Experience Manager] 6.5 continue à améliorer l’intégration et à la rationaliser afin d’exposer davantage de possibilités et de rationaliser les méthodes existantes. 

Read on to know the specific capabilities and integrations of [!DNL Experience Manager] 6.5 that you can leverage to best support your content velocity use cases.

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] renforce la collaboration entre les créatifs et les marketeurs dans le processus de création de contenu. Creatives can access content stored in [!DNL Experience Manager Assets], without leaving the apps that they are most familiar with. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign] apps.

[!DNL Adobe Asset Link] fait partie de l’offre [Creative Cloud abonnement entreprise](https://www.adobe.com/creativecloud/business/enterprise.html) . For more information about it, including necessary configuration of your [!DNL Experience Manager] deployment, see [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html).

![Recherche de ressources dans Adobe Photoshop](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] intégration {#stock}

Your organization can use its [!DNL Adobe Stock] enterprise plan within [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for your creative and marketing projects. You can quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in Experience Manager, using the powerful DAM capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock]Le service permet aux créateurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de haute qualité et libres de droits pour tous leurs projets de création. 

For more info, see [Use Adobe Stock assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Image et licence de l’Prévisualisation Adobe Stock à partir des ressources Experience Manager](assets/stock_image_preview_license_options.png)

*Figure : Prévisualisation[!DNL Adobe Stock]image et licence depuis[!DNL Experience Manager Assets].*

![Recherche et filtrage des images Adobe Stock sous licence dans le Experience Manager](assets/aem-search-filters2.jpg)

*Figure : Recherchez et filtrez les[!DNL Adobe Stock]images sous licence dans[!DNL Experience Manager].*

### Dynamic references in [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] utilisés dans [!DNL Adobe InDesign] les fichiers sont dynamiques. Les références sont automatiquement mises à jour si les ressources référencées se déplacent dans le référentiel. Pour plus d’informations, voir [comment gérer des ressources](/help/assets/managing-linked-subassets.md)composées.

## Fonctionnalités de Brand Portal {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] vous permet d’acquérir facilement, de contrôler efficacement et de distribuer en toute sécurité les ressources approuvées aux fournisseurs/agences externes et aux utilisateurs professionnels internes sur tous les appareils. Il contribue à améliorer l’efficacité du partage des ressources, accélère la mise sur le marché des ressources et élimine le risque d’utilisation non conforme et d’accès non autorisé.

Pour plus d’informations, consultez [Nouveautés de Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html).

## Ressources connectées {#connectedassets}

Dans les grandes entreprises, l’infrastructure requise pour créer des sites web peut être distribuée. Parfois, les capacités de création de sites web et les ressources numériques requises résident dans différents silos.

[!DNL Experience Manager Sites] offre des fonctionnalités pour créer des pages web.  est le système de gestion des actifs numériques (DAM) qui fournit les ressources requises pour les sites web.[!DNL Experience Manager Assets] [!DNL Experience Manager] prend désormais en charge le cas d’utilisation ci-dessus en intégrant [!DNL Sites] et [!DNL Assets]. Voir [comment configurer et utiliser la fonction](/help/assets/use-assets-across-connected-assets-instances.md)Ressources connectées.

![Faire glisser un fichier d’un [!DNL Experience Manager] déploiement sur une [!DNL Sites] page d’un autre [!DNL Experience Manager] déploiement](assets/connected-assets-drag-and-drop-only.gif)

*Figure : Faites glisser un fichier d’un[!DNL Experience Manager]déploiement sur une[!DNL Sites]page d’un autre[!DNL Experience Manager]déploiement.*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] offre une création et une diffusion de contenu multimédia enrichi [!DNL Experience Manager Assets] pour générer des expériences de pointe immersives et personnalisées. En téléchargeant un seul fichier original de haute qualité et en utilisant le rendu avancé du cloud et les visionneuses, vous pouvez fournir toute combinaison de rendus instantanément pour prendre en charge la stratégie multimédia de votre entreprise.

For more details on new [!DNL Dynamic Media] features see [Dynamic Media Release Notes](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html).

### Prise en charge de la vidéo à 360°{#video-support}

Manage your 360-video files directly in [!DNL Experience Manager] using the cutting edge viewers to deliver VR-experiences to desktops, mobile and VR-headsets. Pour plus d’informations, consultez [Utilisation de la vidéo 360°](/help/assets/360-video.md)

### Miniatures vidéo personnalisées {#custom-video-thumbnails}

Vous pouvez maintenant personnaliser les vignettes de vos ressources vidéo à l’aide d’images de la vidéo ou de tout autre contenu stocké dans DAM. Pour obtenir des instructions supplémentaires, consultez la section [Ȃ propos des vignettes vidéo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### Amélioration de l’accessibilité {#accessibility-enhancements}

[!DNL Dynamic Media] les lecteurs d’écran prennent désormais en charge des fonctions d’accessibilité améliorées, telles que la prise en charge Aria, les lecteurs d’écran et Alt-text. Pour plus de détails, consultez les [notes de mise à jour des visionneuses de Dynamic Media](https://docs.adobe.com/content/help/fr-FR/dynamic-media-developer-resources/library/home.html).

## Amélioration de l’expérience de recherche {#search-experience-enhancement}

[!DNL Experience Manager] A partir de la version 6.5, les marketeurs peuvent découvrir les ressources de leur choix plus rapidement à partir de la page des résultats de la recherche. Les facettes de recherche sont mises à jour avec le nombre de ressources avant même d’appliquer le filtre de recherche. L’affichage du nombre attendu par rapport au filtre aide les utilisateurs à naviguer efficacement dans les résultats de la recherche. For more information, see [Search assets in Experience Manager](../assets/search-assets.md).

![Afficher le nombre de ressources sans filtrer les résultats de la recherche dans les facettes de recherche](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Figure : Affichez le nombre de fichiers sans filtrer les résultats de la recherche dans les facettes de recherche.*

## Amélioration de la convivialité {#usability-enhancement}

Vous pouvez désormais sélectionner toutes les ressources chargées dans un dossier ou à partir d’un résultat de recherche en une seule opération. Vous pouvez ainsi gérer plusieurs ressources rapidement. The check box selects all the assets that fits the scenario, say a search result and not just the assets that are visible in the [!DNL Experience Manager] interface.

![Utilisez l’option Sélectionner tout pour sélectionner tous les fichiers chargés en un seul clic.](assets/select-all-in-aem-assets.gif)

*Figure : Utilisez l’option Sélectionner tout pour sélectionner tous les fichiers chargés en un seul clic.*

## Améliorations des métadonnées {#metadata-enhancements}

[!DNL Assets] vous permet de créer des schémas de métadonnées pour des dossiers de ressources. Ces schémas définissent la disposition et les métadonnées affichées dans les pages de propriétés des dossiers. Vous pouvez désormais attribuer un schéma de métadonnées de dossier à un dossier existant ou lors de la création d’un dossier. Pour plus d’informations, consultez la section [Schéma de métadonnées de dossier](/help/assets/folder-metadata-schema.md).

Lors de la spécification des métadonnées en cascade, les options peuvent être chargées à partir d’un fichier JSON à l’exécution, au lieu de les saisir manuellement dans le formulaire. Pour plus d’informations, consultez la section [Schéma de métadonnées de dossier](/help/assets/cascading-metadata.md).

## Amélioration des rapports {#reporting-enhancements}

Les fragments de contenu et les partages de liens sont désormais inclus dans le rapport téléchargé. Pour plus d’informations, consultez la section [Rapports d’Assets](/help/assets/asset-reports.md).
