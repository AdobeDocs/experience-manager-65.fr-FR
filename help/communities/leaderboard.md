---
title: Notions fondamentales relatives au tableau de bord
seo-title: Notions fondamentales relatives au tableau de bord
description: Présentation des fonctionnalités du tableau de classement
seo-description: Présentation des fonctionnalités du tableau de classement
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

# Notions fondamentales sur le tableau de bord {#leaderboard-essentials}

Cette page fournit les informations essentielles pour utiliser la fonctionnalité de classement.

Avant d’inclure le composant de classement sur une page, il est nécessaire de configurer [Notation et badges des communautés](implementing-scoring.md).

Voir [Notions fondamentales sur la notation et les badges](configure-scoring.md).

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/Leadboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
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

Une structure de site de communauté qui comprend la fonction [Leaderboard](functions.md#leaderboard-function), comprend un composant `leaderboard` configuré.
