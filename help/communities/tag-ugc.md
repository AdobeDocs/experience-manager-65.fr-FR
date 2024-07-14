---
title: Balisage du contenu généré par l’utilisateur
description: Le balisage du contenu généré par l’utilisateur (UGC) permet aux membres de la communauté d’aider d’autres membres à rechercher du contenu.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 4%

---

# Balisage du contenu généré par l’utilisateur {#tagging-user-generated-content}

## Vue d’ensemble {#overview}

Le balisage du contenu généré par les utilisateurs est le moyen par lequel les membres de la communauté peuvent aider d’autres membres à rechercher du contenu.

En règle générale, les balises sont appliquées par les auteurs et les administrateurs dans l’environnement de création. Le balisage UGC est unique dans la mesure où les balises UGC sont appliquées par les membres de la communauté dans l’environnement de publication.

Les espaces de noms de balise et les taxonomies sont identiques pour les deux applications.

## Fonctions de communauté {#communities-features}

Les fonctionnalités AEM Communities qui peuvent être configurées pour autoriser le balisage sont les suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Questions et réponses](working-with-qna.md)

## Administration des balises {#administering-tags}

Voir [Administration des balises](../../help/sites-administering/tags.md#tagging-console) pour créer et gérer des espaces de noms et des taxonomies de balise.

Voir [Notions fondamentales sur les balises](tag.md) pour plus d’informations sur les développeurs.

Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour ajouter un composant Nuage de balises sociales à une page afin de faciliter la recherche de contenu généré par l’utilisateur à l’aide des balises appliquées.

### Autorisations de balise {#tag-permissions}

Les autorisations par défaut sont définies de manière à ne pas autoriser la lecture des espaces de noms de balise par tous les membres de l’environnement de publication.

Les balises étant appliquées au contenu créé par l’utilisateur dans l’environnement de publication, les autorisations de lecture doivent être activées pour les membres de la communauté afin qu’ils puissent sélectionner les balises à appliquer.

Voir [Définition des autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions).

Voici comment il apparaît dans CRXDE lorsqu’un administrateur applique des autorisations de lecture à `/etc/tag/discussions` pour le groupe `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
