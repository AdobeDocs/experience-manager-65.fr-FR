---
title: Présentation du fournisseur de ressources de stockage
seo-title: Présentation du fournisseur de ressources de stockage
description: Stockage commun pour les communautés
seo-description: Stockage commun pour les communautés
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# Présentation du fournisseur de ressources de stockage {#storage-resource-provider-overview}

## Présentation {#introduction}

Depuis AEM Communities 6.1, le contenu de la communauté, communément appelé contenu généré par l’utilisateur, est stocké dans un seul magasin commun fourni par un [fournisseur de ressources de stockage](working-with-srp.md) (SRP).

Il existe plusieurs options de SRP, qui accèdent toutes au contenu généré par l’utilisateur via une nouvelle interface AEM Communities, l’[API SocialResourceProvider](srp-and-ugc.md) (API SRP), qui inclut toutes les opérations de création, de lecture, de mise à jour et de suppression (CRUD).

Tous les composants SCF sont implémentés à l’aide de l’API SRP, ce qui permet au code d’être développé sans connaissance de la [topologie sous-jacente](topologies.md) ou de l’emplacement du contenu généré par l’utilisateur.

***L’API SocialResourceProvider est disponible uniquement pour les clients sous licence d’AEM Communities.***

>[!NOTE]
>
>**Composants** personnalisés : Pour les clients sous licence d’AEM Communities, l’API SRP est disponible pour les développeurs de composants personnalisés dans le but d’accéder au contenu généré par l’utilisateur sans tenir compte de la topologie sous-jacente. Voir [Notions fondamentales relatives à la SRP et au contenu généré par l’utilisateur](srp-and-ugc.md).

Voir également :

* [SRP et UGC Essentials](srp-and-ugc.md)  - Méthodes et exemples d’utilitaire SRP.
* [Accès au contenu généré par l’utilisateur avec SRP](accessing-ugc-with-srp.md)  - Instructions de codage.
* [Refactorisation de SocialUtils](socialutils.md)  : mappage de méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles.

## À propos du référentiel {#about-the-repository}

Pour comprendre la SRP, il est utile de comprendre le rôle du référentiel AEM (OAK) dans un site de communauté AEM.

**Java Content Repository (JCR)**
Cette norme définit un modèle de données et une interface de programmation d’application ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) pour les référentiels de contenu. Il combine les caractéristiques des systèmes de fichiers classiques avec celles des bases de données relationnelles et ajoute un certain nombre de fonctions supplémentaires dont les applications de contenu ont souvent besoin.

Une implémentation de JCR est le référentiel AEM, OAK.

