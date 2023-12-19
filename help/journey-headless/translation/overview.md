---
title: Parcours de traduction découplée AEM
description: Faites vos premiers pas avec ce parcours guidé pour découvrir comment traduire votre contenu découplé à l’aide des puissants outils de traduction d’AEM.
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 94%

---

# Parcours de traduction découplée AEM {#aem-headless-translation-journey}

Faites vos premiers pas avec ce parcours guidé pour découvrir comment traduire votre contenu découplé à l’aide des puissants outils de traduction d’AEM.

## Présentation {#introduction}

L’implémentation découplée devient de plus en plus importante pour offrir des expériences à votre public, où qu’il se trouve et quel que soit son canal, sa zone ou ses paramètres géographiques.

L’implémentation découplée renonce à la gestion des pages et des composants, comme c’est généralement le cas avec les solutions complètes, et se concentre sur la création de fragments de contenu réutilisables et neutres du point de vue du canal, ainsi que sur leur diffusion entre canaux. En utilisant les puissants outils de traduction d’AEM, ces fragments réutilisables peuvent être facilement traduits et diffusés à votre audience, où qu’elle soit.

Ce guide détaille les sujets les plus importants concernant la traduction découplée afin que vous puissiez :

* disposer d’une vue d’ensemble sur la diffusion découplée ;
* disposer d’une compréhension de base des fonctions découplées d’AEM ;
* connaître les fonctionnalités de traduction d’AEM et leur lien avec le contenu découplé ;
* être capable de traduire votre propre contenu découplé.

L’objectif est de vous donner une compréhension globale de la technologie découplée, de la manière dont AEM diffuse du contenu découplé et de la manière dont vous pouvez le traduire. Si vous ne connaissez aucun de ces sujets, ce parcours représente le parfait point de départ.

