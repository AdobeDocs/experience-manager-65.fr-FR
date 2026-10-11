---
title: Calendar Essentials
description: Découvrez comment utiliser la fonctionnalité Calendrier dans Experience Manager Communities. Le calendrier prend en charge l'identification des groupes d'utilisateurs membres privilégiés.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
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
source-wordcount: '244'
ht-degree: 2%
---
# Calendar Essentials {#calendar-essentials}

Cette page fournit des informations essentielles sur l’utilisation de la fonction de calendrier.

## Essentials pour le côté client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>Non</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>modèles</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td><br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>voir <a href="calendar.md"> Utilisation des calendriers </a></td>
  </tr>
 </tbody>
</table>

* [Personnalisations côté client](client-customize.md)

## Essentials pour côté serveur {#essentials-for-server-side}

* [API de calendrier](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Points d’entrée du calendrier](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personnalisations côté serveur](server-customize.md)

### Fonction Calendrier {#calendar-function}

Une structure de site communautaire qui inclut la fonction [Calendrier](functions.md#calendar-function) comporte un composant `calendar` configuré. La fonction Calendrier prend en charge l’identification d’un [groupe d’utilisateurs membre privilégié](users.md#privileged-members-group).

### Accès aux publications du calendrier (UGC) {#accessing-calendar-posts-ugc}

Depuis AEM 6.1 Communities, l’utilisation d’un [magasin commun](working-with-srp.md) pour le contenu créé par l’utilisateur inclut un accès programmatique au contenu créé par l’utilisateur, quelle que soit l’option de stockage choisie (telle que ASRP, MSRP ou JSRP).

**L’emplacement et le format du contenu créé par l’utilisateur dans le référentiel peuvent être modifiés sans avertissement**.

Voir :

* [Présentation du fournisseur de ressources de stockage](srp.md) - introduction et présentation de l’utilisation du référentiel
* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles
