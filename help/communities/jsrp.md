---
title: JSRP - Fournisseur de ressources de stockage JCR
seo-title: JSRP - Fournisseur de ressources de stockage JCR
description: Le JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
seo-description: Le JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - Fournisseur de ressources de stockage JCR {#jsrp-jcr-storage-resource-provider}

## A propos de JSRP {#about-jsrp}

Lorsque les communautés AEM utilisent JSRP comme option de stockage (valeur par défaut), le contenu de la communauté est stocké dans le JCR et le contenu généré par l’utilisateur (UGC) n’est accessible que depuis l’instance d’auteur ou de publication à laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est généralement mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance d’auteur.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Configuration{#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option de stockage pour l’UGC.

La console [Configuration du](srp-config.md) stockage permet de sélectionner la configuration de stockage par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Dans l’environnement d’auteur, pour accéder à la console Configuration de stockage

* A partir de la navigation globale : **[!UICONTROL Outils > Communautés > Configuration du stockage]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* Sélectionnez **[!UICONTROL Envoyer]**

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, pour vous assurer que la configuration identique est définie dans l’environnement de publication :

* Sur l&#39;auteur :

   * A partir de la navigation globale : **[!UICONTROL Outils > Déploiement > Réplication]**
   * Sélectionner **[!UICONTROL Activer l&#39;arborescence]**
   * **[!UICONTROL Chemin de début]**:

      * Naviguer jusqu’à `/conf/global/settings/community/srpc/`
   * Sélectionner **[!UICONTROL Activer]**


## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent entrés dans l’environnement de publication, consultez la page

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des incidents {#troubleshooting}

### UGC invisible dans JCR {#ugc-not-visible-in-jcr}

Vérifiez que JSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option de stockage. Par défaut, le fournisseur de ressources de stockage est JSRP.

Sur toutes les instances d’auteur et de publication AEM, consultez de nouveau la console Configuration du stockage ou vérifiez le référentiel AEM :

* dans JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , cela signifie que le fournisseur de stockage est JSRP
   * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut

### UGC invisible sur l’instance d’auteur {#ugc-not-visible-on-author-instance}

Ce n&#39;est pas un bug. L’une des caractéristiques du JSRP est que le contenu de la communauté entré dans l’environnement de publication ne sera visible que dans l’environnement de publication.

### UGC invisible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une instance de publication unique ou si une grappe de publication est déployée, suivez les instructions pour l’ [UGC non visible dans le JCR](#ugc-not-visible-in-jcr).

Si une batterie de publication est déployée, l’une des caractéristiques de JSRP est que le contenu de la communauté n’est visible que sur l’instance de publication à laquelle il a été publié.

Pour que l’UGC soit visible à partir de n’importe quelle instance de publication, une grappe de publication est requise.
