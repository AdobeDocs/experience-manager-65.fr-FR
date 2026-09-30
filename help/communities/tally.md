---
title: Tally Essentials
description: Découvrez comment Tally est une classe abstraite qui fournit une méthode standard de collecte des commentaires des membres sur la manière dont ils accordent de la valeur à des produits et services spécifiques.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%
---
# Tally Essentials {#tally-essentials}

Tally est une classe abstraite qui fournit une méthode standard pour recueillir les commentaires des membres sur la façon dont ils apprécient des produits et services spécifiques. Les commentaires anonymes ne sont pas pris en charge. Les visiteurs du site doivent s’inscrire et se connecter pour participer et se connecter pour modifier leurs commentaires. L&#39;obligation de se connecter facilite la modération et améliore la valeur du retour d&#39;informations en empêchant la publication de plusieurs publications.

Un composant Tally personnalisé peut être créé en étendant la classe Abstract Tally.

[Liking](essentials-liking.md) est une mise en œuvre du calcul qui est une forme simple d&#39;expression d&#39;une opinion positive.

Le [vote](essentials-voting.md) est une mise en œuvre du décompte qui est une forme simple d&#39;expression d&#39;une opinion positive ou négative.

[Rating](rating-basics.md) est une implémentation de tally qui utilise un système d&#39;étoiles pour exprimer une gamme d&#39;opinions, positives ou négatives.

Depuis AEM 6.1, le composant sondage n’est plus disponible.

[Examens](reviews-basics.md) est un composant SCF qui est un hybride de [commentaires](essentials-comments.md) et [évaluation](rating-basics.md).

## Essentials pour le côté client {#essentials-for-client-side}

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Tally](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Total des points d’entrée](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux comptes publiés (UGC) {#accessing-posted-tallies-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - Introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles.
