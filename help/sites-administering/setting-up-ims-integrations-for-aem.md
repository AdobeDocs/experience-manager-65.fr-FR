---
title: Configurer des intégrations IMS pour AEM
description: Découvrir comment configurer des intégrations IMS pour AEM
feature: Security
role: Admin
exl-id: 3c6dbb7e-847f-407b-ac9c-4676dba671a5
source-git-commit: c2d996586d2ec7299e856a97ae1b744245c730bb
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 78%

---

# Configurer des intégrations IMS pour AEM {#setting-up-ims-integrations-for-aem}


>[!NOTE]
>
>Les clients Adobe utilisent la variable [Console Adobe Developer](https://developer.adobe.com/console) pour générer des informations d’identification qui permettent l’accès à diverses API. Les clientes et clients effectuent un choix parmi différents types d’informations d’identification, allant d’OAuth serveur à serveur jusqu’à l’application monopage. Le type d’informations d’identification Service Account (JWT) est désormais obsolète au profit des informations d’identification OAuth Server-to-Server avec le Service Pack 20. Cette modification peut être renvoyée vers les packs de services plus anciens, à partir du pack de services 11 jusqu’au pack de services 20, avec l’utilisation d’un correctif que vous pouvez télécharger [ici](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/ims-jwt-compatibility-package-6.5-1.0.zip).

Adobe Experience Manager (AEM) peut être intégré à de nombreuses autres solutions Adobe. Par exemple, Adobe Target, Adobe Analytics et d’autres.

Les intégrations utilisent une intégration IMS configurée avec S2S OAuth.

* Après avoir créé :

   * [Les informations d’identification dans la Developer Console](#credentials-in-the-developer-console)

* Vous pouvez ensuite effectuer ce qui suit :

   * Créer une (nouvelle) [configuration OAuth](#creating-oauth-configuration)

   * [Migrer une configuration JWT existante vers une configuration OAuth](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>Auparavant, les configurations étaient effectuées avec les [informations d’identification JWT désormais sujettes à l’obsolescence dans Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>De telles configurations ne peuvent plus être créées ou mises à jour, mais peuvent être migrées vers des configurations OAuth.

## Informations d’identification dans la Developer Console {#credentials-in-the-developer-console}

Pour commencer, vous devez configurer les informations d’identification OAuth dans la console Adobe Developer.

Pour plus d’informations sur la manière d’effectuer cette configuration, consultez la documentation de Developer Console en fonction de vos besoins :

* Vue d’ensemble :

   * [Authentification de serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Créer de nouvelles informations d’identification OAuth :

   * [Guide de mise en œuvre des informations d’identification OAuth de serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* Migrer des informations d’identification JWT existantes vers des informations d’identification OAuth :

   * [Migrer des informations d’identification du compte de service (JWT) vers les informations d’identification OAuth de serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

Par exemple :

![Informations d’identification OAuth dans la Developer Console](assets/ims-configuration-developer-console.png)

## Créer une configuration OAuth {#creating-oauth-configuration}

Pour créer une nouvelle intégration Adobe IMS à l’aide d’OAuth, procédez comme suit :

1. Dans AEM, accédez à **Outils**, **Sécurité**, **Intégration Adobe IMS**.

1. Sélectionnez **Créer**.

1. Complétez la configuration en fonction des détails de la [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Par exemple :

   ![Créer une configuration OAuth](assets/ims-create-oauth-configuration.png)

1. **Enregistrez** vos modifications.

## Migrer une configuration JWT existante vers une configuration OAuth {#migrating-existing-JWT-configuration-to-oauth}

Pour migrer une intégration Adobe IMS existante basée sur les informations d’identification JWT, procédez comme suit :

>[!NOTE]
>
>Cet exemple montre une configuration IMS de lancement.

1. Dans AEM, accédez à **Outils**, **Sécurité**, **Intégration Adobe IMS**.

1. Sélectionnez la configuration JWT qui doit être migrée. Les configurations JWT affichent l’avertissement **Informations d’identification JWT (obsolètes)**.

1. Sélectionnez **Propriétés** :

   ![Sélection de la configuration JWT](assets/ims-migrate-jwt-select-configuration.png)

1. La configuration s’ouvre en lecture seule :

   ![Propriétés de configuration - Lecture seule](assets/ims-migrate-jwt-properties-read-only.png)

1. Sélectionnez **OAuth** dans la liste déroulante des **types d’authentification** :

   ![Sélection du type d’authentification](assets/ims-migrate-jwt-authentication-type.png)

1. Les propriétés disponibles sont mises à jour. Utilisez les détails de la Developer Console pour les compléter :

   ![Saisie des détails OAuth](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Sélectionnez **Enregistrer et fermer** pour conserver vos mises à jour.
Lorsque vous revenez à la console, la variable **Informations d’identification JWT (obsolète)** l&#39;avertissement a disparu.
