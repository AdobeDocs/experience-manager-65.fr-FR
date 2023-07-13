---
title: Authentification pour les requêtes GraphQL Adobe Experience Manager distantes sur les fragments de contenu
description: Comprenez l’authentification requise pour les requêtes GraphQL d’Adobe Experience Manager à distance afin de sécuriser votre diffusion de contenu sans interface utilisateur.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Authentification pour les requêtes GraphQL Adobe Experience Manager distantes sur les fragments de contenu {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un cas d’utilisation Principal pour la variable [API GraphQL Adobe Experience Manager (AEM) pour la diffusion de fragments de contenu](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) accepte des requêtes distantes provenant d’applications ou de services tiers. Ces requêtes distantes peuvent nécessiter un accès à l’API authentifié pour sécuriser la diffusion de contenu sans interface utilisateur.

>[!NOTE]
>
>Pour les tests et le développement, vous pouvez également accéder à l’API GraphQL d’AEM directement à l’aide de la variable [Interface GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

Pour l’authentification, le service tiers doit s’authentifier à l’aide du nom d’utilisateur et du mot de passe du compte AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
