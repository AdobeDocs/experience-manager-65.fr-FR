---
title: En savoir plus sur le contenu découplé et comment le traduire dans AEM
description: Apprenez les concepts du découplage, en quoi ils s’appliquent à AEM et la théorie de la traduction dans AEM.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
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
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
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
source-wordcount: '775'
ht-degree: 100%
---
# En savoir plus sur le contenu découplé et comment le traduire dans AEM {#learn-about}

Apprenez les concepts du découplage, en quoi ils s’appliquent à AEM et la théorie de la traduction dans AEM.

## Objectif {#objective}

Ce document vous aide à comprendre la diffusion de contenu découplé, comment AEM prend en charge le découplage et comment ce contenu peut être traduit. Après avoir lu ce document, vous devriez :

* comprendre les concepts de base de la diffusion de contenus en mode découplé ;
* être familiarisé avec la façon dont AEM prend en charge le découplage et la traduction.

## Diffusion de contenu full-stack {#full-stack}

Depuis l’émergence des systèmes de gestion de contenu (CMS) à grande échelle et faciles d’utilisation, les organisations les utilisent comme emplacement central pour gérer les messages, le branding et la communication. L’utilisation d’un CMS comme point central pour administrer les expériences a permis des gains d’efficacité en éliminant la nécessité de dupliquer les tâches dans des systèmes disparates.

![CMS full stack classique](/help/journey-headless/developer/assets/full-stack.png)

Dans un CMS full-stack, toutes les fonctionnalités de manipulation du contenu se trouvent dans le CMS. Les fonctionnalités de ce système constituent différents composants de la pile CMS. Une solution full stack présente de nombreux avantages.

* Il n’y a qu’un seul système à maintenir.
* Le contenu est géré de manière centralisée.
* Tous les services du système sont intégrés.
* La création de contenu est transparente.

Ainsi, si un nouveau canal doit être ajouté ou si la prise en charge de nouveaux types d’expériences est requise, un (ou plusieurs) nouveaux composants peuvent être insérés dans la pile et il n’y a qu’un seul emplacement pour apporter des modifications.

![Ajout d’un nouveau canal à la pile](/help/journey-headless/developer/assets/adding-channel.png)

Cependant, la complexité des dépendances au sein de la pile apparaît rapidement, car d’autres éléments nécessitent des ajustements pour tenir compte des modifications.

## La tête d’un système découplé {#the-head}

La tête de tout système est généralement constituée du moteur de rendu de sortie, généralement sous la forme d’une interface utilisateur graphique ou d’une autre sortie graphique.

Lorsque nous parlons d’un CMS découplé, le CMS gère le contenu et continue de le diffuser aux consommateurs et consommatrices. Cependant, en n’effectuant que la diffusion du **contenu** de manière standardisée, un CMS découplé omet le rendu de sortie final, laissant la **présentation** du contenu au service consommateur.

![CMS découplé](/help/journey-headless/developer/assets/headless-cms.png)

Les services consommateurs (expériences de réalité augmentée, boutiques web, expériences mobiles, applications web progressives (PWA), etc.) récupèrent le contenu du CMS découplé et fournissent leur propre rendu. Ils se chargent de fournir leur propre rendu pour votre contenu.

Le mode découplé permet de simplifier le CMS en éliminant sa complexité. Vous pouvez ainsi transférer la responsabilité de rendu du contenu vers les services qui en ont réellement besoin et qui sont souvent mieux adaptés pour cela.

## Traduction de contenu découplé dans AEM {#translating-in-aem}

En plus d’offrir des outils fiables pour la création, la gestion et la diffusion de pages web traditionnelles en mode full stack, AEM offre la possibilité de créer des sélections de contenu autonomes et de les diffuser de manière découplée.

La puissance d’AEM lui permet de diffuser du contenu découplé, en mode full stack ou dans les deux modes de façon simultanée. Pour le spécialiste de la traduction, le même ensemble d’outils de traduction peut être utilisé pour les deux types de contenu, ce qui vous donne une approche unifiée de la traduction de votre contenu.

Plus loin dans le parcours, vous découvrirez en détail comment AEM traduit le contenu, mais à un niveau général, le concept est simple :

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
* La variable [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
