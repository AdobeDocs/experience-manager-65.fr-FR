---
title: Principes fondamentaux des composants, des fonctions et des fonctionnalités
description: Fonctionnement des sites, modèles et groupes de la communauté
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
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
source-wordcount: '211'
ht-degree: 16%
---
# Principes fondamentaux des composants, des fonctions et des fonctionnalités  {#component-function-and-feature-essentials}

Les fonctionnalités des communautés Adobe Experience Manager (AEM) exigent des visiteurs du site qu’ils deviennent membres et se connectent au [site de la communauté](overview.md#communitiessites) avant de pouvoir publier du contenu. Ainsi, les [modèles de site communautaire](sites.md), à partir desquels un site communautaire est [créé](sites-console.md), sont conçus pour inclure une fonctionnalité de connexion et des profils utilisateur, la messagerie, la recherche, la modération et la traduction.

Un site communautaire prend en charge les membres qui créent des groupes communautaires lorsque la fonction [groupes communautaires](functions.md#groups-function) est incluse dans le modèle de site communautaire sélectionné.

Vous trouverez ci-dessous des liens vers des informations essentielles sur les composants, fonctions et fonctionnalités de Communities.

## Composants de base {#base-components}

* [Commentaires](essentials-comments.md)
* [Révisions](reviews-basics.md)
* [Décompte](tally.md)

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

## Fonctionnalités {#features}

* [Bibliothèques clientes](clientlibs.md)
* [Sites de la communauté](sites-for-developers.md)
* [Événements OSGi de composant](events.md)
* [Chargement latéral des composants](sideloading.md)
* [Message](essentials-messaging.md)
* [Éditeur de texte enrichi](rte.md)
* [Notation et badges](configure-scoring.md)
* [Recherche](search-implementation.md)
* [Graphique des réseaux sociaux](essentials-socialgraph.md)
* [Fournisseur de ressources de stockage](srp-and-ugc.md) `(SRP)`

* [Balisage](tag.md)

## Javadocs {#javadocs}

Les [javadocs en ligne](../../help/sites-developing/reference-materials.md) reflètent les API disponibles dans la version 6.3 d’AEM.
Les API Communities se trouvent dans des packages `com.adobe.cq.social.*`.

Pour chaque pack de fonctionnalités [pack](deploy-communities.md#latestfeaturepack), un fichier javadoc jar est disponible. Pour plus d’informations, consultez [Utilisation de Maven pour les communautés](maven.md#javadocs).

## Informations supplémentaires {#additional-information}

* [Structure des composants sociaux (SCF)](scf.md)

  * [Personnalisations côté client](client-customize.md)
  * [Personnalisations côté serveur](server-customize.md)
  * [Présentation du fournisseur de ressources de stockage](srp.md)

* [Consignes de codage](code-guide.md)
* [Tutoriels](tutorials.md)
* [Résolution des problèmes](troubleshooting.md)
