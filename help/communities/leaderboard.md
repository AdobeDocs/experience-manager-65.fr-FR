---
title: Notions fondamentales relatives au tableau de bord
description: Découvrez comment configurer la notation et les badges des communautés afin de pouvoir utiliser le composant Leaderboard dans les communautés Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

---

# Notions fondamentales relatives au tableau de bord {#leaderboard-essentials}

Cette page fournit les informations essentielles pour utiliser la fonctionnalité de classement.

Avant d’inclure le composant de classement sur une page, il est nécessaire de configurer le [score et badges de communautés](implementing-scoring.md).

Voir [Notions fondamentales sur la notation et les badges](configure-scoring.md).

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/lead-board</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>Voir <a href="enabling-leaderboard.md">Fonctionnalité de classement</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site de communauté qui inclut la [fonction Leaderboard](functions.md#leaderboard-function), inclut un composant `leaderboard` configuré.
