---
title: Le framework de protection CSRF
seo-title: Le framework de protection CSRF
description: Le framework utilise des jetons pour garantir que la demande du client est légitime
seo-description: Le framework utilise des jetons pour garantir que la demande du client est légitime
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518

---


# Le framework de protection CSRF{#the-csrf-protection-framework}

En plus du filtre Apache Sling Referrer, Adobe fournit également un nouveau framework de protection CSRF pour se protéger contre ce type d’attaque.

Le framework utilise des jetons pour garantir que la demande du client est légitime. Les jetons sont générés lorsque le formulaire est envoyé au client et validé lorsque le formulaire est renvoyé au serveur.

>[!NOTE]
>
>Il n’existe aucun jeton sur les instances de publication pour les utilisateurs anonymes.

## Conditions requises {#requirements}

### Dépendances {#dependencies}

Tout composant associé à la dépendance `granite.jquery` bénéficie automatiquement du framework de protection CSRF. Si ce n’est pas le cas pour l’un de vos composants, vous devez déclarer une dépendance à `granite.csrf.standalone` avant de pouvoir utiliser le framework.

### Réplication de la clé de chiffrement {#replicating-crypto-keys}

In order to make use of the tokens, you need to replicate the `/etc/keys/hmac` binary to all of the instances in your deployment. Un moyen pratique de copier la clé HMAC sur toutes les instances consiste à créer un module contenant la clé et à l’installer via le gestionnaire de modules sur toutes les instances.

>[!NOTE]
>
>Assurez-vous également d’effectuer les [modifications de configuration du dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)nécessaires pour utiliser le framework de protection CSRF.

>[!NOTE]
>
>If you use the manifest cache with your web application, make sure you add &quot;**&amp;ast;**&quot; to the manifest in order to make sure the token does not take the CSRF token generation call offline. Pour plus d’informations, consultez ce [lien](https://www.w3.org/TR/offline-webapps/).
>
>Pour plus d’informations sur les attaques CSRF et les moyens de s’en protéger, consultez la page [Cross-Site Request Forgery OWASP](https://owasp.org/www-community/attacks/csrf).
