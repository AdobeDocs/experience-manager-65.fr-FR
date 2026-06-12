---
title: Accès au contenu créé par l’utilisateur avec SRP
description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu créé par l’utilisateur réel n’est pas stocké dans le magasin de nœuds AEM (JCR)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Accès au contenu créé par l’utilisateur avec SRP {#accessing-ugc-with-srp}

## À propos du SRP {#about-srp}

Tous les composants et fonctionnalités d’AEM Communities sont basés sur le [Social Component Framework (SCF)](/help/communities/scf.md) qui appelle l’API SocialResourceProvider pour accéder à tout le contenu généré par l’utilisateur (UGC).

Avant la création d’un site communautaire, le [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md) doit être configuré pour sélectionner une implémentation cohérente avec la [topologie](/help/communities/topologies.md) sous-jacente. Les implémentations de SRP reposent sur trois options de stockage :

1. [ASRP](/help/communities/asrp.md) - Stockage à la demande Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## À propos du stockage du contenu créé par l’utilisateur {#about-ugc-storage}

Ce qu’il est important de savoir sur le stockage du contenu créé par l’utilisateur est que, lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu créé par l’utilisateur n’est pas stocké dans AEM [magasin de nœuds](/help/sites-deploying/data-store-config.md) (JCR).

Bien qu’il puisse y avoir des nœuds dans JCR qui masquent le contenu créé par l’utilisateur pour fournir des métadonnées utiles, ces nœuds ne doivent pas être confondus avec le contenu créé par l’utilisateur réel.

Voir [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md).

## Bonne pratique {#best-practice}

Lors du développement de composants personnalisés, l’équipe de développement doit veiller à coder indépendamment de la topologie actuelle choisie, afin de conserver la possibilité de passer à une nouvelle topologie à l’avenir.

### Supposons que JCR ne soit pas disponible. {#assume-jcr-not-available}

Les méthodes spécifiques à JCR doivent être évitées.

Méthodes d’utilisation :

* API Sling (ressource Sling)

   * ne supposons pas qu’il existe des nœuds JCR.

* Événements OSGi

   * ne supposons pas qu’il existe des événements JCR.

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Méthodes à éviter :

* API Node
* Événements JCR
* les lanceurs de workflow (qui utilisent des événements JCR) ;

### Utilisation de la recherche de collections {#use-search-collections}

Différents SRP peuvent avoir différents langages de requête natifs. Utilisez les méthodes du package [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) pour exécuter le langage de requête approprié.

Pour plus d’informations, voir [Search Essentials](/help/communities/search-implementation.md).

## Ressources {#resources}

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md) - Décrit les choix SRP disponibles pour un magasin commun de contenu créé par l’utilisateur
* [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md) - introduction et présentation de l’utilisation du référentiel
* [SRP et UGC Essentials](/help/communities/srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP
* [Search Essentials](/help/communities/search-implementation.md) - Informations essentielles pour la recherche de contenu créé par l’utilisateur
* [SocialUtils Refactoring](/help/communities/socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles
