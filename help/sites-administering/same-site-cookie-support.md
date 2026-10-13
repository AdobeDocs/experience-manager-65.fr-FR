---
title: Prise en charge des cookies Same Site pour AEM 6.5
description: Découvrez la prise en charge des cookies du SameSite pour AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 100%
---
# Prise en charge des cookies Same Site pour AEM 6.5 {#same-site-cookie-support-for-aem-65}

Depuis la version 80, Chrome et ultérieurement Safari ont introduit un nouveau modèle de sécurité des cookies. Ce modèle a été conçu pour introduire des contrôles de sécurité dans les sites tiers sur la disponibilité des cookies par le biais d’un paramètre appelé `SameSite`. Pour plus d’informations, reportez-vous à l’article [web.dev : les cookies SameSite expliqués](https://web.dev/samesite-cookies-explained/).

La valeur par défaut de ce paramètre (`SameSite=Lax`) peut entraîner l’échec de l’authentification entre les instances ou services AEM. Ce dysfonctionnement est dû au fait que les domaines ou les structures d’URL de ces services peuvent ne pas être soumis aux contraintes de cette politique de cookies.

Pour contourner ce problème, vous devez définir l’attribut de cookie `SameSite` sur `None` pour le jeton de connexion.

>[!CAUTION]
>
>Le paramètre `SameSite=None` n’est appliqué que si le protocole est sécurisé (HTTPS).
>
>Si le protocole n’est pas sécurisé (HTTP), le paramètre est ignoré et le serveur affiche ce message d’AVERTISSEMENT :
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Vous pouvez ajouter ce paramètre en procédant comme suit :

1. Accédez à la console web à l’adresse `http://serveraddress:serverport/system/console/configMgr`
1. Recherchez et cliquez sur le **gestionnaire d’authentification de jeton Granite Adobe**
1. Définissez l’**attribut SameSite pour le cookie de jeton de connexion** sur `None`, comme illustré dans l’image ci-dessous
   ![samesite](assets/samesite1.png)
1. Cliquez sur Enregistrer
1. Une fois que ce paramètre a été mis à jour et que les utilisateurs se sont déconnectés puis reconnectés, l’attribut `None` sera défini pour les cookies `login-token` et ils seront inclus dans les requêtes intersites.