**Apache Jackrabbit Oak (OAK)**
[](../../help/sites-deploying/platform.md) OAK est une implémentation de JCR 2.0 qui est un système de stockage de données spécialement conçu pour les applications centrées sur le contenu. Il s’agit d’un type de base de données hiérarchique conçu pour les données non structurées et semi-structurées. Le référentiel stocke le contenu affiché aux utilisateurs et l’ensemble du code, des modèles et des données internes utilisés par l’application. L’interface utilisateur d’accès au contenu est [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR et OAK sont généralement utilisés pour faire référence au référentiel AEM.

Après avoir développé le contenu du site dans l’environnement de création privé, il doit être copié dans l’environnement de publication public. Cela est souvent effectué au moyen d’une opération appelée *[réplication](deploy-communities.md#replication-agents-on-author)*. Cela se produit sous le contrôle de l’auteur/du développeur/de l’administrateur.

Pour le contenu généré par l’utilisateur, le contenu est saisi par les visiteurs enregistrés du site (membres de la communauté) dans l’environnement de publication public. Cela se produit de manière aléatoire.

À des fins de gestion et de création de rapports, il est utile d’avoir accès au contenu généré par l’utilisateur à partir de l’environnement de création privé. Grâce à la SRP, l’accès au contenu généré par l’utilisateur à partir de l’auteur est plus cohérent et performant, car la réplication inverse de la publication vers l’auteur n’est pas nécessaire.

## À propos de SRP {#about-srp}

Lorsque le contenu créé par l’utilisateur est enregistré dans le stockage partagé, il existe une instance unique du contenu membre qui peut, dans la plupart des déploiements, être accessible à partir des environnements de création et de publication. Quel que soit le choix de SRP (MSRP, ASRP, JSRP), tous ces éléments doivent être accessibles par programmation avec l’API SRP.

>[!NOTE]
>
>Voir [Notions fondamentales relatives à la SRP et au contenu généré par l’utilisateur](srp-and-ugc.md) pour obtenir un exemple de code et des détails supplémentaires.
>
>Voir [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md) pour connaître les bonnes pratiques en matière de codage.

### ASRP {#asrp}

Dans le cas d’ASRP, le contenu créé par l’utilisateur n’est pas stocké dans JCR, il est stocké dans un service cloud hébergé et géré par Adobe. Le contenu généré par l’utilisateur stocké dans ASRP ne peut ni être affiché avec le CRXDE Lite, ni accessible à l’aide de l’API JCR.

Voir [ASRP - Fournisseur de ressources de stockage d’Adobe](asrp.md).

Il n’est pas possible pour les développeurs d’accéder directement au contenu créé par l’utilisateur.

ASRP utilise Adobe Cloud pour les requêtes.

### MSRP {#msrp}

Dans le cas de MSRP, le contenu généré par l’utilisateur n’est pas stocké dans JCR, mais dans MongoDB. Le contenu généré par l’utilisateur stocké dans MSRP ne peut pas être affiché avec CRXDE Lite ni accessible à l’aide de l’API JCR.

Voir [MSRP - MongoDB Storage Resource Provider](msrp.md).

Bien que MSRP soit comparable à ASRP, puisque toutes les instances AEM serveur accèdent au même contenu généré par l’utilisateur, il est possible d’utiliser des outils communs pour accéder directement au contenu créé par l’utilisateur stocké dans MongoDB.

MSRP utilise Solr pour les requêtes.

### JSRP {#jsrp}

JSRP est le fournisseur par défaut pour accéder à tout le contenu créé par l’utilisateur sur une seule instance AEM. Il permet de tester rapidement AEM Communities 6.1 sans avoir à configurer MSRP ou ASRP.

Voir [JSRP - JCR Storage Resource Provider](jsrp.md).

Dans le cas de JSRP, alors que le contenu créé par l’utilisateur est stocké dans JCR et accessible via l’API CRXDE Lite et JCR, il est vivement recommandé de ne jamais utiliser l’API JCR pour le faire, sinon les modifications futures peuvent affecter le code personnalisé.

En outre, le référentiel pour les environnements de création et de publication n’est pas partagé. Bien qu’un cluster d’instances de publication génère un référentiel de publication partagé, le contenu créé par l’utilisateur entré lors de la publication ne sera pas visible sur l’auteur, ce qui empêche la gestion du contenu créé par l’auteur. Le contenu généré par l’utilisateur n’est conservé que dans le référentiel AEM (JCR) de l’instance sur laquelle il a été saisi.

JSRP utilise les index Oak pour les requêtes.

## À propos des noeuds fantômes dans JCR {#about-shadow-nodes-in-jcr}

Les noeuds fantômes, qui imitent le chemin d’accès au contenu généré par l’utilisateur, existent dans le référentiel local pour servir deux objectifs :

1. [Contrôle d’accès (ACL)](#for-access-control-acls)
1. [Ressources non existantes (NER)](#for-non-existing-resources-ners)

Quelle que soit l’implémentation de la SRP, le contenu généré par l’utilisateur réel ne sera *pas visible au même emplacement que le noeud fantôme.

### Pour le contrôle d’accès (ACL) {#for-access-control-acls}

Certaines mises en oeuvre de la SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification de l’ACL. Les noeuds fantômes fournissent un emplacement dans le référentiel local auquel les listes de contrôle d’accès peuvent être appliquées.

À l’aide de l’API SRP, toutes les options de SRP effectuent la même vérification de l’emplacement fantôme avant toutes les opérations CRUD.

La vérification ACL utilise une méthode utilitaire qui renvoie un chemin approprié pour vérifier les autorisations appliquées au contenu généré par l’utilisateur de la ressource.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour consulter un exemple de code.

### Pour les ressources non existantes (NER) {#for-non-existing-resources-ners}

Certains composants de Communities sont inclus dans un script et nécessitent donc un noeud adressable Sling pour prendre en charge les fonctionnalités de Communities. [Les ](scf.md#add-or-include-a-communities-component) composants inclus sont appelés ressources non existantes (NER).

Les noeuds fantômes fournissent un emplacement adressable Sling dans le référentiel.

>[!CAUTION]
>
>Comme le noeud fantôme présente plusieurs utilisations, la présence d’un noeud fantôme n’implique pas ** que le composant soit un NER.

### Emplacement de stockage {#storage-location}

Voici un exemple de noeud fantôme, à l’aide du [composant Commentaires](http://localhost:4502/content/community-components/en/comments.html) dans le [Guide des composants de la communauté](components-guide.md) :

* Le composant existe dans le référentiel local à l’adresse :

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Le noeud fantôme correspondant existe dans le référentiel local à l’adresse :

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Aucun contenu généré par l’utilisateur ne sera trouvé sous le noeud fantôme.

Le comportement par défaut consiste à configurer des noeuds fantômes sur une instance de publication chaque fois que la sous-arborescence appropriée est référencée pour une lecture ou une écriture.

Par exemple, supposons que le déploiement soit [MSRP](msrp.md) avec une ferme de publication TarMK.

Lorsqu’un [membre](users.md) publie du contenu généré par l’utilisateur sur pub1 (stocké dans MongoDB), les noeuds fantômes sont créés dans JCR sur pub1.

La première fois que le contenu créé par l’utilisateur est lu sur pub2, si rien n’est configuré, le comportement par défaut est de créer les noeuds fantômes.

Si un autre comportement que le comportement par défaut est souhaité, il doit être configuré sur l’instance de création et déployé sur toutes les instances de publication, ce qui est généralement un processus manuel.
