---
title: Notions fondamentales sur les composants, les fonctions et les fonctionnalités
description: Fonctionnement des sites, modèles et groupes de communautés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 18%

---

# Notions fondamentales sur les composants, les fonctions et les fonctionnalités  {#component-function-and-feature-essentials}

Les fonctionnalités d’Adobe Experience Manager (AEM) Communities exigent que les visiteurs du site deviennent membres et se connectent au [site communautaire](overview.md#communitiessites) avant de pouvoir publier du contenu. Ainsi, [modèles de site de communauté](sites.md), à partir de laquelle un site communautaire est [created](sites-console.md), sont conçues pour inclure une fonction de connexion et des profils utilisateur, la messagerie, la recherche, la modération et la traduction.

Un site communautaire prend en charge les membres qui créent des groupes communautaires lorsque [fonction de groupes communautaires](functions.md#groups-function) est inclus dans le modèle de site de la communauté sélectionné.

Vous trouverez ci-dessous des liens vers des informations essentielles pour les composants, fonctions et fonctionnalités de Communities.

## Composants de base {#base-components}

* [Commentaires](essentials-comments.md)
* [Révisions](reviews-basics.md)
* [Tally](tally.md)

   * [Aimer](essentials-liking.md)
   * [Évaluation](rating-basics.md)
   * [Votant](essentials-voting.md)
   * *Sondage (n’est plus disponible)*

## Composants avec fonctions {#components-with-functions}

* [Flux d’activités](essentials-activities.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

* [Calendrier](calendar-basics-for-developers.md)
* [Contenu proposé](essentials-featured.md)
* [Bibliothèque de fichiers](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Groupes](essentials-groups.md)
* [Conceptualisation](ideation.md)
* [Classement](leaderboard.md)
* [Questions et réponses](qna-essentials.md) `(QnA)`

## Fonctions {#features}

* [Bibliothèques clientes](clientlibs.md)
* [Sites de la communauté](sites-for-developers.md)
* [Événements OSGi des composants](events.md)
* [Chargement partiel des composants](sideloading.md)
* [Message](essentials-messaging.md)
* [Éditeur de texte enrichi](rte.md)
* [Notation et badges](configure-scoring.md)
* [Recherche](search-implementation.md)
* [Graphique des réseaux sociaux](essentials-socialgraph.md)
* [Fournisseur de ressources de stockage](srp-and-ugc.md) `(SRP)`

* [Balisage](tag.md)

## Javadocs {#javadocs}

Le [javadocs en ligne](../../help/sites-developing/reference-materials.md) reflètent les API disponibles dans la version 6.3 d’AEM.
Les API Communities se trouvent dans `com.adobe.cq.social.*` modules.

Pour chaque [feature pack](deploy-communities.md#latestfeaturepack), un jar javadoc est disponible. Pour plus d’informations, voir [Utilisation de Maven pour Communities](maven.md#javadocs).

## Informations supplémentaires {#additional-information}

* [Structure des composants sociaux (SCF)](scf.md)

   * [Personnalisations côté client](client-customize.md)
   * [Personnalisations côté serveur](server-customize.md)
   * [Présentation du fournisseur de ressources de stockage](srp.md)

* [Consignes de codage](code-guide.md)
* [Tutoriels](tutorials.md)
* [Résolution des problèmes](troubleshooting.md)
