---
title: Accès au contenu généré par l’utilisateur avec SRP
seo-title: Accès au contenu généré par l’utilisateur avec SRP
description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu généré par l’utilisateur réel n’est pas stocké dans AEM magasin de noeuds (JCR).
seo-description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu généré par l’utilisateur réel n’est pas stocké dans AEM magasin de noeuds (JCR).
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
source-wordcount: '366'
ht-degree: 0%

---

# Accès au contenu généré par l’utilisateur avec SRP {#accessing-ugc-with-srp}

## À propos de SRP {#about-srp}

Tous les composants et fonctionnalités AEM Communities sont créés sur la [structure de composants sociaux (SCF)](/help/communities/scf.md), qui appelle l’API SocialResourceProvider pour accéder à tout le contenu généré par l’utilisateur.

Avant la création d’un site communautaire, le [fournisseur de ressources de stockage (SRP)](/help/communities/working-with-srp.md) doit être configuré pour sélectionner une implémentation conforme à la [topologie sous-jacente](/help/communities/topologies.md). Les mises en oeuvre de la SRP reposent sur trois options de stockage :

1. [ASRP](/help/communities/asrp.md)  : stockage Adobe à la demande
1. [MSRP](/help/communities/msrp.md)  - MongoDB
1. [JSRP](/help/communities/jsrp.md)  - JCR

## À propos du stockage UGC {#about-ugc-storage}

Ce qu’il est important de savoir sur le stockage du contenu généré par l’utilisateur, c’est que lorsqu’un site est configuré pour utiliser ASRP ou MSRP, le contenu généré par l’utilisateur réel n’est pas stocké dans AEM [magasin de noeuds](/help/sites-deploying/data-store-config.md) (JCR).

Bien qu’il puisse y avoir des noeuds dans JCR qui cachent le contenu créé par l’utilisateur pour fournir des métadonnées utiles, ces noeuds ne doivent pas être confondus avec le contenu créé par l’utilisateur réel.

Voir [Présentation du fournisseur de ressources de stockage.](/help/communities/srp.md)

## Bonne pratique {#best-practice}

Lors du développement de composants personnalisés, les développeurs doivent veiller à ne pas coder en fonction de la topologie actuelle choisie, en conservant ainsi la possibilité de passer à une nouvelle topologie à l’avenir.

### Supposons que JCR n’est pas disponible {#assume-jcr-not-available}

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

Différents SRP peuvent avoir différents langages de requête natifs. Il est recommandé d’utiliser des méthodes du package [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) pour exécuter le langage de requête approprié.

Pour plus d’informations, voir [Notions fondamentales sur la recherche](/help/communities/search-implementation.md).

## Ressources {#resources}

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md)  : discute des choix de SRP disponibles pour un magasin commun UGC.
* [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md)  - Présentation et utilisation du référentiel
* [Notions fondamentales relatives à la SRP et au contenu généré par l’utilisateur](/help/communities/srp-and-ugc.md)  - Exemples et méthodes d’utilitaire SRP
* [Notions fondamentales sur la recherche](/help/communities/search-implementation.md)  : informations essentielles pour rechercher le contenu généré par l’utilisateur
* [Refactorisation](/help/communities/socialutils.md)  de SocialUtils : mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.
