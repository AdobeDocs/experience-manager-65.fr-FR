---
title: Introduction et présentation des applications monopage (SPA)
description: Cet article présente les concepts d’une SPA et décrit l’utilisation d’une SPA élémentaire à des fins de création, indiquant comment cette utilisation est liée à l’éditeur de SPA AEM sous-jacent.
topic-tags: spa
content-type: reference
exl-id: 95990112-2afc-420a-a7c7-9613f40d4c4a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 100%

---


# Introduction et présentation des applications monopage (SPA) {#spa-introduction-and-walkthrough}

Les applications monopage (SPA) peuvent améliorer considérablement l’expérience des sites web. Les développeurs et développeuses souhaitent pouvoir créer des sites avec des frameworks SPA. Les auteurs et autrices, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de tels frameworks.

L’éditeur de SPA constitue une solution complète pour la prise en charge des SPA dans AEM. Cet article décrit l’utilisation d’une SPA élémentaire à des fins de création et indique comment cette utilisation est liée à l’éditeur de SPA AEM sous-jacent.

{{ue-over-spa}}

## Présentation {#introduction}

### Objectif de l’article {#article-objective}

Cet article présente les concepts de base des SPA, puis passe en revue l’éditeur de SPA en utilisant une SPA simple pour démontrer les fonctions de base de modification de contenu. Il détaille ensuite la construction de la page et indique comment la SPA est liée à l’éditeur de SPA AEM et interagit avec lui.

L’objectif de cette introduction et de cette présentation est de montrer aux développeurs AEM pourquoi les SPA sont pertinentes, comment elles fonctionnent, comment elles sont gérées par l’éditeur de SPA AEM et en quoi elles diffèrent d’une application AEM standard.

## Conditions requises {#requirements}

La présentation repose sur les fonctionnalités AEM standard et l’exemple d’application de projet SPA WKND. Pour suivre cette présentation, vous devez disposer des éléments suivants.

* [Version 6.5.4 ou ultérieure d’AEM](/help/release-notes/release-notes.md)
   * Vous devez disposer des droits d’administration sur le système.
