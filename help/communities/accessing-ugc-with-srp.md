---
title: Accès UGC avec SRP
seo-title: Accès UGC avec SRP
description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans le magasin de noeuds d’AEM (JCR).
seo-description: Lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans le magasin de noeuds d’AEM (JCR).
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf

---


# Accès UGC avec SRP {#accessing-ugc-with-srp}

## À propos de SRP {#about-srp}

Tous les composants et fonctionnalités des communautés AEM sont construits sur le cadre des composants [sociaux (SCF)](/help/communities/scf.md), qui appelle l’API SocialResourceProvider pour accéder à tout le contenu généré par l’utilisateur (UGC).

Avant la création d’un site communautaire, le fournisseur de ressources de  de (SRP) [](/help/communities/working-with-srp.md) doit être configuré pour sélectionner une implémentation compatible avec la [topologie](/help/communities/topologies.md)sous-jacente. Les implémentations du SRP sont basées sur trois options  de  :

1. [ASRP](/help/communities/asrp.md) - Adobe à la demande 
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## A propos de l&#39; UGC {#about-ugc-storage}

Ce qui est important à savoir sur   de l’UGC est que lorsqu’un site est configuré pour utiliser ASRP ou MSRP, l’UGC réel n’est pas stocké dans le magasin [de](/help/sites-deploying/data-store-config.md) noeuds d’AEM (JCR).

Bien qu’il puisse y avoir des noeuds dans le JCR qui cachent l’UGC pour fournir des métadonnées utiles, ces noeuds ne doivent pas être confondus avec l’UGC réel.

Voir [Présentation du fournisseur de ressources .](/help/communities/srp.md)

## Best Practice {#best-practice}

Lors du développement de composants personnalisés, les développeurs doivent prendre soin de coder indépendamment de la topologie actuelle choisie, ce qui leur permet de conserver une certaine souplesse pour passer à une nouvelle topologie dans le futur.

### Supposons que JCR n’est pas disponible {#assume-jcr-not-available}

Les méthodes spécifiques au RJC doivent être évitées.

Méthodes à utiliser :

* API Sling (ressource Sling)

   * ne supposent pas qu’il existe des noeuds JCR

* OSGi

   * ne supposez pas qu’il existe des JCR 

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Méthodes à éviter :

* API de noeud
*  JCR
* lanceurs de processus (qui utilisent des  JCR)

### Utiliser les collections de recherche {#use-search-collections}

Différents fichiers SRP peuvent avoir différentes langues de natives. Il est recommandé d’utiliser les méthodes du package [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) pour exécuter la langue  appropriée.

For more information, see [Search Essentials](/help/communities/search-implementation.md).

## Ressources {#resources}

* [de contenu de la communauté](/help/communities/working-with-srp.md) - aborde les choix SRP disponibles pour une boutique commune UGC.
* [Aperçu](/help/communities/srp.md) du fournisseur de ressources  - présentation et utilisation du référentiel
* [SRP et UGC Essentials](/help/communities/srp-and-ugc.md) - Méthodes et exemples d&#39;utilitaires SRP
* [Essentials](/help/communities/search-implementation.md) de recherche - informations essentielles pour la recherche UGC
* [SocialUtils Refactoring](/help/communities/socialutils.md) - mappage des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

