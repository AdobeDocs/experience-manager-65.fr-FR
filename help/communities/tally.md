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

---


# Tally Essentials {#tally-essentials}

Tally est une classe abstraite qui fournit une méthode standard pour recueillir les commentaires des membres sur la façon dont ils évaluent des produits et des services particuliers. Les commentaires anonymes ne sont pas pris en charge. Le du site doit s&#39;inscrire et se connecter pour participer et se connecter pour changer ses commentaires. L’obligation de se connecter facilite la modération et améliore la valeur des commentaires en empêchant plusieurs publications.

Un composant tally personnalisé peut être créé en étendant la classe tally abstraite.

[J&#39;aime](essentials-liking.md) est une mise en oeuvre du décompte qui est une forme simple d&#39;exprimer une opinion positive.

[Le vote](essentials-voting.md) est une mise en oeuvre du décompte qui est une forme simple d&#39;expression d&#39;une opinion positive ou négative.

[La notation](rating-basics.md) est une mise en oeuvre de la mesure qui utilise un système d&#39;étoiles pour exprimer une gamme d&#39;opinions allant du positif au négatif.

Depuis AEM 6.1, le composant d’interrogation n’est plus disponible.

[Reviews](reviews-basics.md) est un composant SCF qui est un hybride de [commentaires](essentials-comments.md) et de [cotation](rating-basics.md).

## Essentials for Client-Side {#essentials-for-client-side}

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Points de terminaison du décompte](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux tests publiés (UGC) {#accessing-posted-tallies-ugc}

L’UGC doit être modérée à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

Depuis la version 6.1 des Communautés AEM, l’utilisation d’un magasin [](working-with-srp.md) commun pour l’UGC inclut l’accès par programmation à l’UGC, quelle que soit l’option de   choisie (par exemple, ASRP, MSRP ou JSRP).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Aperçu](srp.md) du fournisseur de ressources  - Présentation et aperçu de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [Réfactorisation](socialutils.md) de SocialUtils : mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

