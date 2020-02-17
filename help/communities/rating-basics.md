---
title: Notation Essentials
seo-title: Notation Essentials
description: Présentation du composant Évaluation
seo-description: Présentation du composant Évaluation
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Notation Essentials {#rating-essentials}

Le composant de notation, une sous-classe [de décompte](tally.md) , permet aux membres de la communauté connectés d’évaluer une fonction sur le site Web.

Le placement de plusieurs instances d’un composant de vote sur la même page est autorisé ; chaque instance doit être configurée avec une `tally name` propriété unique.

La publication anonyme d’une évaluation n’est pas possible. Les visiteurs du site ne doivent s’inscrire et se connecter qu’une seule fois pour participer à une évaluation. Le visiteur (membre) connecté peut modifier sa note à tout moment.

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

* [Points de terminaison des chiffres](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux notes publiées (UGC) {#accessing-posted-ratings-ugc}

L’UGC doit être modérée à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

Depuis les communautés AEM 6.1, l’utilisation d’un magasin [](working-with-srp.md) commun pour l’UGC inclut l’accès par programmation à l’UGC, quelle que soit l’option de stockage choisie (par exemple, ASRP, MSRP ou JSRP).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md) du fournisseur de ressources de stockage - présentation et présentation de l&#39;utilisation du référentiel
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d&#39;utilitaires SRP
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage
* [SocialUtils Refactoring](socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

