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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Présentation du fournisseur de ressources de stockage {#storage-resource-provider-overview}

## Présentation {#introduction}

Depuis la version 6.1 des Communautés AEM, le contenu de la communauté, communément appelé contenu généré par l’utilisateur (UGC), est stocké dans un seul magasin commun fourni par un fournisseur [de ressources de](working-with-srp.md) stockage (SRP).

Il existe plusieurs options SRP, qui accèdent toutes à l’UGC via une nouvelle interface Communautés AEM, l’API [](srp-and-ugc.md) SocialResourceProvider (API SRP), qui comprend toutes les opérations de création, de lecture, de mise à jour et de suppression (CRUD).

Tous les composants SCF sont implémentés à l’aide de l’API SRP, ce qui permet de développer le code sans connaître la topologie [](topologies.md) sous-jacente ou l’emplacement de l’UGC.

***L’API SocialResourceProvider est disponible uniquement pour les clients titulaires d’une licence des communautés AEM.***

>[!NOTE]
>
>**Composants** personnalisés : Pour les clients disposant d’une licence pour les communautés AEM, l’API SRP est disponible pour les développeurs de composants personnalisés en vue d’accéder à l’UGC sans tenir compte de la topologie sous-jacente. Voir [SRP et UGC Essentials](srp-and-ugc.md).

Voir également:

* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d&#39;utilitaires SRP
* [Accès UGC avec SRP](accessing-ugc-with-srp.md) - Instructions de codage
* [Réfactorisation](socialutils.md) de SocialUtils - Association des méthodes d’utilitaire obsolètes aux méthodes d’utilitaire SRP actuelles

## A propos du référentiel {#about-the-repository}

Pour comprendre SRP, il est utile de comprendre le rôle du référentiel AEM (OAK) dans un site de la communauté AEM.

**Java Content Repository (JCR)** Cette norme définit un modèle de données et une interface de programmation d’applications (API[](https://jackrabbit.apache.org/jcr/jcr-api.html)JCR) pour les référentiels de contenu. Il combine les caractéristiques des systèmes de fichiers conventionnels avec celles des bases de données relationnelles et ajoute un certain nombre de fonctionnalités supplémentaires dont les applications de contenu ont souvent besoin.

Une implémentation du JCR est le référentiel AEM, OAK.

**Apache Jackrabbit Oak (OAK)**[OAK](../../help/sites-deploying/platform.md) est une implémentation de JCR 2.0 qui est un système de stockage de données spécialement conçu pour les applications axées sur le contenu. Il s’agit d’un type de base de données hiérarchique conçue pour les données non structurées et semi-structurées. Le référentiel stocke le contenu affiché aux utilisateurs et l’ensemble du code, des modèles et des données internes utilisés par l’application. L’interface utilisateur d’accès au contenu est [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR et OAK sont généralement utilisés pour faire référence au référentiel AEM.

Une fois le contenu du site développé dans l’environnement d’auteur privé, il doit être copié dans l’environnement de publication public. Cela se fait souvent au moyen d’une opération appelée *[réplication](deploy-communities.md#replication-agents-on-author)*. Cela se produit sous le contrôle de l’auteur/développeur/administrateur.

Pour l’UGC, le contenu est saisi par les visiteurs enregistrés du site (membres de la communauté) dans l’environnement de publication public. Ça se passe de manière aléatoire.

Aux fins de gestion et de création de rapports, il est utile d&#39;avoir accès à l&#39;UGC depuis l&#39;environnement d&#39;auteur privé. Avec SRP, l’accès à l’UGC à partir de l’auteur est plus cohérent et performant, car la réplication inversée de la publication à l’auteur n’est pas nécessaire.

## À propos de SRP {#about-srp}

Lorsque l’UGC est enregistré dans un stockage partagé, il existe une instance unique du contenu des membres qui peut, dans la plupart des déploiements, être accessible à partir des environnements d’auteur et de publication. Quel que soit le choix SRP (MSRP, ASRP, JSRP), tous doivent être accessibles par programmation avec l’API SRP.

>[!NOTE]
>
>Voir [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code et des détails supplémentaires.
>
>Voir [Accès UGC avec SRP](accessing-ugc-with-srp.md) pour connaître les meilleures pratiques en matière de codage.

### ASRP {#asrp}

Dans le cas d’ASRP, l’UGC n’est pas stockée dans le JCR, mais dans un service cloud hébergé et géré par Adobe. Les fichiers UGC stockés dans ASRP ne peuvent être ni affichés avec CRXDE Lite, ni accessibles à l’aide de l’API JCR.

Voir [ASRP - Fournisseur](asrp.md)de ressources de stockage Adobe.

Il n&#39;est pas possible pour les développeurs d&#39;accéder directement à l&#39;UGC.

ASRP utilise Adobe Cloud pour les requêtes.

### MSRP {#msrp}

Dans le cas de MSRP, UGC n’est pas stocké dans JCR, il est stocké dans MongoDB. L’UGC stocké dans MSRP ne peut être ni affiché avec CRXDE Lite, ni accessible à l’aide de l’API JCR.

See [MSRP - MongoDB Storage Resource Provider](msrp.md).

Bien que MSRP soit comparable à ASRP, puisque toutes les instances de serveur AEM accèdent au même UGC, il est possible d’utiliser des outils courants pour accéder directement à l’UGC stocké dans MongoDB.

MSRP utilise Solr pour les requêtes.

### JSRP {#jsrp}

JSRP est le fournisseur par défaut pour accéder à l’ensemble des fichiers UGC sur une seule instance AEM. Il permet de découvrir rapidement les communautés AEM 6.1 sans avoir à configurer MSRP ou ASRP.

Voir [JSRP - Fournisseur](jsrp.md)de ressources de stockage JCR.

Dans le cas du JSRP, alors que l’UGC est stockée dans le JCR et accessible via CRXDE Lite et l’API JCR, il est vivement recommandé de ne jamais utiliser l’API JCR pour ce faire, faute de quoi les modifications futures peuvent affecter le code personnalisé.

En outre, le référentiel pour les environnements d’auteur et de publication n’est pas partagé. Alors qu’un cluster d’instances de publication génère un référentiel de publication partagé, l’UGC saisi lors de la publication ne sera pas visible sur l’auteur, ce qui empêche la gestion de l’UGC à partir de l’auteur. L’UGC n’est conservée que dans le référentiel AEM (JCR) de l’instance sur laquelle elle a été entrée.

JSRP utilise les indices Oak pour les requêtes.

## A propos des noeuds fantômes dans JCR {#about-shadow-nodes-in-jcr}

Les noeuds fantômes, qui imitent le chemin d’accès à UGC, existent dans le référentiel local pour deux raisons :

1. [Contrôle d&#39;accès (ACL](#for-access-control-acls))
1. [Ressources non existantes (NER)](#for-non-existing-resources-ners)

Quelle que soit l’implémentation SRP, l’UGC réel ne sera *pas *visible au même emplacement que le noeud fantôme.

### Pour le contrôle d&#39;accès (ACL) {#for-access-control-acls}

Certaines implémentations SRP, telles que ASRP et MSRP, stockent le contenu de la communauté dans des bases de données qui ne fournissent aucune vérification ACL. Les noeuds d’ombre fournissent un emplacement dans le référentiel local auquel les ACL peuvent être appliquées.

A l’aide de l’API SRP, toutes les options SRP effectuent la même vérification de l’emplacement de l’ombre avant toutes les opérations CRUD.

La vérification ACL utilise une méthode utilitaire qui renvoie un chemin approprié pour vérifier les autorisations appliquées au fichier UGC de la ressource.

Voir [SRP et UGC Essentials](srp-and-ugc.md) pour obtenir un exemple de code.

### Pour les ressources non existantes (NER) {#for-non-existing-resources-ners}

Certains composants Communities sont inclus dans un script et nécessitent donc un noeud adressable Sling pour prendre en charge les fonctionnalités Communities. [Les composants](scf.md#add-or-include-a-communities-component) inclus sont appelés ressources non existantes.

Les noeuds d’ombre fournissent un emplacement adressable Sling dans le référentiel.

>[!CAUTION]
>
>Le noeud fantôme ayant plusieurs utilisations, la présence d’un noeud fantôme *n’implique pas* que le composant soit un NER.

### Emplacement de stockage {#storage-location}

Voici un exemple de noeud fantôme, à l’aide du composant [](http://localhost:4502/content/community-components/en/comments.html) Commentaires du Guide [des composants de la](components-guide.md)communauté :

* Le composant existe dans le référentiel local à l’adresse suivante :

   /content/community-components/fr/commentaires/jcr:content/content/includable/commentaires

* Le noeud fantôme correspondant existe dans le référentiel local à l’adresse suivante :

   /content/usergenerated/content/community-components/fr/commentaires/jcr:content/content/includable/commentaires

Aucune UGC ne sera trouvée sous le noeud fantôme.

Le comportement par défaut consiste à configurer des noeuds fantômes sur une instance de publication chaque fois que la sous-arborescence appropriée est référencée pour une lecture ou une écriture.

Par exemple, supposons que le déploiement soit [MSRP](msrp.md) avec une batterie de publication TarMK.

Lorsqu’un [membre](users.md) publie l’UGC sur pub1 (stocké dans MongoDB), les noeuds d’ombre sont créés dans JCR sur pub1.

La première fois que l’UGC est lu sur pub2, si rien n’est configuré, le comportement par défaut est de créer les noeuds d’ombre.

Si vous souhaitez autre chose que le comportement par défaut, vous devez le configurer sur l’instance d’auteur et l’étendre à toutes les instances de publication, ce qui est généralement un processus manuel.