* [Exemple d’application de projet WKND SPA disponible sur GitHub](https://github.com/adobe/aem-guides-wknd-spa)
   * Téléchargez la [dernière version de l’application React.](https://github.com/adobe/aem-guides-wknd-spa/releases) Son nom sera similaire à `wknd-spa-react.all.classic-X.Y.Z-SNAPSHOT.zip`.
   * Téléchargez les [exemples d’images les plus récents](https://github.com/adobe/aem-guides-wknd-spa/releases) pour l’application. Son nom sera similaire à `wknd-spa-sample-images-X.Y.Z.zip`.
   * [Utilisez le gestionnaire de modules](/help/sites-administering/package-manager.md) pour installer les packages comme vous le feriez pour tout autre package dans AEM.
   * L’application n’a pas besoin d’être installée à l’aide de Maven pour cette présentation.

>[!CAUTION]
>
>Ce document utilise l’[exemple d’application de projet WKND SPA](https://github.com/adobe/aem-guides-wknd-spa) des fins de démonstration uniquement. Ne l’utilisez pas dans le cadre d’un projet.
>
>Tout projet AEM doit utiliser l’[archétype de projet AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr), qui prend en charge les projets SPA à l’aide de React ou d’Angular et utilise le SDK SPA.

### Qu’est-ce qu’une SPA ? {#what-is-a-spa}

Une application monopage (SPA) diffère d’une page conventionnelle en cela qu’elle est rendue côté client et qu’elle est principalement pilotée par JavaScript, en utilisant les appels Ajax pour charger les données et mettre la page à jour dynamiquement. La plupart ou la totalité du contenu est récupérée une fois au chargement d’une seule page avec des ressources supplémentaires chargées de manière asynchrone, selon les besoins, en fonction de l’interaction de l’utilisateur avec la page.

Cela limite la nécessité d’actualiser la page et offre à l’utilisateur une expérience harmonieuse, rapide et rappelant davantage l’expérience d’une application native.

L’éditeur de SPA d’AEM permet aux développeurs et aux développeuses front-end de créer des SPA qui peuvent être intégrées à un site AEM, ce qui permet aux créateurs et créatrices de contenu de modifier le contenu de SPA aussi facilement qu’un autre contenu AEM.

### Pourquoi une SPA ?  {#why-a-spa}

Plus rapide, fluide et ressemblant davantage à une application native, une SPA, de par son fonctionnement, offre une expérience très attrayante, non seulement pour le visiteur de la page web, mais aussi pour les spécialistes du marketing et les développeurs.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visiteurs**

* Lorsqu’ils interagissent avec du contenu, les visiteurs souhaitent des expériences similaires à l’expérience d’une application native.
* Il existe des données claires indiquant que plus une page est rapide, plus une conversion est probable.

**Spécialistes du marketing**

* Les spécialistes du marketing veulent offrir des expériences riches et similaires à l’expérience d’une application native pour inciter les visiteurs à interagir pleinement avec le contenu.
* La personnalisation peut rendre ces expériences encore plus attrayantes.

**Équipe de développement**

* L’équipe de développement veut une séparation nette entre les aspects liés au contenu et à la présentation.
* Une séparation nette rend le système plus extensible et permet un développement front-end indépendant.

### Comment fonctionne une SPA ? {#how-does-a-spa-work}

L’idée principale sous-jacente à une SPA est que les appels à un serveur et la dépendance envers un serveur sont réduits pour minimiser les retards liés aux appels du serveur, de sorte que la SPA s’approche de la réactivité d’une application native.

Sur une page web séquentielle traditionnelle, seules les données nécessaires à la page immédiate sont chargées. Cela signifie que lorsque vous passez à une autre page, le serveur est appelé pour que les ressources supplémentaires soient mises à disposition. Des appels supplémentaires peuvent s’avérer nécessaires lorsque le visiteur interagit avec les éléments de la page. Ces appels multiples peuvent donner une impression de retard ou de lenteur, car la page doit rattraper les requêtes du visiteur.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Pour offrir une expérience plus fluide, qui s’approche de ce qu’un visiteur attend des applications mobiles natives, une SPA charge toutes les données nécessaires pour le visiteur au premier chargement. Bien que cette opération puisse nécessiter au début un peu plus de temps, elle élimine ensuite la nécessité d’appels supplémentaires au serveur.

Parce que le rendu est effectué côté client, les éléments de la page réagissent plus rapidement et les interactions du visiteur avec la page sont immédiates. Toutes les données supplémentaires qui peuvent être nécessaires sont appelées de manière asynchrone afin d’optimiser la vitesse de la page.

>[!NOTE]
>
>Pour plus d’informations sur le fonctionnement des SPA dans AEM, reportez-vous à l’article [Prise en main des SPA dans AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Pour observer de plus près la conception, l’architecture et le workflow technique de l’éditeur de SPA, consultez l’article [Aperçu de l’éditeur de SPA](/help/sites-developing/spa-overview.md). 

## Expérience de modification de contenu avec une SPA {#content-editing-experience-with-spa}

Lorsqu’une SPA est créée pour exploiter l’éditeur de SPA d’AEM, le créateur ou la créatrice de contenu ne remarque aucune différence lors de la modification et de la création de contenu. Des fonctionnalités AEM communes sont disponibles et aucune modification du workflow du créateur n’est requise.

1. Modifiez l’application de projet SPA WKND dans AEM.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Étape 1](assets/spa-walkthrough-step-1.png)

1. Sélectionnez un composant d’en-tête et notez qu’une barre d’outils s’affiche comme pour tout autre composant. Sélectionnez **Modifier**.

   ![Étape 2](assets/spa-walkthrough-step-2.png)

1. Modifiez le contenu comme d’habitude dans AEM. Les modifications sont conservées.

   ![Étape 3](assets/spa-walkthrough-step-3.png)

   >[!NOTE]
   >
   >Consultez la section [Aperçu de l’éditeur de SPA](spa-overview.md#requirements-limitations) pour plus d’informations sur l’éditeur de texte et les SPA en place.

1. Utilisez l’explorateur de ressources pour faire glisser et déposer une nouvelle image dans un composant d’image.

   ![Étape 4](assets/spa-walkthrough-step-4.png)

1. La modification est conservée.

   ![Étape 5](assets/spa-walkthrough-step-5.png)

D’autres outils de création, tels que le glisser-déposer de composants supplémentaires sur la page, la réorganisation des composants et la modification de la disposition, sont pris en charge comme dans toute application autre que SPA.

>[!NOTE]
>
>L’éditeur de SPA ne modifie pas le modèle DOM de l’application. La SPA elle-même est responsable du DOM.
>
>Pour découvrir le fonctionnement de cet aspect, passez à la section suivante de cet article, [Applications SPA et éditeur de SPA AEM](#spa-apps-and-the-aem-spa-editor).

## Applications SPA et éditeur de SPA AEM {#spa-apps-and-the-aem-spa-editor}

Expérimenter le comportement d’une SPA pour l’utilisateur final puis inspecter la page SPA permet de mieux comprendre le fonctionnement d’une SPA avec l’éditeur de SPA dans AEM.

### Utilisation d’une SPA {#using-an-spa-application}

1. Chargez l’application de projet SPA WKND sur le serveur de publication ou à l’aide de l’option **Afficher comme publié(e)** du menu **Informations sur la page** de l’éditeur de page.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Étape 1](assets/spa-walkthrough-step-1-1.png)

   Notez la structure des pages, notamment la navigation vers les pages enfants, le widget Météo et les articles.

1. Accédez à une page enfant à l’aide du menu et observez que la page se charge immédiatement sans qu’il faille procéder à une actualisation.

   ![Étape 2](assets/spa-walkthrough-step-1-2.png)

1. Ouvrez les outils de développement intégrés de votre navigateur et surveillez l’activité du réseau lorsque vous naviguez sur les pages enfants.

   ![Étape 3](assets/spa-walkthrough-step-1-3.png)

   Le trafic est très faible, car vous passez d’une page à l’autre dans l’application. La page n’est pas rechargée et seules les nouvelles images sont demandées.

   La SPA gère le contenu et le routage entièrement du côté client.

Aussi, si la page n’est pas rechargée lors de la navigation sur les pages enfants, comment est-elle chargée ?

La section suivante, [Chargement d’une application SPA](#loading-an-spa-application), examine de plus près la procédure de chargement de la SPA et indique comment le contenu peut être chargé de façon synchrone et asynchrone.

### Chargement d’une SPA {#loading-an-spa-application}

1. Si ce n’est pas déjà fait, chargez l’application du projet de la SPA WKND sur le serveur de publication ou à l’aide de l’option **Afficher comme publié(e)** du menu **Informations sur la page** de l’éditeur de page.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Étape 1](assets/spa-walkthrough-step-1-1.png)

1. Utilisez l’outil intégré de votre navigateur pour afficher la source de la page.
1. Le contenu de la source est extrêmement limité.

   * Le corps de la page ne renferme aucun contenu. La page est principalement composée de feuilles de styles et d’un appel à divers scripts tels que `clientlib-react.min.js`.
   * Ces scripts sont les pilotes principaux de cette application et sont responsables du rendu de tout le contenu.

1. Utilisez les outils intégrés de votre navigateur pour inspecter la page. Affichez le contenu du DOM entièrement chargé.

   ![Étape 4](assets/spa-walkthrough-step-1-4.png)

1. Basculez vers l’onglet **Réseau** des outils de développement et chargez à nouveau la page.

   Sans tenir compte des requêtes d’image, notez que les principales ressources de la page qui sont chargées sont la page elle-même, le code CSS, le code JavaScript React, ses dépendances, ainsi que les données JSON de la page.

   ![Étape 5](assets/spa-walkthrough-step-1-5.png)

1. Chargez `react.model.json` dans un nouvel onglet.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![Étape 6](assets/spa-walkthrough-step-1-6.png)

   L’éditeur de SPA AEM exploite [AEM Content Services](/help/assets/content-fragments/content-fragments.md) pour diffuser l’intégralité du contenu de la page sous la forme d’un modèle JSON.

   En implémentant des interfaces spécifiques, les modèles Sling fournissent les informations nécessaires à la SPA. La diffusion des données JSON est déléguée vers le bas à chaque composant (de la page, au paragraphe, au composant, etc).

   Chaque composant choisit les données qu’il expose et le mode de rendu de ces données (côté serveur avec HTL ou côté client avec React). Cet article porte sur le rendu côté client avec React.

1. Le modèle peut également regrouper les pages afin qu’elles soient chargées de manière synchrone, ce qui réduit le nombre de rechargements de page nécessaires.

   Dans l’exemple de l’application du projet du SPA WKND, les pages `home`, `page-1`, `page-2` et `page-3` sont chargées de manière synchrone, car les visiteurs visitent généralement toutes ces pages.

   Ce comportement n’est pas obligatoire et est entièrement définissable.

   ![Étape 7](assets/spa-walkthrough-step-1-7.png)

1. Pour voir cette différence de comportement, chargez à nouveau la page et effacez l’activité de réseau des outils de développement. Accédez à la `page-1` dans le menu de page et vérifiez que la seule activité de réseau est une requête d’image de la `page-1`. La `page-1` elle-même n’a pas besoin de se charger.

   ![Étape 8](assets/spa-walkthrough-step-1-8.png)

### Interaction avec l’éditeur de SPA {#interaction-with-the-spa-editor}

L’exemple d’application de projet SPA WKND montre clairement comment l’application se comporte et est chargée lorsqu’elle est publiée, en exploitant les services de contenu pour la diffusion de contenu JSON et le chargement asynchrone des ressources.

De plus, pour le créateur de contenu, la création de contenu à l’aide d’un éditeur de SPA est transparente dans AEM.

Dans la section suivante, nous allons examiner le contrat qui permet à l’éditeur de SPA de relier les composants de la SPA aux composants d’AEM et d’offrir cette expérience de modification transparente.

1. Chargez l’application de projet SPA WKND dans l’éditeur et passez en mode **Aperçu**.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. À l’aide des outils de développement intégrés de votre navigateur, inspectez le contenu de la page. À l’aide de l’outil de sélection, sélectionnez un composant modifiable sur la page et affichez le détail de l’élément.

   Le composant possède un nouvel attribut de données `data-cq-data-path`.

   ![Étape 2](assets/spa-walkthrough-step-2-2.png)

   Par exemple :

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Ce chemin d’accès permet de récupérer et d’associer l’objet de configuration de contexte de modification de chaque composant.

   Il s’agit du seul attribut de balisage nécessaire à l’éditeur pour reconnaître ce composant comme un composant modifiable dans la SPA. En fonction de cet attribut, l’éditeur de SPA détermine quelle configuration modifiable est associée au composant, de sorte que le bon cadre, la bonne barre d’outils etc., soient chargés.

   Certains noms de classe spécifiques sont également ajoutés en vue de marquer les espaces réservés, ainsi que pour la fonctionnalité de glisser-déposer des ressources.

   >[!NOTE]
   >
   >Ce comportement diffère de celui des pages générées côté serveur dans AEM, où un élément `cq` est inséré pour chaque composant modifiable.
   >
   >
   >Cette approche dans la SPA élimine la nécessité d’injecter des éléments personnalisés, en n’utilisant qu’un attribut de données supplémentaire, ce qui rend le balisage plus simple pour l’équipe de développement front-end.

## Étapes suivantes {#next-steps}

Maintenant que vous comprenez l’expérience de modification de SPA dans AEM et que vous savez comment une SPA est liée à l’éditeur de SPA, nous allons examiner de plus près la conception des SPA.

* La section [Prise en main des SPA dans AEM](/help/sites-developing/spa-getting-started-react.md) montre comment une SPA de base est créée pour fonctionner avec l’éditeur de SPA dans AEM.
* La section [Présentation de l’éditeur de SPA](/help/sites-developing/spa-overview.md) examine de plus près le modèle de communication entre AEM et la SPA.
* La section [Développement de SPA pour AEM](/help/sites-developing/spa-architecture.md) décrit comment impliquer les développeurs et développeuses front-end dans le développement d’une SPA pour AEM et décrit de quelle manière les SPA interagissent avec l’architecture d’AEM.

