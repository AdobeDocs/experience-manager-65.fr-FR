---
title: Couplage et découplage dans AEM
description: Il est possible de mettre en œuvre des projets AEM sur des modèles couplés et découplés, mais ce choix n’a pas besoin d’être si binaire. AEM offre la flexibilité nécessaire pour exploiter les avantages des deux modèles dans un même projet.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 80%
---
# Couplage et découplage dans AEM {#headful-headless}

Il est possible de mettre en œuvre des projets Adobe Experience Manager sur des modèles couplés et découplés, sans que toutefois ce choix soit binaire. AEM offre la flexibilité nécessaire pour exploiter les avantages des deux modèles dans un même projet. Ce document donne un aperçu des différents modèles et décrit les niveaux d’intégration des applications sur une seule page (SPA).

## Vue d’ensemble {#overview}

AEM offre de puissants outils pour gérer à la fois la création de contenus et leur diffusion sur une seule plateforme. Il s’agit d’un modèle traditionnel de gestion de contenu « couplé », où les auteurs et les développeurs de contenu travaillent sur la même plateforme pour mettre les expériences à la disposition des consommateurs de contenu.

Il est également possible d’utiliser AEM simplement pour gérer le contenu, ce qui permet de traiter la présentation et la diffusion du contenu à l’aide d’une autre plateforme. Il s’agit du modèle traditionnel de gestion de contenu « découplé », où les auteurs et les développeurs de contenu travaillent sur différentes plateformes pour mettre les expériences à la disposition des consommateurs de contenu.

Il ne s’agit pas nécessairement d’un choix binaire. AEM offre une flexibilité sans précédent, ce qui vous permet d’exploiter les avantages des deux modèles pour votre projet.

