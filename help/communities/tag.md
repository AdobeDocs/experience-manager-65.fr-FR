---
title: Notions fondamentales sur les balises
seo-title: Tag Essentials
description: Présentation des balises
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 3%

---

# Notions fondamentales sur les balises {#tag-essentials}

Lorsque les composants AEM Communities sont configurés avec le balisage activé, les membres de la communauté peuvent baliser le contenu qu’ils publient dans l’environnement de publication.

L’infrastructure sous-jacente des balises appliquées dans l’environnement de publication est la même que pour les balises appliquées au contenu dans l’environnement de création, telles que les pages et les ressources :

* Voir [Administration des balises](../../help/sites-administering/tags.md) et [Balisage du contenu généré par l’utilisateur](tag-ugc.md) (contenu généré par l’utilisateur) pour plus d’informations sur la création et la gestion des balises.

* Voir [Balisage pour les développeurs](../../help/sites-developing/tags.md) pour plus d’informations sur le [framework de balisage](../../help/sites-developing/framework.md) ainsi que l’inclusion et l’extension de balises dans [applications personnalisées](../../help/sites-developing/building.md).

* Voir [Utilisation de Social Tag Cloud](tagcloud.md) pour plus d’informations pour les auteurs sur la manière d’ajouter une `social tag cloud` à une page pour mettre en surbrillance les balises appliquées au contenu généré par l’utilisateur dans l’environnement de publication.

Le balisage du contenu généré par l’utilisateur peut être activé lors de la configuration d’un [site communautaire](sites-console.md#tagging) ou l’une des fonctionnalités suivantes :

* [Blog](blog-feature.md)
* [Calendrier](calendar.md)
* [Bibliothèque de fichiers](file-library.md)
* [Forum](forum.md)
* [Q&amp;R](working-with-qna.md)

## Principes élémentaires pour le côté client {#essentials-for-client-side}

### Nuage de balises sociales {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
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
   <td>Voir <a href="tagcloud.md">Utilisation de Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API Social Tag Cloud](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gestionnaire de balises sociales](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

## Recherche de balises {#tag-searching}

À partir de [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), la recherche de balises est effectuée à l’aide de [titres de balise](../../help/sites-developing/framework.md#tag-characteristics).

Avant FP1, la recherche était effectuée à l’aide de [ID de balise](../../help/sites-developing/framework.md#tagid).
