---
title: QnA Essentials
seo-title: QnA Essentials
description: Fonctionnalité du forum des questions et réponses
seo-description: Fonctionnalité du forum des questions et réponses
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 3%

---


# QnA Essentials {#qna-essentials}

Cette page fournit les informations essentielles pour travailler sur le forum des questions et réponses (QnA).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">inclus</a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> templates</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> properties</td>
   <td>See <a href="working-with-qna.md">Q&amp;A Forum Feature</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Points de terminaison QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Q&amp;R {#qna-function}

Une structure de site communautaire qui inclut la fonction [](functions.md#qna-function) QnA aura un `QnA` composant configuré, ainsi que des paramètres affectant la modération et le balisage. La fonction QnA prend en charge l&#39;identification d&#39;un groupe [d&#39;utilisateurs](users.md#privileged-members-group)privilégiés.

### Accès aux publications du forum QnA (UGC) {#accessing-qna-forum-posts-ugc}

L’UGC doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](moderate-ugc.md)généré par l’utilisateur.

AEM 6.1 Collectivités, l&#39;utilisation d&#39;un magasin [](working-with-srp.md) commun pour l&#39;UGC comprend l&#39;accès programmatique à l&#39;UGC, quelle que soit l&#39;option d&#39;enregistrement choisie (comme ASRP, MSRP ou JSRP).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation](srp.md) du fournisseur de ressources d&#39;Enregistrement - présentation et présentation de l&#39;utilisation du référentiel.
* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - directives de codage.
* [SocialUtils Refactoring](socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

