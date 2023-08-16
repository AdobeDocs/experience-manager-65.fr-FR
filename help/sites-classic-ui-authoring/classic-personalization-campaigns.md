---
title: Gestion de campagnes
description: La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses. Il vous permet d’orchestrer vos campagnes marketing sur le Web, par e-mail et sur les services mobiles, et d’impliquer ainsi vos visiteurs.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 26%

---


# Gestion de campagnes{#campaign-management}

La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses.

Il vous permet d’orchestrer vos campagnes marketing sur le Web, par e-mail et sur les services mobiles, et d’impliquer ainsi vos visiteurs. Vous pouvez créer du contenu, segmenter les visiteurs, diffuser et promouvoir du contenu ciblé pour des profils utilisateur spécifiques et gérer des campagnes sur plusieurs canaux.

Ce document décrit les différents éléments qui composent les campagnes. Des informations plus détaillées sont disponibles dans les documents suivants :

* [Teasers et stratégies](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing par e-mail](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Pages de destination](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Offres Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Utilisation de Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Compréhension de la segmentation](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuration d’une campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La gestion de campagne se compose de plusieurs éléments :

* **Marques**
Dans Adobe Experience Manager (AEM), les marques constituent l’unité de niveau supérieur et forment un ensemble de **Campagnes**.

* **Campagnes**
Une campagne est une collection de **Expériences**.

* **Expériences**
Le contenu ciblé forme les différentes expériences, présentées au visiteur au **Points de contact**. Plusieurs types d’expérience sont disponibles :

   * **Teasers**
     [Les paragraphes / pages de teaser](#teasers) sont utilisés pour diriger des **Segments** de visiteurs spécifiques vers le contenu qui est centré sur leurs intérêts.

     Les pages de teaser peuvent :

      * présenter une gamme d’options parmi lesquelles le visiteur peut effectuer un choix ;
      * n’afficher qu’un seul paragraphe de teaser basé sur un segment de visiteurs spécifique. Par exemple, le paragraphe de teaser affiché peut dépendre de l’âge du visiteur.

     En règle générale, une page de teaser est une action temporaire qui dure pendant une période spécifique, jusqu’à ce qu’elle soit remplacée par la page de teaser suivante.

   * **Bulletins d’information**

     [Les communications par e-mail](#emailmarketing) sont utilisées pour inciter les utilisateurs à visiter votre site Web. Elles prennent généralement la forme d’une newsletter, envoyée à votre **Pistes** (regroupées en **Listes**). **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.  La recommandation est [utiliser Adobe Campaign et l’intégration pour AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Cela permet l’intégration à Adobe Target (anciennement Test&amp;Target), qui dote les marketeurs d’un outil d’optimisation de site web de conversion disposant des fonctionnalités nécessaires pour adapter continuellement leur contenu et leurs offres en ligne à leurs clients, ce qui leur permet de générer de meilleures conversions. Adobe Target offre une interface intuitive pour concevoir et exécuter des tests, créer des segments d’audience et cibler du contenu à partir d’une seule application.

* **Points de contact**

  Il s’agit des points de contact entre le visiteur et votre campagne. Les points de contact sont liés aux expériences que vous avez créées.

  Par exemple, pour les teasers, il s’agit de la page de contenu où se trouve le paragraphe du teaser, tandis que pour une newsletter, il s’agit de la liste de distribution.

* **Prospects**

  Les informations que vous avez recueillies sur vos visiteurs et la manière de les contacter constituent la base de vos prospects. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

  La recommandation est [utiliser Adobe Campaign et l’intégration pour AEM](/help/sites-administering/campaign.md).

* **Listes**

  Les pistes sont regroupées dans des listes afin que vous puissiez agir de manière collective. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

  La recommandation est [utilisez Adobe Campaign et l’intégration pour AEM.](/help/sites-administering/campaign.md)

* **Segments**

  Les visiteurs et visiteuses de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. L’analyse de ces données en fonction de facteurs tels que l’activité sur le site web, les informations de profil enregistrées et l’activité sur d’autres sites web vous aide à définir des segments. Le contenu peut ensuite être ciblé en fonction des besoins et des centres d’intérêt du visiteur en fonction des segments correspondants.

* **MCM**

  Marketing Campaign Manager (MCM) est une console qui vous permet d’accéder à toutes les fonctionnalités nécessaires pour créer et contrôler vos campagnes, marques, expériences, points de contact, pistes, listes, segments et rapports.

  Il est accessible à partir de différents emplacements (étiquetés comme **Campagnes**), ou avec, par exemple, l’URL :

  `http://localhost:4502/libs/mcm/content/admin.html`
