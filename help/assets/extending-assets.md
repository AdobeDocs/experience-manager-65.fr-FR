---
title: Personnalisation et extension d’ [!DNL Assets]
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 50%

---

# Personnalisation et extension d’[!DNL Assets] {#customizing-and-extending-assets}

Asset Editor est le point d’accès principal que les utilisateurs d’un site web Enterprise Manager d’Adobe utilisent pour rechercher, afficher et manipuler les ressources numériques de votre référentiel.

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

* Logo : vous pouvez ajouter le logo de votre propre organisation à l’interface.
* Couleurs et polices : vous pouvez modifier les couleurs et les polices utilisées dans l’interface.
* Code de HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code de HTML sous-jacent qui définit les interfaces.

## Personnalisation des rendus {#customizing-renditions}

Dans la terminologie d’[!DNL Experience Manager Assets], un rendu est la forme dans laquelle une ressource est présentée. En règle générale, une ressource particulière peut comporter plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, un autre dans sa taille réduite et un autre dans sa taille réduite et converti en niveaux de gris.

Les rendus qu’une ressource particulière est disponible dans peuvent être personnalisés et de nouveaux rendus créés.
