---
title: Mise à niveau vers AEM 6.5 Communities
description: Mise à niveau d’une version antérieure vers AEM 6.5 Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Mise à niveau vers AEM 6.5 Communities {#upgrading-to-aem-communities}

Selon la topologie et les fonctionnalités de chaque site, les actions suivantes peuvent être nécessaires lors de la mise à niveau vers AEM Communities 6.5 ou de l’installation du dernier Feature Pack.

Cette section est spécifique à Communities et complète les informations fournies dans [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md) (plateforme).

## Mise à niveau à partir d’AEM 6.1 ou version ultérieure {#upgrading-from-aem-or-later}

### Réindexation Solr {#reindex-solr}

Lors de l’installation d’un nouveau Feature Pack Communities sur un déploiement configuré avec MSRP, il sera nécessaire de :

1. Installez le [dernier Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installez les [derniers fichiers de configuration Solr](/help/communities/msrp.md#upgrading).
1. Réindexation MSRP
Voir la section [Outil de réindexation MSRP](/help/communities/msrp.md#msrp-reindex-tool).

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

Si le contenu généré par l’utilisateur préexistant doit être conservé, les moyens à mettre en oeuvre dépendent du stockage du contenu créé par l’utilisateur [on-premise](#on-premise-storage) dans le [cloud d’Adobe](#adobe-cloud-storage).

### Stockage dans le cloud Adobe {#adobe-cloud-storage}

Si le site mis à niveau a été configuré pour utiliser l’espace de stockage dans le cloud Adobe, il peut s’afficher (de manière incorrecte) comme si tout le contenu généré par l’utilisateur a été perdu, car les méthodes SRP ne pourront pas localiser le contenu créé par l’utilisateur existant à l’ancien emplacement.

Il existe donc la possibilité de demander à ASRP d’utiliser `AEM 6.0 compatability-mode` pour accéder au contenu créé par l’utilisateur.

Pour toutes les instances de création et de publication AEM 6.3 :

* Connectez-vous avec les privilèges d’administrateur.
* Configurez [ASRP](/help/communities/asrp.md).
* Pour rendre visible le contenu créé par l’utilisateur existant, procédez comme suit :

   * Accédez à la console web :

      * Par exemple, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Recherchez la configuration **AEM Communities Utilities** .
      * Sélectionnez cette option pour développer le panneau de configuration :

         * *Décocher* `Cloud Storage`

         * Sélectionnez **Enregistrer**.

     ![Utilitaires](assets/utilities.png)

### Stockage On-premise {#on-premise-storage}

Si le site mis à niveau n’a pas utilisé l’espace de stockage dans le cloud, tout contenu généré par l’utilisateur préexistant doit être converti pour se conformer à la nouvelle structure introduite dans AEM 6.1 Communities pour prendre en charge le magasin commun.

À cette fin, un outil de migration Open Source est disponible sur GitHub :
[Outil de migration AEM Communities UGC](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Lors de la mise à niveau d’AEM 6.0 communautés sociales vers AEM 6.3 Communities, de nombreuses API ont été réorganisées en différents packages. La plupart de ces problèmes doivent être facilement résolus lors de l’utilisation d’un IDE pour la personnalisation des fonctionnalités de Communities.

Pour plus d’informations sur le package obsolète SocialUtils, consultez la page [Refactorisation de SocialUtils](/help/communities/socialutils.md).

Voir aussi [Utilisation de Maven pour Communities](/help/communities/maven.md).

### Aucun modèle de composant JSP {#no-jsp-component-templates}

Le [framework de composant social](/help/communities/scf.md) (SCF) utilise le langage de modèle [HandlebarsJS](https://handlebarsjs.com/) (HBS) à la place des pages de serveur Java (JSP) utilisées avant AEM 6.0.

Dans AEM 6.0, les composants JSP sont restés aux côtés des nouveaux composants de structure HBS au même emplacement, les composants HBS se trouvant généralement dans des sous-dossiers appelés &quot;hbs&quot;.

À compter de la version AEM 6.1, les composants JSP ont été complètement supprimés. Pour Communities, il est recommandé de remplacer toute utilisation de composants JSP par des composants SCF.

## Outil de migration UGC AEM Communities {#aem-communities-ugc-migration-tool}

L’ [outil de migration du contenu créé par l’utilisateur AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) est un outil de migration open source disponible sur GitHub qui peut être personnalisé pour exporter le contenu créé par l’utilisateur à partir de versions antérieures de communautés de réseaux sociaux et l’importer dans AEM Communities 6.1 ou version ultérieure.

En plus de déplacer le contenu généré par l’utilisateur des versions antérieures, il est également possible d’utiliser l’outil pour déplacer le contenu créé par l’utilisateur d’un [SRP](/help/communities/working-with-srp.md) à un autre, comme de MSRP à DSRP.

## Mise à niveau à partir d’AEM 5.6.1 ou d’une version antérieure {#upgrading-from-aem-or-earlier}

Sur le plan conceptuel, il existe trois générations de composants de communautés :

**Gen 1** : Environ CQ 5.4 à AEM 5.6.0, il s’agit des composants **collab** qui ont stocké le contenu créé par l’utilisateur dans le référentiel local à l’aide de la réplication comme moyen de synchroniser le contenu créé par l’utilisateur sur plusieurs plateformes. D’autres différences concernent l’implémentation à l’aide de Java Server Pages (JSP) et la fonction de blog consistant à créer uniquement dans l’environnement de création.

**Gen 2** : de AEM 5.6.1 à AEM 6.1, il s’agit d’un mélange de **collab** et de **social** composants. AEM 6.0 a introduit le nouveau [framework de composant social](/help/communities/scf.md) (SCF) et AEM 6.2 a introduit un [magasin UGC commun](/help/communities/working-with-srp.md) où l’UGC est accessible à l’aide d’un [fournisseur de ressources de stockage](/help/communities/srp.md) (SRP).

**Gen 3** : à partir de la version 6.2 d’AEM, il n’y a que des composants **social**, implémentés dans SCF en tant que composants Handlebars (HBS) nécessitant un choix de SRP pour le contenu généré par l’utilisateur.
