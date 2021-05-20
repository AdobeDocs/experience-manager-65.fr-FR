---
title: Notions fondamentales sur les commentaires
seo-title: Notions fondamentales sur les commentaires
description: Présentation du composant Commentaires
seo-description: Présentation du composant Commentaires
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---

# Notions fondamentales sur les commentaires {#comments-essentials}

Cette page fournit l’essentiel de l’utilisation du système de commentaires (composant de commentaires) et des options de gestion du contenu généré par l’utilisateur (contenu généré par les utilisateurs) lorsque les membres publient des commentaires ou des réponses.

Le composant Commentaires établit un système de commentaire, de sorte que chaque publication soit représentée par un composant de commentaire (au singulier). Il s’agit du système de commentaires inclus sur la page. Le système de commentaires crée les commentaires individuels lorsqu’ils sont appelés.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>conception </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.votes</td>
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
   <td> Voir <a href="comments.md">Utilisation des commentaires</a></td>
  </tr>
 </tbody>
</table>

[Personnalisations côté client](client-customize.md)

### Une instance par page {#one-instance-per-page}

La pagination et l’utilisation d’URL pour la mise en cache et la liaison nécessitent que l’URL soit unique par système de commentaire. Par conséquent, une seule instance d’un système de commentaires est autorisée par page.

D’autres fonctionnalités incluent déjà le système de commentaires. à savoir :

* [Blog](blog-developer-basics.md)
* [Calendrier](calendar-basics-for-developers.md)
* [Bibliothèque de fichiers](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Q&amp;R](qna-essentials.md)
* [Révisions](reviews-basics.md)

### Marquer la liste de motifs {#flag-reason-list}

La liste des raisons de marquage peut être personnalisée en ajoutant flagreasonlist.hbs à votre application pour remplacer ce qui se trouve dans .

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Cela s’applique à tout composant qui étend un système de commentaires.

## Principes élémentaires côté serveur {#essentials-for-server-side}

* [API de commentaires](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Points de fin des commentaires](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux commentaires publiés (UGC) {#accessing-posted-comments-ugc}

Le contenu généré par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération de contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu généré par l’utilisateur inclut l’accès programmatique au contenu généré par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md)  - Présentation et utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md)  - Méthodes et exemples d’utilitaire SRP.
* [Accès au contenu généré par l’utilisateur avec SRP](accessing-ugc-with-srp.md)  - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md)  : mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
