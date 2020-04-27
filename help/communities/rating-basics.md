---
title: Notation Essentials
seo-title: Notation Essentials
description: Présentation du composant de notation
seo-description: Présentation du composant de notation
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
translation-type: tm+mt
source-git-commit: b7318370c45f37a7faf5434b2de3f145b8d64bce

---


# Notation Essentials {#rating-essentials}

Le composant de notation, une sous-classe [de décompte](tally.md) , permet aux membres de la communauté connectés d’évaluer une fonction sur le site Web.

Le placement de plusieurs instances d’un composant de vote sur la même page est autorisé ; chaque instance doit être configurée avec une `tally name` propriété unique.

La publication anonyme d’une évaluation n’est pas possible. Les du site doivent s&#39;inscrire et se connecter pour participer à une évaluation une seule fois. Le (membre) connecté(e) peut modifier sa note à tout moment.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Oui - les propriétés sont modifiables en <i>mode </i>de conception</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>Voir <a href="rating.md">Utilisation de la notation</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Points de terminaison du décompte](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux notes publiées (UGC) {#accessing-posted-ratings-ugc}

L’UGC doit être modérée à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

Depuis la version 6.1 des Communautés AEM, l’utilisation d’un magasin [](working-with-srp.md) commun pour l’UGC inclut l’accès par programmation à l’UGC, quelle que soit l’option de   choisie (par exemple, ASRP, MSRP ou JSRP).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Aperçu](srp.md) du fournisseur de ressources  - présentation et aperçu de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage.
* [Réfactorisation](socialutils.md) de SocialUtils : mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

