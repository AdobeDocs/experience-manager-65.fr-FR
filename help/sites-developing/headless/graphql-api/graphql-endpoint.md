---
title: Gérer les points d’entrée GraphQL dans AEM
description: Découvrez comment gérer les points d’entrée GraphQL dans Adobe Experience Manager pour la diffusion de contenu découplé.
exl-id: a59a5e50-0787-4c1c-a83d-bb3eac1479a8
source-git-commit: a8616b3b30ac04ea24c4a869cabd47518af1a35f
workflow-type: ht
source-wordcount: '511'
ht-degree: 100%

---

# Gérer les points d’entrée GraphQL dans AEM {#graphql-aem-endpoint}

Le point d’entrée est le chemin utilisé pour accéder à GraphQL pour AEM. Avec ce chemin, vous (ou votre application) pouvez :

* accéder au schéma GraphQL ;
* envoyer vos requêtes GraphQL ;
* recevoir les réponses (à vos requêtes GraphQL).

Dans AEM, il existe deux types de points d’entrée :

* Global
   * Disponible pour tous les sites.
   * Ce point d’entrée peut utiliser tous les modèles de fragment de contenu de toutes les configurations Sites (définis dans l’[explorateur de configurations](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * S’il existe des modèles de fragment de contenu à partager entre les configurations Sites, ils doivent être créés sous les configurations Sites globales.
* Configurations Sites :
   * Correspond à une configuration Sites, comme défini dans l’[explorateur de configurations](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Spécifique à un site/projet spécifique.
   * Un point d’entrée spécifique à la configuration Sites utilisera les modèles de fragment de contenu de cette configuration Sites spécifique, ainsi que ceux de la configuration Sites globale.

>[!CAUTION]
>
>L’éditeur de fragment de contenu peut permettre à un fragment de contenu d’une configuration Sites de référencer un fragment de contenu d’une autre configuration Sites (à l’aide de stratégies).
>
>Dans ce cas, tout le contenu ne peut pas être récupéré à l’aide d’un point d’entrée spécifique à la configuration Sites.
>
>L’auteur du contenu doit contrôler ce scénario ; par exemple, il peut être utile de placer des modèles de fragment de contenu partagés sous la configuration de sites globaux.

Le chemin d’accès au référentiel du point d’entrée global GraphQL pour AEM est :

`/content/cq:graphql/global/endpoint`

Pour lequel votre application peut utiliser le chemin d’accès suivant dans l’URL de la requête :

`/content/_cq_graphql/global/endpoint.json`

Pour activer le point d’entrée de GraphQL pour AEM, vous devez procéder comme suit :

* [Activation de votre point d’entrée GraphQL](#enabling-graphql-endpoint)
* [Publication de votre point d’entrée GraphQL](#publishing-graphql-endpoint)

## Activation de votre point d’entrée GraphQL {#enabling-graphql-endpoint}

Pour activer un point d’entrée GraphQL, vous devez d’abord disposer d’une configuration appropriée. Voir [Fragments de contenu – Explorateur de configurations](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Si l’[utilisation des modèles de contenu du fragment n’a pas été activée](/help/assets/content-fragments/content-fragments-configuration-browser.md), l’option **Créer** n’est pas disponible.

Pour activer le point d’entrée correspondant :

1. Accédez à **Outils**, **Ressources**, puis sélectionnez **GraphQL**.
1. Sélectionnez **Créer**.
1. La boîte de dialogue **Créer un point d’entrée GraphQL** s’ouvre. Vous pouvez spécifier ici les éléments suivants :
   * **Nom** : nom du point d’entrée ; vous pouvez saisir du texte.
   * **Utiliser le schéma GraphQL fourni par** : utilisez la liste déroulante pour sélectionner le site/projet requis.

   >[!NOTE]
   >
   >L’avertissement suivant s’affiche dans la boîte de dialogue :
   >
   >* *Les points d’entrée GraphQL peuvent présenter des problèmes de sécurité et de performance des données s’ils ne sont pas gérés de manière adaptée. Veillez à définir les autorisations appropriées après la création d’un point d’entrée.*

1. Confirmez avec **Créer**.
1. La boîte de dialogue **Étapes suivantes** fournit un lien direct vers la console de sécurité afin que vous puissiez vous assurer que le nouveau point d’entrée dispose des autorisations appropriées.

   >[!CAUTION]
   >
   >Le point d’entrée est accessible à tous. Cela peut entraîner un problème de sécurité, en particulier pour les instances de publication, car les requêtes GraphQL peuvent imposer une charge importante au serveur.
   >
   >Vous pouvez configurer des listes de contrôle d’accès pour le point d’entrée en fonction de votre cas d’utilisation.

## Publication de votre point d’entrée GraphQL {#publishing-graphql-endpoint}

Sélectionnez le nouveau point d’entrée et **Publier** pour le rendre entièrement disponible dans tous les environnements.

>[!CAUTION]
>
>Le point d’entrée est accessible à tous.
>
>Cela peut entraîner un problème de sécurité sur les instances de publication, car les requêtes GraphQL peuvent imposer une charge importante au serveur.
>
>Vous devez configurer des listes de contrôle d’accès pour le point d’entrée en fonction de votre cas d’utilisation.
