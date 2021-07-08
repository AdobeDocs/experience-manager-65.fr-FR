---
title: En-têtes HTTP personnalisés
description: Configuration d’en-têtes HTTP personnalisés
source-git-commit: 7d174be35cb99d802e4aeff6f4d955b1b92cab74
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# En-têtes HTTP personnalisés {#custom-http-headers}

## Présentation {#overview}

Pour mieux contrôler leur serveur principal, les auteurs peuvent configurer des en-têtes HTTP personnalisés qui seraient envoyés au moteur de commerce, ainsi que ceux déjà envoyés par CIF. Les cas d’utilisation courants incluent des configurations multi-magasin dans lesquelles vous pouvez utiliser des en-têtes HTTP pour contrôler la réponse du serveur principal Commerce.

>[!NOTE]
>
>Les développeurs peuvent toujours configurer des en-têtes HTTP personnalisés à l’aide de la configuration client GraphQL.


## Configuration {#configuration}

Pour configurer les en-têtes HTTP personnalisés, vous devez d’abord les définir. Les en-têtes HTTP personnalisés doivent d’abord être définis en les ajoutant à la configuration de service `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` à l’aide d’une configuration OSGi.

Vous pouvez configurer les valeurs des en-têtes HTTP dans la page Configuration du Cloud Service pour votre projet :

1. Accédez à la page de configuration du Cloud Service dans Outils -> Cloud Services -> Configuration CIF.
1. Ouvrir une configuration existante ou en créer une nouvelle
1. Accédez à l’onglet &quot;Avancé&quot; et recherchez le champ multiple &quot;En-têtes HTTP personnalisés&quot;. Vous pouvez sélectionner les en-têtes que vous avez définis précédemment et leur attribuer des valeurs.

Les composants qui utilisent la configuration de service cloud ci-dessus enverront ces en-têtes HTTP avec chaque requête GraphQL.

## Restrictions {#restrictions}

Bien que le service permette de définir des noms d’en-tête, y compris les noms standard, ils ne sont pas disponibles pour la configuration. En d’autres termes, vous ne pouvez pas remplacer les en-têtes HTTP standard à l’aide de cette fonctionnalité. Vous trouverez une liste de noms d’en-tête restreints [ici](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). En outre, deux en-têtes supplémentaires ne peuvent pas être utilisés :

* &quot;Magasin&quot; : utilisé par CIF pour identifier le magasin du Magento.
* &quot;Preview-Version&quot; : utilisé par CIF pour récupérer les produits intermédiaires.
