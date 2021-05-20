---
title: Stockage   Configuration
seo-title: Stockage   Configuration
description: Accès à la console de configuration de stockage
seo-description: Accès à la console de configuration de stockage
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Administrator
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---

# Configuration du stockage {#storage-configuration}

La configuration du stockage est le moyen d’identifier le stockage choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC).

Ce paramètre informe le code AEM Communities sur l’implémentation du fournisseur de ressources de stockage (SRP) à utiliser lors de l’accès au contenu créé par l’utilisateur et doit refléter la topologie définie lors du déploiement d’AEM.

Pour une discussion sur les options de stockage et les topologies de déploiement, consultez :

* [Community Content Store](working-with-srp.md)
* [Topologies recommandées](topologies.md)

## Console de configuration de stockage {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Dans l’environnement de création, pour accéder à la console de configuration du stockage.

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration du stockage]**

Pour sélectionner une option de stockage autre que le JCR par défaut :

* Sélectionner une option
* Configurer correctement

   * Voir les détails de la [sélection de MSRP](msrp.md#select-msrp)
   * Voir les détails de la [sélection de DSRP](dsrp.md#select-dsrp)
   * Voir les détails de la [sélection de l’ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**.

### À propos du stockage JCR {#about-jcr-storage}

Notez que si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR est *et non* un magasin commun partagé par les environnements de création et de publication. Le contenu de la communauté n’est visible que depuis l’environnement de création ou de publication dans lequel il a été créé.

Pour plus d’informations, consultez la [boutique JCR](jsrp.md).

>[!NOTE]
>
>L’absence du noeud `srpc` sous `/etc/socialconfig` indique le [magasin JCR par défaut](jsrp.md).
