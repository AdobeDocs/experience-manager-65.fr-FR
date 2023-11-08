---
title: Le framework de protection CSRF
description: Le framework utilise des jetons pour garantir que la demande du client est légitime
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 54%

---

# Le framework de protection CSRF {#the-csrf-protection-framework}

Outre le filtre de référent Apache Sling, Adobe fournit également un nouveau framework de protection CSRF pour se protéger contre ce type d’attaque.

Le framework utilise des jetons pour garantir que la demande du client est légitime. Les jetons sont générés lorsque le formulaire est envoyé au client et validé lorsque le formulaire est renvoyé au serveur.

>[!NOTE]
>
>Il n’y a aucun jeton sur les instances de publication pour les utilisateurs anonymes.

## Conditions requises {#requirements}

### Dépendances {#dependencies}

Tout composant associé à la dépendance `granite.jquery` bénéficie automatiquement du framework de protection CSRF. Si ce n’est pas le cas pour l’un de vos composants, vous devez déclarer une dépendance à `granite.csrf.standalone` avant de pouvoir utiliser le framework.

### Réplication de la clé de chiffrement {#replicating-crypto-keys}

Pour utiliser les jetons, vous devez répliquer le binaire HMAC sur toutes les instances de votre déploiement. Voir [Répliquer la clé HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) pour plus d’informations.

>[!NOTE]
>
>Veillez également à [Modifications de la configuration de Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/user-guide.html) pour utiliser la structure de protection CSRF.

>[!NOTE]
>
>Si vous utilisez le cache de manifeste avec votre application web, veillez à ajouter &quot;**&amp;ast;**&quot; au manifeste pour s’assurer que le jeton ne prend pas l’appel de génération de jeton CSRF hors ligne. Pour plus d’informations, consultez ce [lien](https://www.w3.org/TR/offline-Webapps/).
>
>Pour plus d’informations sur les attaques CSRF et les moyens de s’en protéger, consultez la page [Cross-Site Request Forgery OWASP](https://owasp.org/www-community/attacks/csrf).
