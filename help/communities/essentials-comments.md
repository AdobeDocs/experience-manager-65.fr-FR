---
title: Commentaires essentiels
seo-title: Commentaires essentiels
description: Présentation du composant Commentaires
seo-description: Présentation du composant Commentaires
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---


# Commentaires essentiels {#comments-essentials}

Cette page fournit l&#39;essentiel de l&#39;utilisation du système de commentaires (composant de commentaires) et des options de gestion du contenu généré par l&#39;utilisateur (UGC) produit lorsque les membres publient des commentaires ou des réponses.

Le composant Commentaires établit un système de commentaires de sorte que chaque publication individuelle soit représentée par un composant Commentaire (singulier). C&#39;est le système de commentaires qui est inclus sur la page. Le système de commentaires crée les commentaires individuels lorsqu’ils sont appelés.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/biens communs/composants/hbs/commentaires</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Oui - les propriétés sont modifiables en <i>mode </i>conception</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.vote</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td> Voir <a href="comments.md">Utilisation de commentaires</a></td>
  </tr>
 </tbody>
</table>

[Personnalisations côté client](client-customize.md)

### Une instance par page {#one-instance-per-page}

La pagination et l’utilisation d’URL pour la mise en cache et la liaison nécessitent que l’URL soit unique par système de commentaires. Par conséquent, une seule instance d’un système de commentaires est autorisée par page.

D&#39;autres fonctionnalités incluent déjà le système de commentaires. à savoir :

* [Blog](blog-developer-basics.md)
* [Calendrier](calendar-basics-for-developers.md)
* [Bibliothèque de fichiers](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Q&amp;R](qna-essentials.md)
* [Révisions](reviews-basics.md)

### Marquer la liste de motifs {#flag-reason-list}

La liste de motif de marquage peut être personnalisée en ajoutant flagreasonlist.hbs à votre application pour remplacer ce qui se trouve dans

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Cela s&#39;applique à tout composant qui étend un système de commentaires.

## Essentials for Server-Side {#essentials-for-server-side}

* [API de commentaires](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Points de terminaison des commentaires](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux commentaires publiés (UGC) {#accessing-posted-comments-ugc}

L’UGC doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

AEM 6.1 Collectivités, l&#39;utilisation d&#39;un magasin [](working-with-srp.md) commun pour l&#39;UGC comprend l&#39;accès programmatique à l&#39;UGC, quelle que soit l&#39;option d&#39;enregistrement choisie (comme ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - Présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - Règles de codage.
* [Refactorisation](socialutils.md) de SocialUtils - Mise en correspondance des méthodes d’utilitaire obsolètes avec les méthodes d’utilitaire SRP actuelles.