Si vous connaissez déjà les principes d’AEM, du découplage et de la traduction, vous disposez peut-être déjà des connaissances fondamentales offertes par ce parcours. Pensez à vous référer à notre documentation technique dans la section présentant les [ressources supplémentaires ci-dessous.](#additional-resources)

## Parcours de documentation AEM {#documentation-journeys}

Un [Parcours de documentation](/help/journey-documentation/home.md) relie de nombreux sujets et fonctionnalités différents et parfois complexes en aidant le lecteur, parfois débutant dans AEM, à comprendre et à résoudre un problème d’activité du début à la fin, tout en présupposant un minimum de connaissances préalables concernant le sujet ou AEM.

Les parcours de documentation sont conçus autour des principes de bonne pratique, reposent sur les dernières recherches d’Adobe, sur l’expérience éprouvée de mise en œuvre des consultants Adobe, ainsi que sur les retours de projets clients.

Si vous souhaitez savoir comment Adobe recommande de résoudre des cas d’utilisation découplés avec AEM, les [Parcours découplés AEM](/help/journey-headless/home.md) sont un bon endroit pour commencer.

## Public {#audience}

Ce parcours est conçu pour le profil de spécialiste en traduction, souvent appelé gestionnaire de projet de traduction (TPM). Ce parcours présente les exigences, les étapes et les méthodes de traduction du contenu découplé dans AEM. Il définit les personnes supplémentaires avec lesquelles le spécialiste de la traduction doit interagir, mais le point de vue du parcours est celui du spécialiste de la traduction.

Ce parcours présuppose que le lecteur dispose d’une expérience en traduction de contenu sur un système CMS volumineux sans aucune connaissance de la technologie découplée ou d’AEM.

Voici les personnes qui interagissent dans ce parcours.

| Personne | Description | Rôle dans le parcours |
|---|---|---|
| Spécialiste de traduction | Définit le contenu à traduire et gère les workflows. | Audience ciblée de ce parcours |
| Auteur de contenu | Crée et gère le contenu diffusé de façon découplée | Les auteurs de contenu créent du contenu que le spécialiste de traduction doit traduire. |
| Administrateur | Gère les paramètres et la configuration de base d’AEM | Le spécialiste de la traduction travaille avec l’administrateur pour apporter les modifications de configuration nécessaires à la traduction, telles que l’installation d’un connecteur de traduction. |
| Architecte de contenu | Analyse les exigences relatives aux données qui doivent être diffusées en mode découplé et définit la structure de ces données | Les spécialistes de la traduction travaillent avec l’architecte de contenu pour définir l’organisation du contenu afin qu’il puisse être facilement traduit. |

Les informations contenues dans ce parcours peuvent être utiles à tous les acteurs, mais certaines informations peuvent être superflues à certains rôles. Tenez-vous informés des [prochains parcours couvrant les spécificités des rôles supplémentaires.](/help/journey-documentation/home.md#journeys)

## Le parcours de traduction découplée {#the-journey}

Vous découvrirez de nombreux sujets dans ce parcours. Les articles suivants vous donnent une connaissance fondamentale sur la traduction de contenu découplé dans AEM et vous proposent des liens vers une documentation technique détaillée.

Bien que vous puissiez accéder directement à une partie spécifique du parcours, de nombreux concepts sont présentés dans des articles précédents. Par conséquent, si le concept de traduction découplée dans AEM est nouveau pour vous, nous vous recommandons de commencer par le début et de progresser de manière chronologique.

| Numéro | Article | Description |
|---|---|---|
| 0 | Parcours de traduction découplée AEM | Ce document |
| 1 | [En savoir plus sur le contenu découplé et comment le traduire dans AEM](learn-about.md) | Apprenez les concepts du découplage, en quoi ils s’appliquent à AEM et la théorie de la traduction dans AEM. |
| 2 | [Prise en main de la traduction découplée dans AEM](getting-started.md) | Découvrez comment organiser votre contenu découplé et comment fonctionnent les outils de traduction AEM. |
| 3 | [Configuration de l’intégration de traduction](configure-connector.md) | Découvrez comment connecter AEM à un service de traduction. |
| 4 | [Configuration des règles de traduction](translation-rules.md) | Découvrez comment définir des règles de traduction pour identifier le contenu à traduire. |
| 5 | [Traduction du contenu](translate-content.md) | Utilisez l’intégration de traduction et les règles pour traduire votre contenu sans interface utilisateur. |
| 6 | [Publication du contenu traduit](publish-content.md) | Découvrez comment publier votre contenu traduit et mettre à jour les traductions au fur et à mesure que le contenu est mis à jour. |

## Prochaines étapes {#what-is-next}

Vous êtes maintenant prêt à prendre en main votre parcours de traduction découplée Adobe. Nous vous encourageons à passer à la partie suivante du parcours et à lire l’article [En savoir plus sur le contenu découplé et comment le traduire dans AEM](learn-about.md).

## Ressources supplémentaires {#additional-resources}

Les parcours de documentation vous montrent comment AEM permet de résoudre un problème d’activité en vous fournissant une narration qui vous guide tout au long de processus et de fonctionnalités complexes et interconnectés. Un parcours illustre la façon dont plusieurs fonctionnalités fonctionnent ensemble pour répondre à un unique besoin d’activité.

Ainsi, les parcours sont conçus pour être autonomes. Cependant, plusieurs d’entre elles peuvent être liées les unes aux autres. Consultez ces parcours supplémentaires pour plus d’informations sur la manière dont les puissantes fonctionnalités d’AEM fonctionnent ensemble.

* [Parcours de création découplée](/help/journey-headless/author/overview.md) – Faites vos premiers pas avec cette visite guidée et découvrez les fonctionnalités découplées puissantes et flexibles d’AEM, leurs capacités et comment les modéliser votre contenu dans votre premier projet découplé.
* [Parcours d’architecture découplée](/help/journey-headless/architect/overview.md) – Faites vos premiers pas avec cette introduction sur les fonctionnalités puissantes, flexibles et découplées d’Adobe Experience Manager et comment modéliser le contenu de votre projet.
* [Parcours de développement AEM Headless](/help/journey-headless/developer/overview.md) : faites vos premiers pas avec cette visite guidée et découvrez les fonctionnalités découplées puissantes et flexibles d’AEM, leurs capacités et comment les exploiter dans votre premier projet de développement.
* [Documentation technique d’AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr) – Si vous connaissez déjà bien les technologies AEM et découplées, vous pouvez consulter directement notre documentation technique détaillée.
   * Une [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)
* [Tutoriels pour AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr) : si vous préférez apprendre par la pratique et préférez la technique à la théorie, suivez nos tutoriels pratiques organisés par API et par structure, qui explorent la création et l’utilisation d’applications reposant sur le découplage AEM.
* Le [Portail Développement AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
