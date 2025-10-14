---
title: Notions fondamentales sur les composants, les fonctions et les fonctionnalités
description: Fonctionnement des sites, modèles et groupes de communautés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 16%

---

# Notions fondamentales sur les composants, les fonctions et les fonctionnalités  {#component-function-and-feature-essentials}

Les fonctionnalités de communauté Adobe Experience Manager (AEM) exigent que les visiteurs du site deviennent membres et se connectent au [site de la communauté](overview.md#communitiessites) avant de pouvoir publier du contenu. Par conséquent, les [&#x200B; modèles de site communautaire &#x200B;](sites.md), à partir desquels un site communautaire est [créé](sites-console.md), sont conçus pour inclure une fonction de connexion et des profils utilisateur, la messagerie, la recherche, la modération et la traduction.

Un site communautaire prend en charge la création de groupes communautaires lorsque la [fonction de groupes communautaires](functions.md#groups-function) est incluse dans le modèle de site de communauté sélectionné.

Vous trouverez ci-dessous des liens vers des informations essentielles pour les composants, fonctions et fonctionnalités de Communities.

## Composants de base {#base-components}

* [Commentaires](essentials-comments.md)
* [Révisions](reviews-basics.md)
* [Tally](tally.md)

   * [Aimer](essentials-liking.md)
   * [Évaluation](rating-basics.md)
   * [Votant](essentials-voting.md)
   * *Sondage (plus disponible)*

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

Les [javadocs en ligne](../../help/sites-developing/reference-materials.md) reflètent les API disponibles dans la version AEM 6.3.
Les API Communities se trouvent dans les packages `com.adobe.cq.social.*`.

Pour chaque [feature pack](deploy-communities.md#latestfeaturepack), un jar javadoc est disponible. Pour plus d’informations, consultez la page [Utilisation de Maven pour Communities](maven.md#javadocs).

## Informations supplémentaires {#additional-information}

* [Structure des composants sociaux (SCF)](scf.md)

   * [Personnalisations côté client](client-customize.md)
   * [Personnalisations côté serveur](server-customize.md)
   * [Présentation du fournisseur de ressources de stockage](srp.md)

* [Consignes de codage](code-guide.md)
* [Tutoriels](tutorials.md)
* [Résolution des problèmes](troubleshooting.md)
