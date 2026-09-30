---
title: Blog Essentials
description: Découvrez comment ajouter la fonction Blog à une page afin que les membres de la communauté connectés puissent publier des articles de blog.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 3%
---
# Blog Essentials {#blog-essentials}

Depuis AEM 6.1 Communities, un blog est une activité de la communauté. Les articles de blog sont désormais publiés à partir de l’environnement de publication, où, auparavant, ils ne pouvaient être créés et publiés que dans l’environnement de création.

Les articles de blog peuvent maintenant être créés par n&#39;importe quel membre de la communauté, sauf s&#39;ils sont réservés aux membres privilégiés.

Cette page fournit des informations essentielles sur l’utilisation de la fonctionnalité de blog.

>[!NOTE]
>
>L’infrastructure sous-jacente de la fonction de blog est la fonction de journal.

## Essentials pour le côté client {#essentials-for-client-side}

La fonction de blog est composée de deux composants principaux qui sont disponibles en ajoutant la [fonction de blog](/help/communities/functions.md#blog-function) ou en ajoutant les composants à une page en mode d’édition création.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.votes<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>voir <a href="/help/communities/blog-feature.md"> Fonctionnalité de blog </a></td>
  </tr>
 </tbody>
</table>

### Barre latérale de blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**inclusible**](/help/communities/scf.md#add-or-include-a-communities-component) | Non |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **modèles** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propriétés** | voir [ Fonctionnalité de blog ](/help/communities/blog-feature.md) |

* [Personnalisations côté client](/help/communities/client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API de blog](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Points d’entrée de blog](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Blog {#blog-function}

Une structure de site de communauté qui inclut la [fonction Blog](/help/communities/functions.md#blog-function) comporte des composants `Blog` et `Blog Sidebar` configurés. La fonction Blog prend en charge l’identification d’un [groupe d’utilisateurs membre privilégié](/help/communities/users.md#privileged-members-group).

### Accès aux entrées de blog (UGC) {#accessing-blog-entries-ugc}

Le contenu créé par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](/help/communities/working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md) - introduction et présentation de l’utilisation du référentiel.
* [SRP et UGC Essentials](/help/communities/srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](/help/communities/accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](/help/communities/socialutils.md) - Mappage des méthodes utilitaires obsolètes aux méthodes utilitaires SRP actuelles.

## Principal Publisher {#primary-publisher}

Lorsque le déploiement est une ferme de publication, il est nécessaire d’identifier un éditeur principal qui recherche les articles devant être publiés.

Voir [Principal Publisher](/help/communities/deploy-communities.md#primary-publisher) pour plus d&#39;informations.

## Autorisation des médias riches {#allowing-rich-media}

La plateforme AEM bloque les liens d’autres sites web afin d’empêcher les attaques XSS, comme décrit dans la section

* [la fonctionnalité Protection contre les failles cross-site scripting (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

Depuis AEM 6.2, les modifications précédemment requises pour être effectuées manuellement sont incluses dans le fichier de configuration AntiSamy par défaut.

Les médias riches sont incorporés dans un article de blog en sélectionnant l’icône `Embed Media from External Sites` :

![média](assets/media-icon.png)
