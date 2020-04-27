---
title: Reviews Essentials
seo-title: Reviews Essentials
description: Révisions et révision des composants Résumé
seo-description: Révisions et révision des composants Résumé
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Reviews Essentials {#reviews-essentials}

Cette fonctionnalité comprend deux composants qui fonctionnent ensemble : révisez et examinez le résumé.

Reviews est un composant composite basé sur un système [de](essentials-comments.md) commentaires qui contient un ou plusieurs composants de [notation](rating-basics.md) (tally).

La publication anonyme d’une révision n’est pas possible. Les du site doivent s’enregistrer et se connecter pour ajouter une révision. Le (membre) connecté(e) peut mettre à jour sa révision à tout moment.

## Essentials for Client-Side {#essentials-for-client-side}

### Révisions {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Oui - les propriétés sont modifiables en <i>mode </i>de conception</td>
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

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**inclus **](scf.md#add-or-include-a-communities-component) | Oui - les propriétés peuvent être modifiées en *mode de conception * |
| [**clientllibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriétés** | Voir [Utilisation des révisions](reviews.md) |

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API de révision](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Points de fin de révision](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux révisions publiées (UGC) {#accessing-posted-reviews-ugc}

L’UGC doit être modérée à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

Depuis la version 6.1 des Communautés AEM, l’utilisation d’un magasin [](working-with-srp.md) commun pour l’UGC inclut l’accès par programmation à l’UGC, quelle que soit l’option de   choisie (par exemple, ASRP, MSRP ou JSRP).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Aperçu](srp.md) du fournisseur de ressources  - Présentation et aperçu de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [Réfactorisation](socialutils.md) de SocialUtils : mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

