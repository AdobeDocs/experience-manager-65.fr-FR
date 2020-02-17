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
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Service de gestion des utilisateurs et du contenu qu’ils génèrent dans AEM Communities{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Le RDMD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les règles de protection des données et de protection de la vie privée; comme le RMR, l&#39;ACCP, etc.

Les communautés AEM exposent les API prêtes à l’emploi pour gérer les profils utilisateur et gérer en bloc le contenu généré par l’utilisateur (UGC). Once enabled, the **UserUgcManagement** service allows the privileged users (community administrators and moderators) to disable user profiles, and bulk delete or bulk export UGC for specific users. Ces API permettent également aux contrôleurs et aux processeurs des données des clients de se conformer au Règlement général sur la protection des données (RGMD) de l&#39;Union européenne et à d&#39;autres mandats de confidentialité inspirés par le RGMD.

Pour plus d’informations, voir la [page RGPD du centre de traitement des données personnelles d’Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Si vous avez configuré [Adobe Analytics sur le site des communautés](/help/communities/analytics.md) AEM, les données utilisateur capturées sont envoyées au serveur Adobe Analytics. Adobe Analytics fournit des API qui vous permettent d’accéder aux données utilisateur, de les exporter et de les supprimer, et de respecter les règles du GDPR. Pour plus d’informations, voir [Envoyer des requêtes](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html)d’accès et de suppression.

To put these APIs to use, you need to enable the **/services/social/ugcmanagement** endpoint by activating the UserUgcManagement service. To activate this service, install the [sample servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) available on [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet). Ensuite, accédez au point de terminaison sur l’instance de publication de votre site Communities avec les paramètres appropriés à l’aide d’une requête HTTP, similaire à :

**https://localhost:port/services/social/ugcmanagement?user=&lt;ID autorisé>&amp;operation=&lt;getUgc>**. Cependant, vous pouvez également créer une IU (interface utilisateur) pour gérer les profils utilisateur et le contenu généré par les utilisateurs dans le système.

Ces API permettent de remplir les fonctions suivantes.

## Récupération du contenu généré par un utilisateur {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, utilisateur de chaîne, OutputStream outputStream) **permet d’exporter tout le contenu UGC d’un utilisateur à partir du système.

* **user**: ID autorisé d’un utilisateur.
* **outputStream** : le résultat est renvoyé sous la forme d’un flux de sortie, qui est un fichier ZIP comprenant le contenu généré par l’utilisateur (un fichier JSON) et les pièces jointes (y compris les images ou les vidéos téléchargées par l’utilisateur).

Par exemple, pour exporter le contenu généré par un utilisateur nommé Weston McCall, qui utilise weston.mccall@dodgit.com comme ID autorisable afin de se connecter au site Communities, vous pouvez envoyer une requête HTTP GET similaire à ce qui suit :

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Suppression du contenu généré par un utilisateur {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, utilisateur String) **permet de supprimer du système tous les fichiers UGC d’un utilisateur.

* **user** : ID autorisable d’un utilisateur.

Par exemple, pour supprimer l’UGC d’un utilisateur ayant un ID autorisé weston.mccall@dodgit.com via une requête http-POST, utilisez les paramètres suivants :

* user= weston.mccall@dodgit.com
* operation= deleteUgc

### Suppression du fichier UGC d’Adobe Analytics {#delete-ugc-from-adobe-analytics}

Pour supprimer les données utilisateur d’Adobe Analytics, suivez le processus [d’analyse](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/an_gdpr_workflow.html)GDPR ; car l’API ne supprime pas les données utilisateur d’Adobe Analytics.

Pour les mappages de variables Adobe Analytics utilisés par les communautés AEM, reportez-vous à l’image suivante :

![Mappage des variables de communautés AEM pour Adobe Analytics](assets/analytics-communities-mapping.png)

## Désactivation d’un compte utilisateur {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, utilisateur de chaîne) **permet de désactiver un compte utilisateur.

* **user** : ID autorisable d’un utilisateur.

>[!NOTE]
>
>La désactivation d’un utilisateur supprime tout le contenu qu’il a généré et qui se trouve sur le serveur.

Par exemple, pour supprimer le profil d’un utilisateur ayant un ID autorisé weston.mccall@dodgit.com via une requête http-POST, utilisez les paramètres suivants :

* user= weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>L’API deleteUserAccount() désactive un seul profil utilisateur dans le système, puis supprime le contenu généré par l’utilisateur. However, to delete a user profile from the system, navigate to **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), locate the user node and delete it.

