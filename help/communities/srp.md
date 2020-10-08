---
title: Présentation du fournisseur de ressources d'Enregistrement
seo-title: Présentation du fournisseur de ressources d'Enregistrement
description: Enregistrement commun pour les communautés
seo-description: Enregistrement commun pour les communautés
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# Présentation du fournisseur de ressources d&#39;Enregistrement {#storage-resource-provider-overview}

## Présentation {#introduction}

Depuis AEM Communities 6.1, le contenu de la communauté, communément appelé contenu généré par l’utilisateur (UGC), est stocké dans un seul magasin commun fourni par un fournisseur [de ressources d’](working-with-srp.md) enregistrement (SRP).

Il existe plusieurs options SRP, qui accèdent toutes à l’UGC par le biais d’une nouvelle interface AEM Communities, l’API [](srp-and-ugc.md) SocialResourceProvider (API SRP), qui inclut toutes les opérations de création, de lecture, de mise à jour et de suppression (CRUD).

Tous les composants SCF sont implémentés à l&#39;aide de l&#39;API SRP, ce qui permet de développer le code sans connaître la topologie [](topologies.md) sous-jacente ou l&#39;emplacement de l&#39;UGC.

***L’API SocialResourceProvider n’est disponible que pour les clients disposant d’une licence d’AEM Communities.***

>[!NOTE]
>
>**Composants** personnalisés : Pour les clients disposant d’une licence d’AEM Communities, l’API SRP est disponible pour les développeurs de composants personnalisés afin d’accéder à l’UGC sans tenir compte de la topologie sous-jacente. Voir [SRP et UGC Essentials](srp-and-ugc.md).

Voir également :

* [SRP et UGC Essentials](srp-and-ugc.md) - Exemples et méthodes d&#39;utilitaire SRP.
* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) - Règles de codage.
* [Refactorisation](socialutils.md) de SocialUtils - Mise en correspondance des méthodes d’utilitaire obsolètes avec les méthodes d’utilitaire SRP actuelles.

## A propos du référentiel {#about-the-repository}

Pour comprendre le PRS, il est utile de comprendre le rôle du référentiel AEM (OAK) dans un site communautaire AEM.

