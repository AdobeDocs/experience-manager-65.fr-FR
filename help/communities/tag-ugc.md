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
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Balisage de contenu généré par l’utilisateur {#tagging-user-generated-content}

## Présentation {#overview}

Le balisage du contenu généré par l’utilisateur (UGC) est le moyen par lequel les membres de la communauté peuvent aider d’autres membres à rechercher du contenu.

En règle générale, les balises sont appliquées par les auteurs et les administrateurs dans le  l’auteur . Le balisage UGC est unique dans la mesure où les balises UGC sont appliquées par les membres de la communauté dans l’environnement de publication.

La balise   et les taxonomies sont identiques pour les deux applications.

## Fonctionnalités des communautés {#communities-features}

Les fonctionnalités des communautés AEM qui peuvent être configurées pour autoriser le balisage sont les suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md#configuretheaddedforum)
* [Questions et réponses](working-with-qna.md)

## Administration des balises {#administering-tags}

Voir [Administration des balises](../../help/sites-administering/tags.md#tagging-console) pour la création et la gestion des balises   et taxonomies.

Voir [Tag Essentials](tag.md) pour en savoir plus sur les développeurs.

Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour l’ajout d’un composant Social Tag Cloud à une page afin de faciliter la recherche d’UGC publié à l’aide des balises appliquées.

### Autorisations de balise {#tag-permissions}

Les autorisations par défaut sont définies de manière à ne pas autoriser les balises  les à être lus par tout le monde dans le de publication .

Etant donné que les balises sont appliquées à l’UGC dans le  de publication , l’autorisation de lecture doit être activée pour les membres de la communauté afin qu’ils puissent sélectionner les balises à appliquer.

See [Setting Tag Permissions](../../help/sites-administering/tags.md#setting-tag-permissions).

Voici comment il s’affiche dans CRXDE lorsqu’un administrateur applique des autorisations de lecture `/etc/tag/discussions` pour le groupe `Community Engage Members`.

![chlimage_1-74](assets/chlimage_1-74.png)

