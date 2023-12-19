---
title: En savoir plus sur le contenu découplé et comment le traduire dans AEM
description: Apprenez les concepts du découplage, en quoi ils s’appliquent à AEM et la théorie de la traduction dans AEM.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 93%

---

# En savoir plus sur le contenu découplé et comment le traduire dans AEM {#learn-about}

Apprenez les concepts du découplage, en quoi ils s’appliquent à AEM et la théorie de la traduction dans AEM.

## Objectif {#objective}

Ce document vous aide à comprendre la diffusion de contenu découplé, comment AEM prend en charge le découplage et comment ce contenu peut être traduit. Après avoir lu ce document, vous devriez :

* comprendre les concepts de base de la diffusion de contenus en mode découplé ;
* être familiarisé avec la façon dont AEM prend en charge le découplage et la traduction.

## Diffusion de contenu full-stack {#full-stack}

Depuis l’émergence des systèmes de gestion de contenu (CMS) à grande échelle et faciles d’utilisation, les organisations les utilisent comme emplacement central pour la gestion des messages, de leur image de marque et de leur communication. L’utilisation d’un CMS comme point central pour administrer les expériences a permis des gains d’efficacité en éliminant la nécessité de dupliquer les tâches dans des systèmes disparates.

![CMS full stack classique](/help/journey-headless/developer/assets/full-stack.png)

Dans un CMS en pile complète, toutes les fonctionnalités de manipulation de contenu se trouvent dans le CMS. Les fonctionnalités de ce système constituent différents composants de la pile CMS. Une solution full stack présente de nombreux avantages.

* Il n’y a qu’un seul système à maintenir.
* Le contenu est géré de manière centralisée.
* Tous les services du système sont intégrés.
* La création de contenu est transparente.

Ainsi, si un nouveau canal doit être ajouté ou si la prise en charge de nouveaux types d’expériences est requise, un (ou plusieurs) nouveaux composants peuvent être insérés dans la pile et il n’y a qu’un seul emplacement pour apporter des modifications.

![Ajout d’un nouveau canal à la pile](/help/journey-headless/developer/assets/adding-channel.png)

Cependant, la complexité des dépendances au sein de la pile apparaît rapidement, car d’autres éléments nécessitent des ajustements pour tenir compte des modifications.

## La tête d’un système découplé {#the-head}

La tête de tout système est généralement constituée du moteur de rendu de sortie, généralement sous la forme d’une interface utilisateur graphique ou d’une autre sortie graphique.

Lorsque nous parlons d’un CMS découplé (ou sans tête), il s’agit d’un système de gestion de contenu qui assure la diffusion en continu vers les consommateurs. Cependant, en n’effectuant que la diffusion du **contenu** de manière standardisée, un CMS découplé omet le rendu de sortie final, laissant la **présentation** du contenu au service consommateur.

![CMS découplé](/help/journey-headless/developer/assets/headless-cms.png)

Les services consommateurs, qu’il s’agisse d’expériences AR, d’un magasin web, d’expériences mobiles, d’applications web progressives (PWA), etc., récupèrent le contenu du CMS sans interface et fournissent leur propre rendu. Ils se chargent de fournir leurs propres têtes à votre contenu.

Omettre la tête (en mode découplé) permet de simplifier le CMS en éliminant sa complexité. Vous pouvez ainsi transférer la responsabilité de rendu du contenu vers les services qui en ont réellement besoin et qui sont souvent mieux adaptés pour cela.

## Traduction de contenu découplé dans AEM {#translating-in-aem}

En plus d’offrir des outils fiables pour la création, la gestion et la diffusion de pages web traditionnelles en mode full stack, AEM offre la possibilité de créer des sélections de contenu autonomes et de les diffuser de manière découplée.

La puissance d’AEM lui permet de diffuser du contenu découplé, en mode full stack ou dans les deux modes de façon simultanée. Pour le spécialiste de la traduction, le même ensemble d’outils de traduction peut être utilisé pour les deux types de contenu, ce qui vous donne une approche unifiée de la traduction de votre contenu.

Plus loin dans le parcours, vous découvrirez les détails de la traduction de contenu AEM, mais à un niveau général, le concept est simple :

1. Définissez une connexion à un service de traduction en configurant la structure d’intégration de traduction.
1. Définissez le contenu à traduire à l’aide des règles de traduction.
1. Créez un projet de traduction pour récolter le contenu, l’envoyer au service de traduction et recevoir les résultats.
1. Vérifiez et publiez le contenu traduit.

## Prochaines étapes {#what-is-next}

Merci de vous être engagé sur ce parcours de traduction découplée AEM ! Maintenant que vous avez lu ce document, vous devriez :

* comprendre les concepts de base de la diffusion de contenus en mode découplé ;
* être familiarisé avec la façon dont AEM prend en charge le découplage et la traduction.

Appuyez-vous sur ces connaissances et poursuivez votre parcours de traduction découplée AEM en consultant le document [Prise en main de la traduction découplée AEM](getting-started.md) dans lequel vous trouverez un aperçu sur la manière dont AEM gère le contenu découplé et sur ses outils de traduction.

## Ressources supplémentaires {#additional-resources}

Bien qu’il soit recommandé de passer à la partie suivante du parcours de traduction découplée en examinant le document [Prise en main de la traduction découplée AEM](getting-started.md), vous trouverez ci-dessous quelques ressources supplémentaires pour approfondir un certain nombre de concepts mentionnés dans ce document, sans être obligatoires pour poursuivre ce parcours découplé.

* [MSM et traduction](/help/sites-administering/msm-and-translation.md) – Informations sur AEM Multi-Site Manager et sur le fonctionnement de ses outils de traduction
* Une [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)
* Le [Portail de développement AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
