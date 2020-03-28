---
title: '  de diffusion en continu Essentials'
seo-title: '  de diffusion en continu Essentials'
description: des activités récentes effectuées par un membre ou un d’un  récent de la  sur un seul thread de contenu
seo-description: des activités récentes effectuées par un membre ou un d’un  récent de la  sur un seul thread de contenu
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


#   de diffusion en continu Essentials {#activity-stream-essentials}

Le  d’un membre de la communauté connecté, tel qu’une publication sur un forum ou un blog, est collecté dans un flux qui peut être filtré et affiché de différentes manières par le biais de la configuration du composant de flux de de la .

La capacité de suivre ajoute un autre ensemble de   lorsque les membres de la communauté suivent des messages d&#39;intérêt ou d&#39;autres membres de la communauté.

Tous les sites [de la](/help/communities/overview.md#communitiessites) communauté incluent une page de  d’utilisateur pour le membre connecté qui affichera  de membre de la même manière.

## Concepts {#concepts}

Un flux *de* est le d’un récenteffectué par un membre ou un d’un récent sur un seul fil de contenu, tel qu’un sujet de forum ou un blog.

Un membre peut suivre un flux  , soit en suivant un autre individu, soit en suivant un autre contenu.

Un flux *d&#39;informations* est une fusion des flux  de  suivis par un membre dans un seul flux.

Un graphique *[](/help/communities/essentials-socialgraph.md)*social capture les relations suivantes entre un membre et un autre.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystream/components/hbs/activitystream</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystream</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>voir <a href="/help/communities/activities.md">fonction  flux de</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API de flux](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API d’écoute de flux](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Flux d&#39;activités {#activity-stream-function}

Une structure de site de la communauté qui inclut la fonction [de flux de  de](/help/communities/functions.md#activity-stream-function), inclut un `activity streams` composant configuré.
