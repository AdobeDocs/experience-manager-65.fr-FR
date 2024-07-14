---
title: Tally Essentials
description: Découvrez comment Tally est une classe abstraite qui fournit une méthode standard pour recueillir les commentaires des membres sur la valeur de produits et services spécifiques.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally est une classe abstraite qui fournit une méthode standard de collecte des commentaires des membres sur la manière dont ils évaluent des produits et services spécifiques. Les commentaires anonymes ne sont pas pris en charge. Les visiteurs du site doivent s’inscrire et se connecter pour participer et se connecter afin de modifier leurs commentaires. L’obligation de se connecter facilite la modération et améliore la valeur des commentaires en empêchant plusieurs publications.

Un composant tally personnalisé peut être créé en étendant la classe tally abstraite.

[J’aime](essentials-liking.md) est une mise en oeuvre d’un décompte qui est une forme simple d’expression d’une opinion positive.

[Voting](essentials-voting.md) est une mise en oeuvre d&#39;un décompte qui est une forme simple d&#39;expression d&#39;une opinion positive ou négative.

[Évaluation](rating-basics.md) est une mise en oeuvre de tally qui utilise un système star pour exprimer un éventail d’opinions, du positif au négatif.

À compter de la version AEM 6.1, le composant Sondage n’est plus disponible.

[Reviews](reviews-basics.md) est un composant SCF hybride de [commentaires](essentials-comments.md) et [rating](rating-basics.md).

## Principes élémentaires pour le côté client {#essentials-for-client-side}

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [Tally APIs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Points de terminaison Tally](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux balises publiées (UGC) {#accessing-posted-tallies-ugc}

Le contenu généré par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut l’accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu généré par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement.**

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - Présentation et utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes de l’utilitaire SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md) - Mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
