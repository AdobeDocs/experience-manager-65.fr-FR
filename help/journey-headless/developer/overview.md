---
title: Parcours de développement découplé AEM
description: AEM Documentation CMS sans affichage. Faites vos premiers pas avec cette visite guidée et découvrez les fonctionnalités découplées puissantes et flexibles d’AEM, leurs capacités et comment les exploiter dans votre premier projet de développement.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 52%

---

# Parcours de développement découplé AEM {#aem-headless-developer-journey}

Faites vos premiers pas avec cette visite guidée et découvrez les fonctionnalités découplées puissantes et flexibles d’AEM, leurs capacités et comment les exploiter dans votre premier projet de développement découplé. Ce parcours vous fournit toute la documentation AEM sans affichage dont vous avez besoin pour développer votre première application sans interface utilisateur.

## Présentation {#introduction}

L’implémentation découplée renonce à la gestion des pages et des composants, comme c’est généralement le cas avec les solutions complètes, et se concentre sur la création de fragments de contenu réutilisables et neutres du point de vue du canal, ainsi que sur leur diffusion entre canaux. Il s’agit d’un modèle de développement moderne et dynamique pour l’implémentation d’expériences numériques.

Ce guide vous guide tout au long des rubriques d’implémentation les plus headless d’AEM afin que vous puissiez :

* comprendre pleinement ce qu’est la diffusion de contenu découplé et ses avantages ;
* comprendre les fonctionnalités découplées AEM et comment elles s’associent pour vous offrir une expérience découplée ;
* effectuer les premières étapes de la mise en œuvre de votre premier projet AEM découplé.

## AEM Parcours de documentation {#documentation-journeys}

[Un Parcours de documentation](/help/journey-documentation/home.md) Il relie de nombreux sujets et caractéristiques différents et peut-être complexes en fournissant un récit qui aide le lecteur, qui peut être nouveau pour AEM, comprendre et résoudre un problème commercial du début à la fin, tout en assumant un minimum de connaissances préalables ou AEM.

Les Parcours de documentation sont conçus autour des principes de bonnes pratiques, reposant sur les dernières recherches d’Adobe, l’expérience de mise en oeuvre éprouvée des consultants Adobe, ainsi que les commentaires des projets clients.

Si vous souhaitez savoir comment Adobe recommande de résoudre des affaires sans interface avec AEM, [AEM Parcours sans affichage](/help/journey-headless/home.md) où commencer.

