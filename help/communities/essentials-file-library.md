---
title: Principes de base de la bibliothèque de fichiers
description: Découvrez les principes de base de l’utilisation de la fonction Bibliothèque de fichiers dans Adobe Experience Manager Communities.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6d653331-c1ce-4ccb-bb45-656b6413ac3e
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%
---
# Principes de base de la bibliothèque de fichiers {#file-library-essentials}

Cette page présente les informations fondamentales relatives à l&#39;utilisation de la fonction Bibliothèque de fichiers.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.votes<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
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

## Essentials pour côté serveur {#essentials-for-server-side}

* [API de bibliothèque de fichiers](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [Points d’entrée de la bibliothèque de fichiers](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site de communauté qui inclut la fonction [Bibliothèque de fichiers](functions.md#file-library-function) comprend un composant `file library` configuré.

### Accès aux commentaires publiés pour les bibliothèques de fichiers (UGC) {#accessing-comments-posted-for-file-libraries-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes utilitaires obsolètes aux méthodes utilitaires SRP actuelles.
