---
title: Présentation et présentation des applications monopages
seo-title: Présentation et présentation des applications monopages
description: Cet article présente les concepts d’une application d’une seule page et décrit l’utilisation d’une application d’une seule page pour la création, en montrant comment elle se rapporte à l’éditeur d’une seule page d’une application d’une seule page.
seo-description: Cet article présente les concepts d’une application d’une seule page et décrit l’utilisation d’une application d’une seule page pour la création, en montrant comment elle se rapporte à l’éditeur d’une seule page d’une application d’une seule page.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 3d9bcc706a1fa7a15d0ce8729f7b85c4226b394f

---


# Présentation et présentation des applications monopages{#spa-introduction-and-walkthrough}

Les applications d’une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

L’éditeur de SPA constitue une solution complète pour la prise en charge des SPA dans AEM. Cet article décrit l’utilisation d’une application d’application d’une seule page pour la création et explique en quoi elle est liée à l’éditeur d’applications d’une seule page.

>[!NOTE]
>
>L’éditeur d’application d’une seule page est la solution recommandée pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

### Objectif de l&#39;article {#article-objective}

Cet article présente les concepts de base des applications monopages (SPA) avant de guider le lecteur dans une présentation de l’éditeur d’applications monopages (SPA) à l’aide d’une simple application d’applications monopages (SPA) pour démontrer l’édition de contenu de base. Il détaille ensuite la construction de la page et la manière dont l’application SPA se rapporte à l’éditeur SPA AEM et interagit avec lui.

L’objectif de cette introduction et de cette présentation est de montrer à un développeur AEM pourquoi les applications monopages sont pertinentes, comment elles fonctionnent généralement, comment une application monopage est gérée par l’éditeur d’applications monopages AEM et en quoi elles sont différentes d’une application AEM standard.

La présentation repose sur la fonctionnalité standard d’AEM et l’exemple d’application de We.Retail. Les conditions suivantes doivent être remplies :

* [AEM version 6.4 avec Service Pack 2 ou version ultérieure
   ](/help/release-notes/sp-release-notes.md)
