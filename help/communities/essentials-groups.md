---
title: Essentials du groupe communautaire
seo-title: Essentials du groupe communautaire
description: Création dynamique de sites de la communauté
seo-description: Création dynamique de sites de la communauté
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Essentials du groupe communautaire {#community-group-essentials}

La fonction des groupes communautaires permet à une sous-communauté d’être créée dynamiquement dans un site communautaire par des utilisateurs autorisés à partir des environnements de publication et d’auteur.

A compter du [Feature Pack 1](deploy-communities.md#latestfeaturepack)Collectivités, il est possible d’imbriquer des groupes dans d’autres groupes.

## Essentials for Client-Side {#essentials-for-client-side}

### Liste des membres des groupes communautaires {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/groupe/composants/hbs/community/groupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.community.groups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir Groupe <a href="creating-groups.md">de communautés</a></td>
  </tr>
 </tbody>
</table>

### Groupes communautaires {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/groupe/composants/hbs/groupes communautaires</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.community.groups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Groupe de communautés](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Points de fin du groupe de communautés](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Groupes {#groups-function}

Une structure de site de la communauté qui comprend une fonction [](functions.md#groups-function) Groupes permettra de créer de nouveaux sites `community groups` à partir des environnements de publication et d’auteur. Le groupe de communauté créé comprendra un `community groups member list` composant qui dressera la liste des membres du groupe.

Un ou plusieurs modèles [de groupe](tools-groups.md)communautaire, qui fournissent la conception des pages de groupe communautaire, peuvent être configurés pour la fonction Groupes lorsque la fonction est ajoutée à un modèle [de site](sites.md) communautaire ou imbriquée dans un modèle de groupe communautaire.

L’inclusion de plusieurs modèles de groupes communautaires entraîne la présentation d’une conception à l’utilisateur autorisé au moment de la création d’un nouveau groupe communautaire pour le site communautaire, comme le montre la section sur les groupes [](creating-groups.md) communautaires pour les auteurs.

### Groupes imbriqués {#nested-groups}

Depuis le [FP1](deploy-communities.md#latestfeaturepack)Collectivités, il est possible d&#39;inclure une fonction Groupes dans un modèle de groupe, ce qui permet d&#39;inclure des groupes imbriqués (sous-communautés).

Lorsqu’un site de la communauté ou un modèle de groupe inclut la fonction Groupes, il est possible de

* Création d’une sous-communauté dans l’environnement de création
* Créez un groupe dans l’environnement de publication, lorsqu’il est configuré pour l’autoriser.

Lors de la création d’un groupe dans l’environnement d’auteur, vous devez d’abord publier le site de la communauté, puis le groupe. La publication du site de la communauté publiera les pages du groupe, sans créer les groupes de membres de la sous-communauté auxquels les listes ACL sont définies. Ainsi, un groupe restreint (secret) peut être visible jusqu’à ce que le groupe soit explicitement publié.

## Liens et informations connexes {#links-and-related-information}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Console Groupes de communautés](groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe](tools-groups.md)

