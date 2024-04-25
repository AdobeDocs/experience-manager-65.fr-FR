---
title: Notions fondamentales relatives aux idées
description: Découvrez les principes de base de l’utilisation de la fonctionnalité d’idéation dans les communautés, qui est similaire à un forum, mais avec une approche plus collaborative.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# Notions fondamentales relatives aux idées {#ideation-essentials}

Cette page fournit les informations essentielles pour travailler avec la fonction d’idéation, qui est similaire à un forum, mais qui permet d’enregistrer en tant que brouillon et d’avoir un aspect plus collaboratif.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ideation/components/hbs/ideation</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.votes<br /> cq.social.hbs.liking<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="ideation-feature.md">Fonctionnalité d’orientation</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction de conceptualisation {#ideation-function}

Une structure de site de communauté qui inclut [Fonction d’information](functions.md#ideation-function), inclut une `ideation` composant.
