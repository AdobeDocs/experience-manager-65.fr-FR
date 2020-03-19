---
title: Blog Essentials
seo-title: Blog Essentials
description: Présentation du blog
seo-description: Présentation du blog
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Blog Essentials {#blog-essentials}

Depuis AEM 6.1 Communities, un blog est une communauté  . Les articles de blog sont maintenant publiés à partir du  de publication , où auparavant, les articles de blog ne pouvaient être créés que dans l&#39;auteur  le et publié.

Les articles de blog peuvent désormais être créés par n&#39;importe quel membre de la communauté, sauf s&#39;ils sont réservés aux membres privilégiés.

Cette page fournit les informations essentielles pour travailler avec la fonction de blog.

>[!NOTE]
>
>L&#39;infrastructure sous-jacente de la fonction de blog est la fonction de .

## Essentials for Client-Side {#essentials-for-client-side}

La fonction de blog est composée de deux composants principaux disponibles en ajoutant la fonction [de](/help/communities/functions.md#blog-function) blog ou en ajoutant les composants à une page en mode d&#39;édition de l&#39;auteur.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social//composants/hbs/</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.</td>
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
   <td>voir Fonctionnalité <a href="/help/communities/blog-feature.md">du blog</a></td>
  </tr>
 </tbody>
</table>

### Barre latérale de blog {#blog-sidebar}

| **resourceType** | social//components/hbs/sidebar |
|---|---|
| [**inclus **](/help/communities/scf.md#add-or-include-a-communities-component) | Non |
| [**clientllibs **](/help/communities/clientlibs.md) | cq.social.hbs.._barre latérale |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propriétés** | voir Fonctionnalité [du blog](/help/communities/blog-feature.md) |

* [Personnalisations côté client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Points de fin du blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](/help/communities/server-customize.md)

### Fonction Blog {#blog-function}

Une structure de site communautaire qui inclut la fonction [](/help/communities/functions.md#blog-function) Blog aura configuré `Blog` et `Blog Sidebar` des composants. La fonction Blog prend en charge l&#39;identification d&#39;un groupe [d&#39;utilisateurs membres](/help/communities/users.md#privileged-members-group)privilégiés.

### Accès aux entrées de blog (UGC) {#accessing-blog-entries-ugc}

L’UGC doit être modérée à l’aide de l’une des méthodes standard de modération.
Voir [Modération du contenu](/help/communities/moderate-ugc.md)généré par l’utilisateur.

Depuis la version 6.1 des Communautés AEM, l’utilisation d’un magasin [](/help/communities/working-with-srp.md) commun pour l’UGC inclut l’accès par programmation à l’UGC, quelle que soit l’option de   choisie (par exemple, ASRP, MSRP ou JSRP).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Aperçu](/help/communities/srp.md) du fournisseur de ressources  - présentation et utilisation du référentiel
* [SRP et UGC Essentials](/help/communities/srp-and-ugc.md) - Méthodes et exemples d&#39;utilitaires SRP
* [Accès UGC avec SRP](/help/communities/accessing-ugc-with-srp.md) - directives de codage
* [SocialUtils Refactoring](/help/communities/socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

## Éditeur principal {#primary-publisher}

Lorsque le déploiement est une batterie de publication, il est nécessaire d’identifier un éditeur principal qui interrogera les articles dont la publication est planifiée.

Voir Editeur [](/help/communities/deploy-communities.md#primary-publisher) principal pour plus d’informations.

## Autoriser les médias enrichis {#allowing-rich-media}

La plate-forme AEM bloque les liens d’autres sites Web pour empêcher les attaques XSS, comme décrit dans la section

* [Protection contre les scripts de site à site (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

Depuis AEM 6.2, les modifications qui devaient être apportées manuellement sont incluses dans le fichier de configuration par défaut d’AntiSamy.

Les médias enrichis sont incorporés dans un article de blog en sélectionnant l&#39; `Embed Media from External Sites` icône :

![chlimage_1-199](assets/chlimage_1-199.png)

