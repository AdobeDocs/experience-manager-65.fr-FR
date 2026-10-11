---
title: Présentation du fournisseur de ressources de stockage
description: Découvrez comment le contenu de la communauté, appelé contenu créé par l’utilisateur, est stocké dans un magasin simple et commun fourni par un fournisseur de ressources de stockage (SRP).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 2%
---
# Présentation du fournisseur de ressources de stockage {#storage-resource-provider-overview}

## Présentation {#introduction}

Depuis Adobe Experience Manager (AEM) Communities 6.1, le contenu de la communauté, généralement appelé contenu créé par l’utilisateur, est stocké dans un magasin unique et commun fourni par un [fournisseur de ressources de stockage](working-with-srp.md) (SRP).

Il existe plusieurs options SRP, qui accèdent toutes au contenu créé par l’utilisateur par le biais d’une nouvelle interface d’AEM Communities, l’[API SocialResourceProvider](srp-and-ugc.md) (API SRP), qui inclut toutes les opérations CRUD (create, read, update et delete).

Tous les composants SCF sont implémentés à l’aide de l’API SRP, ce qui permet de développer le code sans connaître la [ topologie sous-jacente ](topologies.md) ou l’emplacement du contenu créé par l’utilisateur.

***L’API SocialResourceProvider est disponible uniquement pour les clients sous licence d’AEM Communities.***

>[!NOTE]
>
>**Composants personnalisés** : pour les clients sous licence d’AEM Communities, l’API SRP est disponible pour les développeurs de composants personnalisés permettant d’accéder au contenu créé par l’utilisateur sans tenir compte de la topologie sous-jacente. Voir [SRP et UGC Essentials](srp-and-ugc.md).

Voir également :

* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires SRP.
* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) - Instructions de codage.
* [SocialUtils Refactoring](socialutils.md) - Mappage des méthodes d&#39;utilitaire obsolètes aux méthodes d&#39;utilitaire SRP actuelles.

## À propos du référentiel {#about-the-repository}

Pour comprendre le protocole SRP, il est utile de comprendre le rôle du référentiel AEM (Oak) dans un site de la communauté AEM.

**Java™ Content Repository (JCR)**
Cette norme définit un modèle de données et une interface de programmation d’application ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) pour les référentiels de contenu. Il associe les caractéristiques des systèmes de fichiers classiques à celles des bases de données relationnelles et ajoute plusieurs fonctionnalités supplémentaires dont les applications de contenu ont souvent besoin.

Une implémentation de JCR est le référentiel AEM, Oak.

**Apache Jackrabbit Oak**
[](../../help/sites-deploying/platform.md) est une implémentation de JCR 2.0 qui est un système de stockage de données conçu pour les applications orientées contenu. Il s’agit d’un type de base de données hiérarchique conçu pour les données non structurées et semi-structurées. Le référentiel stocke non seulement le contenu destiné à l’utilisateur ou à l’utilisatrice, mais également l’ensemble du code, des modèles et des données internes utilisés par l’application. L’interface utilisateur permettant d’accéder au contenu est [](../../help/sites-developing/developing-with-crxde-lite.md).

JCR et Oak sont généralement utilisés pour faire référence au référentiel AEM.

