---
title: Bibliothèque de fichiers Essentials
seo-title: Bibliothèque de fichiers Essentials
description: Utilisation de la fonction de bibliothèque de fichiers
seo-description: Utilisation de la fonction de bibliothèque de fichiers
uuid: 0630f13e-97b4-4f93-9dce-07f559287c29
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9019b967-fff8-4dda-bc5a-fd4a3e14a4ef
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---


# Fichier Library Essentials {#file-library-essentials}

Cette page fournit les informations essentielles pour utiliser la fonction de bibliothèque de fichiers.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="file-library.md">Fonction de bibliothèque de fichiers</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API de bibliothèque de fichiers](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [Points de terminaison de la bibliothèque de fichiers](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site communautaire qui comprend la fonction [Bibliothèque de fichiers](functions.md#file-library-function), comprend un composant `file library` configuré.

### Accès aux commentaires publiés pour les bibliothèques de fichiers (UGC) {#accessing-comments-posted-for-file-libraries-ugc}

L’UGC doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

À partir de AEM 6.1 Communautés, l&#39;utilisation d&#39;un [magasin commun](working-with-srp.md) pour l&#39;UGC comprend l&#39;accès programmatique à l&#39;UGC, quelle que soit l&#39;option d&#39;enregistrement choisie (comme ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Aperçu](srp.md)  du fournisseur de ressources d&#39;Enregistrement - présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md)  - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec des directives de codage SRP](accessing-ugc-with-srp.md) .
* [SocialUtils Refactoring](socialutils.md)  - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

