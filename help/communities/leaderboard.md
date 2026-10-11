---
title: Leaderboard Essentials
description: Découvrez comment configurer la notation et les badges des communautés afin de pouvoir utiliser le composant Tableau des scores dans les communautés Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
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
source-wordcount: '114'
ht-degree: 5%
---
# Leaderboard Essentials {#leaderboard-essentials}

Cette page contient les informations essentielles relatives à l&#39;utilisation de la fonction Tableau des scores.

Avant d’inclure le composant Tableau des scores sur une page, il est nécessaire de configurer [Notation et pastilles de communautés](implementing-scoring.md).

Voir [ Notions fondamentales sur la notation et l’attribution de badges](configure-scoring.md).

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/leaderboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td> <br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="enabling-leaderboard.md">Fonction du tableau de classement</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site de communauté qui inclut la fonction [Tableau des scores](functions.md#leaderboard-function) comprend un composant `leaderboard` configuré.
