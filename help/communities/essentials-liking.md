---
title: Essentials
seo-title: Essentials
description: Présentation du composant J’aime
seo-description: Présentation du composant J’aime
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---


# Essentials {#liking-essentials}

Le composant &quot;J’aime&quot;, une sous-classe [dénombrable](tally.md) , est un outil utile qui permet aux membres d’exprimer une opinion positive sur un élément de contenu particulier en sélectionnant simplement l’icône du coeur.

Le placement de plusieurs instances d’un composant de type J’aime sur la même page est autorisé ; chaque instance doit être configurée avec une `tally name` propriété unique.

La publication anonyme d’un &quot;j’aime&quot; n’est pas prise en charge. Les visiteurs du site doivent s&#39;inscrire et se connecter pour participer à aimer. Le visiteur (membre) connecté peut basculer comme activé et désactivé à tout moment.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/like</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Oui - les propriétés sont modifiables en <i>mode </i>conception</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>Voir <a href="liking.md">Utilisation de la fonction J’aime</a></p> </td>
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

AEM 6.1 Collectivités, l&#39;utilisation d&#39;un magasin [](working-with-srp.md) commun pour l&#39;UGC comprend l&#39;accès programmatique à l&#39;UGC, quelle que soit l&#39;option d&#39;enregistrement choisie (comme ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage.
* [SocialUtils Refactoring](socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

