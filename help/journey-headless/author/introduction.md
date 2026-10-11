---
title: Créer en découplage avec Adobe Experience Manager
description: Cette section présente les fonctionnalités puissantes, flexibles et découplées d’Adobe Experience Manager et explique comment créer du contenu pour votre projet.
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer, User, Leader
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 99%
---
# Création pour le mode découplé avec AEM - Introduction {#author-headless-introduction}

Dans cette partie du [Parcours de création de contenu découplé AEM](overview.md), vous pouvez découvrir les concepts (de base) et la terminologie nécessaires pour comprendre la création de contenu pour une diffusion de contenu découplé avec Adobe Experience Manager (AEM).

## Objectif {#objective}

* **Audience** : débutant
* **Objectif** : découvrez les concepts et la terminologie relatifs à la création découplée.

## Système de gestion de contenu (CMS) {#content-management-system}

Qu’est-ce qu’un système de gestion de contenu ?

Le nom de système de gestion de contenu (CMS) est parfaitement parlant : il s’agit d’un système informatique utilisé pour gérer le contenu. Ce concept est un peu général. Pour être plus précis, il est (généralement) utilisé pour gérer le contenu que vous souhaitez rendre disponible sur votre ou vos sites web.

## CMS découplé {#headless-cms}

Le découplage est un terme utilisé pour décrire les systèmes qui dissocient efficacement le contenu de la manière d’afficher ce contenu sur le web.

Traditionnellement, vous gérez le contenu dans un CMS qui est responsable du rendu de ce contenu sur vos pages web.

Dans ce contexte, le mode découplé signifie que votre jeu de contenu peut être géré dans le CMS, puis être accessible par le biais d’une ou de plusieurs applications (indépendantes).

Cela signifie que votre contenu peut être diffusé sur n’importe quel appareil, dans de nombreux formats. Cela rend l’ensemble du processus beaucoup plus flexible et signifie également que vous n’avez pas à vous soucier de la mise en page et de la mise en forme.

>[!NOTE]
>
>Si vous souhaitez en savoir plus sur les détails techniques d’un CMS découplé, consultez la section En savoir plus sur le développement CMS découplé.

## Adobe Experience Manager {#aem-cms}

Qu’est-ce qu’AEM ?

Tout d’abord, AEM est un système de gestion de contenu qui propose un large éventail de fonctionnalités qui peuvent également être personnalisées pour répondre à vos besoins.

Cela signifie qu’il peut être utilisé en tant que :

* CMS découplé
  * Votre contenu découplé peut être créé en tant que **Fragments de contenu**.
    Il s’agit d’éléments de contenu autonomes accessibles directement par le biais de nombreuses applications, car ils disposent d’une structure prédéfinie basée sur les **Modèles de fragment de contenu**.
    Cela signifie que votre contenu peut atteindre de nombreux appareils différents, dans de nombreux formats et avec une grande variété de fonctionnalités.
    De plus, ces fragments peuvent également être utilisés lors de la construction de pages web AEM, si vous le souhaitez.

* CMS « traditionnel »
  * Le contenu est créé pour les pages web à l’aide de divers composants qui définissent la manière dont le contenu sera rendu sur votre site web. AEM fait également preuve dans ce cas d’une extrême flexibilité, car votre équipe de projet peut développer des composants personnalisés.

## Modélisation de contenu {#content-modeling}

La modélisation de contenu (également appelée modélisation des données) est donc un autre terme technique. Pourquoi devrait-il vous intéresser en tant qu’auteur ou autrice ?

Pour que les applications découplées puissent accéder à votre contenu et en faire quelque chose, votre contenu a vraiment besoin d’une structure prédéfinie. Il serait possible de donner à votre contenu une forme libre, mais cela rendrait la vie *vraiment* compliquée aux applications.

Fondamentalement, le processus de définition de la structure à laquelle votre contenu doit se conformer implique la conception d’un modèle, processus appelé « modélisation des données ».

Pour AEM, le rôle d’architecte de contenu (souvent une autre personne) effectue la modélisation des données afin de concevoir un éventail de **Modèles de fragment de contenu** que vous utilisez ensuite comme base pour votre contenu en utilisant les **Fragments de contenu**.

>[!NOTE]
>
>Si vous souhaitez en savoir plus sur la modélisation des données, consultez le parcours d’architecture de contenu découplé AEM.

## Prochaines étapes {#whats-next}

Maintenant que vous avez découvert les concepts et la terminologie, l’étape suivante consiste à [découvrir les principes de base de la création de fragments de contenu](basics.md). Cela permettra d’introduire la manipulation de base d’AEM ainsi que la création de fragments de contenu.

## Ressources supplémentaires {#additional-resources}

* Parcours du développeur découplé AEM
  * [En savoir plus sur le développement CMS découplé](/help/journey-headless/developer/learn-about.md)

* [Parcours d’architecture de contenu découplé AEM](/help/journey-headless/architect/overview.md)

* [Parcours de traduction de contenu découplé AEM](/help/journey-headless/translation/overview.md)

* [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)

* [Portail du développeur AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)

* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
