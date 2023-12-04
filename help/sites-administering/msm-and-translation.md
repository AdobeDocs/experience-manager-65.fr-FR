---
title: Administration de sites web
seo-title: Website Administration
description: Découvrez comment gérer des sites web multilingues à l’aide de Adobe Experience Manager.
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 39%

---

# Administration de sites web{#website-administration}

Les outils d’administration suivants sont disponibles pour gérer les sites et les pages web :

* Multi Site Manager (MSM) vous permet d’utiliser le même contenu de site à plusieurs endroits différents, tout en autorisant des variations :

   * [Réutilisation de contenu : Multi-Site Manager et Live Copy](/help/sites-administering/msm.md)

* La traduction permet d’automatiser la traduction du contenu, des ressources et du contenu de la page généré par l’utilisateur afin de créer et de gérer des sites web multilingues :

   * [Traduction de contenu pour les sites multilingues](/help/sites-administering/translation.md)

* Ces deux fonctionnalités peuvent être combinées pour prendre en charge les sites web qui sont tous deux [Multinationale et multilingue](#multinational-and-multilingual-sites).

## Sites internationaux et multilingues {#multinational-and-multilingual-sites}

Vous pouvez créer efficacement du contenu pour les sites internationaux et multilingues par l’utilisation conjointe de Multi Site Manager et du workflow de traduction. Créez un site maître dans une langue, pour un pays spécifique, puis utilisez ce contenu comme base pour les autres sites, en utilisant la traduction si nécessaire :

* [Traduisez](/help/sites-administering/translation.md) le site de gabarit dans différentes langues.

* Utilisez [Multi Site Manager](/help/sites-administering/msm.md) pour effectuer les tâches suivantes :

   * Réutilisez le contenu du site maître et les traductions pour créer des sites pour d’autres pays et cultures.
   * Veillez à limiter l’utilisation de Multi Site Manager au contenu dans une langue, par exemple, le gabarit anglais > branches de langue anglaise dans les sites de pays, le gabarit français > branches de langue française dans les sites de pays.
   * Si nécessaire, désolidarisez des éléments des Live Copies pour ajouter des détails de localisation.

Le diagramme suivant illustre la manière dont les principaux concepts sont en corrélation (mais n’affiche pas tous les niveaux/éléments impliqués) :

![Diagramme présentant les principaux concepts de MSM et de traduction](assets/chlimage_1-71a.png)

>[!NOTE]
>
>Dans ces scénarios et dans d’autres scénarios comparables, MSM ne gère pas les différentes versions de langues en tant que telles.
>
>* [MSM](/help/sites-administering/msm.md) gère le déploiement du contenu traduit d’un plan directeur (par exemple, un gabarit global) vers les Live Copies (par exemple, les sites locaux), dans les limites d’une langue.
>* La variable [translation](/help/sites-administering/translation.md) les fonctionnalités d’intégration d’AEM, en association avec des services de gestion de traduction tiers, gèrent les langues et la traduction de contenu dans ces différentes langues.
>
>Pour les cas d’utilisation plus avancés, MSM peut également être utilisé dans les gabarits de langue.

>[!NOTE]
>
>Dans tous les cas, il est recommandé de lire les bonnes pratiques suivantes :
>
>* [Bonnes pratiques pour MSM](/help/sites-administering/msm-best-practices.md), en particulier :
>
>   * [Créer un site](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM et sites web multilingues](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [Bonnes pratiques de traduction](/help/sites-administering/tc-bp.md)
