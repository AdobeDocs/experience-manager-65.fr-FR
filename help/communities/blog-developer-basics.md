---
title: Notions fondamentales sur les blogs
seo-title: Blog Essentials
description: Présentation des blogs
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# Notions fondamentales sur les blogs {#blog-essentials}

Depuis AEM 6.1 Communities, un blog est une activité communautaire. Les articles de blog sont maintenant publiés à partir de l’environnement de publication, où auparavant, les articles de blog ne pouvaient être créés que dans l’environnement de création et publiés.

Les articles de blog peuvent maintenant être créés par n&#39;importe quel membre de la communauté, sauf si cela est limité aux membres privilégiés.

Cette page fournit les informations essentielles pour utiliser la fonction de blog.

>[!NOTE]
>
>L&#39;infrastructure sous-jacente de la fonction de blog est la fonction de journal.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

La fonction de blog est composée de deux composants principaux disponibles en ajoutant la fonction [Fonction de blog](/help/communities/functions.md#blog-function) ou en ajoutant les composants à une page en mode d’édition de création.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.votes<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>see <a href="/help/communities/blog-feature.md">Fonctionnalité de blog</a></td>
  </tr>
 </tbody>
</table>

### Barre latérale de blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**incluable**](/help/communities/scf.md#add-or-include-a-communities-component) | Non |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propriétés** | see [Fonctionnalité de blog](/help/communities/blog-feature.md) |

* [Personnalisations côté client](/help/communities/client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Points de fin de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Blog {#blog-function}

Une structure de site de communauté qui inclut [Fonction de blog](/help/communities/functions.md#blog-function) sera configuré `Blog` et `Blog Sidebar` composants. La fonction Blog prend en charge l’identification d’une [groupe d’utilisateurs de membres privilégiés](/help/communities/users.md#privileged-members-group).

### Accès aux entrées de blog (UGC) {#accessing-blog-entries-ugc}

Le contenu généré par l’utilisateur doit être modéré à l’aide de l’une des méthodes standard de modération.
Voir [Modération de contenu généré par l’utilisateur](/help/communities/moderate-ugc.md).

À partir de AEM 6.1 Communities, utilisez un [magasin commun](/help/communities/working-with-srp.md) pour le contenu généré par l’utilisateur inclut l’accès programmatique au contenu généré par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement.**.

Voir :

* [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md) - introduction et présentation de l’utilisation du référentiel.
* [Principes de base de la SRP et du contenu généré par l’utilisateur](/help/communities/srp-and-ugc.md) - Méthodes et exemples de l’utilitaire SRP.
* [Accès au contenu généré par l’utilisateur avec SRP](/help/communities/accessing-ugc-with-srp.md) - Instructions de codage.
* [Refactorisation de SocialUtils](/help/communities/socialutils.md) - mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

## Éditeur Principal {#primary-publisher}

Lorsque le déploiement est une ferme de publication, il est nécessaire d’identifier un éditeur Principal qui interroge les articles planifiés pour publication.

Voir [Éditeur Principal](/help/communities/deploy-communities.md#primary-publisher) pour plus d’informations.

## Autoriser les médias riches {#allowing-rich-media}

La plateforme AEM bloque les liens d’autres sites Web afin d’éviter les attaques XSS, comme décrit dans la section

* [Protection contre les scripts de site à site (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

À compter de la version AEM 6.2, les modifications qui devaient auparavant être effectuées manuellement sont incluses dans le fichier de configuration AntiSamy par défaut.

Les médias riches sont incorporés dans un article de blog en sélectionnant l’option `Embed Media from External Sites` icon :

![media](assets/media-icon.png)