Une fois le contenu du site développé dans l’environnement de création privé, il doit être copié dans l’environnement de publication public. Cela s’effectue souvent par le biais d’une opération appelée *[réplication](deploy-communities.md#replication-agents-on-author)*. Cela se produit sous le contrôle de l’auteur/développeur/administrateur.

Pour le contenu créé par l’utilisateur, le contenu est saisi par les visiteurs du site enregistrés (membres de la communauté) dans l’environnement de publication public. Cela se produit de manière aléatoire.

À des fins de gestion et de création de rapports, il est utile d’avoir accès au contenu créé par l’utilisateur à partir de l’environnement de création privé. Avec SRP, l’accès au contenu créé par l’utilisateur depuis l’instance de création est plus cohérent et plus performant, car la réplication inverse de la publication vers l’instance de création n’est pas nécessaire.

## À propos du SRP {#about-srp}

Lorsque du contenu créé par l’utilisateur est enregistré dans le stockage partagé, il existe une seule instance de contenu membre qui est accessible dans la plupart des déploiements à partir des environnements de création et de publication. Quel que soit le choix du SRP (MSRP, ASRP, JSRP), tous doivent être accessibles par programmation avec l’API SRP.

>[!NOTE]
>
>Consultez [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code et des détails supplémentaires.
>
>Consultez [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) pour connaître les bonnes pratiques en matière de codage.

### ASRP {#asrp}

S’il existe un ASRP, le contenu créé par l’utilisateur n’est pas stocké dans JCR, il est stocké dans un service cloud hébergé et géré par Adobe. Il est impossible de visualiser le contenu créé par l’utilisateur stocké dans ASRP avec CRXDE Lite ou d’y accéder à l’aide de l’API JCR.

Voir [ASRP - Fournisseur de ressources de stockage Adobe](asrp.md).

Les développeurs ne peuvent pas accéder directement au contenu créé par l’utilisateur.

ASRP utilise le cloud Adobe pour les requêtes.

### MSRP {#msrp}

S’il y en a un, MSRP, le contenu créé par l’utilisateur n’est pas stocké dans JCR, il est stocké dans MongoDB. Le contenu créé par l’utilisateur stocké dans MSRP n’est pas consultable avec CRXDE Lite ou accessible via l’API JCR.

Voir [MSRP - Fournisseur de ressources de stockage MongoDB](msrp.md).

Bien que MSRP soit comparable à ASRP, étant donné que toutes les instances de serveur AEM accèdent au même contenu créé par l’utilisateur, il est possible d’utiliser des outils communs pour accéder directement au contenu créé par l’utilisateur stocké dans MongoDB.

MSRP utilise Solr pour les requêtes.

### JSRP {#jsrp}

JSRP est le fournisseur par défaut pour l’accès à tout le contenu créé par l’utilisateur sur une seule instance AEM. Il vous permet de tester rapidement AEM Communities 6.1 sans avoir à configurer MSRP ou ASRP.

Voir [JSRP - Fournisseur de ressources de stockage JCR](jsrp.md).

S’il existe un JSRP lorsque le contenu créé par l’utilisateur est stocké dans JCR et qu’il est accessible dans CRXDE Lite et l’API JCR, Adobe recommande de ne jamais utiliser l’API JCR pour ce faire. Si vous le faites, les modifications ultérieures peuvent affecter le code personnalisé.

De plus, le référentiel des environnements de création et de publication n’est pas partagé. Bien qu’un cluster d’instances de publication entraîne un référentiel de publication partagé, le contenu créé par l’utilisateur entré dans l’instance de publication n’est pas visible dans l’instance de création, ce qui empêche de gérer ce contenu depuis l’instance de création. Le contenu créé par l’utilisateur n’est conservé que dans le référentiel AEM (JCR) de l’instance sur laquelle il a été saisi.

JSRP utilise les index Oak pour les requêtes.

## À propos des nœuds fantômes dans JCR {#about-shadow-nodes-in-jcr}

Les nœuds fantômes, qui imitent le chemin d’accès au contenu créé par l’utilisateur, existent dans le référentiel local à deux fins :

1. [Contrôle d’accès (ACL)](#for-access-control-acls)
1. [Ressources non existantes (NER)](#for-non-existing-resources-ners)

Quelle que soit l’implémentation de SRP, le contenu créé par l’utilisateur n’est *visible* même emplacement que le nœud fantôme.

### Pour le contrôle d’accès (ACL) {#for-access-control-acls}

Certaines implémentations de SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification d’ACL. Les nœuds fantômes fournissent un emplacement dans le référentiel local auquel les listes de contrôle d’accès peuvent être appliquées.

Grâce à l’API SRP, toutes les options SRP effectuent la même vérification de l’emplacement caché avant toutes les opérations CRUD.

La vérification de l’ACL utilise une méthode utilitaire qui renvoie un chemin d’accès approprié pour vérifier les autorisations appliquées au contenu créé par l’utilisateur de la ressource.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code.

### Pour les ressources non existantes {#for-non-existing-resources-ners}

Certains composants de Communities sont inclusibles dans un script et nécessitent donc un nœud adressable Sling pour prendre en charge les fonctionnalités de Communities. Les [composants inclus](scf.md#add-or-include-a-communities-component) sont appelés ressources non existantes (NER).

Les nœuds fantômes fournissent un emplacement adressable Sling dans le référentiel.

>[!CAUTION]
>
>Comme le nœud fantôme a plusieurs utilisations, la présence d’un nœud fantôme n’implique *pas* que le composant est un NER.

### Emplacement de stockage {#storage-location}

Voici un exemple de nœud fantôme, utilisant le composant [Commentaires](http://localhost:4502/content/community-components/en/comments.html) dans le [Guide des composants de communauté](components-guide.md) :

* Le composant existe dans le référentiel local à l’emplacement suivant :

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Le nœud fantôme correspondant existe dans le référentiel local à l’emplacement suivant :

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Aucun contenu créé par l’utilisateur n’a été trouvé sous le nœud fantôme.

Le comportement par défaut consiste à configurer des nœuds fantômes sur une instance de publication chaque fois que la sous-arborescence appropriée est référencée pour une lecture ou une écriture.

Par exemple, supposons que le déploiement soit [MSRP](msrp.md) avec une ferme de publication TarMK.

Lorsqu’un [membre](users.md) publie du contenu créé par l’utilisateur sur pub1 (stocké dans MongoDB), les nœuds fantômes sont créés dans JCR sur pub1.

La première fois que le contenu créé par l’utilisateur est lu sur pub2, si rien n’est configuré, le comportement par défaut consiste à créer les nœuds fantômes.

Si un comportement autre que celui par défaut est souhaité, il doit être configuré sur l’instance d’auteur et déployé sur toutes les instances de publication, ce qui correspond généralement à un processus manuel.