![Modèles d’implémentation AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

Dans un modèle couplé ou full stack, le contenu est géré dans le référentiel AEM et les composants AEM basés sur Java, HTL, etc., servent à effectuer le rendu du contenu pour l’expérience client. Dans ce modèle, la création du contenu, sa mise en forme, sa présentation et sa diffusion sont traitées dans AEM.

Dans un modèle découplé, le contenu est géré dans le référentiel AEM, mais diffusé à l’aide d’API telles que REST et GraphQL vers un autre système afin de générer le contenu pour l’expérience utilisateur. Dans ce modèle, le contenu est créé dans AEM, mais il est mis en forme, présenté et diffusé sur une autre plateforme.

Les applications monopages sont souvent destinataires du contenu diffusé par AEM à l’aide du modèle découplé. Cependant, ces SPA ne doivent pas nécessairement être entièrement externes à AEM. AEM vous donne la possibilité de décider jusqu’où votre SPA est intégrée à AEM. Prenons un exemple.

## Exemple d’une boutique web {#web-shop-example}

Supposons que votre entreprise dispose d’un site web sous la forme d’une SPA. Vous y trouverez tous les détails et images de votre produit. Vous introduisez ensuite AEM pour optimiser vos efforts marketing avec notamment du contenu de sites promotionnels, de blogs et de campagnes. Comment intégrer les deux ? AEM offre tout un éventail d’options :

* **Permettre aux systèmes de fonctionner de manière indépendante.**
* **Fournir à la boutique en ligne un contenu limité d’AEM via GraphQL.** Le contenu peut être créé par les auteurs dans AEM, mais uniquement visible via la SPA de la boutique en ligne.
* **Incorporer la SPA de la boutique en ligne dans AEM.** Le contenu peut être créé par les auteurs dans AEM et visualisé dans AEM dans le cadre de la boutique en ligne, mais pas manipulé.
* **Incorporez la SPA de la boutique en ligne dans AEM et activez les points modifiables.** Le contenu peut être créé par les auteurs dans AEM et visualisé dans AEM dans le cadre de la boutique en ligne. De plus, les auteurs ont une capacité limitée à manipuler le contenu de la SPA de la boutique en ligne dans AEM.
* **Incorporez la SPA de la boutique web dans AEM et activez des zones entières pour la modification.** Le contenu peut être créé par les auteurs dans AEM et visualisé dans AEM dans le cadre de la boutique en ligne. De plus, les auteurs ont une capacité limitée à manipuler le contenu de la SPA de la boutique en ligne dans AEM.

La section suivante examine ces niveaux d’intégration de manière plus détaillée.

>[!NOTE]
>
>Bien sûr, vous pouvez également réimplémenter la SPA de la boutique en ligne en tant que SPA d’AEM entièrement fonctionnelle [à l’aide du framework de l’éditeur de SPA d’AEM](/help/sites-developing/spa-walkthrough.md). Si vous disposez déjà d’AEM et que vous souhaitez créer une boutique en ligne ou une autre SPA, il s’agit de la méthode recommandée, mais elle n’est pas comprise dans ce document.

## Niveaux d’intégration SPA {#integration-levels}

L’intégration d’une SPA comporte une étendue de quatre niveaux dans AEM.

* **Niveau 0 : Aucune intégration**
  * La SPA et AEM existent séparément et n’échangent aucune information.
  * Le contenu est créé, géré et distribué indépendamment sur deux systèmes distincts.
* **Niveau 1 : Intégration de fragments de contenu**
  * Dans AEM, les [fragments de contenu](/help/assets/content-fragments/content-fragments.md) servent à créer et gérer du contenu limité pour la SPA.
  * La SPA récupère ce contenu par l’intermédiaire de l’[API GraphQL.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)
  * Certains contenus sont gérés dans AEM et d’autres dans un système externe.
  * Le contenu ne peut être affiché que dans la SPA.
* **Niveau 2 : Incorporation de la SPA dans AEM**
  * Dans AEM, les [fragments de contenu](/help/assets/content-fragments/content-fragments.md) servent à créer et gérer le contenu pour la SPA.
  * La SPA récupère ce contenu par l’intermédiaire de l’[API GraphQL.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)
  * Certains contenus sont gérés dans AEM et d’autres dans un système externe.
  * AEM permet de visualiser le contenu replacé dans son contexte.
  * Le contenu limité peut être modifié dans AEM.
* **Niveau 3 : Incorporation et activation complète des SPA dans AEM**
  * Dans AEM, les [fragments de contenu](/help/assets/content-fragments/content-fragments.md) servent à créer et gérer le contenu pour la SPA.
  * La SPA récupère ce contenu par l’intermédiaire de l’[API GraphQL.](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)
  * AEM permet de visualiser le contenu replacé dans son contexte.
  * L’essentiel du contenu peut être modifié dans AEM.

Le niveau 1 est un exemple typique d’une mise en œuvre découplée. Cependant, les auteurs de contenu ne peuvent afficher le contenu que replacé dans son contexte dans la SPA. AEM est un simple outil de création.

L’avantage et la souplesse d’AEM deviennent évidents avec les niveaux 2 et 3, tout en conservant les avantages des SPA. Les auteurs de contenu peuvent créer dans AEM, mais également le voir en le replaçant dans son contexte avec AEM. La SPA a l’avantage de pouvoir être écrite dans AEM, mais en restant diffusée sous la forme d’une SPA.

## Mise en œuvre des niveaux d’intégration {#implementing}

Différents outils sont proposés par AEM en fonction du niveau d’intégration choisi. Chaque niveau s’appuie sur les outils utilisés au niveau précédent. La liste suivante indique des liens vers des ressources appropriées.

* **Niveau 1 :** Les fragments de contenu et le [framework découplé d’AEM](/help/sites-developing/headless/introduction.md) permettent de diffuser du contenu AEM vers la SPA.
* **Niveau 2 :** En plus du niveau 1 :
  * [Le composant RemotePage](/help/sites-developing/spa-remote-page.md) permet d’incorporer la SPA externe dans AEM, le contenu AEM pouvant ainsi être affiché dans son contexte.
  * Certains points de la SPA peuvent également être activés pour [autoriser une modification limitée dans AEM.](/help/sites-developing/spa-edit-external.md)
* **Niveau 3 :** En plus du niveau 2 :
  * Des zones entières de la SPA peuvent être activées pour autoriser une modification complète dans AEM.
