---
title: Notions fondamentales sur les révisions
description: Découvrez comment les révisions dans AEM Communities est un composant composite basé sur un système de commentaires contenant un ou plusieurs composants d’évaluation (dièse).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# Notions fondamentales sur les révisions {#reviews-essentials}

Cette fonctionnalité se compose de deux composants qui fonctionnent ensemble : les révisions et la synthèse des révisions.

Les révisions sont un composant composite basé sur un [système de commentaires](essentials-comments.md) qui contient un ou plusieurs composants [rating](rating-basics.md) (tally).

La publication anonyme d’une révision n’est pas prise en charge. Les visiteurs du site doivent s’inscrire et se connecter pour ajouter une révision. Le visiteur connecté (membre) peut mettre à jour sa révision à tout moment.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

### Révisions {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/review/components/hbs/review</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>design </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir <a href="reviews.md">Utilisation des révisions</a></td>
  </tr>
 </tbody>
</table>

### Résumé des critiques {#review-summary}

| **resourceType** | social/review/components/hbs/summary |
|---|---|
| [**includable**](scf.md#add-or-include-a-communities-component) | Oui - les propriétés sont modifiables en mode *conception* |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriétés** | Voir [Utilisation des révisions](reviews.md) |

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API de révision](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Points de terminaison de révision](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux révisions publiées (UGC) {#accessing-posted-reviews-ugc}

Le contenu généré par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut l’accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu généré par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement.**

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - Présentation et utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes de l’utilitaire SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md) - Mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
