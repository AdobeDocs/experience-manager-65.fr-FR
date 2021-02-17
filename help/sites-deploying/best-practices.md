---
title: Meilleures pratiques de déploiement
seo-title: Meilleures pratiques de déploiement
description: Meilleures pratiques de déploiement et de maintenance.
seo-description: Meilleures pratiques de déploiement et de maintenance.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 57%

---


# Meilleures pratiques de déploiement{#deploying-best-practices}

Les meilleures pratiques de déploiement expliquent comment déployer ou maintenir AEM de la façon la plus efficace possible. Cette liste croissante de rubriques inclut une variété d’aspects dans AEM.

Les domaines suivants contiennent de la documentation sur le déploiement et la mise à jour des meilleures pratiques et des recommandations :

* [OAK](#oak)
* [Communautés](#communities)
* [Interface utilisateur](#ui)
* [Performances](#performance)

Pour les meilleures pratiques d’administration, de développement ou de création, consultez l’un des liens suivants :

* [Meilleures pratiques d’administration](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques de développement](/help/sites-developing/best-practices.md)
* [Meilleures pratiques de création](/help/sites-authoring/best-practices.md)

Des documents spécifiques sont décrits dans les tableaux qui suivent et y sont reliés.

## OAK {#oak}

[OAK](/help/sites-deploying/platform.md) est un référentiel de contenu hiérarchique évolutif et performant qui constitue la base d’AEM.

<table>
 <tbody>
  <tr>
   <td><p>Évolutivité, performances et reprise après sinistre</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Performance et évolutivité</a></td>
   <td>Fournit un livre blanc sur l'agilité technique, les performances élevées et les fonctionnalités de reprise après sinistre fiables.</td>
  </tr>
  <tr>
   <td>Déploiements OAK recommandés</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Déploiements recommandés</a></td>
   <td>Décrit les scénarios de déploiement</td>
  </tr>
  <tr>
   <td>Topologie Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Meilleures pratiques en matière de topologie Mongo</a></td>
   <td>Décrit la topologie du mongo - quand utiliser quelle topologie.</td>
  </tr>
  <tr>
   <td>Options de la banque de données</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuration des entrepôts de données et de noeuds</a></td>
   <td>Ce document décrit les meilleures pratiques relatives au stockage des données binaires et des noeuds de contenu. Inclut des informations sur l’utilisation de l’entrepôt de données Amazon S3.</td>
  </tr>
  <tr>
   <td>Recherche dans OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Bonnes pratiques relatives aux requêtes et à l’indexation</a><br /> </td>
   <td>Décrit les meilleures pratiques d’indexation du contenu.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities simplifie la création et la gestion de communautés sur site. Les bonnes pratiques pour AEM Communities sont décrites ici :

[Communauté Content Store](/help/communities/working-with-srp.md)  - Discute de la nouvelle fonctionnalité d’enregistrement partagé pour le contenu généré par l’utilisateur (UGC) et des considérations à prendre en compte lors du choix de la  [topologie](/help/communities/topologies.md) sous-jacente.

[Déploiements recommandés pour les communautés](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  - Décrit les déploiements recommandés pour les communautés. |

## Interface utilisateur {#ui}

Les meilleures pratiques relatives à l’interface utilisateur sont présentées ici :

[Recommandations d’interfaces utilisateur aux clients](/help/sites-deploying/ui-recommendations.md)

AEM dispose actuellement de deux interfaces utilisateur : IU classique et optimisée pour les écrans tactiles dans la même version. Les clients doivent donc décider laquelle utiliser lors de la mise en œuvre du projet. Ce document vise à aider à trouver le bon choix.

## Performances {#performance}

Les meilleures pratiques relatives à la performance sont répertoriées ici :

<table>
 <tbody>
  <tr>
   <td>Meilleures pratiques pour l’assurance qualité</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Meilleures pratiques pour l’assurance qualité</a></td>
   <td>Présentation standardisée des problèmes liés à la définition d'un concept de test spécifiquement pour les tests de performances sur votre environnement <em>publish</em>. Il intéressera principalement les ingénieurs d’assurance qualité, les chefs de projets et les administrateurs système.</td>
  </tr>
  <tr>
   <td>Utilisation de Dispatcher avec un CDN </td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilisation de Dispatcher avec un CDN </a></td>
   <td>Un réseau de distribution de contenu (CDN), par exemple Akamai Edge Delivery ou Amazon Cloud Front, distribue du contenu à partir d’un emplacement proche de l’utilisateur final.</td>
  </tr>
  <tr>
   <td>Optimisation des performances</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Optimisation des performances</a></td>
   <td>L’un des problèmes majeurs est le temps que met votre site web pour répondre aux requêtes des visiteurs.</td>
  </tr>
  <tr>
   <td>Test de performance</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Bonnes pratiques pour les tests de performance</a></td>
   <td>Présente les meilleures pratiques pour l’exécution de tests de performance sur un déploiement AEM.<br /> </td>
  </tr>
 </tbody>
</table>

