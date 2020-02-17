---
title: Leaderboard Essentials
seo-title: Leaderboard Essentials
description: Présentation des fonctionnalités du tableau de bord
seo-description: Présentation des fonctionnalités du tableau de bord
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Leaderboard Essentials {#leaderboard-essentials}

Cette page fournit les informations essentielles pour travailler avec la fonction de leadership.

Avant d’inclure le composant du tableau de bord dans une page, il est nécessaire de configurer le score [des communautés et les badges](implementing-scoring.md). Voir aussi [Scoring and Badges Essentials](configure-scoring.md).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/composants/hbs/lead board</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclus</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.lead.board</td>
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
   <td>Voir Fonctionnalité <a href="enabling-leaderboard.md">de classement</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

### Fonction Bibliothèque de fichiers {#file-library-function}

Une structure de site de la communauté qui inclut la fonction [](functions.md#leaderboard-function)Leaderboard, inclut un `leaderboard` composant configuré.
