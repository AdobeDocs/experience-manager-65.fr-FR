---
title: Notions fondamentales sur les révisions
seo-title: Notions fondamentales sur les révisions
description: Composants Révisions et Résumé des révisions
seo-description: Composants Révisions et Résumé des révisions
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 6%

---

# Notions fondamentales sur les révisions {#reviews-essentials}

Cette fonctionnalité se compose de deux composants qui fonctionnent ensemble : révisions et résumé de révision.

Les révisions sont un composant composite basé sur un [système de commentaires](essentials-comments.md) qui contient un ou plusieurs composants [rating](rating-basics.md) (tally).

La publication anonyme d’une révision n’est pas possible. Les visiteurs du site doivent s’inscrire et se connecter pour ajouter une révision. Le visiteur connecté (membre) peut mettre à jour sa révision à tout moment.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

### Révisions {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/review/components/hbs/review</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>conception </i></td>
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
| [**incluable**](scf.md#add-or-include-a-communities-component) | Oui - les propriétés sont modifiables en mode *conception* |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriétés** | Voir [Utilisation des révisions](reviews.md) |

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires côté serveur {#essentials-for-server-side}

* [API de révision](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Points de fin de révision](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux révisions publiées (UGC) {#accessing-posted-reviews-ugc}

Le contenu généré par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu généré par l’utilisateur inclut l’accès programmatique au contenu généré par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md)  - Présentation et utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md)  - Méthodes et exemples d’utilitaire SRP.
* [Accès au contenu généré par l’utilisateur avec SRP](accessing-ugc-with-srp.md)  - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md)  : mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
