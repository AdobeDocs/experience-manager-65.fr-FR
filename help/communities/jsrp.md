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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# JSRP - Fournisseur de ressources d&#39;Enregistrement JCR {#jsrp-jcr-storage-resource-provider}

## À propos de JSRP {#about-jsrp}

Lorsque AEM Communities utilise JSRP comme option d’enregistrement (valeur par défaut), le contenu de la communauté est stocké dans le JCR et le contenu généré par l’utilisateur (UGC) n’est accessible que depuis l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.

Voir aussi [Caractéristiques des options SRP](working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](topologies.md).

## Configuration {#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option d’enregistrement pour UGC.

La [console de configuration d&#39;Enregistrement](srp-config.md) permet de sélectionner la configuration d&#39;enregistrement par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Dans l’environnement d’auteur, pour accéder à la console de configuration de l’Enregistrement

* A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de l&#39;Enregistrement]**

* Sélectionnez **[!UICONTROL JCR Enregistrement Resource Provider (JSRP)]**

* Sélectionnez **[!UICONTROL Envoyer]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, pour s’assurer que la configuration identique est définie dans l’environnement de publication :

* A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
* Sélectionnez **[!UICONTROL Activer l&#39;arborescence]** > **[!UICONTROL chemin de Début]** :

   * Accédez à `/conf/global/settings/community/srpc/`

* Sélectionnez **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *les utilisateurs*, *les profils utilisateur* et *les groupes d’utilisateurs*, souvent saisis dans l’environnement de publication, consultez :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des incidents {#troubleshooting}

### UGC invisible dans le JCR {#ugc-not-visible-in-jcr}

Assurez-vous que JSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option enregistrement. Par défaut, le fournisseur de ressources d’enregistrement est JSRP.

Sur toutes les instances d’AEM création et de publication, revisitez la console de configuration de l’Enregistrement ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), cela signifie que le fournisseur d’enregistrement est JSRP.
   * Si le noeud srpc existe et contient le noeud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### UGC invisible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bug. L’une des caractéristiques de JSRP est que le contenu de la communauté saisi dans l’environnement de publication n’est visible que dans l’environnement de publication.

### UGC invisible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une instance de publication unique ou si une grappe de publication est déployée, suivez les instructions pour [UGC invisible dans JCR](#ugc-not-visible-in-jcr).

Si une batterie de publication est déployée, une caractéristique de JSRP est que le contenu de la communauté ne sera visible que sur l’instance de publication à laquelle il a été publié.

Pour que l’UGC soit visible à partir de n’importe quelle instance de publication, une grappe de publication est requise.
