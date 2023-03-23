---
title: Intégration à Adobe Experience Cloud
description: Découvrez comment intégrer Adobe Experience Manager à Adobe Experience Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 56%

---

# Intégration à Adobe Experience Cloud{#integrating-with-the-adobe-marketing-cloud}

Le [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html), comprend de puissants produits d’analyse web et d’optimisation de site web qui fournissent des données et des informations exploitables en temps réel pour stimuler les initiatives en ligne. Il constitue une plateforme ouverte et intégrée pour l’optimisation des entreprises en ligne. Le cloud est constitué d’applications intégrées permettant de collecter et de libérer la puissance des informations sur les clients afin d’optimiser les efforts d’acquisition, de conversion et de rétention des clients, ainsi que la création et la distribution de contenu.

Avec Adobe Experience Manager (AEM), vous pouvez intégrer facilement les produits Adobe Experience Cloud suivants :

* Adobe Analytics fournit aux marketeurs des données d’analyse web exploitables et en temps réel au sujet des stratégies en ligne et des initiatives marketing.
* Adobe Target donne aux marketeurs la possibilité d’adapter continuellement leur contenu en ligne à leurs clients de manière à accroître le taux de conversion.
* Adobe Dynamic Media Classic automatise la gestion des médias, simplifie la publication web et améliore les expériences web, le tout dans un environnement hébergé.
* Adobe Dynamic Tag Management offre aux marketeurs des outils intuitifs grâce auxquels ils peuvent gérer facilement et rapidement un nombre illimité de balises Adobe et tierces.
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign vous permet de gérer le contenu de diffusion par e-mail directement dans Adobe Experience Manager.

En outre, vous pouvez [intégrer AEM à Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) et à des [services tiers](/help/sites-administering/third-party-services.md).

## Intégration à Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) est la solution leader du secteur qui fournit aux marketeurs un emplacement pour mesurer, analyser et optimiser les données intégrées de toutes les initiatives en ligne à travers plusieurs canaux marketing. Il fournit aux marketeurs des données d’analyse web en temps réel et exploitables au sujet des stratégies numériques et des initiatives marketing. Adobe Analytics permet aux marketeurs d’identifier rapidement les chemins les plus rentables d’un site web, de segmenter le trafic pour repérer les visiteurs web à forte valeur ajoutée, de déterminer où les visiteurs quittent le site et d’identifier les mesures de succès critiques pour les campagnes marketing en ligne.

Vous pouvez utiliser Adobe Analytics pour analyser les données de vos sites.

L’intégration à Adobe Analytics vous permet d’effectuer les opérations suivantes :

* Activer le suivi des utilisateurs d’Adobe Analytics
* Mappez vos modes d’exécution (par exemple, création, publication) à différentes suites de rapports.
* Envoyez les variables ClientContext en tant que variables de conversion ou propriétés de trafic.
* Utilisez des mappages de variables prédéfinis.
* Configurez toutes les sections du site à la fois.
* Suivi des événements personnalisés.

Pour plus d’informations sur l’intégration d’AEM à Analytics, voir [Intégration à Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Vous pouvez également utiliser l’[assistant d’accord préalable](/help/sites-administering/opt-in.md) pour exécuter facilement l’intégration.

## Intégration à Adobe Target {#integrating-with-adobe-target}

[Adobe Target](https://business.adobe.com/products/target/adobe-target.html) est utilisé par les spécialistes marketing pour concevoir et exécuter des tests en ligne, créer des segments ciblés à la volée (en fonction du comportement) et automatiser le ciblage du contenu et les expériences en ligne.

Les besoins des cyberconsommateurs sont aujourd’hui en constante évolution et ils attendent des très nombreux sites et sources de contenus qu’ils leur offrent des contenus pertinents, voire personnalisés. Pour séduire ce public, il est essentiel que les marketeurs identifient rapidement les offres et les contenus pertinents et attrayants pour leurs publics. Forts de ces connaissances, les marketeurs ont besoin de la capacité d’évoluer continuellement leurs sites et de cibler le contenu approprié vers différentes audiences.

[Intégration à Adobe Target](/help/sites-administering/target.md) explique comment intégrer votre site à Target.

Vous pouvez également utiliser l’[assistant d’accord préalable](/help/sites-administering/opt-in.md) pour exécuter facilement l’intégration.

## Souscription à Analytics et Target {#opting-in-to-analytics-and-target}

AEM propose une procédure de souscription simple pour s’intégrer avec Adobe Analytics et Target. Lorsque vous vous connectez en tant qu’administrateur et que vous accédez à la console Projets, un assistant de souscription s’affiche.

![chlimage_1-107](assets/chlimage_1-107a.png)

Souscrivez à l’intégration avec Analytics et/ou Target afin de permettre l’utilisation de leurs fonctionnalités de suivi et d’analyse des pages, ainsi que des fonctionnalités de personnalisation. Lorsque vous souscrivez, fournissez les informations de votre compte utilisateur et spécifiez les pages qui font l’objet d’un suivi.

Pour plus d’informations, voir [Souscription à Adobe Analytics et Adobe Target.](/help/sites-administering/opt-in.md)

## Intégration à Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic est une solution hébergée qui permet de publier, gérer, améliorer et diffuser des ressources marketing dynamiques et de réaliser un marchandisage visuel riche sur le web, les appareils mobiles, les e-mails, les médias sociaux, les écrans connectés à Internet et l’impression.

Dans Adobe Experience Manager, vous pouvez publier des ressources numériques directement d’Adobe Experience Manager vers Dynamic Media Classic et vous pouvez publier des ressources numériques de Dynamic Media Classic vers Adobe Experience Manager.

En outre, vous pouvez afficher les ressources Adobe Experience Manager publiées dans Dynamic Media Classic dans différentes visionneuses telles que le Zoom de base et la Vidéo.

Pour plus d’informations sur l’intégration d’Adobe Experience Manager à Dynamic Media Classic, consultez la [Documentation pour l’intégration à Dynamic Media Classic](/help/sites-administering/scene7.md).

## Intégration à Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) offre aux marketeurs des outils intuitifs grâce auxquels ils peuvent gérer facilement et rapidement un nombre illimité de balises Adobe et de tierces parties. Vous disposez d’un plus grand contrôle et d’une plus grande flexibilité pour optimiser pratiquement n’importe quel élément en ligne, tout en réduisant la dépendance aux ressources informatiques.

[Intégrez la gestion dynamique des balises Adobe](/help/sites-administering/dtm.md) à AEM afin de pouvoir utiliser vos propriétés web de gestion dynamique des balises pour effectuer le suivi des sites AEM.

## Intégration à Adobe Audience Manager {#integrating-with-adobe-audience-manager}

L’intégration d’Audience Manager a été supprimée dans AEM 6.3.

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Intégration à Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) vous permet de gérer le contenu de diffusion par e-mail directement dans Adobe Experience Manager.

Pour plus d’informations sur la façon dont AEM s’intègre à Adobe Campaign, consultez la section [Intégration à Adobe Campaign](/help/sites-administering/campaignstandard.md).