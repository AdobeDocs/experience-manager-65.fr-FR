---
title: Principes de base du groupe de la communauté
description: Découvrez comment les utilisateurs et utilisatrices autorisés peuvent utiliser la fonction Groupes de communautés pour créer de manière dynamique une sous-communauté au sein d’un site de communauté.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%
---
# Principes de base du groupe de la communauté  {#community-group-essentials}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement au sein d’un site communautaire par des utilisateurs autorisés des environnements de publication et de création.

À partir de Communities [pack de fonctionnalités 1](deploy-communities.md#latestfeaturepack), il est possible que les groupes soient imbriqués dans d’autres groupes.

## Essentials pour le côté client {#essentials-for-client-side}

### Liste des membres des groupes communautaires {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir <a href="creating-groups.md">Groupe communautaire</a></td>
  </tr>
 </tbody>
</table>

### Groupes communautaires {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Community Group](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Points d’entrée du groupe de la communauté](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction de groupes {#groups-function}

Une structure de site de communauté qui comprend une [fonction Groups](functions.md#groups-function) prend en charge la création de nouveaux `community groups` à partir des environnements de publication et de création. Le groupe communautaire créé comprend un composant `community groups member list` qui répertorie les membres du groupe .

Un ou plusieurs [modèles de groupe de la communauté](tools-groups.md), qui fournissent la conception des pages du groupe de la communauté, peuvent être configurés pour la fonction Groupes. C’est le cas lorsque la fonction est ajoutée à un [modèle de site de la communauté](sites.md) ou imbriquée dans un modèle de groupe de la communauté.

L’inclusion de plusieurs modèles de groupe de la communauté permet de faire un choix. C’est-à-dire le choix de la conception qui est présenté à l’utilisateur ou à l’utilisatrice autorisé(e) au moment de la création d’un groupe communautaire pour le site communautaire. Voir la section sur les [groupes de communautés](creating-groups.md) pour les auteurs.

### Groupes imbriqués {#nested-groups}

Depuis Communities [FP1](deploy-communities.md#latestfeaturepack), il est possible d&#39;inclure une fonction de groupes dans un modèle de groupe, ce qui permet d&#39;imbriquer des groupes (sous-communautés).

Lorsqu’un site de la communauté ou un modèle de groupe inclut la fonction Groupes , il est possible de :

* Créez une sous-communauté dans l’environnement de création.

* Créez un groupe dans l’environnement de publication lorsque vous le configurez pour l’autoriser.

Lors de la création d’un groupe dans l’environnement de création, il est nécessaire de publier d’abord le site de la communauté, puis de publier le groupe. La publication du site de la communauté publie les pages du groupe, sans créer les groupes membres de la sous-communauté auxquels des listes de contrôle d’accès sont définies. Ainsi, un groupe restreint (secret) peut être visible jusqu’à ce que le groupe soit explicitement publié.

## Liens et informations connexes {#links-and-related-information}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Console Groupes de communautés](groups.md)
* [Fonction de groupes](functions.md#groups-function)
* [Modèles de groupe](tools-groups.md)
