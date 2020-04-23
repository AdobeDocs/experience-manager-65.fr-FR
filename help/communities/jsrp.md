---
title: 'JSRP - JCR  fournisseur de ressources '
seo-title: 'JSRP - JCR  fournisseur de ressources '
description: Le JSRP est généralement mieux adapté pour la démonstration ou le développement  le  d’une instance de publication et d’une instance d’auteur
seo-description: Le JSRP est généralement mieux adapté pour la démonstration ou le développement  le  d’une instance de publication et d’une instance d’auteur
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# JSRP - JCR  fournisseur de ressources {#jsrp-jcr-storage-resource-provider}

## A propos de JSRP {#about-jsrp}

Lorsque les communautés AEM utilisent JSRP comme option de  de  (valeur par défaut), le contenu de la communauté est stocké dans le JCR et le contenu généré par l’utilisateur (UGC) n’est accessible que depuis l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est généralement mieux adapté pour la démonstration ou le développement  le  d’une instance de publication et d’une instance d’auteur.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Configuration{#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option   pour UGC.

La console [de configuration de  de](srp-config.md) permet de sélectionner la configuration de par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Dans le de  de l’auteur , pour accéder à la console de configuration des 

* A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL de configuration des]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* Sélectionnez **[!UICONTROL Envoyer]**

### Publication de la configuration {#publishing-the-configuration}

Alors que JSRP est la configuration par défaut, pour vous assurer que la configuration identique est définie dans le  de publication  :

* Sur l&#39;auteur :

   * A partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
   * Sélectionnez **[!UICONTROL Activer l’arborescence]** > Chemin **[!UICONTROL de]**:

      * Naviguer jusqu’à `/conf/global/settings/community/srpc/`
   * Sélectionner **[!UICONTROL Activer]**


## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les *des* utilisateurs et les groupes *d’* utilisateurs, souvent saisis dans le  de publication, consultez la page :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des incidents {#troubleshooting}

### UGC invisible dans JCR {#ugc-not-visible-in-jcr}

Assurez-vous que JSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option de  de . Par défaut, le fournisseur de ressources   est JSRP.

Sur toutes les instances d’AEM de création et de publication, consultez de nouveau la console de configuration   ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , cela signifie que le fournisseur de  de  est JSRP.
   * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### UGC invisible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bug. L’une des caractéristiques de JSRP est que le contenu de la communauté saisi dans le de publication  ne sera visible que dans le de publication .

### UGC invisible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une instance de publication unique ou si une grappe de publication est déployée, suivez les instructions pour l’ [UGC non visible dans le JCR](#ugc-not-visible-in-jcr).

Si une batterie de publication est déployée, l’une des caractéristiques de JSRP est que le contenu de la communauté n’est visible que sur l’instance de publication à laquelle il a été publié.

Pour que l’UGC soit visible à partir de n’importe quelle instance de publication, une grappe de publication est requise.
