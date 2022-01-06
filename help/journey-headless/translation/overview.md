---
title: AEM Parcours de traduction sans affichage
description: Commencez ici pour un parcours guidé en traduisant votre contenu sans tête à l’aide AEM puissants outils de traduction.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 8%

---

# AEM Parcours de traduction sans affichage {#aem-headless-translation-journey}

Commencez ici pour un parcours guidé en traduisant votre contenu sans tête à l’aide AEM puissants outils de traduction.

## Présentation {#introduction}

L’implémentation sans affichage devient de plus en plus importante pour diffuser des expériences à votre audience, où qu’elle soit et indépendamment du canal, de la région ou des paramètres régionaux.

L’implémentation découplée renonce à la gestion des pages et des composants, comme c’est généralement le cas avec les solutions complètes, et se concentre sur la création de fragments de contenu réutilisables et neutres du point de vue du canal, ainsi que sur leur diffusion entre canaux. En utilisant AEM puissants outils de traduction, ces fragments réutilisables peuvent être facilement traduits et diffusés à votre audience où qu’il soit.

Ce guide vous guide tout au long des rubriques de traduction sans tête les plus importantes afin que vous puissiez :

* disposer d’une vue d’ensemble de la diffusion de contenu sans interface ;
* Ayez une compréhension de base AEM les fonctions sans tête.
* Découvrez AEM fonctionnalités de traduction et comment elles sont liées au contenu sans interface.
* Vous pouvez commencer à traduire votre propre contenu sans tête.

Le but est de vous donner une large compréhension de la technologie sans tête, comment AEM diffuse du contenu sans tête, et comment vous pouvez le traduire. Si vous ne connaissez aucun de ces sujets, voici le point de départ idéal.

Si vous connaissez déjà l&#39;AEM, l&#39;absence de tête et la traduction, vous disposez peut-être déjà des connaissances fondamentales de ce parcours. Pensez à vous référer à notre documentation technique liée au [ressources supplémentaires section ci-dessous.](#additional-resources)

## AEM Parcours de documentation {#documentation-journeys}

[Un Parcours de documentation](/help/journey-documentation/home.md) Il relie de nombreux sujets et caractéristiques différents et peut-être complexes en fournissant un récit qui aide le lecteur, qui peut être nouveau pour AEM, comprendre et résoudre un problème commercial du début à la fin, tout en assumant un minimum de connaissances préalables ou AEM.

Les Parcours de documentation sont conçus autour des principes de bonnes pratiques, reposant sur les dernières recherches d’Adobe, l’expérience de mise en oeuvre éprouvée des consultants Adobe, ainsi que les commentaires des projets clients.

Si vous souhaitez savoir comment Adobe recommande de résoudre des affaires sans interface avec AEM, [AEM Parcours sans affichage](/help/journey-headless/home.md) où commencer.

## Public {#audience}

Ce parcours est conçu pour le personnage spécialisé en traduction, souvent appelé gestionnaire de projet de traduction ou TPM. Ce parcours présente les exigences, les étapes et les méthodes de traduction du contenu headless dans AEM. Le parcours peut définir des personnes supplémentaires avec lesquelles le traducteur doit interagir, mais le point de vue du parcours est celui du traducteur.

Ce parcours suppose que le lecteur a l’expérience de la traduction d’un contenu sur un système CMS volumineux, mais n’a aucune connaissance de la technologie sans interface ni de l’AEM.

Voici les personnages qui interagissent dans ce parcours.

| Personnage | Description | Rôle dans le Parcours |
|---|---|---|
| Spécialiste de traduction | Définit le contenu à traduire et gère ces workflows. | Audience de ce parcours |
| Auteur de contenu | Crée et gère du contenu diffusé sans interface | Les auteurs de contenu créent du contenu que le spécialiste de traduction doit traduire. |
| Administrateur | Gère la configuration et la configuration de base d’AEM | Le spécialiste des traductions travaille avec l’administrateur pour apporter les modifications de configuration nécessaires à la traduction, telles que l’installation d’un connecteur de traduction. |
| Architecte de contenu | Analyse les exigences relatives aux données qui doivent être distribuées sans interface et définit la structure de ces données | Les spécialistes de traduction travaillent avec l’architecte de contenu pour définir l’organisation du contenu afin qu’il puisse être facilement traduit. |

