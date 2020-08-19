---
title: Service de gestion des utilisateurs et du contenu qu’ils génèrent dans AEM Communities
seo-title: Service de gestion des utilisateurs et du contenu qu’ils génèrent dans AEM Communities
description: Utilisez des API pour supprimer et exporter en masse du contenu généré par les utilisateurs et désactiver des comptes utilisateur.
seo-description: Utilisez des API pour supprimer et exporter en masse du contenu généré par les utilisateurs et désactiver des comptes utilisateur.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 18f401babef4cb2aad47e6e4cbb0500b0f8365e2
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 30%

---


# Service de gestion des utilisateurs et du contenu qu’ils génèrent dans AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations relatives à la protection des données et à la protection de la vie privée ; comme le RGPD, l&#39;ACCP, etc.


aem communities expose les API prêtes à l’emploi pour gérer les profils utilisateur et gérer en bloc le contenu généré par l’utilisateur. Once enabled, the **UserUgcManagement** service allows the privileged users (community administrators and moderators) to disable user profiles, and bulk delete or bulk export UGC for specific users. Ces API permettent également aux contrôleurs et aux processeurs des données client de se conformer au Règlement général sur la protection des données (RGPD) de l&#39;Union européenne et à d&#39;autres mandats de confidentialité inspirés du RGPD.

Pour plus d’informations, voir la [page RGPD du centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Si vous avez configuré [Adobe Analytics sur le site AEM Communities](/help/communities/analytics.md) , les données utilisateur capturées sont envoyées au serveur Adobe Analytics. adobe analytics fournit des API qui vous permettent d’accéder, d’exporter et de supprimer des données utilisateur et de respecter les règles GDPR. Pour plus d’informations, voir [Envoyer des demandes d’accès et de suppression](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).


To put these APIs to use, you need to enable the `/services/social/ugcmanagement` endpoint by activating the UserUgcManagement service. To activate this service, install the [sample servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) available on [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Ensuite, accédez au point de terminaison de l’instance de publication de votre site de communautés avec les paramètres appropriés à l’aide d’une requête http, semblable à :

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Cependant, vous pouvez également créer une IU (interface utilisateur) pour gérer les profils utilisateur et le contenu généré par les utilisateurs dans le système.

Ces API permettent de remplir les fonctions suivantes.

## Récupération du contenu généré par un utilisateur {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, utilisateur de chaîne, OutputStream outputStream)** permet d’exporter tout l’UGC d’un utilisateur à partir du système.

* **utilisateur**: ID autorisé d’un utilisateur.
* **outputStream**: Le résultat est renvoyé sous forme de flux de sortie, qui est un fichier zip comprenant le contenu généré par l’utilisateur (sous forme de fichier json) et les pièces jointes (qui incluent des images ou des vidéos téléchargées par l’utilisateur).

Par exemple, pour exporter le contenu généré par un utilisateur nommé Weston McCall, qui utilise weston.mccall@dodgit.com comme ID autorisable afin de se connecter au site Communities, vous pouvez envoyer une requête HTTP GET similaire à ce qui suit :

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Suppression du contenu généré par un utilisateur {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, utilisateur de chaîne)** permet de supprimer du système tous les fichiers UGC d&#39;un utilisateur.

* **utilisateur**: ID autorisé de l’utilisateur.

Par exemple, pour supprimer l’UGC d’un utilisateur disposant d’un ID pouvant être autorisé weston.mccall@dodgit.com via une requête de POST HTTP, utilisez les paramètres suivants :

* l’utilisateur = `weston.mccall@dodgit.com`
* opération = `deleteUgc`

### Supprimer l&#39;UGC d&#39;Adobe Analytics {#delete-ugc-from-adobe-analytics}

Pour supprimer les données utilisateur de l’Adobe Analytics, suivez le processus [](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)GDPR Analytics ; car l’API ne supprime pas les données utilisateur d’Adobe Analytics.

Pour les mappages de variables Adobe Analytics utilisés par AEM Communities, reportez-vous à l’image suivante :

![Mappage des variables de communautés AEM pour Adobe Analytics](assets/analytics-communities-mapping.png)

## Désactivation d’un compte utilisateur {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, utilisateur String)** permet de désactiver un compte utilisateur.

* **utilisateur**: ID autorisé de l’utilisateur.

>[!NOTE]
>
>La désactivation d’un utilisateur supprime tout le contenu qu’il a généré et qui se trouve sur le serveur.


For example, to delete the profile of a user having authorizable ID `weston.mccall@dodgit.com` through http-POST request, use the following parameters:

* l’utilisateur = `weston.mccall@dodgit.com`
* opération = `deleteUser`

>[!NOTE]
>
>L’API deleteUserAccount() désactive un seul profil utilisateur dans le système, puis supprime le contenu généré par l’utilisateur. However, to delete a user profile from the system, navigate to **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), locate the user node and delete it.


