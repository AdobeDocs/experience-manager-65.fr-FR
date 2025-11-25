---
title: Content Insight
description: Content Insight fournit des informations sur les performances des pages à l’aide de l’analyse Web et des recommandations d’optimisation pour les moteurs de recherche.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 100%

---

# Content Insight{#content-insight}

Content Insight fournit des informations sur les performances des pages à l’aide de l’analyse web et des recommandations SEO. Utilisez Content Insight pour prendre des décisions sur la modification des pages ou pour découvrir comment les modifications précédentes ont modifié les performances. Pour chaque page que vous créez, vous pouvez ouvrir Content Insight afin d’analyser la page.

![chlimage_1-311](assets/chlimage_1-311.png)

La disposition de la page Content Insight s’adapte à la dimension et à l’orientation de l’écran de l’appareil que vous utilisez.

## Données de rapport

La page Content Insight comprend des rapports qui utilisent les données Adobe SiteCatalyst, Adobe Target, Adobe Social et BrightEdge :

* SiteCatalyst : des rapports pour les mesures suivantes sont disponibles :

   * Pages vues
   * Durée de consultation moyenne de la page
   * Sources

* Target : rapport sur l’activité de campagne pour laquelle votre page contient des offres.
* BrightEdge : émet des rapports sur les fonctionnalités de la page qui améliorent sa visibilité pour les moteurs de recherche et recommande des fonctionnalités à implémenter.

Reportez-vous à [Ouverture de l’analyse et des recommandations concernant une page](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Période de reporting

Les rapports présentent les données pour une période que vous contrôlez. Lorsque vous ajustez la période de reporting, les rapports sont automatiquement actualisés avec les données de cette période. Des repères visuels indiquent le moment où les versions de page ont changé, de sorte que vous pouvez comparer les performances de chaque version.

>[!NOTE]
>
>Le journal du tableau de bord Content Insight se trouve dans `GMT`.

Vous pouvez également spécifier la granularité des données des rapports. Par exemple, vous pouvez afficher les données quotidiennes, hebdomadaires, mensuelles ou annuelles.

Voir [Modifier la période de reporting](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>Les rapports Content Insights nécessitent que votre administrateur ait intégré AEM à SiteCatalyst, Target et BrightEdge. Reportez-vous à [Intégration avec SightCatalyst](/help/sites-administering/adobeanalytics.md), [Intégration avec Adobe Target](/help/sites-administering/target.md) et [Intégration avec BrightEdge](/help/sites-administering/brightedge.md).

## Rapport de vues {#the-views-report}

Le rapport de vues comprend les fonctionnalités suivantes pour évaluer le trafic de pages :

* Nombre total de vues pour une page pendant la période de reporting.
* Graphe montrant le nombre de vues sur la période de reporting :

   * Nombre total de vues.
   * Visiteurs ou visiteuses uniques.

![chlimage_1-312](assets/chlimage_1-312.png)

## Rapport de l’engagement moyen des pages {#the-page-average-engaged-report}

Le rapport de l’engagement moyen des pages comprend les fonctionnalités suivantes pour évaluer l’efficacité des pages :

* Durée moyenne pendant laquelle la page reste ouverte sur l’ensemble de la période de reporting.
* Graphe montrant la durée moyenne d’une page vue pendant la période de reporting.

![chlimage_1-313](assets/chlimage_1-313.png)

## Rapport Sources {#the-sources-report}

Le rapport Sources indique comment les utilisateurs et utilisatrices ont accédé à la page, par exemple, à partir des résultats du moteur de recherche ou à l’aide de l’URL connue.

![chlimage_1-314](assets/chlimage_1-314.png)

## Rapport Rebonds {#the-bounces-report}

Le rapport Rebonds comprend un graphe qui indique le nombre de rebonds qui se sont produits pour une page au cours de la période de reporting sélectionnée.

![chlimage_1-315](assets/chlimage_1-315.png)

## Rapport d’activité de la campagne {#the-campaign-activity-report}

Pour chaque campagne pour laquelle la page est active, un rapport s’affiche nommé Activité *Nom de la campagne*. Le rapport affiche les impressions et les conversions de page pour chaque segment pour lequel une offre est fournie.

![chlimage_1-316](assets/chlimage_1-316.png)

## Rapport de recommendations SEO {#the-seo-recommendations-report}

Le rapport de recommendations SEO contient les résultats de l’analyse BrightEdge pour la page. Le rapport est une liste de contrôle des fonctionnalités de page qui indique quelles fonctionnalités la page inclut ou n’inclut pas pour optimiser la recherche à l’aide des moteurs de recherche.

Le rapport permet de créer des tâches afin d’améliorer la recherche des pages. Les recommandations indiquent que des tâches ont été créées pour la mise en œuvre de la recommandation. Voir [Attribution de tâches pour les recommandations SEO](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
