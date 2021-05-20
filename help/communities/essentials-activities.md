---
title: Notions fondamentales sur les flux d’activités
seo-title: Notions fondamentales sur les flux d’activités
description: Liste des activités récentes effectuées par un membre ou liste des activités récentes sur un seul fil de contenu
seo-description: Liste des activités récentes effectuées par un membre ou liste des activités récentes sur un seul fil de contenu
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---

# Notions fondamentales sur les flux d’activités {#activity-stream-essentials}

Les activités d’un membre de la communauté connecté, comme la publication sur un forum ou un blog, sont collectées dans un flux qui peut être filtré et affiché de différentes manières via la configuration du composant Flux d’activités.

La possibilité de suivre ajoute un autre ensemble d’activités lorsque les membres de la communauté suivent des messages d’intérêt ou d’autres membres de la communauté.

Tous les [sites communautaires](/help/communities/overview.md#communitiessites) incluent une page de profil utilisateur pour le membre connecté qui affichera les activités du membre de la même manière.

## Concepts  {#concepts}

Un *flux d’activités* est la liste des activités récentes exécutées par un membre ou une liste des activités récentes sur un seul fil de contenu, tel qu’un sujet de forum ou un blog.

Un membre peut suivre un flux d’activité en suivant un autre individu ou un autre contenu.

Un *fil d’actualités* est une fusion des flux d’activité suivis par un membre dans un seul flux.

Un *[graphique social](/help/communities/essentials-socialgraph.md)* capture les relations suivantes d’un membre à un autre.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
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
   <td>Voir <a href="/help/communities/activities.md">Fonctionnalité de flux d’activités</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](/help/communities/client-customize.md)

## Principes élémentaires côté serveur {#essentials-for-server-side}

* [API Flux d’activités](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API du récepteur de flux d’activités](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Flux d&#39;activités {#activity-stream-function}

Une structure de site de communauté qui comprend la fonction [Flux d’activités](/help/communities/functions.md#activity-stream-function), comprend un composant `activity streams` configuré.
