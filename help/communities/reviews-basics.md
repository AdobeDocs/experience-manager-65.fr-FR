---
title: Reviews Essentials
description: Découvrez comment Reviews in AEM Communities est un composant composite basé sur un système de commentaires qui contient un ou plusieurs composants d’évaluation (total).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 2%
---
# Reviews Essentials {#reviews-essentials}

Cette fonctionnalité se compose de deux composants qui fonctionnent ensemble : révisions et résumé de révision.

Reviews est un composant composite basé sur un système [comment](essentials-comments.md) qui contient un ou plusieurs composants [rating](rating-basics.md) (tally).

La publication anonyme d’une révision n’est pas prise en charge. Les visiteurs du site doivent s’enregistrer et se connecter pour ajouter une révision. Le visiteur connecté (membre) peut mettre à jour sa révision à tout moment.

## Essentials pour le côté client {#essentials-for-client-side}

### Révisions {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>réseaux sociaux/avis/composants/hbs/avis</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>conception</i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.views</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
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

| **resourceType** | réseaux sociaux/révisions/composants/hbs/summary |
|---|---|
| [**inclusible**](scf.md#add-or-include-a-communities-component) | Oui - les propriétés sont modifiables en mode *conception* |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.views |
| **modèles** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriétés** | Voir [Utilisation des révisions](reviews.md) |

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [Vérifier l’API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Vérifier les points d’entrée](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux avis publiés (UGC) {#accessing-posted-reviews-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - Introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles.
