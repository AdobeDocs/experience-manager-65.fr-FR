---
title: QnA Essentials
description: Découvrez les principes de base de l’utilisation de la fonctionnalité Forum des questions et réponses (QnA) dans les communautés Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%
---
# QnA Essentials {#qna-essentials}

Cette page fournit des informations essentielles sur l’utilisation de la fonctionnalité de forum des questions et réponses (QnA).

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">include</a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.votes<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> modèles</td>
   <td> <br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> properties</td>
   <td>Voir <a href="working-with-qna.md">Fonctionnalité Forum Questions/Réponses</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API QnA](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Points d’entrée QnA](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Q&amp;R {#qna-function}

Une structure de site de communauté qui inclut la fonction [QnA](functions.md#qna-function) comporte un composant `QnA` configuré, ainsi que des paramètres affectant la modération et le balisage. La fonction QnA prend en charge l’identification d’un [groupe d’utilisateurs membre privilégié](users.md#privileged-members-group).

### Accès aux publications du forum QnA (UGC) {#accessing-qna-forum-posts-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu créé par l’utilisateur](moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes utilitaires obsolètes aux méthodes utilitaires SRP actuelles.
