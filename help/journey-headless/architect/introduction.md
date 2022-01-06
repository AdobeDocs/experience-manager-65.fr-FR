---
title: AEM Parcours d’architecture de contenu sans affichage
description: Cette section présente les fonctionnalités puissantes, flexibles et sans interface d’Adobe Experience Manager et explique comment modéliser le contenu de votre projet.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 38%

---

# Modélisation de contenu pour sans affichage avec AEM - Introduction {#architect-headless-introduction}

Dans cette partie du [AEM Parcours d’architecture de contenu sans affichage](overview.md), vous pouvez découvrir les concepts (de base) et la terminologie nécessaires pour comprendre la modélisation de contenu pour la diffusion de contenu sans interface avec Adobe Experience Manager (AEM).

Ce document vous aide à comprendre la diffusion de contenu sans interface utilisateur graphique, comment AEM prend en charge l’interface sans interface utilisateur graphique et comment le contenu est modélisé pour l’interface utilisateur graphique. Après l’avoir lu, vous devriez :

* Découvrez les concepts de base de la diffusion de contenu sans interface utilisateur.
* Familiarisez-vous avec la façon dont AEM prend en charge la modélisation sans interface et de contenu.

## Objectif {#objective}

* **Audience** : débutant
* **Objectif**: Découvrez les concepts et la terminologie relatifs à la modélisation de contenu sans affichage.

## Diffusion de contenu full stack {#full-stack}

Depuis l’émergence des systèmes de gestion de contenu (CMS) à grande échelle et faciles d’utilisation, les entreprises les utilisent comme emplacement central pour la gestion des messages, des marques et de leur communication. L’utilisation d’un CMS comme point central pour administrer les expériences a permis des gains d’efficacité en éliminant la nécessité de dupliquer les tâches dans des systèmes disparates.

![CMS full stack classique](/help/journey-headless/developer/assets/full-stack.png)

Dans un CMS en pile complète, toutes les fonctionnalités de manipulation de contenu se trouvent dans le CMS. Les fonctionnalités de ce système constituent différents composants de la pile CMS. Une solution full stack présente de nombreux avantages.

* Il y a un système à maintenir.
* Le contenu est géré de manière centralisée.
* Tous les services du système sont intégrés.
* La création de contenu est transparente.

Ainsi, si un nouveau canal doit être ajouté ou si la prise en charge de nouveaux types d’expériences est requise, un (ou plusieurs) nouveaux composants peuvent être insérés dans la pile et il n’y a qu’un seul emplacement pour apporter des modifications.

![Ajout d’un nouveau canal à la pile](/help/journey-headless/developer/assets/adding-channel.png)

Toutefois, la complexité des dépendances au sein de la pile devient rapidement visible, car d’autres éléments de la pile doivent être ajustés pour tenir compte des modifications.

## La tête d’un système découplé {#the-head}

La tête de tout système est généralement constituée du moteur de rendu de sortie, généralement sous la forme d’une interface utilisateur graphique ou d’une autre sortie graphique.

Lorsque nous parlons d’un CMS découplé (ou sans tête), il s’agit d’un système de gestion de contenu qui assure la diffusion en continu vers les consommateurs. Cependant, en n’effectuant que la diffusion du **contenu** de manière standardisée, un CMS découplé omet le rendu de sortie final, laissant la **présentation** du contenu au service consommateur.

![CMS découplé](/help/journey-headless/developer/assets/headless-cms.png)

Les services consommateurs (expériences de réalité augmentée, boutiques web, expériences mobiles, applications web progressives (PWA), etc.) récupèrent le contenu du CMS découplé et fournissent leur propre rendu. Ils se chargent de fournir leurs propres têtes à votre contenu.

Omettre la tête (en mode découplé) permet de simplifier le CMS en éliminant sa complexité. Vous pouvez ainsi transférer la responsabilité de rendu du contenu vers les services qui en ont réellement besoin et qui sont souvent mieux adaptés pour cela.

## Modélisation de contenu {#content-modeling}

La modélisation de contenu (également appelée modélisation de données) est votre spécialité. Par conséquent, que doit-on prendre en compte lors de la modélisation pour headless ?

Pour que les applications sans interface utilisateur puissent accéder à votre contenu et en faire quelque chose, le contenu a vraiment besoin d’une structure prédéfinie. Il serait possible d&#39;avoir votre contenu comme forme libre, mais cela rendrait la vie *very* compliqué pour les applications.

Pour AEM, en tant qu’architecte de contenu, vous exécuterez la modélisation de contenu pour concevoir une plage de **Modèles de fragment de contenu**. Elles définissent la structure utilisée lorsque les auteurs de contenu créent la variable **Fragments de contenu** qui contiennent le contenu.

### Accès au contenu {#access-content}

C&#39;est plus un détail de développement, mais ça pourrait vous intéresser, juste pour terminer l&#39;histoire.

Une fois que vous avez créé les modèles de fragment de contenu et que vos auteurs les ont utilisés pour générer le contenu, les applications sans interface utilisateur doivent accéder à ce contenu.

Adobe Experience Manager (AEM) peut accéder de manière sélective à vos fragments de contenu à l’aide de l’API GraphQL AEM, afin de renvoyer uniquement le contenu nécessaire. Grâce à l’API, un développeur peut formuler des requêtes qui sélectionnent un contenu spécifique. Ce processus de sélection est basé sur *your* Modèles de fragment de contenu.

Cela signifie que votre projet peut réaliser la diffusion sans interface de contenu structuré à utiliser dans vos applications.

## Et après ? {#whats-next}

Maintenant que vous avez appris les concepts et la terminologie, l’étape suivante consiste à [Découvrez les principes de base de la modélisation avec des modèles de fragment de contenu](basics.md).

## Ressources supplémentaires {#additional-resources}

* Parcours de développement découplé AEM
   * [En savoir plus sur le développement CMS découplé](/help/journey-headless/developer/learn-about.md)
   * [Découvrez comment modéliser votre contenu](/help/journey-headless/developer/model-your-content.md)
