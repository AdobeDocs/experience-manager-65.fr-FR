---
title: Tag Essentials
seo-title: Tag Essentials
description: Présentation des balises
seo-description: Présentation des balises
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---


# Tag Essentials {#tag-essentials}

Lorsque les composants AEM Communities sont configurés avec le balisage activé, les membres de la communauté peuvent baliser le contenu qu’ils publient dans l’environnement de publication.

L’infrastructure sous-jacente pour les balises appliquées dans l’environnement de publication est la même que pour les balises appliquées au contenu dans l’environnement d’auteur, telles que les pages et les ressources :

* See [Administering Tags](../../help/sites-administering/tags.md) and [Tagging User Generated Content](tag-ugc.md) (UGC) for information about creating and managing tags.

* See [Tagging for Developers](../../help/sites-developing/tags.md) for information about the [tagging framework](../../help/sites-developing/framework.md) as well as including and extending tags in [custom applications](../../help/sites-developing/building.md).

* Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour en savoir plus pour les auteurs sur la façon d’ajouter un `social tag cloud` composant à une page afin de mettre en surbrillance les balises appliquées à UGC dans l’environnement de publication.

* Voir Ressources [d’activation du](tag-resources.md) balisage pour en savoir plus sur les ressources de balisage pour les catalogues.

Le balisage de l’UGC peut être activé lors de la configuration d’un site [](sites-console.md#tagging) communautaire ou de l’une des fonctionnalités suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md)
* [Q&amp;R](working-with-qna.md)

## Essentials for Client-Side {#essentials-for-client-side}

### Nuage de balises sociales {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/composants/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>See <a href="tagcloud.md">Using Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API Cloud de balises sociales](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gestionnaire de balises sociales](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

## Recherche de balises {#tag-searching}

A compter de [Feature Pack 1](deploy-communities.md#latestfeaturepack) (FP1), la recherche de balises est effectuée à l’aide des titres [de](../../help/sites-developing/framework.md#tag-characteristics)balises.

Avant FP1, la recherche était effectuée à l’aide des identifiants [de](../../help/sites-developing/framework.md#tagid)balise.
