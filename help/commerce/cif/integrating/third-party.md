---
title: Intégration d’AEM et de solutions de commerce tierces à l’aide de Commerce Integration Framework
description: Les entreprises peuvent avoir besoin de solutions commerciales tierces supplémentaires pour alimenter leur storefront. Commerce Integration Framework (CIF) peut être utilisé dans de tels scénarios d’intégration pour connecter une solution commerciale tierce à Adobe Experience Manager à l’aide de l’environnement I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 96%

---

# Intégration d’AEM et de solutions de commerce tierces à l’aide de Commerce Integration Framework {#aem-third-party}

L’intégration d’une solution de commerce autre qu’Adobe est un scénario courant pour l’environnement CIF. Les solutions tierces avec différentes API et différents schémas sont connectées par le biais d’une couche d’intégration.

## Architecture {#architecture}

L’architecture globale se présente comme suit :

![Aperçu de l’architecture d’AEM avec des solutions non Magento/tierces](../assets//AEM_nonMagento_Architecture.png)

Cette couche d’intégration a pour but de mapper des API et des schémas tiers vis-à-vis des API et des schémas Adobe Commerce GraphQL pris en charge en dehors d’Experience Manager. Grâce à cette encapsulation, la logique d’intégration et les systèmes peuvent être mis à jour sans modifier le code dans Experience Manager.

## Exigences de solution pour une intégration

Lorsqu’Experience Manager récupère des données à la demande, des API en temps réel pour le catalogue de produits sont requises.

>[!TIP]
>
>Si aucune API en temps réel n’est disponible, un cache de produit externe avec les API doit être utilisé pour l’intégration. Exemple [Magento open-source](https://business.adobe.com/fr/products/magento/open-source.html).

Il n’est pas nécessaire de mettre en œuvre le schéma GraphQL complet, mais simplement les objets du schéma pour activer les cas d’utilisation souhaités.

## Cas d’utilisation du back-end

CIF étend Experience Manager avec un accès au catalogue de produits en temps réel et des outils de gestion de l’expérience produit. Cette intégration transparente permet aux auteurs d’accéder aux données commerciales à l’aide d’interfaces utilisateur intégrées si nécessaire, sans quitter le contexte de contenu.

L’intégration des API de catalogue de produits est nécessaire pour déverrouiller ces cas d’utilisation.

## Cas d’utilisation du front-end

Les [Composants principaux AEM CIF](https://github.com/adobe/aem-core-cif-components) récupèrent et échangent des données par le biais des API Commerce d’Adobe prises en charge par CIF. Pour réutiliser des composants, les API respectives doivent être implémentées.

Il est recommandé de communiquer directement avec la solution tierce afin d’éviter toute latence, ce qui est essentiel pour les performances des composants côté client.

## Développement d’une intégration {#develop-integration}

Adobe recommande d’utiliser [Adobe I/O Runtime](https://developer.adobe.com/apis/experienceplatform/runtime.html?lang=fr) pour la couche d’intégration. Il est inclus dans le module complémentaire CIF pour les solutions tierces. Comme il fonctionne avec une approche de microservice, il est bien adapté pour intégrer facilement plusieurs solutions.

La [mise en œuvre de référence](https://github.com/adobe/commerce-cif-graphql-integration-reference) est un excellent point de départ pour créer l’intégration à votre solution commerciale. Bien qu’il prenne en charge GraphQL, il peut également être intégré à tout autre type d’API comme REST.

Cette couche d’intégration n’est pas requise si une couche tierce est disponible (par exemple, Mulesoft) ou si l’intégration est créée sur la solution tierce.

## Connecteurs préconfigurés {#connectors}

Les connecteurs constituent un bon point de départ pour les projets. Ces éléments sont fournis avec une connexion spécifique à une solution de commerce et un mappage d’API par défaut. Ces connecteurs sont créés par des tiers et ne sont pas gérés par Adobe. Contactez le partenaire concerné pour obtenir des informations.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), configuré par Diconium
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), configuré par Diconium

>[!TIP]
>
>Bien que les connecteurs aident les projets à accélérer l’intégration du commerce, ils ne sont pas plug-n-play. Les solutions de commerce d’entreprise sont fortement personnalisées et nécessitent une intégration personnalisée. Une bonne connaissance de la plateforme commerciale, des schémas Adobe Commerce GraphQL et d’Adobe I/O Runtime est requise.