* [Installez l&#39;exemple d&#39;application de We.Retail disponible sur GitHub ici.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

### Qu&#39;est-ce qu&#39;un SPA ? {#what-is-a-spa}

Une application d’une seule page (SPA) diffère d’une page conventionnelle en ce qu’elle est rendue côté client et qu’elle est principalement pilotée par Javascript, en utilisant les appels Ajax pour charger les données et mettre à jour dynamiquement la page. La plupart ou l’ensemble du contenu est récupéré une fois au chargement d’une seule page avec des ressources supplémentaires chargées de manière asynchrone, selon les besoins, en fonction de l’interaction de l’utilisateur avec la page.

Cela réduit le besoin d’actualisation des pages et offre à l’utilisateur une expérience fluide, rapide et qui ressemble davantage à une expérience d’application native.

L’éditeur d’applications monopages AEM permet aux développeurs frontaux de créer des applications monopages qui peuvent être intégrées à un site AEM, ce qui permet aux auteurs de contenu de modifier le contenu des applications monopages aussi facilement que tout autre contenu AEM.

### Pourquoi un SPA ? {#why-a-spa}

En étant plus rapide, fluide et ressemblant davantage à une application native, une application SPA devient une expérience très attrayante non seulement pour le de la page Web, mais aussi pour les marketeurs et les développeurs en raison de la nature du fonctionnement des applications SPA.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visiteurs**

* Les souhaitent des expériences de type natif lorsqu’ils interagissent avec le contenu.
* Il existe des données claires indiquant que plus une page est rapide, plus une conversion est probable.

**Marqueurs**

* Les marketeurs veulent  des expériences riches et originales de type pour inciter les à s&#39;engager pleinement dans le contenu.
* La personnalisation peut rendre ces expériences encore plus attrayantes.

**Développeurs**

* Les développeurs veulent une séparation nette des préoccupations entre le contenu et la présentation.
* Une séparation nette rend le système plus extensible et permet un développement frontal indépendant.

### Comment fonctionne un SPA ? {#how-does-a-spa-work}

L’idée principale d’une application d’une seule page est que les appels et la dépendance sur un serveur sont réduits afin de minimiser les retards causés par les appels au serveur, de sorte que l’application d’une seule page d’une application native puisse répondre.

Dans une page Web séquentielle traditionnelle, seules les données nécessaires à la page immédiate sont chargées. Cela signifie que lorsque le passe à une autre page, le serveur est appelé pour les ressources supplémentaires. Des appels supplémentaires peuvent être nécessaires lorsque le interagit avec les éléments de la page. Ces appels multiples peuvent donner une impression de retard ou de retard car la page doit rattraper les demandes de  du.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Pour une expérience plus fluide, qui approche ce qu’un attend des applications mobiles natives, une application d’application d’application d’application d’application d’application (SPA) charge toutes les données nécessaires pour le au premier chargement. Bien que cela puisse prendre un peu plus de temps au départ, cela élimine ensuite la nécessité d’appels serveur supplémentaires.

En effectuant le rendu côté client, l’élément de page réagit plus rapidement et les interactions avec la page par le sont immédiates. Toute donnée supplémentaire qui peut être nécessaire est appelée de manière asynchrone pour optimiser la vitesse de la page.

>[!NOTE]
>
>Pour plus d’informations techniques sur le fonctionnement des applications monopages dans AEM, reportez-vous à l’article [Prise en main des applications monopages dans AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Pour en savoir plus sur la conception, l’architecture et le processus technique de l’éditeur d’applications monopages, consultez l’article Présentation [de l’éditeur d’applications](/help/sites-developing/spa-overview.md)monopages.

## Modification du contenu avec l’application d’une seule page {#content-editing-experience-with-spa}

Lorsqu’une application d’une seule page est créée pour tirer parti de l’éditeur d’application d’une seule page, l’auteur du contenu ne remarque aucune différence lors de la modification et de la création de contenu. La fonctionnalité commune d’AEM est disponible et aucune modification du flux de travail de l’auteur n’est requise.

>[!NOTE]
>
>La présentation repose sur la fonctionnalité standard d’AEM et l’exemple d’application de We.Retail. Les conditions suivantes doivent être remplies :
>
>* [AEM version 6.4 avec Service Pack 2](/help/release-notes/sp-release-notes.md)
>* [Installez l&#39;exemple d&#39;application de We.Retail disponible sur GitHub ici.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. Modifiez l’application de  Web.Retail dans AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Sélectionnez un composant d’en-tête et notez qu’une barre d’outils s’affiche comme pour tout autre composant. Sélectionnez **Modifier**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Modifiez le contenu normalement dans AEM et notez que les modifications sont conservées.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >Pour plus d’informations sur l’éditeur de texte en place et les applications monopages, consultez la Présentation [de l’éditeur d’](spa-overview.md#requirements-limitations) application d’une seule page.

1. Utilisez l’explorateur de ressources pour faire glisser une nouvelle image dans un composant d’image.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. Le changement est persistant.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

D’autres outils de création, tels que le glisser-déposer de composants supplémentaires sur la page, la réorganisation des composants et la modification de la mise en page, sont pris en charge, comme dans toute application autre que SPA.

>[!NOTE]
>
>L’éditeur d’applications monopages ne modifie pas le DOM de l’application. L&#39;APS lui-même est responsable du DOM.
>
>Pour voir comment cela fonctionne, passez à la section suivante de cet article Applications [d’application d’une seule page et à l’éditeur](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)d’application d’une seule page.

## Applications SPA et éditeur d’application d’une seule page {#spa-apps-and-the-aem-spa-editor}

L’expérience d’une application d’une seule page permet de mieux comprendre le comportement d’une application SAP avec l’éditeur d’une application d’une seule page dans AEM.

### Utilisation d’une application SPA {#using-an-spa-application}

1. Chargez l’application  Web.Retail sur le serveur de publication ou en utilisant l’option **Publié** dans le menu Informations **sur la** page de l’éditeur de page.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Notez la structure des pages, y compris la navigation vers les pages enfants, le widget météorologique et les articles.

1. Accédez à une page enfant à l’aide du menu et constatez que la page se charge immédiatement sans qu’il faille procéder à une actualisation.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Ouvrez les outils de développement intégrés de votre navigateur et surveillez les réseau   lorsque vous parcourez les pages enfants.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Le trafic est très faible lorsque vous passez d’une page à l’autre dans l’application. La page n’est pas rechargée et seules les nouvelles images sont demandées.

   L’application d’une seule page gère le contenu et les  entièrement côté client.

Si la page n’est pas rechargée lors de la navigation dans les pages enfants, comment est-elle chargée ?

La section suivante, [Chargement d’une application](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)d’application d’application d’une seule page, approfondit la procédure de chargement de l’application d’une seule page et explique comment le contenu peut être chargé de manière synchrone et asynchrone.

### Chargement d’une application SPA {#loading-an-spa-application}

1. Si ce n’est pas déjà fait, chargez l’application de We.Retail sur le serveur de publication ou utilisez l’option **as Published** du menu Informations **sur la** page dans l’éditeur de page.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilisez l’outil intégré de votre navigateur pour  la source de la page.
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

   La page ne comporte aucun contenu dans son corps. Il est principalement composé de feuilles de style et d’un appel à un script React `we-retail-journal-react.js`.

   Ce script React est le principal pilote de cette application et est responsable du rendu de tout le contenu.

1. Utilisez les outils intégrés de votre navigateur pour inspecter la page. Voir le contenu du DOM entièrement chargé.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Accédez à l’onglet Réseau de l’Inspecteur et rechargez la page.

   Ignorant les demandes d’image, notez que les ressources principales chargées pour la page sont la page elle-même, le fichier CSS, le code JavaScript de réaction, ses dépendances et les données JSON de la page.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Chargez le `react.model.json` dans un nouvel onglet.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   L’éditeur d’applications monopages AEM tire parti d’ [AEM Content Services](/help/assets/content-fragments.md) pour diffuser l’intégralité du contenu de la page sous forme de modèle JSON.

   En implémentant des interfaces spécifiques, les modèles Sling fournissent les informations nécessaires à l’application d’une seule page. Le  des données JSON est délégué vers le bas à chaque composant (de la page, au paragraphe, au composant, etc.).

   Chaque composant choisit ce qu’il expose et la manière dont il est rendu (côté serveur avec HTL ou côté client avec React). Bien sûr, cet article se concentre sur le rendu côté client avec React.

1. Le modèle peut également regrouper les pages afin qu’elles soient chargées de manière synchrone, ce qui réduit le nombre de rechargements de page nécessaires.

   Dans l&#39;exemple de We.Retail, les pages `home`, `blog`et `aboutus` sont chargées de manière synchrone, car les visitent généralement toutes ces pages. Toutefois, la `weather` page est chargée de manière asynchrone, car les sont moins susceptibles de la consulter.

   Ce comportement n’est pas obligatoire et est entièrement définissable.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Pour  cette différence de comportement, rechargez la page et effacez l&#39; réseau de l&#39;inspecteur. Accédez au blog et aux pages qui nous concernent dans le menu de la page et voyez qu&#39;il n&#39;y a aucun réseau  signalé.

   Accédez à la page météo et voyez que l’ `weather.model.json` appel est asynchrone.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interaction avec l’éditeur d’applications monopages {#interaction-with-the-spa-editor}

En utilisant l’exemple d’application de We.Retail, il est clair comment l’application se comporte et est chargée lorsqu’elle est publiée, en exploitant les services de contenu pour le de contenu JSON  ainsi que le chargement asynchrone des ressources.

De plus, pour l’auteur du contenu, la création de contenu à l’aide d’un éditeur d’application d’une seule page est transparente dans AEM.

Dans la section suivante, nous allons explorer le contrat qui permet à l’éditeur d’application d’une seule page d’établir des relations entre les composants de l’application d’une seule page et les composants d’AEM et d’obtenir cette expérience de modification transparente.

1. Chargez l’application de We.Retail dans l’éditeur et passez en mode de **** .

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. A l’aide des outils de développement intégrés de votre navigateur, inspectez le contenu de la page. A l’aide de l’outil de sélection, sélectionnez un composant modifiable sur la page et les détails de l’élément.

   Notez que le composant possède un nouvel attribut de données `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Par exemple

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Ces chemins permettent de récupérer et d’associer l’objet de configuration de contexte de modification de chaque composant.

   Il s’agit du seul attribut de balisage requis par l’éditeur pour reconnaître qu’il s’agit d’un composant modifiable dans l’application d’une seule page d’une seule page. En fonction de cet attribut, l’éditeur d’application d’une seule page détermine la configuration modifiable associée au composant, de sorte que le cadre, la barre d’outils, etc. appropriés soient définis. est chargée.

   Certains noms de classe spécifiques sont également ajoutés pour le marquage des espaces réservés et pour la fonctionnalité de glisser-déposer des ressources.

   >[!NOTE]
   >
   >Il s’agit d’un changement de comportement par rapport aux pages générées côté serveur dans AEM, où un `cq` élément est inséré pour chaque composant modifiable.
   >
   >
   >Cette approche dans l’application d’une seule page permet de supprimer la nécessité d’injecter des éléments personnalisés, en ne comptant que sur un attribut de données supplémentaire, ce qui simplifie le balisage pour le développeur frontal.

## Étapes suivantes {#next-steps}

Maintenant que vous connaissez l’expérience de modification des applications monopages dans AEM et la relation entre une application monopage et l’éditeur d’applications monopages, approfondissez votre compréhension de la création d’une application monoposte.

* [Prise en main des applications monopages dans AEM](/help/sites-developing/spa-getting-started-react.md) montre comment une application monopage de base est créée pour fonctionner avec l’éditeur d’applications monopages dans AEM
* [Présentation](/help/sites-developing/spa-overview.md) de l’éditeur d’applications monopages (SPA Editor) approfondit le modèle de communication entre AEM et l’application d’une seule page.
* [Le développement d’applications monopages pour AEM](/help/sites-developing/spa-architecture.md) explique comment impliquer les développeurs frontaux dans le développement d’une application monopage pour AEM et comment les applications monopages interagissent avec l’architecture d’AEM.
