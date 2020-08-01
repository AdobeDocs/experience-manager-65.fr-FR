---
title: Personnalisez et étendez [!DNL Adobe Experience Manager Assets].
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 52%

---


# Personnaliser et étendre [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor est le principal point d’accès utilisé par les utilisateurs d’un site Web Adobe Enterprise Manager pour rechercher, vue et manipuler les ressources numériques de votre référentiel.

As an [!DNL Experience Manager] developer, you can customize and extend the Asset Editor in a number of ways, presenting users with a specifically tailored interface and set of functionality.

Les aspects suivants de la fonctionnalité peuvent être adaptés ou développés :

* [Étendre l’éditeur de fichiers](asseteditorx.md)
* [Étendre la recherche de ressources](searchx.md)
* [Traiter les ressources à l’aide des gestionnaires et des Workflows de médias](media-handlers.md)
* [Intégration des ressources au flux d’activités](extending-activity-stream.md)
* [Développement du proxy de ressources](proxy.md)
* [Recommandations relatives à la configuration d’ImageMagick](best-practices-for-imagemagick.md)

## Personnalisation de l’aspect {#customizing-the-look-and-feel}

Les aspects suivants de l’aspect de l’éditeur de ressources peuvent être personnalisés :

* Logo : vous pouvez ajouter le logo de votre entreprise à l’interface.
* Couleurs et polices : vous pouvez changer les couleurs et polices de l’interface.
* Code HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code HTML sous-jacent qui définit les interfaces.

## Personnalisation des rendus {#customizing-renditions}

In [!DNL Experience Manager Assets] terminology a rendition is the form in which an asset is presented. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
