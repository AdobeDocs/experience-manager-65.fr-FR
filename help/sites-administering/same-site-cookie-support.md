---
title: Prise en charge des cookies du même site pour AEM 6.5
description: Prise en charge des cookies du même site pour AEM 6.5
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 69%

---

# Prise en charge du même cookie de site pour AEM 6.5 {#same-site-cookie-support-for-aem-65}

Depuis la version 80, Chrome et ultérieurement Safari ont introduit un nouveau modèle de sécurité des cookies. Ce mode est conçu pour introduire des contrôles de sécurité sur la disponibilité des cookies aux sites tiers, via un paramètre appelé `SameSite`. Pour en savoir plus, consultez cet [article](https://web.dev/samesite-cookies-explained/).

La valeur par défaut de ce paramètre (`SameSite=Lax`) peut entraîner l’échec de l’authentification entre les instances ou services AEM. Ce dysfonctionnement est dû au fait que les domaines ou les structures d’URL de ces services peuvent ne pas être soumis aux contraintes de cette stratégie de cookies.

Pour contourner ce problème, vous devez définir l’attribut de cookie SameSite sur `None` pour le jeton de connexion.

Pour ce faire, procédez comme suit :

1. Accédez à la console web à l’adresse `http://serveraddress:serverport/system/console/configMgr`
1. Recherchez et cliquez sur le **gestionnaire d’authentification de jeton Granite Adobe**
1. Définissez l’**attribut SameSite pour le cookie de jeton de connexion** sur `None`, comme illustré dans l’image ci-dessous
   ![samesite](assets/samesite1.png)
1. Cliquez sur Enregistrer
1. Une fois que ce paramètre a été mis à jour et que les utilisateurs se sont déconnectés puis reconnectés, l’attribut `None` sera défini pour les cookies `login-token` et ils seront inclus dans les requêtes intersites.