L&#39;information dans ce parcours peut bien sûr être utile à tous les acteurs, mais certaines informations peuvent être superflues à certains rôles. Restez à l’écoute pour [les prochains parcours couvrant des rôles supplémentaires.](/help/journey-documentation/home.md#journeys)

## Parcours de traduction sans affichage {#the-journey}

Vous allez explorer de nombreux sujets dans ce parcours. Les articles suivants vous donnent des connaissances fondamentales sur la traduction de contenu headless dans AEM et vous proposent des liens vers une documentation technique détaillée.

Bien que vous puissiez accéder directement à une partie spécifique du parcours, de nombreux concepts sont présentés dans des articles précédents. Par conséquent, si vous commencez à traduire sans interface en AEM, nous vous recommandons de commencer par le début et de progresser de manière séquentielle.

| Numéro | Article | Description |
|---|---|---|
| 0 | AEM Parcours de traduction sans affichage | Ce document |
| 1 | [Découvrez le contenu sans tête et comment le traduire en AEM](learn-about.md) | Apprenez les concepts sans tête, comment ils s&#39;adaptent à AEM, et la théorie de la traduction AEM. |
| 2 | [Prise en main de AEM traduction sans interface](getting-started.md) | Découvrez comment organiser votre contenu sans interface et comment AEM outils de traduction fonctionnent. |
| 3 | [Configuration du connecteur de traduction](configure-connector.md) | Découvrez comment connecter AEM à un service de traduction. |
| 4 | [Configuration des règles de traduction](translation-rules.md) | Découvrez comment définir des règles de traduction pour identifier le contenu à traduire. |
| 5 | [Traduire le contenu](translate-content.md) | Utilisez le connecteur et les règles de traduction pour traduire votre contenu sans interface utilisateur graphique. |
| 6 | [Publier le contenu traduit](publish-content.md) | Découvrez comment publier votre contenu traduit et mettre à jour la traduction lorsque le contenu sous-jacent est mis à jour. |

## Et après ? {#what-is-next}

Vous êtes maintenant prêt à prendre en main votre parcours de traduction sans interface Adobe. Nous vous encourageons à passer à la partie suivante du parcours et à lire l’article [Découvrez le contenu sans tête et comment le traduire en AEM](learn-about.md)

## Ressources supplémentaires {#additional-resources}

Les parcours de documentation vous montrent comment AEM résoudre un problème d’entreprise en vous fournissant une narration qui vous guide tout au long de processus et de fonctionnalités complexes et interconnectés. Un parcours illustre la façon dont plusieurs fonctionnalités fonctionnent ensemble pour répondre aux besoins d’une seule entreprise.

Ces parcours sont conçus pour être autonomes. Cependant, un certain nombre d’entre elles peuvent être liées. Consultez ces parcours supplémentaires pour plus d’informations sur la manière dont AEM puissantes fonctionnalités fonctionnent ensemble.

* [Parcours de création sans affichage](/help/journey-headless/author/overview.md) - Commencez ici pour un parcours guidé à travers les puissantes et flexibles fonctionnalités headless d’AEM, leurs fonctionnalités et comment modéliser votre contenu sur votre premier projet headless.
* [Parcours Architecte sans tête](/help/journey-headless/architect/overview.md) - Commencez ici pour découvrir les fonctionnalités puissantes, flexibles et sans interface d’Adobe Experience Manager et comment modéliser le contenu de votre projet.
* [AEM Parcours développeur sans tête](/help/journey-headless/developer/overview.md) - Commencez ici pour un parcours guidé à travers les puissantes et flexibles fonctionnalités headless d’AEM, leurs capacités et comment les exploiter dans votre premier projet de développement.
* [Documentation technique AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr) - Si vous connaissez déjà bien les technologies AEM et sans interface, consultez directement nos documents techniques détaillés.
* [Tutoriels AEM sans affichage](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr) - Si vous préférez apprendre par la pratique et êtes techniquement disposé, suivez nos tutoriels pratiques organisés par API et structure, qui explorent la création et l’utilisation d’applications reposant sur AEM Headless.
