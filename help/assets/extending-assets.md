---
title: Personnalisation et extension d’ [!DNL Assets]
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '253'
ht-degree: 100%

---

# Personnalisation et extension d’[!DNL Assets] {#customizing-and-extending-assets}

L’Éditeur de ressources est le point d’accès principal que les utilisateurs d’un site Web Adobe Enterprise Manager utiliseront pour rechercher, afficher et manipuler les ressources numériques dans votre référentiel.

En tant que développeur [!DNL Experience Manager], vous pouvez personnaliser et étendre l’Éditeur de ressources de multiples façons pour proposer aux utilisateurs une interface et un ensemble de fonctionnalités adaptés spécialement à leurs besoins.

Les aspects suivants de la fonctionnalité peuvent être adaptés ou développés :

* [L’extension de l’éditeur de ressources](asseteditorx.md)
* [L’extension de la recherche de ressources](searchx.md)
* [Le traitement des ressources à l’aide des workflows et des gestionnaires de médias](media-handlers.md)
* [L’intégration des ressources avec le flux d’activités](extending-activity-stream.md)
* [Le développement d’un proxy Assets](proxy.md)
* [Les bonnes pratiques de configuration d’ImageMagick](best-practices-for-imagemagick.md)

## Personnalisation de l’aspect {#customizing-the-look-and-feel}

Les aspects suivants de l’aspect et du comportement de l’Éditeur de ressources sont personnalisables :

* Logo : vous pouvez ajouter le logo de votre entreprise à l’interface.
* Couleurs et polices : vous pouvez changer les couleurs et polices de l’interface.
* Code HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code HTML sous-jacent qui définit les interfaces.

## Personnalisation des rendus {#customizing-renditions}

Dans la terminologie d’[!DNL Experience Manager Assets], un rendu est la forme dans laquelle une ressource est présentée. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
