---
title: Notions fondamentales sur les composants d’AEM Communities
seo-title: Notions fondamentales sur les composants d’AEM Communities
description: Ajouter les fonctionnalités Communautés aux sites AEM en mode d’édition et configurer les composants
seo-description: Ajouter les fonctionnalités Communautés aux sites AEM en mode d’édition et configurer les composants
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: f1870c1222004f582ccf337a59e1f30e2dc2cf32
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 57%

---


# Notions fondamentales sur les composants d’AEM Communities {#communities-components-basics}

## Présentation {#overview}

La section création de la documentation décrit l’ajout de fonctionnalités AEM Communities à AEM Sites en mode d’édition et décrit les configurations des composants.

Components may be explored using an AEM instance and the interactive [Community Components guide](components-guide.md).

## Accès aux composants d’AEM Communities {#accessing-communities-components}

Lors de la création du contenu de la page, si le modèle sous-jacent permet de modifier la conception de la page, il est possible d’activer des composants qui ne sont pas encore disponibles dans le navigateur de composants dans le cadre de la conception du site.

Les composants de communauté disponibles sont répertoriés [ici](author-communities.md#available-communities-components).

>[!NOTE]
>
>For general authoring information, view the [quick guide to authoring pages](../../help/sites-authoring/qg-page-authoring.md).
>
>If not familiar with AEM, view the documentation on [basic handling](../../help/sites-authoring/basic-handling.md).


### Accès au mode de conception {#entering-design-mode}

If a **Communities** component is not found in the components browser (sidekick), it will be necessary to enter `Design Mode` to add other Communities components. [Il peut également être nécessaire d’ajouter des bibliothèques](#required-clientlibs) côté client requises (clientlibs).

For details, see [Configuring Components in Design Mode](../../help/sites-authoring/default-components-designmode.md).

Vous trouverez ci-dessous des images de la sélection de quelques composants Communities et de leur affichage dans l’explorateur de composants :

![chlimage_1-424](assets/chlimage_1-424.png)

Les composants sélectionnés sont à présent disponibles dans le navigateur de composants :

![chlimage_1-425](assets/chlimage_1-425.png)

## Clientlibs requises {#required-clientlibs}

Les [bibliothèques côté client](../../help/sites-developing/clientlibs.md) (clientlibs) sont nécessaires au fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lorsque vous ajoutez un composant de communauté à une page, s’il en résulte une erreur ou une apparence inattendue, la première chose à essayer consiste à ajouter les clientlibs nécessaires au composant de communauté. Pour plus d’informations, reportez-vous à la section [Clientlibs des composants de communauté](clientlibs.md).

### Example: Initially placed reviews without client libraries... {#example-initially-placed-reviews-without-client-libraries}

![chlimage_1-426](assets/chlimage_1-426.png)

### ... And with client libraries {#and-with-client-libraries}

![chlimage_1-427](assets/chlimage_1-427.png)

## Balisage {#tagging}

De nombreuses fonctionnalités de communauté peuvent être configurées de manière à permettre aux membres de baliser le contenu entré (publié) dans l’environnement de publication.

Si le balisage est autorisé, la configuration du site de communauté peut être définie pour limiter les espaces de noms présentés aux membres dans l’environnement de publication. See the [Community Sites console](sites-console.md#tagging).

Features which allow tagging: [blog](blog-feature.md), [calendar](calendar.md), [file library](file-library.md), [forum](forum.md)

Features which use tags: [catalog](catalog.md), [search](search.md), [social tag cloud](tagcloud.md)

Pour les informations de création :

* [Utilisation des balises](../../help/sites-authoring/tags.md)

Pour les informations administratives :

* Creating tag namespaces (taxonomy): [Administering Tags](../../help/sites-administering/tags.md)
* Community Site configuration: see [TAGGING](sites-console.md#tagging)
* [Balisage de contenu généré par l’utilisateur](../../help/sites-authoring/tags.md)
* [Balisage des ressources d’activation](tag-resources.md) 

Pour les informations de développement :

* [Infrastructure de balisage AEM](../../help/sites-developing/framework.md)
* [Notions fondamentales sur le balisage](tag.md)

