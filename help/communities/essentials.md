---
title: Notions fondamentales sur les composants, les fonctions et les fonctionnalités
seo-title: Notions fondamentales sur les composants, les fonctions et les fonctionnalités
description: Fonctionnement des sites, modèles et groupes de communautés
seo-description: Fonctionnement des sites, modèles et groupes de communautés
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 18%

---

# Notions fondamentales sur les composants, les fonctions et les fonctionnalités {#component-function-and-feature-essentials}

Les fonctionnalités d’AEM Communities exigent que les visiteurs du site deviennent membres et se connectent au [site de la communauté](overview.md#communitiessites) avant de pouvoir publier du contenu. Ainsi, les [modèles de site communautaire](sites.md), à partir desquels un site communautaire est [créé](sites-console.md), sont conçus pour inclure une fonction de connexion ainsi que des profils utilisateur, des messages, des recherches, de la modération et des traductions.

Un site communautaire prend en charge la création de groupes communautaires lorsque les [groupes communautaires fonctionnent](functions.md#groups-function) sont inclus dans le modèle de site communautaire sélectionné.

Vous trouverez ci-dessous des liens vers des informations essentielles pour les composants, fonctions et fonctionnalités de Communities.

## Composants de base {#base-components}

* [Commentaires](essentials-comments.md)
* [Révisions](reviews-basics.md)
* [Tally](tally.md)

   * [Aimer](essentials-liking.md)
   * [Évaluation](rating-basics.md)
   * [Vote](essentials-voting.md)
   * *Sondage (n’est plus disponible)*

## Composants avec fonctions {#components-with-functions}

* [Flux d’activités](essentials-activities.md)
* [Affectations](essentials-assignments.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

* [Calendrier](calendar-basics-for-developers.md)
* [Catalogue](catalog-developer-essentials.md)
* [Contenu proposé](essentials-featured.md)
* [Bibliothèque de fichiers](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Groupes](essentials-groups.md)
* [Conceptualisation](ideation.md)
* [Classement](leaderboard.md)
* [Questions et réponses](qna-essentials.md) `(QnA)`

## Fonctions {#features}

* [Bibliothèques clientes](clientlibs.md)
* [Sites communautaires](sites-for-developers.md)
* [Événements OSGi des composants](events.md)
* [Chargement partiel des composants](sideloading.md)
* [Message](essentials-messaging.md)
* [Éditeur de texte enrichi](rte.md)
* [Notation et badges](configure-scoring.md)
* [Rechercher](search-implementation.md)
* [Graphique des réseaux sociaux](essentials-socialgraph.md)
* [Fournisseur de ressources de stockage](srp-and-ugc.md) `(SRP)`

* [Balisage](tag.md)

## Javadocs {#javadocs}

Les [javadocs en ligne](../../help/sites-developing/reference-materials.md) reflètent les API disponibles dans la version 6.3 d’AEM.
Les API Communities se trouvent dans les packages `com.adobe.cq.social.*`.

Pour chaque [Feature Pack](deploy-communities.md#latestfeaturepack), un jar javadoc est disponible. Pour plus d’informations, voir [Utilisation de Maven pour Communities](maven.md#javadocs).

## Informations supplémentaires {#additional-information}

* [Structure des composants sociaux (SCF)](scf.md)

   * [Personnalisations côté client](client-customize.md)
   * [Personnalisations côté serveur](server-customize.md)
   * [Présentation du fournisseur de ressources de stockage](srp.md)

* [Consignes de codage](code-guide.md)
* [Tutoriels](tutorials.md)
* [Résolution des problèmes](troubleshooting.md)
