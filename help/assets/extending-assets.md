---
title: Personnaliser et étendre  [!DNL Assets]
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 52%

---


# Personnaliser et étendre [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor est le Principal point d’accès que les utilisateurs d’un site Web Adobe Enterprise Manager utilisent pour rechercher, vue et manipuler les ressources numériques de votre référentiel.

En tant que développeur [!DNL Experience Manager], vous pouvez personnaliser et étendre l’éditeur de ressources de plusieurs manières, présentant aux utilisateurs une interface et un ensemble de fonctionnalités spécifiquement personnalisés.

Les aspects suivants de la fonctionnalité peuvent être adaptés ou développés :

* [Étendre l’éditeur de fichiers](asseteditorx.md)
* [Étendre la recherche de ressources](searchx.md)
* [Traiter les ressources à l’aide des gestionnaires et des Workflows de médias](media-handlers.md)
* [Intégration des ressources au flux d’activités](extending-activity-stream.md)
* [Développement du proxy de ressources](proxy.md)
* [Recommandations relatives à la configuration d’ImageMagick](best-practices-for-imagemagick.md)

## Personnaliser l&#39;apparence {#customizing-the-look-and-feel}

Les aspects suivants de l’aspect de l’éditeur de ressources peuvent être personnalisés :

* Logo : vous pouvez ajouter le logo de votre entreprise à l’interface.
* Couleurs et polices : vous pouvez changer les couleurs et polices de l’interface.
* Code HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code HTML sous-jacent qui définit les interfaces.

## Personnaliser les rendus {#customizing-renditions}

Dans la terminologie [!DNL Experience Manager Assets], un rendu est la forme sous laquelle un élément est présenté. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
