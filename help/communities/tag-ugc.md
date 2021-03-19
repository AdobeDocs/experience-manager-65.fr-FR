---
title: Balisage de contenu généré par l’utilisateur
seo-title: Balisage de contenu généré par l’utilisateur
description: Le balisage du contenu généré par l’utilisateur (UGC) permet aux membres de la communauté d’aider d’autres membres à rechercher du contenu.
seo-description: Le balisage du contenu généré par l’utilisateur (UGC) permet aux membres de la communauté d’aider d’autres membres à rechercher du contenu.
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 9%

---


# Balisage de contenu généré par l’utilisateur {#tagging-user-generated-content}

## Présentation {#overview}

Le balisage du contenu généré par l’utilisateur est le moyen par lequel les membres de la communauté peuvent aider les autres membres à rechercher du contenu.

En règle générale, les balises sont appliquées par les auteurs et les administrateurs dans l’environnement d’auteur. Le balisage UGC est unique en ce sens que les balises UGC sont appliquées par les membres de la communauté dans l’environnement de publication.

Les espaces de nommage de balise et les taxonomies sont identiques pour les deux applications.

## Fonctionnalités des communautés {#communities-features}

Les fonctionnalités AEM Communities qui peuvent être configurées pour autoriser le balisage sont les suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Questions et réponses](working-with-qna.md)

## Administration des balises {#administering-tags}

Voir [Administration des balises](../../help/sites-administering/tags.md#tagging-console) pour créer et gérer des espaces de nommage et des taxonomies de balises.

Voir [Tag Essentials](tag.md) pour en savoir plus sur les développeurs.

Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour ajouter un composant Social Tag Cloud à une page afin de faciliter la recherche d’UGC publié à l’aide des balises appliquées.

### Permissions de balise {#tag-permissions}

Les autorisations par défaut sont définies de manière à ne pas autoriser la lecture des espaces de nommage de balises par tous les utilisateurs de l’environnement de publication.

Les balises étant appliquées à l’UGC dans l’environnement de publication, les autorisations de lecture doivent être activées pour les membres de la communauté afin qu’ils puissent sélectionner les balises à appliquer.

Voir [Définition des autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions).

Voici comment il apparaît dans CRXDE lorsqu’un administrateur applique des autorisations de lecture à `/etc/tag/discussions` pour le groupe `Community Engage Members`.

![balises-permissions](assets/tag-permissions.png)

