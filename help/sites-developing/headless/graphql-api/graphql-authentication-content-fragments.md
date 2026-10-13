---
title: Authentification pour les requêtes Adobe Experience Manager GraphQL distantes sur les fragments de contenu
description: Comprenez l’authentification requise pour les requêtes GraphQL d’Adobe Experience Manager à distance afin de sécuriser votre diffusion de contenu sans interface utilisateur.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
solution: Experience Manager, Experience Manager Sites
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 100%
---
# Authentification pour les requêtes Adobe Experience Manager GraphQL distantes sur les fragments de contenu {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un des principaux cas d’utilisation de l’[API Adobe Experience Manager (AEM) GraphQL pour la diffusion de fragments de contenu](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) consiste à accepter les requêtes distantes provenant d’applications ou de services tiers. Ces requêtes à distance peuvent nécessiter un accès authentifié à l’API afin de sécuriser la diffusion de contenu découplé.

>[!NOTE]
>
>Pour les tests et le développement, vous pouvez également directement accéder à l’API GraphQL d’AEM avec l’[interface GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

Pour l’authentification, le service tiers doit s’authentifier à l’aide du nom d’utilisateur ou d’utilisatrice et du mot de passe du compte AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third-party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third-party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
