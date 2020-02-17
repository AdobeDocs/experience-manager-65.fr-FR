---
title: Balisage de contenu généré par l’utilisateur
seo-title: Balisage de contenu généré par l’utilisateur
description: Le balisage du contenu généré par l’utilisateur (UGC) permet aux membres de la communauté de rechercher du contenu.
seo-description: Le balisage du contenu généré par l’utilisateur (UGC) permet aux membres de la communauté de rechercher du contenu.
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Balisage de contenu généré par l’utilisateur {#tagging-user-generated-content}

## Présentation {#overview}

Le balisage du contenu généré par l’utilisateur (UGC) est le moyen par lequel les membres de la communauté peuvent aider les autres membres à rechercher du contenu.

En règle générale, les balises sont appliquées par les auteurs et les administrateurs dans l’environnement de création. Le balisage UGC est unique dans la mesure où les balises UGC sont appliquées par les membres de la communauté dans l’environnement de publication.

Les espaces de noms de balises et les taxonomies sont identiques pour les deux applications.

## Fonctionnalités des communautés {#communities-features}

Les fonctionnalités des communautés AEM qui peuvent être configurées pour autoriser le balisage sont

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Questions et réponses](working-with-qna.md)

## Administration des balises {#administering-tags}

Voir [Administration des balises](../../help/sites-administering/tags.md#tagging-console) pour créer et gérer des espaces de noms de balises et des taxonomies.

Voir [Tag Essentials](tag.md) pour en savoir plus sur les développeurs.

Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour l’ajout d’un composant Social Tag Cloud à une page afin de faciliter la recherche d’UGC publié à l’aide des balises appliquées.

### Autorisations de balise {#tag-permissions}

Les autorisations par défaut sont définies de manière à ne pas autoriser tous les utilisateurs de l’environnement de publication à lire les espaces de noms des balises.

Les balises étant appliquées à l’UGC dans l’environnement de publication, les autorisations de lecture doivent être activées pour les membres de la communauté afin qu’ils puissent sélectionner les balises à appliquer.

See [Setting Tag Permissions](../../help/sites-administering/tags.md#setting-tag-permissions).

Voici comment il s’affiche dans CRXDE lorsqu’un administrateur applique des autorisations de lecture `/etc/tag/discussions` pour le groupe `*Community Engage Members*`.

![chlimage_1-74](assets/chlimage_1-74.png)

