---
title: Gestion de campagnes
seo-title: Campaign Management
description: La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses. Il vous permet d’orchestrer vos campagnes marketing sur le Web, par e-mail et sur les services mobiles, et ainsi d’impliquer vos visiteurs.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: 1ba34f95cf3ce3f136482075802d2e4372f28917
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 36%

---


# Gestion de campagnes{#campaign-management}

La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses.

Il vous permet d’orchestrer vos campagnes marketing sur le Web, par e-mail et sur les services mobiles, et ainsi d’impliquer vos visiteurs. Vous pouvez créer du contenu, segmenter les visiteurs, diffuser et promouvoir du contenu ciblé pour des profils utilisateur spécifiques et gérer des campagnes sur plusieurs canaux.

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
Dans AEM, les marques constituent l’unité de niveau supérieur et forment un ensemble de **Campagnes**.

* **Campagnes**
Une campagne est une collection de **Expériences**.

* **Expériences**
Le contenu ciblé forme les différentes expériences, présentées au visiteur au **Points de contact**. Plusieurs types d’expérience sont disponibles :

   * **Teasers**
     [Les paragraphes / pages de teaser](#teasers) sont utilisés pour diriger des **Segments** de visiteurs spécifiques vers le contenu qui est centré sur leurs intérêts.

     Les pages de teaser peuvent :

      * présenter une gamme d’options parmi lesquelles le visiteur peut effectuer un choix ;
      * n’afficher qu’un seul paragraphe de teaser basé sur un segment de visiteurs spécifique ; par exemple, le paragraphe de teaser affiché peut dépendre de l’âge du visiteur.

     En règle générale, une page de teaser est une action temporaire qui dure pendant une période spécifique, jusqu’à ce qu’elle soit remplacée par la page de teaser suivante.

   * **Bulletins d’information**

     [Les communications par e-mail](#emailmarketing) sont utilisées pour inciter les utilisateurs à visiter votre site Web. Elles se présentent généralement sous la forme d’une newsletter, envoyée à vos **Leads** (lesquelles sont habituellement regroupées dans des **Listes**). **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.  Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md). 

   * **Adobe Target**

     Cela permet l’intégration à Adobe Target (anciennement Test&amp;Target), qui dote les marketeurs d’un outil d’optimisation de site web de conversion disposant des fonctionnalités nécessaires pour adapter continuellement leur contenu et leurs offres en ligne à leurs clients, ce qui leur permet de générer de meilleures conversions. Adobe Target offre une interface intuitive pour concevoir et exécuter des tests, créer des segments d’audience et cibler du contenu à partir d’une seule application.

* **Points de contact**

  Il s’agit des points de contact entre le visiteur et votre campagne. Les points de contact sont liés aux expériences que vous avez créées.

  Par exemple, pour les teasers, il s’agit de la page de contenu où se trouve le paragraphe du teaser, tandis que pour une newsletter, il s’agit de la liste de distribution.

* **Prospects**

  Les informations que vous avez recueillies sur vos visiteurs et la manière de les contacter constituent la base de vos prospects. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

   Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

* **Listes**

  Les prospects sont généralement regroupées dans des listes, de sorte que vous puissiez les soumettre à une action collective. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

  Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM.](/help/sites-administering/campaign.md)

* **Segments**

  Les visiteurs et visiteuses de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. L’analyse de ces données en fonction de facteurs tels que l’activité sur le site web, les informations de profil enregistrées et l’activité sur d’autres sites web vous aide à définir des segments. Le contenu peut ensuite être spécifiquement ciblé sur les besoins et centres d’intérêt du visiteur en fonction du ou des segments correspondants.

* **MCM**

  Marketing Campaign Manager (MCM) est une console qui vous permet d’accéder à toutes les fonctionnalités nécessaires pour créer et contrôler vos campagnes, marques, expériences, points de contact, pistes, listes, segments et rapports.

  Il est accessible à partir de divers emplacements (étiquetés comme **Campagnes**), ou avec, par exemple, l’URL :

  `http://localhost:4502/libs/mcm/content/admin.html`
