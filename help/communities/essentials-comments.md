---
title: Commentaires Essentiels
description: Découvrez comment utiliser le système de commentaires (composant Commentaires) et gérer le contenu créé par l’utilisateur dans les publications des membres de la communauté.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 4%
---
# Commentaires Essentiels {#comments-essentials}

Cette page présente les principes de base de l’utilisation du système de commentaires (composant Commentaires) et des options de gestion du contenu créé par l’utilisateur ou l’utilisatrice (UGC) généré lorsque les membres publient des commentaires ou des réponses.

Le composant « Commentaires » établit un système de commentaires de sorte que chaque message individuel soit représenté par un composant « Commentaire » (au singulier). C’est le système de commentaires qui est inclus sur la page. Le système de commentaires crée les commentaires individuels lorsqu’ils sont appelés.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Oui - les propriétés sont modifiables en mode <i>conception</i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.sharing</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td> Voir <a href="comments.md"> Utilisation des commentaires </a></td>
  </tr>
 </tbody>
</table>

[Personnalisations côté client](client-customize.md)

### Une Instance Par Page {#one-instance-per-page}

La pagination et l’utilisation des URL pour la mise en cache et la liaison nécessitent que l’URL soit unique par système de commentaires. Par conséquent, une seule instance d’un système de commentaires est autorisée par page.

D&#39;autres fonctionnalités incluent déjà le système de commentaires. Ces principes sont les suivants :

* [Blog](blog-developer-basics.md)
* [Calendrier](calendar-basics-for-developers.md)
* [Bibliothèque de fichiers](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Q&amp;R](qna-essentials.md)
* [Révisions](reviews-basics.md)

### Marquer la liste de motifs {#flag-reason-list}

La liste des raisons de l’indicateur peut être personnalisée en ajoutant flagreasonlist.hbs à votre application pour remplacer ce qui y est

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Cela s’applique à tout composant qui étend un système de commentaires.

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Comments](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Points d’entrée Comments](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Accès aux commentaires publiés (UGC) {#accessing-posted-comments-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu créé par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - Introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles.
