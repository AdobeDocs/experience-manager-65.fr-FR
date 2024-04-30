---
title: Bonnes pratiques de déploiement
description: Découvrez comment déployer et gérer Adobe Experience Manager (AEM) de la manière la plus efficace possible.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 100%

---

# Bonnes pratiques de déploiement{#deploying-best-practices}

Les bonnes pratiques de déploiement expliquent comment déployer ou garder à jour AEM de la façon la plus efficace possible. Cette liste croissante de sujets englobe un large éventail de domaines dans AEM.

Les recommandations et bonnes pratiques de déploiement et de maintenance sont documentées pour les aspects suivants :

* [Oak](#oak)
* [Communities](#communities)
* [Interface utilisateur](#ui)
* [Performances](#performance)

Pour les bonnes pratiques d’administration, de développement ou de création, consultez l’un des liens suivants :

* [Bonnes pratiques d’administration](/help/sites-administering/administer-best-practices.md)
* [Bonnes pratiques de développement](/help/sites-developing/best-practices.md)
* [Bonnes pratiques de création](/help/sites-authoring/best-practices.md)

Les documents spécifiques sont décrits et associés dans les tableaux qui suivent.

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) est un référentiel de contenu hiérarchique évolutif et performant qui constitue la base d’AEM.

<table>
 <tbody>
  <tr>
   <td><p>Évolutivité, performances et reprise après sinistre</p> </td>
   <td><a href="/help/sites-deploying/performance.md">Performance et évolutivité</a></td>
   <td>Livre blanc sur l’agilité technique, les performances élevées et les fonctionnalités fiables de reprise après sinistre.</td>
  </tr>
  <tr>
   <td>Déploiements OAK recommandés</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Déploiements recommandés</a></td>
   <td>Décrit les scénarios de déploiement</td>
  </tr>
  <tr>
   <td>Topologie Mongo</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Bonnes pratiques relatives à la topologie Mongo</a></td>
   <td>Décrit la topologie de Mongo, et quand utiliser quelle topologie.</td>
  </tr>
  <tr>
   <td>Options de magasin de données</td>
   <td><a href="/help/sites-deploying/data-store-config.md">Configuration des entrepôts de nœuds et des magasins de données</a></td>
   <td>Ce document explique les bonnes pratiques relatives au stockage de données binaires et de nœuds de contenu. Inclut des informations sur l’utilisation du magasin de données Amazon S3.</td>
  </tr>
  <tr>
   <td>Rechercher dans OAK</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Bonnes pratiques relatives aux requêtes et à l’indexation</a><br /> </td>
   <td>Décrit les bonnes pratiques relatives à l’indexation du contenu.</td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities simplifie la création et la gestion des communautés sur site. Les bonnes pratiques pour AEM Communities sont présentées ici :

[Magasin de contenu de la communauté](/help/communities/working-with-srp.md) - Discute de la nouvelle fonctionnalité de stockage partagé pour le contenu généré par l’utilisateur ou l’utilisatrice et des considérations à prendre en compte pour le choix de la [topologie](/help/communities/topologies.md) sous-jacente.

[Déploiements recommandés pour les communautés](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Décrit les déploiements recommandés pour les communautés. |

## Interface utilisateur {#ui}

Les bonnes pratiques relatives à l’interface utilisateur sont présentées ici :

[Recommandations d’interfaces utilisateur aux clients](/help/sites-deploying/ui-recommendations.md)

AEM dispose actuellement de deux interfaces utilisateur : l’IU classique et l’IU optimisée pour les écrans tactiles, et ce, dans la même version. Les clients doivent donc décider laquelle utiliser lors de la mise en œuvre du projet. Ce document est destiné à vous aider à faire le bon choix.

## Performances {#performance}

Les bonnes pratiques relatives aux performances sont répertoriées ici :

<table>
 <tbody>
  <tr>
   <td>Bonnes pratiques pour l’assurance qualité</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">Bonnes pratiques pour l’assurance qualité</a></td>
   <td>Un aperçu normalisé des problèmes liés à la définition d’un concept de test, en particulier pour les tests de performance sur votre environnement de <em>publication</em>. Elles s’adressent principalement aux équipes d’ingénierie en assurance qualité, de gestion de projet et d’administration système.</td>
  </tr>
  <tr>
   <td>Utilisation de Dispatcher avec un CDN</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr#using-dispatcher-with-a-cdn">Utilisation de Dispatcher avec un CDN</a></td>
   <td>Un réseau de distribution de contenu (CDN), par exemple Akamai Edge Delivery ou Amazon Cloud Front, distribue du contenu à partir d’un emplacement proche de l’utilisateur final.</td>
  </tr>
  <tr>
   <td>Optimisation des performances</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">Optimisation des performances</a></td>
   <td>L’un des problèmes majeurs est le temps que met votre site Web pour répondre aux requêtes des visiteurs et visiteuses.</td>
  </tr>
  <tr>
   <td>Test de performance</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">Bonnes pratiques pour les tests de performance</a></td>
   <td>Présente les bonnes pratiques pour l’exécution de tests de performance sur un déploiement AEM.<br /> </td>
  </tr>
 </tbody>
</table>
