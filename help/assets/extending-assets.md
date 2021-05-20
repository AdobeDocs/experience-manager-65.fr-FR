---
title: Personnaliser et étendre  [!DNL Assets]
description: Découvrez les moyens par lesquels vous pouvez personnaliser et étendre le Partage de ressources et l’Éditeur de ressources, qui proposent aux utilisateurs une interface et un ensemble de fonctionnalités spécialement adaptés.
contentOwner: AG
role: Developer
feature: Outils de développement
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 52%

---

# Personnaliser et étendre [!DNL Assets] {#customizing-and-extending-assets}

Asset Editor est le point d’accès Principal que les utilisateurs d’un site web Enterprise Manager d’Adobe vont utiliser pour rechercher, afficher et manipuler les ressources numériques de votre référentiel.

En tant que développeur de [!DNL Experience Manager], vous pouvez personnaliser et étendre l’Éditeur de ressources de plusieurs manières, présentant aux utilisateurs une interface et un ensemble de fonctionnalités spécifiquement personnalisés.

Les aspects suivants de la fonctionnalité peuvent être adaptés ou développés :

* [Étendre l’Éditeur de ressources](asseteditorx.md)
* [Étendre la recherche de ressources](searchx.md)
* [Traitement des ressources à l’aide des workflows et des gestionnaires de médias](media-handlers.md)
* [Intégration de ressources à un flux d’activités](extending-activity-stream.md)
* [Développement de proxy de ressources](proxy.md)
* [Bonnes pratiques pour configurer ImageMagick](best-practices-for-imagemagick.md)

## Personnaliser l’aspect {#customizing-the-look-and-feel}

Les aspects suivants de l’apparence de l’Éditeur de ressources sont personnalisables :

* Logo : vous pouvez ajouter le logo de votre entreprise à l’interface.
* Couleurs et polices : vous pouvez changer les couleurs et polices de l’interface.
* Code HTML : pour une personnalisation plus approfondie, vous pouvez modifier le code HTML sous-jacent qui définit les interfaces.

## Personnalisation des rendus {#customizing-renditions}

Dans la terminologie [!DNL Experience Manager Assets], un rendu est la forme sous laquelle une ressource est présentée. En général, une ressource particulière peut posséder plusieurs rendus. Par exemple, une image en couleur peut avoir un rendu dans sa taille d’origine, une autre à un format réduit et une autre à la fois dans un format réduit et un format converti en niveaux de gris.

Les rendus dans lesquels une ressource particulière est disponible peuvent être personnalisés, et de nouveaux rendus peuvent être créés.
