---
title: Aspects essentiels du vote
description: Découvrez comment utiliser le composant Vote qui permet aux membres d’évaluer un élément de contenu particulier en sélectionnant les flèches vers le haut ou vers le bas pour indiquer leur opinion.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%
---
# Aspects essentiels du vote {#voting-essentials}

Le composant « vote », une sous-classe [tally](tally.md), est un outil utile qui permet aux membres d’évaluer un élément de contenu particulier en sélectionnant simplement les flèches vers le haut ou vers le bas pour indiquer leur opinion.

Le placement de plusieurs instances d’un composant « vote » sur la même page est autorisé ; chaque instance doit être configurée avec une propriété `tally name` unique.

La publication anonyme d&#39;un vote n&#39;est pas prise en charge. Les visiteurs du site doivent s’inscrire et se connecter pour participer au vote une seule fois. Le visiteur connecté (membre) peut modifier son vote à tout moment.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/votes</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>conception</i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.votes</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td><p> <br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>Voir <a href="voting.md"> Utilisation du vote</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Tally](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Total des points d’entrée](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès au vote enregistré (UGC) {#accessing-posted-voting-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes utilitaires obsolètes aux méthodes utilitaires SRP actuelles.
