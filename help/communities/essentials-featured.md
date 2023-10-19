---
title: Notions fondamentales sur le contenu proposé
description: Découvrez les principes de base de l’utilisation du contenu présenté que vous souhaitez mettre en évidence n’importe où sur le site de la communauté.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 70b0ad6a-c891-4588-8515-449aed206805
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Notions fondamentales sur le contenu proposé  {#featured-content-essentials}

Cette page fournit les informations essentielles pour utiliser le contenu présenté.

Contrairement à l’épinglage d’une publication en haut d’un forum, cette fonctionnalité permet de mettre en évidence le contenu n’importe où sur le site de la communauté.


## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/featuredcontent</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td> <i>default</i></td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/featuredcontent/featuredcontent.hbs<br /> /libs/social/commons/components/hbs/featuredtopic/featuredtopic.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/featuredcontent/clientlibs/featuredcontent.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="featured.md">Contenu en vedette</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site de communauté qui inclut [Fonction Contenu en vedette](functions.md#featured-content-function), inclut une `featured content` composant.
