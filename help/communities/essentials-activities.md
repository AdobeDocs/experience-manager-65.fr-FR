---
title: Essentiels du flux d’activités
description: Liste des activités récentes effectuées par un membre ou liste des activités récentes sur un seul thread de contenu
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
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
source-wordcount: '311'
ht-degree: 2%
---
# Essentiels du flux d’activités {#activity-stream-essentials}

Les activités d’un membre de la communauté connecté, telles que la publication sur un forum ou un blog, sont collectées dans un flux qui peut être filtré et affiché de différentes manières par le biais de la configuration du composant flux d’activités.

La possibilité de suivre ajoute un autre ensemble d’activités lorsque les membres de la communauté suivent des publications d’intérêt ou d’autres membres de la communauté.

Tous les [sites de la communauté](/help/communities/overview.md#communitiessites) incluent une page de profil utilisateur pour le membre connecté qui affichera les activités du membre de la même manière.

## Concepts {#concepts}

Un *flux d’activités* est la liste des activités récentes effectuées par un membre ou une liste d’activités récentes sur un seul thread de contenu, tel qu’un sujet de forum ou un blog.

Un membre peut suivre un flux d’activités, en suivant un autre individu ou un autre contenu.

Un *flux d’actualités* est une fusion des flux d’activités suivis par un membre en un seul flux.

Un *[graphique social](/help/communities/essentials-socialgraph.md)* capture les relations suivantes d’un membre à l’autre.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="/help/communities/activities.md"> Fonctionnalité Flux d’activités </a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](/help/communities/client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API des flux d’activités](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API Listener des flux d’activités](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Flux d&#39;activités {#activity-stream-function}

Une structure de site de communauté qui inclut la fonction [Flux d’activités](/help/communities/functions.md#activity-stream-function) comprend un composant `activity streams` configuré.
