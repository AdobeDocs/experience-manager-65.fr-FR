---
title: Tally Essentials
seo-title: Tally Essentials
description: Présentation de la classe Tally
seo-description: Présentation de la classe Tally
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally est une classe abstraite qui fournit une méthode standard pour recueillir les commentaires des membres sur la façon dont ils évaluent des produits et services spécifiques. Les commentaires anonymes ne sont pas pris en charge. Le visiteur du site doit s&#39;inscrire et se connecter pour participer et se connecter pour changer ses commentaires. L’obligation de se connecter facilite la modération et améliore la valeur des commentaires en empêchant plusieurs publications.

Un composant tally personnalisé peut être créé en étendant la classe tally abstraite.

[Le ](essentials-liking.md) Likingis est une mise en oeuvre du décompte qui est une forme simple d&#39;expression d&#39;une opinion positive.

[Le ](essentials-voting.md) vote est une mise en oeuvre du décompte qui est une forme simple d&#39;expression d&#39;une opinion positive ou négative.

[](rating-basics.md) Ratingis est une mise en oeuvre de tally qui utilise un système star pour exprimer une gamme d&#39;opinions allant du positif au négatif.

À partir de AEM 6.1, le composant Sondage n’est plus disponible.

[](reviews-basics.md) Révision d&#39;un composant SCF qui est un hybride de  [](essentials-comments.md) commentaires et de  [cotation](rating-basics.md).

## Essentials for Client-Side {#essentials-for-client-side}

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Points de terminaison du décompte](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux tests publiés (UGC) {#accessing-posted-tallies-ugc}

L’UGC doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

À partir de AEM 6.1 Communautés, l&#39;utilisation d&#39;un [magasin commun](working-with-srp.md) pour l&#39;UGC comprend l&#39;accès programmatique à l&#39;UGC, quelle que soit l&#39;option d&#39;enregistrement choisie (comme ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md)  du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md)  - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec des directives de codage SRP](accessing-ugc-with-srp.md) .
* [SocialUtils Refactoring](socialutils.md)  - Mise en correspondance des méthodes d’utilitaire obsolètes avec les méthodes d’utilitaire SRP actuelles.