**Java Content Repository (JCR)** Cette norme définit un modèle de données et une interface de programmation d’applications (API[](https://jackrabbit.apache.org/jcr/jcr-api.html)JCR) pour les référentiels de contenu. Il combine les caractéristiques des systèmes de fichiers classiques avec celles des bases de données relationnelles et ajoute un certain nombre de fonctions supplémentaires dont les applications de contenu ont souvent besoin.

Une implémentation de JCR est le référentiel AEM, OAK.

**Apache Jackrabbit Oak (OAK)**[](../../help/sites-deploying/platform.md) OAKest une implémentation de JCR 2.0 qui est un système d&#39;enregistrement de données spécialement conçu pour les applications axées sur le contenu. Il s’agit d’un type de base de données hiérarchique conçue pour les données non structurées et semi-structurées. Le référentiel stocke le contenu affiché aux utilisateurs et l’ensemble du code, des modèles et des données internes utilisés par l’application. L’interface utilisateur pour l’accès au contenu est [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR et OAK sont généralement utilisés pour faire référence au référentiel AEM.

Après avoir développé le contenu du site dans l’environnement d’auteur privé, il doit être copié dans l’environnement de publication public. Cela se fait souvent par le biais d&#39;une opération appelée *[réplication](deploy-communities.md#replication-agents-on-author)*. Cela se produit sous le contrôle de l’auteur/développeur/administrateur.

Pour UGC, le contenu est saisi par des visiteurs de site enregistrés (membres de la communauté) dans l’environnement de publication public. Ça se passe de manière aléatoire.

Pour des raisons de gestion et de rapports, il est utile d&#39;avoir accès à l&#39;UGC à partir de l&#39;environnement d&#39;auteur privé. Avec SRP, l’accès à l’UGC depuis l’auteur est plus cohérent et performant, car la réplication inversée de la publication vers l’auteur n’est pas nécessaire.

## À propos de SRP {#about-srp}

Lorsque l’UGC est enregistré dans un enregistrement partagé, il existe une instance unique de contenu de membre qui peut, dans la plupart des déploiements, être accessible à partir des environnements d’auteur et de publication. Quel que soit le choix de SRP (MSRP, ASRP, JSRP), tous doivent être accessibles par programmation avec l’API SRP.

>[!NOTE]
>
>Voir [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code et des détails supplémentaires.
>
>Voir [Accès à l’UGC avec SRP](accessing-ugc-with-srp.md) pour connaître les meilleures pratiques en matière de codage.

### ASRP {#asrp}

Dans le cas d’ASRP, UGC n’est pas stocké dans le JCR, il est stocké dans un service de cloud hébergé et géré par Adobe. L’UGC stocké dans ASRP ne peut être ni affiché avec le CRXDE Lite, ni accessible à l’aide de l’API JCR.

Voir [ASRP - Fournisseur](asrp.md)de ressources d&#39;Enregistrement d&#39;Adobe.

Il n&#39;est pas possible pour les développeurs d&#39;accéder directement à l&#39;UGC.

ASRP utilise Adobe cloud pour les requêtes.

### MSRP {#msrp}

Dans le cas de MSRP, UGC n’est pas stocké dans JCR, il est stocké dans MongoDB. L’UGC stocké dans MSRP ne peut être ni affiché avec le CRXDE Lite, ni accessible à l’aide de l’API JCR.

See [MSRP - MongoDB Storage Resource Provider](msrp.md).

Bien que MSRP soit comparable à ASRP, puisque toutes les instances AEM serveur accèdent au même UGC, il est possible d&#39;utiliser des outils communs pour accéder directement à l&#39;UGC stocké dans MongoDB.

MSRP utilise Solr pour les requêtes.

### JSRP {#jsrp}

JSRP est le fournisseur par défaut pour accéder à l’ensemble des fichiers UGC sur une seule instance AEM. Il permet d’expérimenter rapidement AEM Communities 6.1 sans avoir à configurer MSRP ou ASRP.

Voir [JSRP - Fournisseur](jsrp.md)de ressources d’Enregistrement JCR.

Dans le cas de JSRP, alors que l’UGC est stockée dans le JCR et accessible par le biais de l’API CRXDE Lite et JCR, il est fortement recommandé que l’API JCR ne soit jamais utilisée pour ce faire, sinon les modifications futures peuvent affecter le code personnalisé.

En outre, le référentiel des environnements d’auteur et de publication n’est pas partagé. Bien qu’un cluster d’instances de publication produise un référentiel de publication partagé, l’UGC saisi lors de la publication ne sera pas visible sur l’auteur, ce qui empêche la gestion de l’UGC à partir de l’auteur. L’UGC n’est conservé que dans le référentiel AEM (JCR) de l’instance sur laquelle il a été saisi.

JSRP utilise les index de chêne pour les requêtes.

## A propos des noeuds fantômes dans JCR {#about-shadow-nodes-in-jcr}

Les noeuds d’ombre, qui imitent le chemin d’accès à UGC, existent dans le référentiel local pour servir deux objectifs :

1. [contrôle d&#39;accès (ACL)](#for-access-control-acls)
1. [Ressources non existantes (NER)](#for-non-existing-resources-ners)

Quelle que soit la mise en oeuvre SRP, l&#39;UGC réel ne *sera pas visible au même emplacement que le noeud fantôme.

### Pour le Contrôle d&#39;accès (ACL) {#for-access-control-acls}

Certaines implémentations SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification ACL. Les noeuds d’ombre fournissent un emplacement dans le référentiel local auquel les ACL peuvent être appliquées.

A l’aide de l’API SRP, toutes les options SRP effectuent la même vérification de l’emplacement de l’ombre avant toutes les opérations CRUD.

La vérification de l&#39;ACL utilise une méthode utilitaire qui renvoie un chemin approprié pour vérifier les autorisations appliquées à l&#39;UGC de la ressource.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code.

### Pour les ressources non existantes (NER) {#for-non-existing-resources-ners}

Certains composants Communities sont inclus dans un script et nécessitent donc un noeud adressable Sling pour prendre en charge les fonctionnalités Communities. [Les composantes](scf.md#add-or-include-a-communities-component) incluses sont appelées ressources non existantes (NER).

Les noeuds d’ombre fournissent un emplacement adressable Sling dans le référentiel.

>[!CAUTION]
>
>Comme le noeud fantôme a plusieurs utilisations, la présence d’un noeud fantôme *n’implique pas* que le composant est un NER.

### Emplacement de l&#39;Enregistrement {#storage-location}

Voici un exemple de noeud fantôme, qui utilise le composant [](http://localhost:4502/content/community-components/en/comments.html) Comments du Guide [des composants de la](components-guide.md)communauté :

* Le composant existe dans le référentiel local à l’adresse suivante :

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Le noeud fantôme correspondant existe dans le référentiel local à l’adresse suivante :

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Aucun UGC ne sera trouvé sous le noeud fantôme.

Le comportement par défaut consiste à configurer des noeuds fantômes sur une instance de publication chaque fois que la sous-arborescence correspondante est référencée pour une lecture ou une écriture.

Par exemple, supposons que le déploiement soit [MSRP](msrp.md) avec une batterie de publication TarMK.

Lorsqu’un [membre](users.md) publie l’UGC sur pub1 (stocké dans MongoDB), les noeuds d’ombre sont créés dans JCR sur pub1.

La première fois que l&#39;UGC est lu sur pub2, si rien n&#39;est configuré, le comportement par défaut est de créer les noeuds d&#39;ombre.

Si un comportement autre que celui par défaut est souhaité, il doit être configuré sur l’instance d’auteur et reporté sur toutes les instances de publication, ce qui est généralement un processus manuel.
