---
title: Principes fondamentaux d’idéation
description: Découvrez les principes de base de l’utilisation de la fonctionnalité Idéation dans Communities, qui est similaire à un forum, mais avec une atmosphère plus collaborative.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%
---
# Principes fondamentaux d’idéation {#ideation-essentials}

Cette page fournit des informations essentielles sur l’utilisation de la fonctionnalité d’idéation, qui est similaire à un forum, mais avec la possibilité d’enregistrer en tant que brouillon. L’effet est plus collaboratif.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ideation/components/hbs/ideation</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.sharing <br /> cq.social.hbs.liking <br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="ideation-feature.md"> Fonctionnalité d’idéation </a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction de conceptualisation {#ideation-function}

Une structure de site de communauté qui inclut la fonction [Idéation](functions.md#ideation-function) comprend un composant `ideation` configuré.
