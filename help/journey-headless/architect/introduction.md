---
title: Parcours d’architecte de contenu découplé Adobe Experience Manager
description: Cette section présente les fonctionnalités puissantes, flexibles et découplées d’Adobe Experience Manager et explique comment modéliser le contenu de votre projet.
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 96%
---
# Modélisation de contenu pour le découplage avec AEM – Introduction {#architect-headless-introduction}

Dans cette partie du [Parcours d’architecture de contenu découplé AEM](overview.md), vous pouvez découvrir les concepts (de base) et la terminologie nécessaires pour comprendre la modélisation de contenu pour la diffusion de contenu découplé avec Adobe Experience Manager (AEM).

Ce document vous aide à comprendre la diffusion de contenu en mode découplé, comment AEM prend en charge le mode découplé et comment le contenu est modélisé pour ce mode. Après avoir lu ce document, vous devriez :

* comprendre les concepts de base de la diffusion de contenu en mode découplé
* Familiarisez-vous avec la façon dont AEM prend en charge le mode découplé et la modélisation de contenu.

## Objectif {#objective}

* **Audience** : débutant
* **Objectif** : découvrez les concepts et la terminologie relatifs à la modélisation de contenu découplé.

## Diffusion de contenu full-stack {#full-stack}

Depuis l’émergence des systèmes de gestion de contenu (CMS) à grande échelle et faciles d’utilisation, les organisations les utilisent comme emplacement central pour gérer les messages, le branding et la communication. L’utilisation d’un CMS comme point central pour administrer les expériences a permis des gains d’efficacité en éliminant la nécessité de dupliquer les tâches dans des systèmes disparates.

![CMS full stack classique](/help/journey-headless/developer/assets/full-stack.png)

Dans un CMS full-stack, toutes les fonctionnalités de manipulation du contenu se trouvent dans le CMS. Les fonctionnalités de ce système constituent différents composants de la pile CMS. Une solution full stack présente de nombreux avantages.

* Il n’y a qu’un seul système à maintenir.
* Le contenu est géré de manière centralisée.
* Tous les services du système sont intégrés.
* La création de contenu est transparente.

Ainsi, si un nouveau canal doit être ajouté ou si la prise en charge de nouveaux types d’expériences est requise, un ou plusieurs nouveaux composants peuvent être insérés dans la pile et les modifications sont alors effectuées à un seul endroit.

![Ajout d’un nouveau canal à la pile](/help/journey-headless/developer/assets/adding-channel.png)

Cependant, la complexité des dépendances au sein de la pile apparaît rapidement, car d’autres éléments nécessitent des ajustements pour tenir compte des modifications.

## La tête d’un système découplé {#the-head}

La tête de tout système est généralement constituée du moteur de rendu de sortie, généralement sous la forme d’une interface utilisateur graphique ou d’une autre sortie graphique.

Lorsque nous parlons d’un CMS découplé, le CMS gère le contenu et continue de le diffuser aux consommateurs et consommatrices. Cependant, en n’effectuant que la diffusion du **contenu** de manière standardisée, un CMS découplé omet le rendu de sortie final, laissant la **présentation** du contenu au service consommateur.

![CMS découplé](/help/journey-headless/developer/assets/headless-cms.png)

Les services consommateurs (expériences de réalité augmentée, boutiques Web, expériences mobiles, applications Web progressives (PWA), etc.) récupèrent le contenu du CMS découplé et fournissent leur propre rendu. Ils se chargent de fournir leurs propres têtes à votre contenu.

Le mode découplé permet de simplifier le CMS en éliminant sa complexité. Vous pouvez ainsi transférer la responsabilité de rendu du contenu vers les services qui en ont réellement besoin et qui sont souvent mieux adaptés pour cela.

## Modélisation de contenu {#content-modeling}

La modélisation de contenu (également appelée modélisation des données) est votre spécialité. Par conséquent, que doit-on prendre en compte lors de la modélisation pour le découplage ?

Pour que les applications découplées puissent accéder à votre contenu et l’utiliser, le contenu a vraiment besoin d’une structure prédéfinie. Il serait possible de donner à votre contenu une forme libre, mais cela compliquerait *grandement* les choses pour les applications.

Pour AEM, en tant qu’architecte de contenu, vous exécuterez la modélisation de contenu afin de concevoir un ensemble de **Modèles de fragments de contenu**. Ceux-ci définissent la structure utilisée lorsque les créateurs et créatrices de contenu créent les **Fragments de contenu** qui contiennent le contenu.

### Accès au contenu {#access-content}

En matière de développement, il s’agit d’un détail, mais ça pourrait vous intéresser, pour vous fournir une vue globale.

Une fois que vous avez créé les modèles de fragment de contenu et que vos auteurs et autrices les ont utilisés pour générer le contenu, les applications découplées doivent accéder à ce contenu.

Grâce à Adobe Experience Manager (AEM), vous pouvez accéder de manière sélective à vos fragments de contenu à l’aide de l’API GraphQL AEM, pour renvoyer uniquement le contenu nécessaire. Grâce à l’API, un développeur peut formuler des requêtes qui sélectionnent un contenu spécifique.Ce processus de sélection est basé sur *vos* modèles de fragment de contenu.

Cela signifie que votre projet peut réaliser une diffusion découplée d’un contenu structuré pour l’utiliser dans vos applications.

## Prochaines étapes {#whats-next}

Maintenant que vous avez appris les concepts et la terminologie, l’étape suivante consiste à [découvrir les principes de base de la modélisation avec des modèles de fragment de contenu](basics.md).

## Ressources supplémentaires {#additional-resources}

* Parcours du développeur découplé AEM
  * [En savoir plus sur le développement CMS découplé](/help/journey-headless/developer/learn-about.md)
  * [Découvrez comment modéliser votre contenu](/help/journey-headless/developer/model-your-content.md)
* [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)
* [Portail du développeur AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
