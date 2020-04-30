---
title: Mise à niveau vers les communautés AEM 6.5
seo-title: Mise à niveau vers les communautés AEM 6.5
description: Mise à niveau d’une version antérieure vers AEM 6.4 Communities
seo-description: Mise à niveau d’une version antérieure vers AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# Mise à niveau vers les communautés AEM 6.5 {#upgrading-to-aem-communities}

Selon la topologie et les fonctionnalités de chaque site, les actions suivantes peuvent être nécessaires lors de la mise à niveau vers AEM Communities 6.5 ou de l’installation du dernier Feature Pack.

Cette section est spécifique aux communautés et complète les informations fournies dans [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md) (plateforme).

## Mise à niveau à partir d’AEM 6.1 ou version ultérieure {#upgrading-from-aem-or-later}

### Réindexer Solr {#reindex-solr}

Lors de l’installation d’un nouveau Feature Pack de communautés sur un déploiement configuré avec MSRP, vous devez effectuer les opérations suivantes :

1. Installez le [dernier Feature Pack](/help/communities/deploy-communities.md#latestfeaturepack).
1. Installez les [derniers fichiers](/help/communities/msrp.md#upgrading)de configuration Solr.
1. Réindexez MSRPvoir la section Outil [de réindexation](/help/communities/msrp.md#msrp-reindex-tool)MSRP.

### Enablement 2.0 {#enablement}

A compter de la version 6.3 d’AEM, les fonctionnalités d’activation ne stockent plus les informations  dans MySQL. La dépendance MySQL est présente uniquement pour le suivi du contenu SCORM.

Contactez le service à la [clientèle](https://helpx.adobe.com/fr/marketing-cloud/contact-support.html) pour obtenir de l’aide sur la migration de contenu à partir d’Activation 1.0.

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

S’il est nécessaire de conserver les fichiers UGC préexistants, les moyens d’y parvenir dépendent du stockage [local](#on-premise-storage) ou dans le cloud [](#adobe-cloud-storage)Adobe du déploiement.

### Adobe Cloud  {#adobe-cloud-storage}

Si le site mis à niveau a été configuré pour utiliser Adobe Cloud  , il se peut qu’il s’affiche (incorrectement) comme si l’ensemble de l’UGC avait été perdu car les méthodes SRP ne pourront pas localiser l’UGC préexistant à l’ancien emplacement.

Ainsi, il est possible de demander à l&#39;ASRP d&#39;utiliser `AEM 6.0 compatability-mode` l&#39;UGC pour accéder à l&#39;UGC.

Pour toutes les instances d’auteur et de publication AEM 6.3 :

* Connectez-vous avec des droits d’administrateur.
* Configurez [ASRP](/help/communities/asrp.md).
* Pour rendre visible l’UGC préexistant, procédez comme suit :

   * Accédez à la console Web :

      * Par exemple, [https://&lt;hôte>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localisez la configuration des utilitaires **des communautés** AEM.
      * Sélectionnez pour développer le panneau de configuration :

         * *Désélectionner*`Cloud Storage`

         * Sélectionnez **Enregistrer**
      ![chlimage_1-176](assets/chlimage_1-176.png)


###  sur site {#on-premise-storage}

Si le site mis à niveau n’utilisait pas le  de cloud , tout fichier UGC préexistant doit être converti pour être conforme à la nouvelle structure introduite dans les communautés AEM 6.1 pour prendre en charge le magasin commun.

À cette fin, un outil de migration Open Source est disponible sur GitHub :
Outil de migration UGC[AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API Java {#java-apis}

Lors de la mise à niveau des communautés sociales AEM 6.0 vers les communautés AEM 6.3, sachez que de nombreuses API ont été réorganisées en différents packages. La plupart d&#39;entre elles doivent être facilement résolues lors de l&#39;utilisation d&#39;un IDE pour la personnalisation des fonctionnalités des communautés.

Pour plus d’informations sur le package SocialUtils obsolète, consultez [SocialUtils Refactoring](/help/communities/socialutils.md).

Voir aussi [Utilisation de Maven pour les communautés](/help/communities/maven.md).

### Aucun modèle de composant JSP {#no-jsp-component-templates}

Le cadre [du composant](/help/communities/scf.md) social (SCF) utilise le langage de modèle [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) à la place du JSP (Java Server Pages) utilisé avant AEM 6.0.

Dans AEM 6.0, les composants JSP sont restés aux côtés des nouveaux composants de la structure HBS au même emplacement, les composants HBS étant généralement situés dans des sous-dossiers nommés &quot;hbs&quot;.

Depuis AEM 6.1, les composants JSP ont été complètement supprimés. Pour les communautés, il est recommandé de remplacer toute utilisation de composants JSP par des composants SCF.

## Outil de migration UGC des communautés AEM {#aem-communities-ugc-migration-tool}

L’outil [de migration UGC des communautés](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) AEM est un outil de migration Open Source disponible sur GitHub. Il peut être personnalisé pour exporter l’UGC à partir des versions antérieures des communautés sociales AEM et l’importer dans les communautés AEM 6.1 ou une version ultérieure.

En plus de déplacer l&#39;UGC des versions antérieures, il est également possible d&#39;utiliser l&#39;outil pour déplacer l&#39;UGC d&#39;un [SRP](/help/communities/working-with-srp.md) à un autre, par exemple du MSRP vers le DSRP.

## Mise à niveau à partir d’AEM 5.6.1 ou version antérieure {#upgrading-from-aem-or-earlier}

D&#39;un point de vue conceptuel, il existe trois générations de composantes communautaires :

**Gen 1**: D’environ CQ 5.4 à AEM 5.6.0, il s’agit des composants **collab** qui stockaient l’UGC dans le référentiel local à l’aide de la réplication comme moyen de synchroniser l’UGC sur les plateformes. D&#39;autres différences concernent l&#39;implémentation à l&#39;aide de Java Server Pages (JSP) ainsi que la fonctionnalité de blog consistant à créer uniquement dans l&#39;auteur  le .

**Gen 2**: D’AEM 5.6.1 à AEM 6.1, il s’agit d’un mélange de composants **collab** et **sociaux** . AEM 6.0 a introduit le nouveau cadre [des composants](/help/communities/scf.md) sociaux (SCF) et AEM 6.2 a introduit une boutique [UGC](/help/communities/working-with-srp.md) commune dans laquelle l’accès à l’UGC est effectué à l’aide d’un fournisseur [de ressources](/help/communities/srp.md) de (SRP).

**Gen 3**: A partir d’AEM 6.2, il n’existe que des composants **sociaux** , implémentés dans SCF en tant que composants HBS (Handlebars) nécessitant un choix de SRP pour UGC.
