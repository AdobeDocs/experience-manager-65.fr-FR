---
title: SPA Introduction et présentation
seo-title: SPA Introduction et présentation
description: Cet article présente les concepts d’un SPA et décrit comment il se rapporte à l’éditeur de l’ sous-jacent en utilisant une application SPA de base pour la création.
seo-description: Cet article présente les concepts d’un SPA et décrit comment il se rapporte à l’éditeur de l’ sous-jacent en utilisant une application SPA de base pour la création.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 3%

---


# SPA Introduction et présentation{#spa-introduction-and-walkthrough}

Les applications d’une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

L’éditeur de SPA constitue une solution complète pour la prise en charge des SPA dans AEM. Cet article décrit l’utilisation d’une application SPA de base pour la création et montre comment elle se rapporte à l’AEM SPA Editor sous-jacent.

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent un rendu côté client SPA structure (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

### Objectif de l&#39;article {#article-objective}

Cet article présente les concepts de base de SPA avant de guider le lecteur dans une présentation de l&#39;éditeur SPA en utilisant une simple application de la SPA pour démontrer les fonctions de base de la modification du contenu. Il détaille ensuite la construction de la page et comment l&#39;application SPA se rapporte et interagit avec l&#39;AEM rédacteur en chef.

L’objectif de cette introduction et de cette présentation est de montrer à un développeur AEM pourquoi SPA est pertinent, comment ils fonctionnent généralement, comment un SPA est géré par l’éditeur d’ et comment il est différent d’une application d’ standard.

La procédure pas à pas est basée sur la fonctionnalité AEM standard et l&#39;exemple d&#39;application de Journal We.Retail. Les exigences suivantes doivent être respectées :

* [aem version 6.4 avec Service Pack 2 ou plus récent](/help/release-notes/sp-release-notes.md)
* [Installez l&#39;exemple d&#39;application de Journal We.Retail disponible sur GitHub ici.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>Ce document utilise l’application [de Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail à des fins de démonstration uniquement. Il ne doit être utilisé pour aucun travail de projet.
>
>Tout projet AEM doit tirer parti de l&#39;archétype [de projet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)AEM, qui prend en charge les projets SPA à l&#39;aide de React ou Angular et qui utilise le SDK .

### Qu&#39;est-ce qu&#39;un SPA ? {#what-is-a-spa}

Une application d’une seule page (SPA) diffère d’une page conventionnelle en ce qu’elle est rendue côté client et qu’elle est principalement pilotée par JavaScript, en utilisant les appels Ajax pour charger les données et mettre à jour dynamiquement la page. La plupart ou la totalité du contenu est récupérée une fois au chargement d’une seule page avec des ressources supplémentaires chargées de manière asynchrone, selon les besoins, en fonction de l’interaction de l’utilisateur avec la page.

Cela réduit la nécessité d’actualiser les pages et offre à l’utilisateur une expérience transparente, rapide et qui ressemble davantage à une expérience d’application native.

L’AEM SPA Editor permet aux développeurs frontaux de créer des SPA qui peuvent être intégrées dans un site , ce qui permet aux auteurs de contenu de modifier le contenu  aussi facilement que tout autre contenu .

### Pourquoi un SPA ? {#why-a-spa}

En étant plus rapide, fluide et plus semblable à une application native, une SPA devient une expérience très attrayante non seulement pour le visiteur de la page Web, mais aussi pour les marketeurs et les développeurs en raison de la nature du SPA fonctionne.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visiteurs**

* Les visiteurs souhaitent des expériences de type natif lorsqu’ils interagissent avec du contenu.
* Il existe des données claires indiquant que plus une page est rapide, plus une conversion est probable.

**Marqueurs**

* Les marketeurs veulent offre des expériences riches et originales pour inciter les visiteurs à s&#39;engager pleinement dans le contenu.
* La personnalisation peut rendre ces expériences encore plus attrayantes.

**Développeurs**

* Les développeurs veulent une séparation nette des préoccupations entre le contenu et la présentation.
* Une séparation nette rend le système plus extensible et permet un développement frontal indépendant.

### Comment fonctionne un SPA ? {#how-does-a-spa-work}

L&#39;idée Principale derrière une SPA est que les appels et la dépendance sur un serveur sont réduits afin de minimiser les retards causés par les appels serveur de sorte que le SPA s&#39;approche de la réactivité d&#39;une application native.

Dans une page Web séquentielle traditionnelle, seules les données nécessaires à la page immédiate sont chargées. Cela signifie que lorsque le visiteur passe à une autre page, le serveur est appelé pour les ressources supplémentaires. Des appels supplémentaires peuvent s’avérer nécessaires lorsque le visiteur interagit avec les éléments de la page. Ces appels multiples peuvent donner une impression de retard ou de retard car la page doit rattraper les demandes du visiteur.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Pour une expérience plus fluide, qui approche ce qu’un visiteur attend des applications mobiles natives, un SPA charge toutes les données nécessaires pour le visiteur au premier chargement. Bien que cette opération puisse prendre un peu plus de temps au début, elle élimine ensuite la nécessité d’appels de serveur supplémentaires.

En effectuant le rendu côté client, l’élément de page réagit plus rapidement et les interactions avec la page par le visiteur sont immédiates. Toute donnée supplémentaire qui peut être nécessaire est appelée de manière asynchrone afin d’optimiser la vitesse de la page.

>[!NOTE]
>
>Pour plus d&#39;informations techniques sur le fonctionnement de SPA en AEM, reportez-vous à l&#39;article [Prise en main de l&#39;SPA en](/help/sites-developing/spa-getting-started-react.md).
>
>Pour un aperçu plus approfondi de la conception, de l’architecture et du processus technique de SPA Editor, consultez l’article [SPA Editor Overview](/help/sites-developing/spa-overview.md)(Présentationde l’éditeur).

## Modification du contenu avec SPA {#content-editing-experience-with-spa}

Lorsqu’un SPA est créé pour tirer parti de l’AEM Éditeur, l’auteur du contenu ne remarque aucune différence lors de la modification et de la création de contenu. Une fonctionnalité AEM commune est disponible et aucune modification du flux de travail de l’auteur n’est requise.

>[!NOTE]
>
>La procédure pas à pas est basée sur la fonctionnalité AEM standard et l&#39;exemple d&#39;application de Journal We.Retail. Les exigences suivantes doivent être respectées :
>
>* [aem version 6.4 avec Service Pack 2](/help/release-notes/sp-release-notes.md)
>* [Installez l&#39;exemple d&#39;application de Journal We.Retail disponible sur GitHub ici.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>



1. Modifiez l&#39;application de Journal We.Retail dans AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Sélectionnez un composant d’en-tête et notez qu’une barre d’outils s’affiche comme pour tout autre composant. Sélectionnez **Modifier**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Modifiez le contenu normalement dans AEM et notez que les modifications sont conservées.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >Pour plus d’informations sur l’éditeur de texte et l’SPA en place, consultez la Présentation [de](spa-overview.md#requirements-limitations) SPA Editor.

1. Utilisez l’explorateur de ressources pour faire glisser une nouvelle image dans un composant d’image.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. Le changement est maintenu.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

D’autres outils de création, tels que le glisser-déposer de composants supplémentaires sur la page, la réorganisation des composants et la modification de la mise en page, sont pris en charge comme dans toute application non SPA.

>[!NOTE]
>
>L’éditeur SPA ne modifie pas le DOM de l’application. Le SPA lui-même est responsable du DOM.
>
>Pour voir comment cela fonctionne, passez à la section suivante de cet article [SPA Applications et l&#39;AEM éditeur](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)SPA.

## SPA Apps et l&#39;AEM-Éditeur {#spa-apps-and-the-aem-spa-editor}

L’expérience d’un SPA se comporte pour l’utilisateur final, puis l’inspection de la page SPA permet de mieux comprendre le fonctionnement d’une application SAP avec l’Éditeur de SPA dans l’.

### Utilisation d’une application SPA {#using-an-spa-application}

1. Chargez l’application de Journal We.Retail sur le serveur de publication ou à l’aide de l’option **Vue as Published** (Publié **) dans le menu Informations** sur lapage de l’éditeur de page.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Notez la structure des pages, y compris la navigation vers les pages enfants, le widget météorologique et les articles.

1. Accédez à une page enfant à l’aide du menu et voyez que la page se charge immédiatement sans qu’il faille procéder à une actualisation.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Ouvrez les outils de développement intégrés à votre navigateur et surveillez l’activité du réseau lorsque vous parcourez les pages enfants.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Il y a très peu de trafic lorsque vous passez d’une page à l’autre dans l’application. La page n’est pas rechargée et seules les nouvelles images sont demandées.

   Le SPA gère le contenu et le routage entièrement du côté client.

Ainsi, si la page n’est pas rechargée lors de la navigation dans les pages enfants, comment est-elle chargée ?

La section suivante, [Chargement d’une application](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)SPA, approfondit la procédure de chargement du SPA et explique comment le contenu peut être chargé de façon synchrone et asynchrone.

### Chargement d’une application SPA {#loading-an-spa-application}

1. Si ce n’est pas déjà fait, chargez l’application de Journal We.Retail sur le serveur de publication ou à l’aide de la **Vue d’options Publié** dans le menu Informations **sur la** page de l’éditeur de page.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilisez l’outil intégré de votre navigateur pour vue la source de la page.
1. Notez que le contenu de la source est extrêmement limité.

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   La page ne comporte aucun contenu dans son corps. Il est principalement composé de feuilles de style et d&#39;un appel à un script React `we-retail-journal-react.js`.

   Ce script React est le Principal pilote de cette application et est responsable du rendu de tout le contenu.

1. Utilisez les outils intégrés de votre navigateur pour inspecter la page. Affichez le contenu du modèle DOM entièrement chargé.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Accédez à l&#39;onglet Réseau de l&#39;Inspecteur et rechargez la page.

   Ignorant les demandes d’image, notez que les Principales ressources chargées pour la page sont la page elle-même, CSS, le code JavaScript de réaction, ses dépendances, ainsi que les données JSON de la page.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Chargez le `react.model.json` dans un nouvel onglet.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   L’AEM SPA Editor utilise [AEM Content Services](/help/assets/content-fragments/content-fragments.md) pour diffuser l’intégralité du contenu de la page sous la forme d’un modèle JSON.

   En implémentant des interfaces spécifiques, les modèles Sling fournissent les informations nécessaires à la SPA. La diffusion des données JSON est déléguée vers le bas à chaque composant (de la page, au paragraphe, au composant, etc.).

   Chaque composant choisit ce qu’il expose et comment il est rendu (côté serveur avec HTL ou côté client avec React). Bien sûr, cet article se concentre sur le rendu côté client avec React.

1. Le modèle peut également regrouper les pages afin qu’elles soient chargées de manière synchrone, ce qui réduit le nombre de rechargements de page nécessaires.

   Dans l&#39;exemple du Journal We.Retail, les pages `home`, `blog`et `aboutus` les pages sont chargées de manière synchrone, car les visiteurs visitent généralement toutes ces pages. Cependant, la `weather` page est chargée de manière asynchrone, car les visiteurs sont moins susceptibles de la consulter.

   Ce comportement n’est pas obligatoire et est entièrement définissable.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Pour vue cette différence de comportement, rechargez la page et effacez l&#39;activité réseau de l&#39;inspecteur. Accédez au blog et aux pages qui nous concernent dans le menu de la page et vérifiez qu&#39;aucune activité réseau n&#39;est signalée.

   Accédez à la page Météo et vérifiez que l’ `weather.model.json` appel est asynchrone.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interaction avec l’éditeur de SPA {#interaction-with-the-spa-editor}

En utilisant l&#39;exemple d&#39;application de Journal We.Retail, vous savez comment se comporte l&#39;application et comment elle est chargée lorsqu&#39;elle est publiée, en exploitant les services de contenu pour la diffusion de contenu JSON ainsi que le chargement asynchrone des ressources.

De plus, pour l’auteur de contenu, la création de contenu à l’aide d’un éditeur de SPA est transparente dans AEM.

Dans la section suivante, nous étudierons le contrat qui permet à SPA Editor de relier les composants du SPA aux composants de l&#39;AEM et de réaliser cette expérience de modification transparente.

1. Chargez l&#39;application de Journal We.Retail dans l&#39;éditeur et passez en mode **Prévisualisation** .

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. A l’aide des outils de développement intégrés à votre navigateur, inspectez le contenu de la page. A l’aide de l’outil de sélection, sélectionnez un composant modifiable sur la page et vue le détail de l’élément.

   Notez que le composant possède un nouvel attribut de données `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Par exemple, 

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Ces chemins permettent de récupérer et d’associer l’objet de configuration de contexte de modification de chaque composant.

   Il s’agit du seul attribut de balisage nécessaire à l’éditeur pour reconnaître ce composant comme un composant modifiable dans le SPA. En fonction de cet attribut, l&#39;éditeur SPA déterminera la configuration modifiable associée au composant, de sorte que le cadre, la barre d&#39;outils, etc. appropriés soient définis. est chargé.

   Certains noms de classe spécifiques sont également ajoutés pour marquer les espaces réservés et pour la fonctionnalité de glisser-déposer des ressources.

   >[!NOTE]
   >
   >Il s’agit d’un changement de comportement des pages générées côté serveur dans AEM, où un `cq` élément est inséré pour chaque composant modifiable.
   >
   >
   >Cette approche dans SPA élimine la nécessité d’injecter des éléments personnalisés, en n’utilisant qu’un attribut de données supplémentaire, ce qui rend le balisage plus simple pour le développeur frontal.

## Étapes suivantes {#next-steps}

Maintenant que vous comprenez l&#39;expérience de SPA montage en AEM et comment un SPA se rapporte à l&#39;éditeur de , plongez-vous plus profondément dans la compréhension de la façon dont un  est construit.

* [Prise en main des SPA dans AEM](/help/sites-developing/spa-getting-started-react.md) montre comment un SPA de base est créé pour fonctionner avec l’éditeur de  dans l’
* [SPA Editor Overview](/help/sites-developing/spa-overview.md) approfondit le modèle de communication entre AEM et la SPA.
* [Le blog Developing SPA for AEM](/help/sites-developing/spa-architecture.md) décrit comment impliquer les développeurs frontaux dans le développement d&#39;un SPA pour les  ainsi que la manière dont les  interagissent avec l&#39;architecture des .
