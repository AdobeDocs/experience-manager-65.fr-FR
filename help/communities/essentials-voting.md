---
title: Voter les fondamentaux
seo-title: Voter les fondamentaux
description: Présentation du composant de vote
seo-description: Présentation du composant de vote
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 2%

---


# Voter les fondamentaux {#voting-essentials}

La composante de vote, une sous-classe [de décompte](tally.md) , est un outil utile qui permet aux membres d&#39;évaluer un élément de contenu particulier en sélectionnant simplement des flèches vers le haut ou vers le bas pour indiquer leur opinion.

Le placement de plusieurs instances d&#39;un composant de vote sur la même page est autorisé ; chaque instance doit être configurée avec une `tally name` propriété unique.

La publication anonyme d&#39;un vote n&#39;est pas soutenue. Les visiteurs du site ne doivent s&#39;inscrire et se connecter pour participer au vote qu&#39;une seule fois, Le visiteur (membre) signé(e) peut changer son vote à tout moment.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/statistique/composants/hbs/vote</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Oui - les propriétés sont modifiables en <i>mode </i>conception</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>Voir <a href="voting.md">Utilisation du vote</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Points de terminaison du décompte](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès au vote publié (UGC) {#accessing-posted-voting-ugc}

L’UGC doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

Depuis AEM 6.1 Communities, l’utilisation d’un magasin [](working-with-srp.md) commun pour UGC inclut l’accès par programmation à UGC, quelle que soit l’option d’enregistrement choisie (telle que ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage.
* [SocialUtils Refactoring](socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

