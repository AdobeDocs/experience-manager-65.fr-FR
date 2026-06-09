---
title: Service de gestion des utilisateurs et du contenu créé par l’utilisateur dans AEM Communities
description: Utilisez les API pour supprimer et exporter en bloc le contenu généré par l’utilisateur, et désactiver le compte utilisateur.
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: f4fc3b788d4128135ff77ebb87f1369059b1d2ec
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# Service de gestion des utilisateurs et du contenu créé par l’utilisateur dans AEM Communities {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité telles que le RGPD, le CCPA, etc.

AEM Communities offre des API prêtes à l’emploi pour gérer les profils utilisateur et gérer en masse le contenu généré par l’utilisateur. Une fois activé, le service **UserUgcManagement** permet aux utilisateurs dotés de privilèges (administrateurs de communauté et modérateurs) de désactiver les profils utilisateur et de supprimer en bloc le contenu créé par l’utilisateur ou de l’exporter en bloc pour des utilisateurs spécifiques. Ces API permettent également aux responsables du traitement et aux sous-traitants des données clients de se conformer au Règlement général sur la protection des données (RGPD) de l’Union européenne et à d’autres mandats de confidentialité inspirés du RGPD.

Pour plus d’informations, consultez la page [RGPD dans le Centre de traitement des données personnelles d’Adobe.](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html)

>[!NOTE]
>
>Si vous avez configuré [Adobe Analytics sur le site AEM Communities](/help/communities/analytics.md), les données utilisateur capturées sont envoyées aux serveurs Adobe Analytics. Adobe Analytics fournit des API qui vous permettent d’accéder aux données utilisateur, de les exporter et de les supprimer, tout en respectant le RGPD. Pour plus d’informations, voir [Soumettre des demandes d’accès et de suppression](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

Pour utiliser ces API, vous devez activer le point d’entrée `/services/social/ugcmanagement` en activant le service UserUgcManagement. Pour activer ce service, installez le [exemple de servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) disponible sur [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). Ensuite, accédez au point d’entrée sur l’instance de publication de votre site de communautés avec les paramètres appropriés à l’aide d’une requête http, similaire à :

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. Cependant, vous pouvez également créer une interface utilisateur pour gérer les profils utilisateur et le contenu généré par l’utilisateur dans le système.

Ces API permettent d’effectuer les fonctions suivantes.

## Récupérer le contenu créé par l’utilisateur d’un utilisateur {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver, String user, OutputStream outputStream)** permet d’exporter tout le contenu créé par l’utilisateur du système.

* **user** : ID autorisable d’un utilisateur.
* **outputStream** : le résultat est renvoyé en tant que flux de sortie, qui est un fichier zip comprenant le contenu généré par l’utilisateur (en tant que fichier json) et les pièces jointes (qui incluent des images ou des vidéos chargées par l’utilisateur).

Par exemple, pour exporter le contenu créé par l’utilisateur nommé Weston McCall, qui utilise weston.mccall@dodgit.com comme ID autorisable pour se connecter au site Communities, vous pouvez envoyer une requête HTTP GET similaire à ce qui suit :

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## Supprimer le contenu créé par l’utilisateur d’un utilisateur {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver, String user)** permet de supprimer du système tout le contenu créé par l’utilisateur pour un utilisateur.

* **user** : ID autorisable de l’utilisateur.

Par exemple, pour supprimer le contenu créé par l’utilisateur d’un utilisateur dont l’ID autorisable est `weston.mccall@dodgit.com` via une requête http-POST, utilisez les paramètres suivants :

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Supprimer le contenu créé par l’utilisateur d’Adobe Analytics {#delete-ugc-from-adobe-analytics}

Pour supprimer des données utilisateur d’Adobe Analytics, suivez le workflow [RGPD d’Analytics ](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=fr), car l’API ne supprime pas les données utilisateur d’Adobe Analytics.

Pour les mappages de variables Adobe Analytics utilisés par AEM Communities, reportez-vous à l’image suivante :

![Mappage des variables des communautés AEM pour Adobe Analytics](assets/analytics-communities-mapping.png)

## Désactivation d’un compte d’utilisateur {#disable-a-user-account}

**deleteUserAccount(ResourceResolver, String user)** permet de désactiver un compte utilisateur.

* **user** : ID autorisable de l’utilisateur.

>[!NOTE]
>
>La désactivation d’un utilisateur supprime tout le contenu généré par l’utilisateur et présent sur le serveur.

Par exemple, pour supprimer le profil d’un utilisateur dont l’ID autorisable est `weston.mccall@dodgit.com` via une requête http-POST, utilisez les paramètres suivants :

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>L’API `deleteUserAccount()` désactive uniquement un profil utilisateur dans le système et supprime le contenu créé par l’utilisateur. Toutefois, pour supprimer un profil utilisateur du système, accédez à **** à l’adresse `https://<server>:<port>/crx/de`, localisez le nœud utilisateur et supprimez-le.
