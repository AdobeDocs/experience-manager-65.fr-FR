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
source-wordcount: '659'
ht-degree: 1%
---
# Mise à niveau vers AEM 6.5 Communities {#upgrading-to-aem-communities}

Selon la topologie et les fonctionnalités de chaque site, les actions suivantes peuvent être nécessaires lors de la mise à niveau vers AEM Communities 6.5 ou de l’installation du dernier pack de fonctionnalités.

Cette section est spécifique aux communautés et complète les informations fournies dans [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md) (plateforme).

## Mise à niveau à partir d’AEM 6.1 ou version ultérieure {#upgrading-from-aem-or-later}

### Réindexer Solr {#reindex-solr}

Lors de l’installation d’un nouveau pack de fonctionnalités Communities sur un déploiement configuré avec MSRP, il sera nécessaire de :

1. Installez le [dernier pack de fonctionnalités](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installez les [derniers fichiers de configuration Solr](/help/communities/msrp.md#upgrading).
1. Réindexer le MSRP
pour plus d&#39;informations, consultez la section [Outil de réindexation MSRP](/help/communities/msrp.md#msrp-reindex-tool).

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

Si du contenu créé par l’utilisateur préexistant doit être conservé, les moyens de le faire dépendent du déploiement stocké dans le contenu créé par l’utilisateur [On-Premise](#on-premise-storage) ou dans le [cloud Adobe](#adobe-cloud-storage).

### Adobe Cloud Storage {#adobe-cloud-storage}

Si le site mis à niveau a été configuré pour utiliser l’espace de stockage cloud d’Adobe, il peut sembler (incorrectement) que tout le contenu créé par l’utilisateur a été perdu, car les méthodes SRP ne pourront pas localiser le contenu créé par l’utilisateur préexistant dans l’ancien emplacement.

Ainsi, il est possible d’indiquer à ASRP d’utiliser `AEM 6.0 compatability-mode` pour accéder au contenu créé par l’utilisateur.

Pour toutes les instances d’auteur et de publication AEM 6.3 :

* Connectez-vous avec des droits d’administrateur.
* Configurez [&#x200B; ASRP &#x200B;](/help/communities/asrp.md).
* Pour rendre le contenu créé par l’utilisateur préexistant visible, procédez comme suit :

  * Accédez à la console web :

    * Par exemple, [https://&lt;hôte>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

    * Recherchez la configuration **AEM Communities Utilities**.
    * Sélectionnez pour développer le panneau de configuration :

      * *Décocher* `Cloud Storage`

      * Sélectionnez **Enregistrer**.

    ![utilitaires](assets/utilities.png)

### Stockage On-Premise {#on-premise-storage}

Si le site mis à niveau n’utilisait pas l’espace de stockage dans le cloud, tout contenu créé par l’utilisateur préexistant doit être converti conformément à la nouvelle structure introduite dans les communautés AEM 6.1 pour prendre en charge le magasin commun.

À cet effet, un outil de migration open source est disponible sur GitHub :
[Outil de migration du contenu créé par l’utilisateur &#x200B;](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Lors de la mise à niveau des communautés sociales d’AEM 6.0 vers AEM 6.3, de nombreuses API ont été réorganisées en différents packages. La plupart doivent être facilement résolus lors de l’utilisation d’un IDE pour la personnalisation des fonctionnalités de Communities.

Pour plus d’informations sur le package SocialUtils obsolète, consultez [Refactorisation de SocialUtils](/help/communities/socialutils.md).

Consultez également la section [Utilisation de Maven pour les communautés](/help/communities/maven.md).

### Aucun modèle de composant JSP {#no-jsp-component-templates}

Le [framework de composant social](/help/communities/scf.md) (SCF) utilise le langage de modèle [HandlebarsJS](https://handlebarsjs.com/) (HBS) au lieu de Pages de serveur Java (JSP) utilisées avant AEM 6.0.

Dans AEM 6.0, les composants JSP sont restés à côté des nouveaux composants de structure HBS au même emplacement, les composants HBS se trouvant généralement dans des sous-dossiers appelés « hbs ».

Depuis AEM 6.1, les composants JSP ont été complètement supprimés. Pour Communities, il est recommandé de remplacer toute utilisation des composants JSP par des composants SCF.

## Outil de migration du contenu créé par l’utilisateur AEM Communities {#aem-communities-ugc-migration-tool}

L’[outil de migration du contenu créé par l’utilisateur d’](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) est un outil de migration open source disponible sur GitHub. Il peut être personnalisé pour exporter du contenu créé par l’utilisateur à partir de versions antérieures des communautés sociales d’AEM et l’importer dans AEM Communities 6.1 ou une version ultérieure.

En plus de déplacer le contenu créé par l’utilisateur des versions antérieures, il est également possible d’utiliser l’outil pour déplacer le contenu créé par l’utilisateur d’un [SRP](/help/communities/working-with-srp.md) à un autre, comme de MSRP à DSRP.

## Mise à niveau à partir d’AEM 5.6.1 ou version antérieure {#upgrading-from-aem-or-earlier}

Conceptuellement, il existe trois générations de composants de communautés :

**Génération 1** : d’environ CQ 5.4 à AEM 5.6.0, il s’agit des composants **collab** qui stockaient le contenu créé par l’utilisateur dans le référentiel local à l’aide de la réplication pour synchroniser ce contenu entre les plateformes. D’autres différences concernent l’implémentation à l’aide de Java Server Pages (JSP) et la fonctionnalité de blog consistant à créer uniquement dans l’environnement de création.

**Gen 2** : d’AEM 5.6.1 à AEM 6.1, il s’agit d’un mélange de composants **collab** et **social**. AEM 6.0 a introduit la nouvelle [structure des composants sociaux](/help/communities/scf.md) (SCF) et AEM 6.2 a introduit un [magasin UGC commun](/help/communities/working-with-srp.md) où le contenu créé par l’utilisateur est accessible à l’aide d’un [fournisseur de ressources de stockage](/help/communities/srp.md) (SRP).

**Gen 3** : à partir d’AEM 6.2, il n’existe que les composants **sociaux**, implémentés dans SCF en tant que composants Handlebars (HBS), qui nécessitent un choix de SRP pour le contenu créé par l’utilisateur.
