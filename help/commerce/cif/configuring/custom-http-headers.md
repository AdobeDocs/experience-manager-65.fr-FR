---
title: En-têtes HTTP personnalisés
description: Découvrez comment configurer des en-têtes HTTP personnalisés dans Adobe Experience Manager Commerce.
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 82%

---

# En-têtes HTTP personnalisés {#custom-http-headers}

## Vue d’ensemble {#overview}

Pour mieux contrôler leur serveur principal, les auteurs peuvent configurer des en-têtes HTTP personnalisés qui seraient envoyés au moteur de commerce, ainsi que ceux déjà envoyés par CIF. Les cas d’utilisation courants incluent des configurations multi-magasin dans lesquelles vous pouvez utiliser des en-têtes HTTP pour contrôler la réponse du serveur principal de commerce.

>[!NOTE]
>
>Les développeurs peuvent toujours configurer des en-têtes HTTP personnalisés à l’aide de la configuration client GraphQL.
>

## Configuration {#configuration}

Pour configurer les en-têtes HTTP personnalisés, vous devez d’abord les définir. Les en-têtes HTTP personnalisés doivent d’abord être définis par le biais de leur ajout à la configuration de service `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` à l’aide d’une configuration OSGi.

Vous pouvez configurer les valeurs des en-têtes HTTP dans la page Configuration du service cloud pour votre projet :

1. Accédez à la page de configuration du Cloud Service dans Outils > Cloud Services > Configuration CIF.
1. Ouvrez une configuration existante ou créez-en une.
1. Accédez à l’onglet « Avancé » et recherchez le champ multiple « En-têtes HTTP personnalisés ». Vous pouvez sélectionner les en-têtes que vous avez définis précédemment et leur attribuer des valeurs.

Les composants qui utilisent la configuration de service cloud ci-dessus envoient ces en-têtes HTTP avec chaque demande GraphQL.

## Restrictions {#restrictions}

Bien que le service permette de définir des noms d’en-tête, y compris les noms standard, ils ne sont pas disponibles pour configuration. En d’autres termes, vous ne pouvez pas remplacer les en-têtes HTTP standard à l’aide de cette fonctionnalité. Vous trouverez une liste de noms d’en-tête restreints [ici](https://developer.mozilla.org/fr-FR/docs/Web/HTTP/Headers). En outre, deux en-têtes supplémentaires ne peuvent pas être utilisés :

* « Store » : utilisé par CIF pour identifier la boutique Adobe Commerce.
* « Preview-Version » : utilisé par CIF pour récupérer les produits intermédiaires.
