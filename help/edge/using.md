---
title: Utilisation d’Edge Delivery Services
description: Utilisation d’Edge Delivery Services (EDS)
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 2%

---

# Utilisation d’Edge Delivery Services {#usingedge}

Grâce à Edge Delivery, vous pouvez créer rapidement des environnements de développement dans lesquels les auteurs peuvent rapidement mettre à jour et publier du contenu, et de nouveaux sites peuvent être lancés rapidement. Pour ce faire, vous pouvez utiliser plusieurs sources de contenu sur le même site web et la publication sera transparente et rationalisée, quelle que soit la source choisie. Ainsi, il ne faut que quelques secondes pour passer de l&#39;édition à la vue du contenu en direct sur Internet.

## Création {#authoring-edge}

Avec Edge Delivery, la création est facile, rapide et flexible. Vous pouvez choisir deux chemins différents pour la création dans le contexte des Edge Delivery Services :

* Création basée sur des documents (tels que Microsoft Word ou Google Docs) - [Consultez ce lien pour plus de détails](https://www.hlx.live/docs/authoring).
* Éditeur de page/Éditeur universel : contactez votre représentant commercial Adobe.

Dans le cas de la création basée sur des documents, vous pouvez utiliser diverses sources telles que Microsoft Word et Google Docs. Les documents provenant de ces sources deviennent des pages de votre site web. Les en-têtes, listes, images, éléments de police et vidéos peuvent tous être transférés de la source initiale vers votre site web. Vous pouvez ajouter des métadonnées à des fins d’optimisation pour les moteurs de recherche ou utiliser des blocs pour travailler avec du contenu structuré et ajouter des fonctionnalités.

## Publication {#publishing-edge}

Avec Edge Delivery, la publication de contenu est transparente, quelle que soit votre source de contenu. Le processus est le suivant : vous utilisez la méthode [extension sidekick](#using-sidekick) pour déclencher le mécanisme de publication et votre contenu sera disponible en ligne sur votre site web dans quelques secondes.

## Edge Delivery Services et GitHub {#github-edge}

Edge Delivery utilise GitHub afin que les clients puissent gérer et déployer du code directement à partir de leur référentiel GitHub. Par exemple, vous pouvez écrire du contenu dans Google Docs ou Microsoft Word et développer les fonctionnalités de votre site à l’aide de CSS et de JavaScript dans GitHub. Les sites web sont automatiquement créés pour chacune de vos branches, de l’aperçu du contenu à la production. Chaque ressource que vous placez dans votre référentiel GitHub est disponible sur votre site web sans processus de création.

## Utilisation du Sidekick {#using-sidekick}

Le sidekick d’AEM fournit une barre d’outils avec des options contextuelles qui vous permettent de modifier, de prévisualiser et de publier facilement du contenu. Après [installation](https://www.hlx.live/docs/sidekick-extension) L’extension AEM sidekick peut être utilisée dans les environnements de projet ou lorsque vous modifiez votre contenu (par exemple, dans les documents Google). En fonction de l’environnement, plusieurs actions sont disponibles : Aperçu, Recharger, Modifier et Publier. Vous pouvez également changer d’environnement lorsque vous utilisez le sidekick, qui passe de l’aperçu à la production, et vice versa.

**Pour publier**, ouvrez le sidekick sur une page d’aperçu et utilisez l’action Publier . Une fois que vous avez cliqué sur Publier, la version d’aperçu actuelle de la page sera disponible dans les environnements en ligne et de production.

## Intégration d’AEM Assets à la création basée sur des documents {#integrate-assets-edge}

Edge Delivery vous permet d’utiliser des images disponibles dans les référentiels AEM Assets lors de la création de documents dans Microsoft Word ou Google Docs.

Les options permettant d’utiliser des images dans vos documents ne sont disponibles qu’après [configuration du module externe du sidekick AEM Assets](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

Le module externe sidekick pour AEM Assets prend en charge l’accès à :

* AEM Assets as a Cloud Service

* AEM Assets Essentials

Après avoir configuré le module externe du sidekick AEM Assets, vous pouvez [commencer à utiliser des images dans vos documents Google ou Microsoft Word ;](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Autres lectures {#further-reading}

Pour plus d’informations, consultez les pages suivantes :

* Pour plus d’informations sur la prise en main d’Edge Delivery, reportez-vous au [Build](https://www.hlx.live/docs/#build) de la documentation sur les diffusions Edge.
* Pour comprendre comment créer et publier du contenu à l’aide d’Edge Delivery, reportez-vous au [Publication de section](https://www.hlx.live/docs/authoring).
* Pour savoir comment utiliser l’extension sidekick, voir [Utilisation du sidekick](https://www.hlx.live/docs/sidekick) page.
* Pour AEM la création, reportez-vous à la section [Page Concepts de création](/help/sites-authoring/author.md))
