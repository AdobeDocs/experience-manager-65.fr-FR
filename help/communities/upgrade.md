---
title: Mise à niveau vers AEM 6.5 Communities
seo-title: Upgrading to AEM 6.5 Communities
description: Comment mettre à niveau une version antérieure vers AEM 6.5 Communities
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 066a61a332aa620078740d36bd7f8689282fbf14
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 1%

---

# Mise à niveau vers AEM 6.5 Communities {#upgrading-to-aem-communities}

Selon la topologie et les fonctionnalités de chaque site, les actions suivantes peuvent être nécessaires lors de la mise à niveau vers AEM Communities 6.5 ou de l’installation du dernier Feature Pack.

Cette section est spécifique aux communautés et complète les informations fournies dans la section [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md) (plateforme).

## Mise à niveau à partir d’AEM 6.1 ou version ultérieure {#upgrading-from-aem-or-later}

### Réindexation Solr {#reindex-solr}

Lors de l’installation d’un nouveau Feature Pack Communities sur un déploiement configuré avec MSRP, il sera nécessaire de :

1. Installez le [dernier Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installez le [les derniers fichiers de configuration Solr](/help/communities/msrp.md#upgrading).
1. Réindexation MSRP - section [Outil de réindexation MSRP](/help/communities/msrp.md#msrp-reindex-tool).

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

Si le contenu généré par l’utilisateur préexistant doit être conservé, les moyens de le faire dépendent du stockage ou non du contenu stocké par le déploiement. [on-premise](#on-premise-storage) ou dans la variable [Adobe Cloud](#adobe-cloud-storage).

### Stockage dans le cloud Adobe {#adobe-cloud-storage}

Si le site mis à niveau a été configuré pour utiliser l’espace de stockage dans le cloud Adobe, il peut s’afficher (de manière incorrecte) comme si tout le contenu généré par l’utilisateur a été perdu, car les méthodes SRP ne pourront pas localiser le contenu créé par l’utilisateur existant à l’ancien emplacement.

Il est donc possible d’ordonner à ASRP d’utiliser `AEM 6.0 compatability-mode` pour accéder au contenu généré par l’utilisateur.

Pour toutes les instances de création et de publication AEM 6.3 :

* Connectez-vous avec les privilèges d’administrateur.
* Configurer [ASRP](/help/communities/asrp.md).
* Pour rendre visible le contenu créé par l’utilisateur existant, procédez comme suit :

   * Accédez à la console web :

      * Par exemple : [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localiser **Utilitaires AEM Communities** configuration.
      * Sélectionnez cette option pour développer le panneau de configuration :

         * *Décocher* `Cloud Storage`

         * Sélectionnez **Enregistrer**

      ![Utilitaires](assets/utilities.png)


### Stockage On-premise {#on-premise-storage}

Si le site mis à niveau n’a pas utilisé l’espace de stockage dans le cloud, tout contenu généré par l’utilisateur préexistant doit être converti pour se conformer à la nouvelle structure introduite dans AEM 6.1 Communities pour prendre en charge le magasin commun.

À cette fin, un outil de migration Open Source est disponible sur GitHub :
[Outil de migration UGC AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Lors de la mise à niveau d’AEM 6.0 communautés sociales vers AEM 6.3 communautés, sachez que de nombreuses API ont été réorganisées en différents packages. La plupart de ces problèmes doivent être facilement résolus lors de l’utilisation d’un IDE pour la personnalisation des fonctionnalités de Communities.

Pour plus d’informations sur le module SocialUtils obsolète, consultez la page [Refactorisation de SocialUtils](/help/communities/socialutils.md).

Voir aussi [Utilisation de Maven pour Communities](/help/communities/maven.md).

### Aucun modèle de composant JSP {#no-jsp-component-templates}

Le [structure des composants sociaux](/help/communities/scf.md) (SCF) utilise la variable [HandlebarsJS](https://handlebarsjs.com/) (HBS) langage de modèle à la place de Java Server Pages (JSP) utilisé avant AEM 6.0.

Dans AEM 6.0, les composants JSP sont restés aux côtés des nouveaux composants de structure HBS au même emplacement, les composants HBS se trouvant généralement dans des sous-dossiers appelés &quot;hbs&quot;.

À compter de la version AEM 6.1, les composants JSP ont été complètement supprimés. Pour Communities, il est recommandé de remplacer toute utilisation de composants JSP par des composants SCF.

## Outil de migration UGC AEM Communities {#aem-communities-ugc-migration-tool}

Le [Outil de migration UGC AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) est un outil de migration Open Source, disponible sur GitHub, qui peut être personnalisé pour exporter du contenu créé par l’utilisateur à partir de versions antérieures d’AEM communautés sociales et l’importer dans AEM Communities 6.1 ou version ultérieure.

En plus de déplacer le contenu créé par l’utilisateur des versions antérieures, il est également possible d’utiliser l’outil pour déplacer le contenu créé par l’utilisateur d’une version à l’autre. [SRP](/help/communities/working-with-srp.md) à un autre, comme de MSRP à DSRP.

## Mise à niveau à partir d’AEM 5.6.1 ou d’une version antérieure {#upgrading-from-aem-or-earlier}

Conceptuellement, il existe trois générations de composants de communautés :

**Gen 1**: Environ CQ 5.4 à AEM 5.6.0, voici la **collab** les composants qui ont stocké le contenu généré par l’utilisateur dans le référentiel local à l’aide de la réplication comme moyen de synchroniser le contenu créé par l’utilisateur sur toutes les plateformes. D’autres différences concernent l’implémentation à l’aide de Java Server Pages (JSP) ainsi que la fonctionnalité de blog consistant à créer uniquement dans l’environnement de création.

**Gen 2**: De AEM 5.6.1 à AEM 6.1, ceci est un mélange de **collab** et **social** composants. AEM 6.0 a introduit la nouvelle [structure des composants sociaux](/help/communities/scf.md) (SCF) et AEM 6.2 ont introduit une [magasin UGC commun](/help/communities/working-with-srp.md) où le contenu généré par l’utilisateur est accessible à l’aide d’une [fournisseur de ressources de stockage](/help/communities/srp.md) (SRP).

**Gen 3**: À partir de AEM version 6.2, il n’y a que **social** composants, implémentés dans SCF en tant que composants Handlebars (HBS) nécessitant un choix de SRP pour le contenu généré par l’utilisateur.
