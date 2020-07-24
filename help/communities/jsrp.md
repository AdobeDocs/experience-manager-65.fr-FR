---
title: JSRP - Fournisseur de ressources d’Enregistrement JCR
seo-title: JSRP - Fournisseur de ressources d’Enregistrement JCR
description: JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
seo-description: JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: e7268e43620860b7a1f7aa0a1f1a54199dadcf17
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# JSRP - Fournisseur de ressources d’Enregistrement JCR {#jsrp-jcr-storage-resource-provider}

## A propos de JSRP {#about-jsrp}

Lorsque les AEM Communities utilisent JSRP comme option d’enregistrement (par défaut), le contenu de la communauté est stocké dans le JCR et le contenu généré par l’utilisateur (UGC) n’est accessible que depuis l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Configuration {#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option d’enregistrement pour UGC.

La console [Configuration de l&#39;](srp-config.md) Enregistrement permet de sélectionner la configuration d&#39;enregistrement par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Dans l’environnement d’auteur, pour accéder à la console de configuration de l’Enregistrement

* A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > Configuration des **[!UICONTROL Enregistrements]**

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Sélectionnez **[!UICONTROL Envoyer]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, pour s’assurer que la configuration identique est définie dans l’environnement de publication :

* A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
* Sélectionnez **[!UICONTROL Activer l’arborescence]** > Tracé **** de Début :

   * Naviguer jusqu’à `/conf/global/settings/community/srpc/`

* Sélectionner **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *les utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent saisis dans l’environnement de publication, consultez la page :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des incidents {#troubleshooting}

### UGC invisible dans JCR {#ugc-not-visible-in-jcr}

Assurez-vous que JSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option enregistrement. Par défaut, le fournisseur de ressources d’enregistrement est JSRP.

Sur toutes les instances d’AEM d’auteur et de publication, consultez de nouveau la console de configuration d’Enregistrement ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , cela signifie que le fournisseur d’enregistrements est JSRP.
   * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### UGC invisible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bug. L’une des caractéristiques de JSRP est que le contenu de la communauté saisi dans l’environnement de publication n’est visible que dans l’environnement de publication.

### UGC invisible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une instance de publication unique ou si une grappe de publication est déployée, suivez les instructions relatives à l’ [UGC invisible dans le JCR](#ugc-not-visible-in-jcr).

Si une batterie de publication est déployée, une caractéristique de JSRP est que le contenu de la communauté ne sera visible que sur l’instance de publication à laquelle il a été publié.

Pour que l’UGC soit visible à partir de n’importe quelle instance de publication, une grappe de publication est requise.
