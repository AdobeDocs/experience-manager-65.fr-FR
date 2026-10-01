---
title: Tag Essentials
description: Découvrez quand les composants de Communities sont configurés avec le balisage activé, les membres de la communauté peuvent baliser le contenu qu’ils publient dans l’environnement de publication.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 3%
---
# Tag Essentials {#tag-essentials}

Lorsque les composants AEM Communities sont configurés avec le balisage activé, les membres de la communauté peuvent baliser le contenu qu’ils publient dans l’environnement de publication.

L’infrastructure sous-jacente pour les balises appliquées dans l’environnement de publication est la même que pour les balises appliquées au contenu dans l’environnement de création, comme les pages et les ressources :

* Voir [Administration des balises](../../help/sites-administering/tags.md) et [Balisage du contenu créé par l’utilisateur](tag-ugc.md) (UGC) pour plus d’informations sur la création et la gestion des balises.

* Consultez [Balisage pour les développeurs](../../help/sites-developing/tags.md) pour plus d’informations sur le [framework de balisage](../../help/sites-developing/framework.md) ainsi que sur l’inclusion et l’extension de balises dans les [applications personnalisées](../../help/sites-developing/building.md).

* Consultez [Utilisation du cloud de balises sociales](tagcloud.md) pour plus d’informations concernant l’ajout d’un composant `social tag cloud` à une page afin de mettre en évidence les balises appliquées au contenu créé par l’utilisateur dans l’environnement de publication.

Le balisage du contenu créé par l’utilisateur peut être activé lors de la configuration d’un [site communautaire](sites-console.md#tagging) ou de l’une des fonctionnalités suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md)
* [Q&amp;R](working-with-qna.md)

## Essentials pour le côté client {#essentials-for-client-side}

### Nuage de balises sociales {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>Voir <a href="tagcloud.md">Utilisation du cloud de balises sociales</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API Social Tag Cloud](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gestionnaire de balises sociales](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

## Recherche de balises {#tag-searching}

Depuis [Feature Pack 1](deploy-communities.md#latestfeaturepack) (FP1), la recherche de balises est effectuée à l’aide de [titres de balises](../../help/sites-developing/framework.md#tag-characteristics).

Avant FP1, la recherche était effectuée à l’aide de [ID de balise](../../help/sites-developing/framework.md#tagid).
