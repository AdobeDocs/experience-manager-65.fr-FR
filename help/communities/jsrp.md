---
title: JSRP - Fournisseur de ressources de stockage JCR
description: JSRP est mieux adapté aux environnements de démonstration ou de développement d’une instance Publish et d’une instance d’auteur.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---

# JSRP - Fournisseur de ressources de stockage JCR {#jsrp-jcr-storage-resource-provider}

## À propos de JSRP {#about-jsrp}

Lorsqu’AEM Communities utilise JSRP comme option de stockage (valeur par défaut), le contenu de la communauté est stocké dans le JCR et le contenu généré par l’utilisateur est accessible uniquement à partir de l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est mieux adapté aux environnements de démonstration ou de développement d’une instance Publish et d’une instance d’auteur.

Voir aussi [Caractéristiques des options SRP](working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](topologies.md).

## Configuration {#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option de stockage pour le contenu généré par l’utilisateur.

La [console de configuration de stockage](srp-config.md) permet de sélectionner la configuration de stockage par défaut, qui identifie l’implémentation de la SRP à utiliser.

Dans l’environnement de création, pour accéder à la console Configuration de stockage

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de stockage]**

* Sélectionnez **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Sélectionnez **[!UICONTROL Envoyer]**.

![jsrp-configuration](assets/jsrp-configuration.png)

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, assurez-vous que la configuration identique est définie dans l’environnement de publication :

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
* Sélectionnez **[!UICONTROL Activer l’arborescence]** > **[!UICONTROL Chemin de début]** :

   * Accédez à `/conf/global/settings/community/srpc/`

* Sélectionnez **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les *profils utilisateur* et les *groupes d’utilisateurs*, souvent entrés dans l’environnement de publication, consultez :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des problèmes {#troubleshooting}

### UGC invisible dans JCR {#ugc-not-visible-in-jcr}

Assurez-vous que JSRP a été configuré pour être le fournisseur par défaut en vérifiant la configuration de l&#39;option de stockage. Par défaut, le fournisseur de ressources de stockage est JSRP.

Sur toutes les instances d’AEM d’auteur et d’Publish, consultez à nouveau la console Configuration de stockage ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Il ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), cela signifie que le fournisseur de stockage est JSRP.
   * Si le noeud srpc existe et contient le noeud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### Contenu généré par l’utilisateur non visible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bogue. L’une des caractéristiques de JSRP est que le contenu de la communauté saisi dans l’environnement de publication n’est visible que dans l’environnement Publish.

### Contenu généré par l’utilisateur non visible sur l’instance Publish {#ugc-not-visible-on-publish-instance}

Si une instance Publish unique ou si une grappe de publication est déployée, suivez les instructions pour [UGC non visible dans JCR](#ugc-not-visible-in-jcr).

Si une ferme de publication est déployée, une caractéristique de JSRP est que le contenu de la communauté n’est visible que sur l’instance Publish à laquelle il a été publié.

Pour que le contenu généré par l’utilisateur soit visible à partir de n’importe quelle instance Publish, un cluster de publication est requis.
