---
title: Personnalisation et extension des ressources d’Adobe Experience Manager
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 50%

---


# Personnalisation et extension des ressources {#customizing-and-extending-assets}

Asset Editor est le principal point d’accès utilisé par les utilisateurs d’un site Web Adobe Enterprise Manager pour rechercher, vue et manipuler les ressources numériques de votre référentiel.

En tant que développeur Experience Manager, vous pouvez personnaliser et étendre l’éditeur de ressources de plusieurs manières, en présentant aux utilisateurs une interface et un ensemble de fonctionnalités spécifiquement personnalisés.

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

Dans la terminologie des ressources d’Experience Manager, un rendu est le formulaire sous lequel une ressource est présentée. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
