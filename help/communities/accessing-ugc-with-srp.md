---
title: Accès au contenu généré par l’utilisateur avec SRP
seo-title: Accessing UGC with SRP
description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu généré par l’utilisateur réel n’est pas stocké dans AEM magasin de noeuds (JCR).
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Accès au contenu généré par l’utilisateur avec SRP {#accessing-ugc-with-srp}

## À propos de SRP {#about-srp}

Tous les composants et fonctionnalités d’AEM Communities sont construits sur le [structure de composants sociaux (SCF)](/help/communities/scf.md), qui appelle l’API SocialResourceProvider pour accéder à tout le contenu généré par l’utilisateur (UGC).

Avant la création d’un site communautaire, la variable [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md) doit être configuré pour sélectionner une implémentation cohérente avec la sous-jacente [topologie](/help/communities/topologies.md). Les mises en oeuvre de la SRP reposent sur trois options de stockage :

1. [ASRP](/help/communities/asrp.md) - Adobe du stockage à la demande
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## À propos du stockage UGC {#about-ugc-storage}

Ce qu’il est important de savoir sur le stockage du contenu généré par l’utilisateur, c’est que lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu généré par l’utilisateur réel n’est pas stocké dans AEM [magasin de noeuds](/help/sites-deploying/data-store-config.md) (JCR).

Bien qu’il puisse y avoir des noeuds dans JCR qui cachent le contenu créé par l’utilisateur pour fournir des métadonnées utiles, ces noeuds ne doivent pas être confondus avec le contenu créé par l’utilisateur réel.

Voir [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md)

## Bonne pratique {#best-practice}

Lors du développement de composants personnalisés, les développeurs doivent veiller à ne pas coder en fonction de la topologie actuelle choisie, en conservant ainsi la possibilité de passer à une nouvelle topologie à l’avenir.

### Supposons que JCR ne soit pas disponible {#assume-jcr-not-available}

Les méthodes spécifiques à JCR doivent être évitées.

Méthodes d’utilisation :

* API Sling (ressource Sling)

   * ne supposez pas qu’il existe des noeuds JCR

* Événements OSGi

   * ne supposez pas qu’il y ait des événements JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Méthodes à éviter :

* API Node
* Événements JCR
* lanceurs de workflow (qui utilisent des événements JCR)

### Utilisation des collections de recherche {#use-search-collections}

Différents SRP peuvent avoir différents langages de requête natifs. Il est recommandé d’utiliser les méthodes de la variable [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) pour exécuter le langage de requête approprié.

Pour plus d’informations, voir [Principes de recherche](/help/communities/search-implementation.md).

## Ressources {#resources}

* [Stockage de contenu communautaire](/help/communities/working-with-srp.md) - aborde les choix de SRP disponibles pour un magasin commun UGC
* [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md) - présentation et utilisation du référentiel
* [Principes de base de la SRP et du contenu généré par l’utilisateur](/help/communities/srp-and-ugc.md) - Méthodes d’utilitaire SRP et exemples
* [Principes de recherche](/help/communities/search-implementation.md) - informations essentielles pour la recherche du contenu généré par l’utilisateur
* [Refactorisation de SocialUtils](/help/communities/socialutils.md) - mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles
