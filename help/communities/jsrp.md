---
title: JSRP - Fournisseur de ressources de stockage JCR
seo-title: JSRP - Fournisseur de ressources de stockage JCR
description: JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
seo-description: JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Administrator
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# JSRP - Fournisseur de ressources de stockage JCR {#jsrp-jcr-storage-resource-provider}

## À propos de JSRP {#about-jsrp}

Lorsqu’AEM Communities utilise JSRP comme option de stockage (valeur par défaut), le contenu de la communauté est stocké dans JCR et le contenu généré par l’utilisateur est accessible uniquement à partir de l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.

Voir aussi [Caractéristiques des options SRP](working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](topologies.md).

## Configuration {#configuration}

### Sélectionnez JSRP {#select-jsrp}

Par défaut, JSRP est l’option de stockage du contenu généré par l’utilisateur.

La [console Configuration du stockage](srp-config.md) permet de sélectionner la configuration du stockage par défaut, qui identifie l’implémentation de la SRP à utiliser.

Dans l’environnement de création, pour accéder à la console Configuration de stockage

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de stockage]**

* Sélectionnez **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Sélectionnez **[!UICONTROL Envoyer]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, assurez-vous que la configuration identique est définie dans l’environnement de publication :

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
* Sélectionnez **[!UICONTROL Activer l’arborescence]** > **[!UICONTROL Chemin de début]** :

   * Accédez à `/conf/global/settings/community/srpc/`

* Sélectionnez **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les *profils utilisateur* et les *groupes d’utilisateurs*, souvent renseignés dans l’environnement de publication, consultez :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des problèmes {#troubleshooting}

### UGC invisible dans JCR {#ugc-not-visible-in-jcr}

Vérifiez que JSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l&#39;option de stockage. Par défaut, le fournisseur de ressources de stockage est JSRP.

Sur toutes les instances d’AEM de création et de publication, consultez à nouveau la console Configuration de stockage ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), cela signifie que le fournisseur de stockage est JSRP.
   * Si le noeud srpc existe et contient le noeud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### Contenu généré par l’utilisateur non visible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bogue. L’une des caractéristiques de JSRP est que le contenu de la communauté saisi dans l’environnement de publication ne sera visible que dans l’environnement de publication.

### Contenu généré par l’utilisateur non visible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une instance de publication unique ou si une grappe de publication est déployée, suivez les instructions pour [UGC non visible dans JCR](#ugc-not-visible-in-jcr).

Si une ferme de publication est déployée, une caractéristique de JSRP est que le contenu de la communauté n’est visible que sur l’instance de publication à laquelle il a été publié.

Pour que le contenu créé par l’utilisateur soit visible à partir de n’importe quelle instance de publication, un cluster de publication est requis.
