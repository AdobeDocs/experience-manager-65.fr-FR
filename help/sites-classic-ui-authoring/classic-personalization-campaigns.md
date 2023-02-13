---
title: Gestion de campagnes
seo-title: Campaign Management
description: La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs et visiteuses. Cela vous permet également d’orchestrer vos campagnes marketing sur les services de messagerie, web et mobiles, et ainsi de faire participer vos visiteurs.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '628'
ht-degree: 100%

---

# Gestion de campagnes{#campaign-management}

La gestion des campagnes offre aux spécialistes du marketing numérique la possibilité de diffuser du contenu personnalisé et de créer ainsi des expériences dédiées pour les visiteurs.

Cela vous permet également d’orchestrer vos campagnes marketing sur les services de messagerie, web et mobiles, et ainsi de faire participer vos visiteurs. Vous pouvez créer du contenu, segmenter les visiteurs, diffuser et promouvoir du contenu ciblé pour des profils d’utilisateurs spécifiques et gérer des campagnes sur plusieurs canaux.

Ce document décrit les différents éléments qui composent les campagnes. Vous trouverez des informations plus détaillées dans les documents suivants :

* [Teasers et stratégies](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing par e-mail](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Pages d’entrée](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Offres Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Utilisation de Marketing Campaign Manager](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Compréhension de la segmentation](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuration d’une campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La gestion de campagnes comprend plusieurs éléments :

* **Marques**
Dans AEM, les marques constituent l’unité de niveau supérieur et forment un ensemble de 
**Campagnes**.

* **Campagnes**
Une campagne est un ensemble d’ 
**Expériences** individuelles.

* **Expériences**
Le contenu ciblé constitue les différentes expériences présentées au visiteur au niveau des 
**Points de contact**. Plusieurs types d’expérience sont disponibles :

   * **Teasers**
      [Les paragraphes / pages de teaser](#teasers) sont utilisés pour diriger des **Segments** de visiteurs spécifiques vers le contenu qui est centré sur leurs intérêts.

      Les pages de teaser peuvent :

      * proposer au visiteur un éventail d’options,
      * n’afficher qu’un seul paragraphe de teaser basé sur le segment de visiteurs spécifique ; le paragraphe de teaser peut, par exemple, dépendre de l’âge du visiteur.

      Typiquement, une page de teaser est une action temporaire qui dure pour une période spécifique, jusqu’à son remplacement par la page de teaser suivante.

   * **Newsletters**

      [Les communications par e-mail](#emailmarketing) sont utilisées pour inciter les utilisateurs à visiter votre site Web. Elles se présentent généralement sous la forme d’une newsletter, envoyée à vos **Leads** (lesquelles sont habituellement regroupées dans des **Listes**). **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.  Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md). 

   * **Adobe Target**

      Cette expérience permet une intégration à Adobe Target (connu auparavant sous le nom de Test&amp;Target). Elle met à la disposition des spécialistes du marketing un outil d’optimisation de site Web de conversion disposant des fonctionnalités nécessaires pour adapter continuellement leur contenu et leurs offres en ligne à leurs clients, pour des taux de conversion supérieurs. Adobe Target s’accompagne d’une interface intuitive permettant de concevoir et d’exécuter des tests, de créer des segments d’audience et de cibler du contenu, le tout à partir d’une seule et même application.


* **Points de contact**

   Il s’agit des points de contact entre le visiteur et votre campagne. Les points de contact sont connectés aux expériences que vous avez créées.

   Dans le cas des teasers, par exemple, il s’agit de la page de contenu où est situé le paragraphe du teaser, tandis que, pour une newsletter, il s’agit de la liste de distribution.

* **Prospects**

   Les informations que vous avez recueillies sur vos visiteurs et la manière de les contacter constituent la base de vos prospects. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

    Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM](/help/sites-administering/campaign.md).

* **Listes**

   Les prospects sont généralement regroupées dans des listes, de sorte que vous puissiez les soumettre à une action collective. **Remarque :** Adobe ne prévoit pas d’améliorer davantage cette fonctionnalité.

   Il est conseillé d’[utiliser Adobe Campaign et l’intégration à AEM.](/help/sites-administering/campaign.md)

* **Segments**

   Les visiteurs de site se rendent sur un site en fonction d’intérêts et d’objectifs divers. L’analyse de ces informations selon des facteurs tels que les activités sur le site Web, les informations de profil enregistrées et les activités sur d’autres sites Web vous aide à définir des segments. Le contenu peut cibler les besoins et centres d’intérêts spécifiques des visiteurs en fonction du ou des segments correspondants.

* **MCM**

   Marketing Campaign Manager (MCM) est une console qui vous permet d’accéder à toutes les fonctionnalités dont vous avez besoin pour créer et contrôler vos campagnes, marques, expériences, points de contact, pistes, listes, segments et rapports.

   Cette console est accessible à partir de divers emplacements (étiquetés **Campagnes**) ou via l’URL suivante :

   `http://localhost:4502/libs/mcm/content/admin.html`
