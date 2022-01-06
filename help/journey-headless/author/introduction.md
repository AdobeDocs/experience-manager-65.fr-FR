---
title: AEM Parcours de création de contenu sans affichage
description: Cette section présente les fonctionnalités puissantes, flexibles et sans interface d’Adobe Experience Manager et explique comment créer du contenu pour votre projet.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 3%

---

# Création pour sans affichage avec AEM - Introduction {#author-headless-introduction}

Dans cette partie du [AEM Parcours de création de contenu sans affichage](overview.md), vous pouvez découvrir les concepts (de base) et la terminologie nécessaires pour comprendre la création de contenu pour une diffusion de contenu sans interface avec Adobe Experience Manager (AEM).

## Objectif {#objective}

* **Audience** : débutant
* **Objectif**: Découvrez les concepts et la terminologie relatifs à la création sans affichage.

## Système de gestion de contenu (CMS) {#content-management-system}

Qu’est-ce qu’un système de gestion de contenu ?

Un système de gestion de contenu (CMS) est exactement ce qu’il dit être : un système informatique utilisé pour gérer le contenu. C’est un peu général, donc, pour être plus précis, il est (généralement) utilisé pour gérer le contenu que vous souhaitez rendre disponible sur votre ou vos sites web.

## CMS découplé {#headless-cms}

Headless est un terme utilisé pour décrire les systèmes qui détache efficacement le contenu de la manière dont il affiche ce contenu sur le web.

Traditionnellement, vous gérez le contenu dans un CMS, et le même CMS est responsable du rendu de ce contenu sur vos pages web.

Désormais, sans interface utilisateur graphique, votre jeu de contenu peut être géré dans le CMS, puis accessible par une ou plusieurs applications (indépendantes).

Cela signifie que votre contenu peut être diffusé sur n’importe quel appareil, dans un large éventail de formats. Cela rend l’ensemble du processus beaucoup plus flexible et signifie également que vous n’avez pas à vous soucier de la mise en page et de la mise en forme.

>[!NOTE]
>
>Si vous souhaitez en savoir plus sur les détails techniques d’un CMS sans affichage, consultez la section En savoir plus sur le développement sans affichage de CMS .

## Adobe Experience Manager {#aem-cms}

Qu&#39;est-ce que AEM ?

Tout d’abord, AEM est un système de gestion de contenu qui propose un large éventail de fonctionnalités qui peuvent également être personnalisées pour répondre à vos besoins.

Cela signifie qu’il peut être utilisé comme :

* CMS découplé
   * Pour headless, votre contenu peut être créé en tant que **Fragments de contenu**.
Il s’agit d’éléments de contenu autonomes accessibles directement par un large éventail d’applications, car ils disposent d’une structure prédéfinie, basée sur **Modèles de fragment de contenu**.
Cela signifie que votre contenu peut atteindre un large éventail d’appareils, dans un large éventail de formats et avec un large éventail de fonctionnalités.
(Et en guise de double éponge, ces fragments peuvent également être utilisés lors de la construction de AEM pages web, si vous le souhaitez.)

* CMS &quot;traditionnel&quot;
   * Le contenu est créé pour les pages web à l’aide de divers composants qui définissent la manière dont le contenu sera rendu sur votre site web. Même ici, AEM est extrêmement flexible, car votre équipe de projet peut développer des composants personnalisés.

## Modélisation de contenu {#content-modeling}

La modélisation de contenu (également appelée modélisation de données) est donc un autre terme technique. Pourquoi devrait-il vous intéresser en tant qu’auteur ?

Pour que les applications sans interface utilisateur puissent accéder à votre contenu et faire quelque chose avec celui-ci, votre contenu a vraiment besoin d’une structure prédéfinie. Il serait possible d&#39;avoir votre contenu comme forme libre, mais cela rendrait la vie *very* compliqué pour les applications.

Fondamentalement, le processus de définition de la structure à laquelle votre contenu doit se conformer implique la conception d’un modèle, ce qu’on appelle la modélisation des données.

Pour AEM, le rôle d’architecte de contenu (souvent une autre personne) effectue la modélisation des données afin de concevoir une plage de **Modèles de fragment de contenu** : que vous utilisez ensuite comme base pour votre contenu en utilisant **Fragments de contenu**.

>[!NOTE]
>
>Si vous souhaitez en savoir plus sur la modélisation des données, vous pouvez en savoir plus sur le Parcours d’architecture de contenu sans affichage d’AEM.

## Et après ? {#whats-next}

Maintenant que vous avez appris les concepts et la terminologie, l’étape suivante consiste à [Découvrez les principes de base de la création de fragments de contenu](basics.md). Cela permettra d’introduire la gestion de base des AEM ainsi que la création de fragments de contenu.

## Ressources supplémentaires {#additional-resources}

* Parcours de développement découplé AEM
   * [En savoir plus sur le développement CMS découplé](/help/journey-headless/developer/learn-about.md)

* [AEM Parcours d’architecture de contenu sans affichage](/help/journey-headless/architect/overview.md)

* [AEM Parcours de traduction de contenu sans affichage](/help/journey-headless/translation/overview.md)
