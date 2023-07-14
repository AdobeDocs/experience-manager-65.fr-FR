---
title: Notions fondamentales sur les groupes de communautés
description: Création dynamique de sites communautaires
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: 681d1e6bd885b801b930e580d95645f160f17cea
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---

# Notions fondamentales sur les groupes de communautés  {#community-group-essentials}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site de communauté par des utilisateurs autorisés à partir des environnements de publication et de création.

À partir des communautés [feature pack 1](deploy-communities.md#latestfeaturepack), il est possible d’imbriquer des groupes dans d’autres groupes.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

### Liste des membres des groupes communautaires {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community/groupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
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
   <td>Voir <a href="creating-groups.md">Groupe de communautés</a></td>
  </tr>
 </tbody>
</table>

### Groupes communautaires {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community-groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
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

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API du groupe de communautés](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Points de terminaison du groupe de communautés](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Groupes {#groups-function}

Une structure de site communautaire qui comprend [Fonction Groupes](functions.md#groups-function) prend en charge la création de `community groups` dans les environnements de publication et de création. Le groupe de communauté créé comprend une `community groups member list` qui répertorie les membres du groupe.

Un ou plusieurs [modèles de groupe de communautés](tools-groups.md), qui fournissent la conception des pages de groupe de communautés, peut être configuré pour la fonction Groupes lorsque la fonction est ajoutée à une [modèle de site communautaire](sites.md) ou imbriqué dans un modèle de groupe de communautés.

L’inclusion de plusieurs modèles de groupe de communautés entraîne la présentation d’une conception à l’utilisateur autorisé au moment de la création d’un groupe de communautés pour le site de la communauté, comme illustré dans la section sur [groupes communautaires](creating-groups.md) pour les auteurs.

### Groupes imbriqués {#nested-groups}

À partir des communautés [FP1](deploy-communities.md#latestfeaturepack), il est possible qu’une fonction Groupes soit incluse dans un modèle de groupe, ce qui permet d’inclure des groupes imbriqués (sous-communautés).

Lorsqu’un site de communauté ou un modèle de groupe comprend la fonction Groupes , il est possible de :

* Créez une sous-communauté dans l’environnement de création.

* Créez un groupe dans l’environnement de publication, lorsqu’il est configuré pour l’autoriser.

Lors de la création d’un groupe dans l’environnement de création, vous devez d’abord publier le site de la communauté, puis publier le groupe. La publication du site de la communauté publie les pages du groupe, sans créer les groupes de membres de la sous-communauté auxquels des listes de contrôle d’accès sont définies. Ainsi, un groupe restreint (secret) peut être visible jusqu’à ce que le groupe soit publié explicitement.

## Liens et informations connexes {#links-and-related-information}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Console Groupes de communautés](groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe](tools-groups.md)
