---
title: Le framework de protection CSRF
seo-title: The CSRF Protection Framework
description: Le framework utilise des jetons pour garantir que la demande du client est légitime
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 72%

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

Pour utiliser les jetons, vous devez répliquer la variable `/etc/keys/hmac` binaire à toutes les instances de votre déploiement. Un moyen pratique de copier la clé HMAC sur toutes les instances consiste à créer un module contenant la clé et à l’installer via le gestionnaire de modules sur toutes les instances.

>[!NOTE]
>
>Assurez-vous également d’effectuer les [modifications de configuration du dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)nécessaires pour utiliser le framework de protection CSRF.

>[!NOTE]
>
>Si vous utilisez le cache de manifeste avec votre application web, veillez à ajouter &quot;**&amp;ast;**&quot; au manifeste afin de s’assurer que le jeton ne prend pas l’appel de génération de jeton CSRF hors ligne. Pour plus d’informations, consultez ce [lien](https://www.w3.org/TR/offline-webapps/).
>
>Pour plus d’informations sur les attaques CSRF et les moyens de s’en protéger, consultez la page [Cross-Site Request Forgery OWASP](https://owasp.org/www-community/attacks/csrf).
