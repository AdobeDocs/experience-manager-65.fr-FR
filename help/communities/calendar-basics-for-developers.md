---
title: Principes de base du calendrier
description: Découvrez comment utiliser la fonction Calendrier dans les communautés de Experience Manager. Le calendrier prend en charge l’identification des groupes d’utilisateurs privilégiés.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---

# Principes de base du calendrier {#calendar-essentials}

Cette page fournit des informations essentielles sur l’utilisation de la fonction Calendrier.

## Principes élémentaires pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluable</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>see <a href="calendar.md">Utilisation des calendriers</a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Principes élémentaires pour le côté serveur {#essentials-for-server-side}

* [API de calendrier](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Points de fin du calendrier](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Calendrier {#calendar-function}

Une structure de site de communauté qui inclut [Fonction Calendrier](functions.md#calendar-function) a une `calendar` du composant configuré. La fonction Calendrier prend en charge l’identification d’un [groupe d’utilisateurs de membres privilégiés](users.md#privileged-members-group).

### Accès aux publications du calendrier (UGC) {#accessing-calendar-posts-ugc}

À partir de AEM 6.1 Communities, utilisez un [magasin commun](working-with-srp.md) pour le contenu généré par l’utilisateur inclut l’accès par programmation au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (comme ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement.**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - présentation et utilisation du référentiel
* [Principes de base de la SRP et du contenu généré par l’utilisateur](srp-and-ugc.md) - Méthodes d’utilitaire SRP et exemples
* [Accès au contenu généré par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage
* [Refactorisation de SocialUtils](socialutils.md) - mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles
