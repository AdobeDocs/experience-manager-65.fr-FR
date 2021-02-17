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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 57%

---


# Notions fondamentales sur les composants d’AEM Communities {#communities-components-basics}

## Présentation {#overview}

La section création de la documentation décrit l’ajout de fonctionnalités AEM Communities à AEM Sites en mode d’édition et décrit les configurations des composants.

Les composants peuvent être explorés à l&#39;aide d&#39;une instance AEM et du [guide des composants de la communauté](components-guide.md) interactif.

## Accès aux composants d’AEM Communities {#accessing-communities-components}

Lors de la création du contenu de la page, si le modèle sous-jacent permet de modifier la conception de la page, il est possible d’activer des composants qui ne sont pas encore disponibles dans le navigateur de composants dans le cadre de la conception du site.

Les composants de communauté disponibles sont répertoriés [ici](author-communities.md#available-communities-components).

>[!NOTE]
>
>Pour obtenir des informations générales sur la création, vue le [guide rapide de création de pages](../../help/sites-authoring/qg-page-authoring.md).
>
>Si l’AEM n’est pas familière, vue la documentation sur la [gestion de base](../../help/sites-authoring/basic-handling.md).

### Accès au mode de conception {#entering-design-mode}

Si un composant **Communautés** est introuvable dans le navigateur de composants (sidekick), il sera nécessaire d&#39;entrer `Design Mode` pour ajouter d&#39;autres composants de communautés. [Il peut également être nécessaire d’ajouter des bibliothèques](#required-clientlibs)  côté client requises (clientlibs).

Pour plus d&#39;informations, voir [Configuration des composants en mode de conception](../../help/sites-authoring/default-components-designmode.md).

Vous trouverez ci-dessous des images de la sélection de quelques composants Communities et de leur affichage dans l’explorateur de composants :

![conception de composant](assets/component-design.png)

Les composants sélectionnés sont à présent disponibles dans le navigateur de composants :

![composant-design1](assets/component-design1.png)

## Clientlibs requises {#required-clientlibs}

Les [bibliothèques côté client](../../help/sites-developing/clientlibs.md) (clientlibs) sont nécessaires au fonctionnement (JavaScript) et au style (CSS) d’un composant.

Lorsque vous ajoutez un composant de communauté à une page, s’il en résulte une erreur ou une apparence inattendue, la première chose à essayer consiste à ajouter les clientlibs nécessaires au composant de communauté. Pour plus d’informations, reportez-vous à la section [Clientlibs des composants de communauté](clientlibs.md).

### Exemple : Révisions initialement placées sans bibliothèques clientes... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Et avec les bibliothèques client {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Balisage {#tagging}

De nombreuses fonctionnalités de communauté peuvent être configurées de manière à permettre aux membres de baliser le contenu entré (publié) dans l’environnement de publication.

Si le balisage est autorisé, la configuration du site de communauté peut être définie pour limiter les espaces de noms présentés aux membres dans l’environnement de publication. Voir la [console Sites communautaires](sites-console.md#tagging).

Fonctionnalités permettant le balisage : [blog](blog-feature.md), [calendrier](calendar.md), [bibliothèque de fichiers](file-library.md), [forum](forum.md)

Fonctionnalités utilisant des balises : [catalogue](catalog.md), [recherche](search.md), [nuage de balises sociales](tagcloud.md)

Pour les informations de création :

* [Utilisation des balises](../../help/sites-authoring/tags.md)

Pour les informations administratives :

* Création d’espaces de nommage de balises (taxonomie) : [Administration des balises](../../help/sites-administering/tags.md)
* Configuration du site de la communauté : voir [BALISAGE](sites-console.md#tagging)
* [Balisage de contenu généré par l’utilisateur](../../help/sites-authoring/tags.md)
* [Balisage des ressources d’activation](tag-resources.md) 

Pour les informations de développement :

* [Cadre de balisage AEM](../../help/sites-developing/framework.md)
* [Notions fondamentales sur le balisage](tag.md)

