---
title: JSRP - Fournisseur de ressources de stockage JCR
description: JSRP est mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance de création
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%
---
# JSRP - Fournisseur de ressources de stockage JCR {#jsrp-jcr-storage-resource-provider}

## À propos de JSRP {#about-jsrp}

Lorsqu’AEM Communities utilise JSRP comme option de stockage (valeur par défaut), le contenu de la communauté est stocké dans le JCR et le contenu créé par l’utilisateur n’est accessible qu’à partir de l’instance de création ou de publication vers laquelle il a été publié.

En raison de la simplicité du déploiement, JSRP est mieux adapté aux environnements de démonstration ou de développement d’une instance de publication et d’une instance de création.

Consultez également les sections [Caractéristiques des options SRP](working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](topologies.md).

## Configuration {#configuration}

### Sélectionner JSRP {#select-jsrp}

Par défaut, JSRP est l’option de stockage pour le contenu créé par l’utilisateur.

La [console de configuration du stockage](srp-config.md) permet de sélectionner la configuration de stockage par défaut, qui identifie l’implémentation de SRP à utiliser.

Dans l’environnement de création, pour accéder à la console de configuration du stockage

* À partir de la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration du stockage]**

* Sélectionnez **[!UICONTROL Fournisseur de ressources de stockage JCR (JSRP)]**

* Sélectionnez **[!UICONTROL Envoyer]**.

![jsrp-configuration](assets/jsrp-configuration.png)

### Publication de la configuration {#publishing-the-configuration}

Bien que JSRP soit la configuration par défaut, pour vous assurer que la configuration identique est définie dans l’environnement de publication :

* Dans la navigation globale : **[!UICONTROL Outils]** > **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**
* Sélectionnez **[!UICONTROL Activer l’arborescence]** > **[!UICONTROL Démarrer le chemin]** :

  * Accéder à `/conf/global/settings/community/srpc/`

* Sélectionnez **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, *profils utilisateur* et *groupes d’utilisateurs*, souvent saisis dans l’environnement de publication, consultez :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Résolution des problèmes {#troubleshooting}

### Contenu créé par l’utilisateur non visible dans JCR {#ugc-not-visible-in-jcr}

Assurez-vous que JSRP a été configuré en tant que fournisseur par défaut en vérifiant la configuration de l’option de stockage . Par défaut, le fournisseur de ressources de stockage est JSRP.

Sur toutes les instances d’auteur et de publication AEM, accédez de nouveau à la console de configuration du stockage ou vérifiez le référentiel AEM :

* Dans JCR, si [/conf/global/settings/community &#x200B;](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

  * Il ne contient pas de nœud [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), ce qui signifie que le fournisseur de stockage est JSRP.
  * Si le nœud srpc existe et contient le nœud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir JSRP comme fournisseur par défaut.

### Contenu créé par l’utilisateur non visible sur l’instance de création {#ugc-not-visible-on-author-instance}

Ce n’est pas un bug. Une caractéristique de JSRP est que le contenu de la communauté saisi dans l’environnement de publication n’est visible que dans l’environnement de publication.

### Contenu créé par l’utilisateur non visible sur l’instance de publication {#ugc-not-visible-on-publish-instance}

Si une seule instance de publication ou un cluster de publication est déployé, suivez les instructions pour [Contenu créé par l’utilisateur non visible dans JCR](#ugc-not-visible-in-jcr).

Si une ferme de publication est déployée, l’une des caractéristiques de JSRP est que le contenu de la communauté n’est visible que sur l’instance de publication sur laquelle il a été publié.

Pour que le contenu créé par l’utilisateur soit visible à partir de toute instance de publication, un cluster de publication est requis.
