---
title: Personnalisation et extension des ressources AEM
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Personnalisation et extension des ressources {#customizing-and-extending-assets}

L’Éditeur de ressources est le point d’accès principal que les utilisateurs d’un site web Adobe Enterprise Manager (AEM) utiliseront pour rechercher, afficher et manipuler les ressources numériques dans votre référentiel.

En tant que développeur AEM, vous pouvez personnaliser et étendre l’Éditeur de ressources de multiples façons pour proposer aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.

Les aspects suivants de la fonctionnalité peuvent être adaptés ou développés :

* [Etendre l’éditeur de fichiers](asseteditorx.md)
* [Étendre la recherche de ressources](searchx.md)
* [Traiter les ressources à l’aide des gestionnaires de médias et des processus](media-handlers.md)
* [Intégration des ressources au flux d’activité](extending-activity-stream.md)
* [Développement de proxy de ressources](proxy.md)
* [Meilleures pratiques pour configurer ImageMagick](best-practices-for-imagemagick.md)

## Personnalisation de l’aspect {#customizing-the-look-and-feel}

Les aspects suivants de l’apparence de l’éditeur de fichiers peuvent être personnalisés :

* Logo : vous pouvez ajouter le logo de votre entreprise à l’interface.
* Couleurs et polices : vous pouvez changer les couleurs et polices de l’interface.
* Code HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code HTML sous-jacent qui définit les interfaces.

## Personnalisation des rendus {#customizing-renditions}

Dans la terminologie AEM Assets, un rendu est la forme dans laquelle une ressource est présentée. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
