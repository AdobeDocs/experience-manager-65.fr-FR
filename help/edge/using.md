---
title: Utiliser Edge Delivery Services
description: Utiliser Edge Delivery Services
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
solution: Experience Manager, Experience Manager Assets
feature: Edge Delivery Services
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 100%

---

# Utiliser Edge Delivery Services {#usingedge}

Grâce à Edge Delivery, vous pouvez créer rapidement des environnements de développement dans lesquels les personnes créant du contenu peuvent rapidement mettre à jour et publier du contenu, et de nouveaux sites peuvent être lancés rapidement. Pour ce faire, vous pouvez utiliser plusieurs sources de contenu sur le même site web. La publication sera transparente et rationalisée, quelle que soit la source choisie. Ainsi, il ne faut que quelques secondes pour passer de l’édition à la vue du contenu en direct sur Internet.

## Création {#authoring-edge}

Avec Edge Delivery, la création est facile, rapide et flexible. Vous pouvez choisir deux chemins différents pour la création dans le contexte d’Edge Delivery Services :

* Création basée sur des documents (tels que Microsoft Word ou Google Docs) : [consultez ce lien pour plus de détails](https://www.hlx.live/docs/authoring).
* Éditeur de page/Éditeur universel : contactez la personne chargée du service commercial Adobe.

En cas de création basée sur des documents, vous pouvez utiliser diverses sources telles que Microsoft Word et Google Docs. Les documents provenant de ces sources deviennent des pages de votre site web. Les en-têtes, listes, images, éléments de police et vidéos peuvent tous être transférés de la source initiale vers votre site web. Vous pouvez ajouter des métadonnées à des fins d’optimisation pour les moteurs de recherche ou utiliser des blocs pour travailler avec du contenu structuré et ajouter des fonctionnalités.

## Publication {#publishing-edge}

Avec Edge Delivery, la publication de contenu est transparente, quelle que soit votre source de contenu. Le processus est le suivant : vous utilisez l’[extension sidekick](#using-sidekick) pour déclencher le mécanisme de publication et votre contenu est disponible en ligne sur votre site web en quelques secondes.

## Edge Delivery Services et GitHub {#github-edge}

Edge Delivery Services utilise GitHub afin que les clientes et clients puissent gérer et déployer du code directement à partir de leur référentiel GitHub. Par exemple, vous pouvez écrire du contenu dans Google Docs ou Microsoft Word et développer les fonctionnalités de votre site à l’aide de CSS et de JavaScript dans GitHub. Les sites web sont automatiquement créés pour chacune de vos branches, de l’aperçu du contenu à la production. Chaque ressource que vous placez dans votre référentiel GitHub est disponible sur votre site web sans processus de création.

## Utiliser Sidekick {#using-sidekick}

AEM Sidekick fournit une barre d’outils avec des options contextuelles qui vous permettent de modifier, de prévisualiser et de publier facilement du contenu. Après avoir [installé](https://www.hlx.live/docs/sidekick-extension) l’extension AEM Sidekick, elle peut être utilisée dans les environnements de projet ou lorsque vous modifiez votre contenu (par exemple, dans les documents Google). En fonction de l’environnement, plusieurs actions sont disponibles : Prévisualiser, Charger à nouveau, Modifier et Publier. Vous pouvez également changer d’environnement lorsque vous utilisez Sidekick pour passer de l’aperçu à la production, et vice versa.

**Pour publier**, ouvrez Sidekick sur une page d’aperçu et utilisez l’action Publier. Une fois que vous avez cliqué sur Publier, l’aperçu actuel sera disponible dans les environnements en ligne et de production.

## Intégrer AEM Assets à la création basée sur des documents {#integrate-assets-edge}

Edge Delivery vous permet d’utiliser des images disponibles dans les référentiels AEM Assets lors de la création de documents dans Microsoft Word ou Google Docs.

Les options permettant d’utiliser des images dans vos documents ne sont disponibles qu’après [configuration du plug-in Sidekick d’AEM Assets](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

Le plug-in Sidekick pour AEM Assets prend en charge l’accès à :

* AEM Assets as a Cloud Service

* AEM Assets Essentials

Après avoir configuré le plug-in Sidekick d’AEM Assets, vous pouvez [commencer à utiliser des images dans vos documents Google ou Microsoft Word](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## Informations complémentaires {#further-reading}

Pour plus d’informations, voir les pages suivantes :

* Pour plus d’informations sur la prise en main d’Edge Delivery, reportez-vous à la section [Créer](https://www.hlx.live/docs/#build) de la documentation Edge Delivery.
* Pour comprendre comment créer et publier du contenu à l’aide d’Edge Delivery, reportez-vous à la section [Publier](https://www.hlx.live/docs/authoring).
* Pour savoir comment utiliser l’extension Sidekick, consultez la page [Utiliser Sidekick](https://www.hlx.live/docs/sidekick).
* Pour les instances de création AEM, reportez-vous à la page [Concepts de création](/help/sites-authoring/author.md).
