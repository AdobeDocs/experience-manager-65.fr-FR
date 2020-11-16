---
title: Accès à l'UGC avec SRP
seo-title: Accès à l'UGC avec SRP
description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans AEM Node Store (JCR).
seo-description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans AEM Node Store (JCR).
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Accès à l&#39;UGC avec SRP {#accessing-ugc-with-srp}

## À propos de SRP {#about-srp}

Tous les composants et fonctionnalités AEM Communities sont construits sur la structure des composants [sociaux (SCF)](/help/communities/scf.md), qui appelle l’API SocialResourceProvider pour accéder à tout le contenu généré par l’utilisateur (UGC).

Avant la création d’un site communautaire, le fournisseur de ressources [d’enregistrement (SRP)](/help/communities/working-with-srp.md) doit être configuré pour sélectionner une mise en oeuvre compatible avec la [topologie](/help/communities/topologies.md)sous-jacente. Les mises en oeuvre du PSR reposent sur trois options d’enregistrement :

1. [ASRP](/help/communities/asrp.md) - enregistrement à la demande Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## À propos de l&#39;Enregistrement UGC {#about-ugc-storage}

Ce qui est important à savoir sur l’enregistrement de l’UGC, c’est que lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans AEM magasin [de](/help/sites-deploying/data-store-config.md) noeuds (JCR).

Bien qu’il puisse y avoir des noeuds dans le JCR qui cachent l’UGC pour fournir des métadonnées utiles, ces noeuds ne doivent pas être confondus avec l’UGC réel.

Voir Présentation des fournisseurs de ressources [d&#39;Enregistrement.](/help/communities/srp.md)

## Best Practice {#best-practice}

Lors du développement de composants personnalisés, les développeurs doivent veiller à coder indépendamment de la topologie actuelle choisie, en conservant ainsi la flexibilité nécessaire pour passer à une nouvelle topologie à l’avenir.

### Supposons que JCR n&#39;est pas disponible {#assume-jcr-not-available}

Les méthodes spécifiques au JCR doivent être évitées.

Méthodes à utiliser :

* API Sling (ressource Sling)

   * ne supposent pas qu’il existe des noeuds JCR

* ÉVÉNEMENTS OSGi

   * ne supposent pas qu’il existe des événements JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Méthodes à éviter :

* API de noeud
* Événements JCR
* lanceurs de processus (qui utilisent des événements JCR)

### Utiliser les collections de recherche {#use-search-collections}

Différents fournisseurs de services de gestion des ressources peuvent avoir différentes langues de requête natives. Il est recommandé d’utiliser les méthodes du [package com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) pour exécuter la langue de requête appropriée.

For more information, see [Search Essentials](/help/communities/search-implementation.md).

## Ressources {#resources}

* [Enregistrement](/help/communities/working-with-srp.md) de contenu de la communauté - aborde les options SRP disponibles pour un magasin commun UGC.
* [Présentation](/help/communities/srp.md) du fournisseur de ressources d&#39;Enregistrement - présentation et présentation de l&#39;utilisation du référentiel
* [SRP et UGC Essentials](/help/communities/srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP
* [Essentials](/help/communities/search-implementation.md) de recherche - informations essentielles pour rechercher l&#39;UGC
* [SocialUtils Refactoring](/help/communities/socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

