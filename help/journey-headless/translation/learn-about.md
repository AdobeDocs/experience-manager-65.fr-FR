---
title: Découvrez le contenu sans tête et comment le traduire en AEM
description: Apprenez les concepts sans tête, comment ils s'adaptent à AEM, et la théorie de la traduction AEM.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 32%

---

# Découvrez le contenu sans tête et comment le traduire en AEM {#learn-about}

Apprenez les concepts sans tête, comment ils s&#39;adaptent à AEM, et la théorie de la traduction AEM.

## Objectif {#objective}

Ce document vous aide à comprendre la diffusion de contenu sans interface utilisateur graphique, comment AEM prend en charge l’interface utilisateur sans interface utilisateur graphique et comment ce contenu peut être traduit. Après l’avoir lu, vous devriez :

* Découvrez les concepts de base de la diffusion de contenu sans interface utilisateur.
* Familiarisez-vous avec la façon dont AEM prend en charge les traductions et les headless.

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

Toutefois, la complexité des dépendances dans la pile devient rapidement visible, car d’autres éléments de la pile doivent être ajustés pour s’adapter aux modifications.

## La tête d’un système découplé {#the-head}

La tête de tout système est généralement constituée du moteur de rendu de sortie, généralement sous la forme d’une interface utilisateur graphique ou d’une autre sortie graphique.

Lorsque nous parlons d’un CMS découplé (ou sans tête), il s’agit d’un système de gestion de contenu qui assure la diffusion en continu vers les consommateurs. Cependant, en n’effectuant que la diffusion du **contenu** de manière standardisée, un CMS découplé omet le rendu de sortie final, laissant la **présentation** du contenu au service consommateur.

![CMS découplé](/help/journey-headless/developer/assets/headless-cms.png)

Les services consommateurs, qu’il s’agisse d’expériences AR, d’un magasin web, d’expériences mobiles, d’applications web progressives (PWA), etc., récupèrent du contenu du CMS sans interface et fournissent leur propre rendu. Ils se chargent de fournir leurs propres têtes à votre contenu.

Omettre la tête (en mode découplé) permet de simplifier le CMS en éliminant sa complexité. Vous pouvez ainsi transférer la responsabilité de rendu du contenu vers les services qui en ont réellement besoin et qui sont souvent mieux adaptés pour cela.

## Traduction de contenu sans affichage dans AEM {#translating-in-aem}

En plus d’offrir des outils fiables pour créer, gérer et diffuser des pages web traditionnelles de manière complète, AEM offre la possibilité de créer des sélections de contenu autonomes et de les diffuser sans interface.

La puissance d’AEM lui permet de diffuser du contenu en mode sans affichage, en mode plein empilement ou dans les deux modèles en même temps. Pour le spécialiste de la traduction, le même ensemble d’outils de traduction peut être appliqué aux deux types de contenu, ce qui vous donne une approche unifiée de la traduction de votre contenu.

Plus loin dans le parcours, vous découvrirez les détails de la traduction AEM contenu, mais à un niveau général, le concept est simple :

1. Définissez une connexion à un service de traduction en configurant la structure d’intégration de traduction.
1. Définissez le contenu à traduire à l’aide des règles de traduction.
1. Créez un projet de traduction pour récolter le contenu, l’envoyer au service de traduction et recevoir les résultats.
1. Passez en revue et publiez le contenu traduit.

## Et après ? {#what-is-next}

Merci d&#39;être venu sur votre parcours de traduction AEM sans interface ! Maintenant que vous avez lu ce document, vous devriez :

* Découvrez les concepts de base de la diffusion de contenu sans interface utilisateur.
* Familiarisez-vous avec la façon dont AEM prend en charge les traductions et les headless.

Tirez parti de ces connaissances et continuez votre parcours de traduction AEM sans interface utilisateur graphique en consultant le document. [Prise en main de AEM traduction sans interface](getting-started.md) où vous obtiendrez un aperçu de la façon dont AEM gère le contenu sans interface et apprend à connaître ses outils de traduction.

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de traduction sans interface utilisateur graphique en consultant le document [Prise en main de AEM traduction sans interface,](getting-started.md) vous trouverez ci-dessous des ressources facultatives supplémentaires qui approfondissent certains concepts mentionnés dans ce document, mais qui ne sont pas nécessaires pour continuer sur le parcours sans interface.

* [MSM et traduction](/help/sites-administering/msm-and-translation.md) - Détails d’AEM Multi Site Manager et son fonctionnement avec ses outils de traduction
