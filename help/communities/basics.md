---
title: Principes de base des composants de Communities
description: Ajout de fonctionnalités Communities aux sites AEM en mode d’édition et configuration de composants
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%
---
# Principes de base des composants de Communities {#communities-components-basics}

## Vue d’ensemble {#overview}

La section de création de la documentation décrit l’ajout de fonctionnalités Communities à des sites AEM en mode d’édition de création et décrit les configurations de composant.

Les composants peuvent être explorés à l’aide d’une instance AEM et du guide interactif [Guide des composants de la communauté](components-guide.md).

## Accès aux composants de Communities {#accessing-communities-components}

Lors de la création du contenu de la page, si le modèle sous-jacent autorise des modifications de conception de la page, il est possible d’activer des composants qui ne sont pas déjà disponibles dans l’explorateur de composants dans le cadre de la conception du site.

Consultez la liste sous [Composants de communautés disponibles](author-communities.md#available-communities-components).

>[!NOTE]
>
>Pour obtenir des informations générales sur la création, consultez le [guide rapide de création de pages](../../help/sites-authoring/qg-page-authoring.md).
>
>Si vous ne connaissez pas AEM, consultez la documentation sur la [manipulation de base](../../help/sites-authoring/basic-handling.md).

### Activation du mode de conception {#entering-design-mode}

Si un composant **Communities** est introuvable dans le navigateur de composants (sidekick), il sera nécessaire de saisir des `Design Mode` pour ajouter d’autres composants de Communities. Il se peut que vous deviez également ajouter les [bibliothèques côté client requises](#required-clientlibs) (clientlibs).

Pour plus d’informations, voir [Configuration des composants en mode Création](../../help/sites-authoring/default-components-designmode.md).

Vous trouverez ci-dessous des images de la sélection de quelques composants de communautés et de leur affichage dans l’explorateur de composants :

![conception-composant](assets/component-design.png)

Les composants sélectionnés sont désormais disponibles dans l’explorateur de composants :

![component-design1](assets/component-design1.png)

## Bibliothèques clientes requises {#required-clientlibs}

Les [bibliothèques côté client](../../help/sites-developing/clientlibs.md) (clientlibs) sont nécessaires au bon fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lors de l’ajout d’un composant Communities à une page, si le résultat est une erreur ou une apparence inattendue, la première chose à essayer est d’ajouter les bibliothèques clientes requises pour le composant Communities. Pour plus d’informations, voir [Bibliothèques clientes pour les composants de communautés](clientlibs.md).

### Exemple : révisions initialement placées sans bibliothèques clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Et avec les bibliothèques clientes {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Balisage {#tagging}

De nombreuses fonctionnalités de communautés peuvent être configurées pour permettre aux membres de baliser le contenu saisi (publié) dans l’environnement de publication.

Si le balisage est autorisé, la configuration du site de la communauté peut être définie pour limiter les espaces de noms présentés aux membres dans l’environnement de publication. Voir la [console Sites de la communauté](sites-console.md#tagging).

Fonctionnalités permettant le balisage : [blog](blog-feature.md), [calendar](calendar.md), [file library](file-library.md), [forum](forum.md)

Fonctionnalités qui utilisent les balises : [recherche](search.md), [cloud de balises sociales](tagcloud.md)

Pour la création d’informations :

* [Utilisation des balises](../../help/sites-authoring/tags.md)

Pour des informations administratives :

* Création d’espaces de noms de balises (taxonomie) : [Administration des balises](../../help/sites-administering/tags.md)
* Configuration du site de la communauté : voir [&#x200B; BALISAGE &#x200B;](sites-console.md#tagging)
* [Balisage de contenu généré par l’utilisateur](../../help/sites-authoring/tags.md)

Pour obtenir des informations sur le développeur :

* [Framework de balisage AEM](../../help/sites-developing/framework.md)
* [Balisage essentiel](tag.md)