>[!TIP]
>
> Si vous préférez **apprendre en faisant** et sont techniquement utiles, consultez les tutoriels AEM sans affichage, organisés par API et structure et disponibles dans la [Section Ressources supplémentaires](#additional-resources) à la fin de ce document.

## Public {#audience}

Ce parcours est conçu à l’intention des développeurs et présente les exigences, les étapes et l’approche d’un projet AEM découplé du point de vue du développeur. Le parcours définit des personnes supplémentaires avec lesquelles le développeur doit interagir pour un projet réussi, mais le point de vue du parcours est celui du développeur.

Voici les personnages qui interagissent dans ce parcours.

| Personnage | Description | Rôle dans ce Parcours |
|---|---|---|
| Développeur (audience cible) | Expérience dans le développement d’applications sans interface utilisateur graphique qui consomment du contenu provenant de différentes sources | Public cible de ce parcours |
| Auteur de contenu | Crée et gère le contenu diffusé sans interface | Les auteurs de contenu créent du contenu que le développeur diffuse sans interface. |
| Administrateur | Gère la configuration et la configuration de base d’AEM | Le développeur travaille avec l’administrateur pour apporter les modifications de configuration nécessaires au développement. |
| Architecte de contenu | Analyse les exigences relatives aux données qui doivent être distribuées sans interface et définit la structure de ces données | Les développeurs travaillent avec l’architecte de contenu pour comprendre la structure des données et les exigences nécessaires pour les diffuser en toute sécurité. |

L&#39;information dans ce parcours peut bien sûr être utile à tous les acteurs, mais certaines informations peuvent être superflues à certains rôles. Restez à l’écoute pour [les prochains parcours couvrant des rôles supplémentaires.](/help/journey-documentation/home.md#journeys)

## Le parcours de développement découplé {#the-journey}

Vous allez explorer de nombreux sujets dans ce parcours. Les articles suivants vous donnent une connaissance fondamentale sur les projets découplés dans AEM et vous proposent des liens vers une documentation technique détaillée.

Bien que vous puissiez accéder directement à une partie spécifique du parcours, de nombreux concepts sont présentés dans des articles précédents. Par conséquent, si le concept de découplage dans AEM est nouveau pour vous, nous vous recommandons de commencer par le début et de progresser de manière chronologique.

| Numéro | Article | Description |
|---|---|---|
| 0 | Parcours de développement découplé AEM | Ce document |
| 1 | [En savoir plus sur le développement CMS découplé](learn-about.md) | Découvrez la technologie découplée et quand l’utiliser. |
| 2 | [Prise en main d’AEM Headless](getting-started.md) | En savoir plus sur les prérequis d’AEM découplé |
| 3 | [Chemin d’accès à votre première expérience à l’aide d’AEM découplé](path-to-first-experience.md) | Configurez votre environnement de développement et apprenez à intégrer une application simple avec AEM découplé. |
| 4 | [Comment modéliser votre contenu](model-your-content.md) | Découvrez comment modéliser votre structure de contenu. Créez ensuite cette structure pour Adobe Experience Manager (AEM) à l’aide des modèles de fragments de contenu et des fragments de contenu, en vue de la réutiliser sur plusieurs canaux. |
| 5 | [Accès à votre contenu grâce aux API de diffusion AEM](access-your-content.md) | Découvrez comment utiliser des requêtes GraphQL pour accéder au contenu de vos fragments de contenu. |
| 6 | [Comment mettre à jour votre contenu via les API AEM Assets](update-your-content.md) | Découvrez comment utiliser l’API REST pour accéder au contenu de vos fragments de contenu et le mettre à jour. |
| 7 | [Comment tout assembler – votre application et votre contenu dans AEM découplé](put-it-all-together.md) | Découvrez comment prendre votre projet AEM et le préparer pour la mise en ligne avec le SDK AEM découplé. |
| 8 | [Facultatif – Comment créer des applications d’une seule page (SPA) avec AEM](create-spa.md) | Une fois que vous avez compris comment fonctionnent les fonctionnalités découplées AEM, découvrez comment combiner une diffusion utilisateur couplée et découplée et comment créer des SPA modifiables à l’aide de la structure de l’éditeur d’AEM. |

<!-- HM-Links
|8|[How to go live with your headless application](go-live.md)|Learn how to deploy application live and take your local code in Git and move it to Cloud Manager Git for CI/CD pipeline.|
|9|[Optional - How to create single page applications (SPAs) with AEM](create-spa.md)|Once you understand AEM's headless features, explore how to combine headful and headless delivery and learn how you can create editable SPAs using AEM's SPA Editor framework.|
-->

## Et après ? {#what-is-next}

Vous êtes maintenant prêt à prendre en main votre parcours découplé Adobe. Nous vous encourageons à passer à la section suivante du parcours et à lire l’article [Découvrez le développement CMS découplé](learn-about.md).

### Choisissez votre propre parcours {#choose-your-path}

Toutefois, Adobe souhaite que vous réussissiez à démarrer votre projet AEM découplé, quel que soit votre style d’apprentissage. Considérez alors ces deux options.

* Si vous préférez continuer à **découvrir les concepts du mode découplé et les technologies en mode découplé d’AEM**, vous devez continuer votre parcours avec AEM découplé comme le recommande le document [Comment modéliser votre contenu sous la forme de modèles de contenu](model-your-content.md) où vous apprendrez à modéliser votre structure de contenu dans AEM.
* Si vous préférez **apprendre en pratiquant**, vous pouvez passer au [tutoriel de prise en main d’AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=fr). Vous pourrez ainsi accéder directement au développement avec AEM découplé en mettant en œuvre un projet simple pour exposer un contenu découplé.

## Ressources supplémentaires {#additional-resources}

Les parcours de documentation vous montrent comment AEM résoudre un problème d’entreprise en vous fournissant une narration qui vous guide tout au long de processus et de fonctionnalités complexes et interconnectés. Un parcours illustre la façon dont plusieurs fonctionnalités fonctionnent ensemble pour répondre aux besoins d’une seule entreprise.

Ces parcours sont conçus pour être autonomes. Cependant, un certain nombre d’entre elles peuvent être liées. Consultez ces parcours supplémentaires pour plus d’informations sur la manière dont AEM puissantes fonctionnalités fonctionnent ensemble.

* [Tutoriels AEM sans affichage](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr) - Si vous préférez apprendre par la pratique et êtes techniquement disposé, suivez nos tutoriels pratiques organisés par API et structure, qui explorent la création et l’utilisation d’applications reposant sur AEM Headless.
* [AEM Parcours de traduction sans affichage](/help/journey-headless/translation/overview.md) - Ce parcours de documentation vous donne une large compréhension de la technologie sans interface, de la manière dont AEM diffuse du contenu sans interface et de la manière dont vous pouvez le traduire.
* [Parcours de création sans affichage](/help/journey-headless/author/overview.md) - Commencez ici pour un parcours guidé à travers les puissantes et flexibles fonctionnalités headless d’AEM, leurs fonctionnalités et comment modéliser votre contenu sur votre premier projet headless.
* [Parcours Architecte sans tête](/help/journey-headless/architect/overview.md) - Commencez ici pour découvrir les fonctionnalités puissantes, flexibles et sans interface d’Adobe Experience Manager et comment modéliser le contenu de votre projet.
* [Documentation technique AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr) - Si vous connaissez déjà bien les technologies AEM et sans interface, consultez directement nos documents techniques détaillés.
