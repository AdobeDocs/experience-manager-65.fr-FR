---
title: Principes de base des composants des communautés
description: Ajout de fonctionnalités Communities à AEM sites en mode d’édition et configuration de composants
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 2%

---

# Principes de base des composants des communautés {#communities-components-basics}

## Vue d’ensemble {#overview}

La section de création de la documentation décrit l’ajout de fonctionnalités Communities à AEM sites en mode d’édition de création et décrit les configurations de composant.

Les composants peuvent être explorés à l’aide d’une instance AEM et de l’objet interactif [Guide des composants de communauté](components-guide.md).

## Accès aux composants Communities {#accessing-communities-components}

Lors de la création du contenu d’une page, si le modèle sous-jacent permet de modifier la conception de la page, il est possible d’activer les composants qui ne sont pas déjà disponibles dans l’explorateur de composants dans le cadre de la conception du site.

Les composants de communauté disponibles sont répertoriés. [here](author-communities.md#available-communities-components).

>[!NOTE]
>
>Pour obtenir des informations générales sur la création, consultez la [guide rapide pour la création de pages](../../help/sites-authoring/qg-page-authoring.md).
>
>Si vous ne connaissez pas AEM, consultez la documentation sur [gestion de base](../../help/sites-authoring/basic-handling.md).

### Accès au mode Conception {#entering-design-mode}

Si une **Communautés** Le composant est introuvable dans l’explorateur de composants (sidekick), il sera nécessaire de saisir `Design Mode` pour ajouter d’autres composants Communities. [Bibliothèques côté client requises](#required-clientlibs) (clientlibs) doit également être ajouté.

Pour plus d’informations, voir [Configuration des composants en mode de conception](../../help/sites-authoring/default-components-designmode.md).

Vous trouverez ci-dessous des images de la sélection de quelques composants Communities et de leur affichage dans l’explorateur de composants :

![component-design](assets/component-design.png)

Les composants sélectionnés sont désormais disponibles dans l’explorateur de composants :

![component-design1](assets/component-design1.png)

## Clientlibs obligatoires {#required-clientlibs}

[Bibliothèques côté client](../../help/sites-developing/clientlibs.md) (clientlibs) sont nécessaires au bon fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lors de l’ajout d’un composant Communities à une page, si le résultat est une erreur ou une apparence inattendue, la première chose à essayer est d’ajouter les bibliothèques client requises pour le composant Communities. Pour plus d’informations, voir [Clientlibs des composants Communities](clientlibs.md).

### Exemple : révisions placées initialement sans bibliothèques clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### .. Et avec les bibliothèques clientes {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Balisage {#tagging}

De nombreuses fonctionnalités de Communities peuvent être configurées pour permettre aux membres de baliser le contenu saisi (publié) dans l’environnement de publication.

Si le balisage est autorisé, la configuration du site de la communauté peut être définie pour limiter les espaces de noms présentés aux membres dans l’environnement de publication. Voir [Console Sites de communauté](sites-console.md#tagging).

Fonctionnalités qui permettent le balisage : [blog](blog-feature.md), [calendar](calendar.md), [bibliothèque de fichiers](file-library.md), [forum](forum.md)

Fonctionnalités qui utilisent des balises : [search](search.md), [nuage de balises sociales](tagcloud.md)

Pour les informations de création :

* [Utilisation des balises](../../help/sites-authoring/tags.md)

Pour plus d’informations administratives :

* Création d’espaces de noms de balise (taxonomie) : [Administration des balises](../../help/sites-administering/tags.md)
* Configuration du site de la communauté : voir [BALISAGE](sites-console.md#tagging)
* [Balisage du contenu généré par l’utilisateur](../../help/sites-authoring/tags.md)

Pour plus d’informations sur les développeurs :

* [Framework de balisage AEM](../../help/sites-developing/framework.md)
* [Notions fondamentales sur le balisage](tag.md)
