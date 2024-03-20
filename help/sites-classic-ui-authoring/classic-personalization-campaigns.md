---
title: Gestion de campagnes
description: La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses. Cela vous permet d’orchestrer vos campagnes marketing sur le web, par e-mail et sur les services mobiles, et d’impliquer ainsi vos visiteurs et visiteuses.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 100%

---


# Gestion de campagnes{#campaign-management}

La gestion de campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses.

Cela vous permet d’orchestrer vos campagnes marketing sur le web, par e-mail et sur les services mobiles, et d’impliquer ainsi vos visiteurs et visiteuses. Vous pouvez créer du contenu, segmenter les visiteurs et visiteuses, diffuser et promouvoir du contenu ciblé pour des profils spécifiques et gérer des campagnes sur plusieurs canaux.

Ce document décrit les différents éléments qui composent les campagnes. Pour obtenir des informations plus détaillées, consultez les documents suivants :

* [Teasers et stratégies](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing par e-mail](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Pages de destination](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Offres Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Utilisation de Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Compréhension de la segmentation](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuration d’une campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La gestion de campagnes se compose de plusieurs éléments :

* **Marques**
Dans Adobe Experience Manager (AEM), les marques constituent l’unité de niveau supérieur et forment un ensemble de **campagnes**.

* **Campagnes**
Une campagne est un ensemble d’**expériences** individuelles.

* **Expériences**
Le contenu ciblé constitue les différentes expériences présentées au visiteur ou à la visiteuse au niveau des **Touchpoints**.  Plusieurs types d’expériences sont disponibles :

   * **Teasers**
     [Les paragraphes / pages de teaser](#teasers) sont utilisés pour diriger des **Segments** de visiteurs spécifiques vers le contenu qui est centré sur leurs intérêts.

     Les pages de teaser peuvent :

      * présenter une diverses options parmi lesquelles le visiteur ou la visteuse peut effectuer un choix ;
      * n’afficher qu’un seul paragraphe de teaser basé sur un segment de visiteurs et de visiteuses spécifique. Par exemple, le paragraphe de teaser affiché peut dépendre de l’âge du visiteur ou de la visiteuse.

     En règle générale, une page de teaser est une action temporaire qui dure pendant une période spécifique, jusqu’à ce qu’elle soit remplacée par la page de teaser suivante.

   * **Newsletters**

     [Les communications par e-mail](#emailmarketing) sont utilisées pour inciter les utilisateurs à visiter votre site Web. Elles se présentent généralement sous la forme d’une newsletter, envoyée à vos **prospects** (lesquelles sont regroupées dans des **Listes**). **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité. Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Cette expérience permet une intégration à Adobe Target (connu auparavant sous le nom de Test&amp;Target). Elle met à la disposition des spécialistes du marketing un outil d’optimisation de site web de conversion disposant des fonctionnalités nécessaires pour adapter continuellement leur contenu et leurs offres en ligne à leur clientèle, pour des taux de conversion supérieurs. Adobe Target s’accompagne d’une interface intuitive permettant de concevoir et d’exécuter des tests, de créer des segments d’audience et de cibler du contenu, le tout à partir d’une seule et même application.

* **Points de contact**

  Il s’agit des points de contact entre le visiteur ou la visiteuse et votre campagne. Les points de contact sont liés aux expériences que vous avez créées.

  Par exemple, pour les teasers, il s’agit de la page de contenu où se trouve le paragraphe du teaser, tandis que pour une newsletter, il s’agit de la liste de publipostage.

* **Prospects**

  Les informations que vous avez recueillies sur vos visiteurs et la manière de les contacter constituent la base de vos prospects. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

  Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

* **Listes**

  Les prospects sont regroupés dans des listes, de sorte que vous puissiez les soumettre à une action collective. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

  Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

* **Segments**

  Les visiteurs et visiteuses de site se rendent sur un site en fonction de centres d’intérêts et d’objectifs divers. L’analyse de ces données en fonction de facteurs tels que l’activité sur le site web, les informations de profil enregistrées et l’activité sur d’autres sites web vous aide à définir des segments. Le contenu peut alors cibler les besoins et centres d’intérêts des visiteurs et visiteuses en fonction des segments qui leur correspondent.

* **MCM**

  Marketing Campaign Manager (MCM) est une console qui vous permet d’accéder à toutes les fonctionnalités nécessaires pour créer et contrôler vos campagnes, marques, expériences, points de contact, prospects, listes, segments et rapports.

  Elle est accessible à partir de différents emplacements (libellés **Campagnes**, par exemple), ou avec, par exemple, l’URL :

  `http://localhost:4502/libs/mcm/content/admin.html`
