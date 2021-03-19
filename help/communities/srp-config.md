---
title: Stockage   Configuration
seo-title: Stockage   Configuration
description: Accès à la console de configuration d'Enregistrement
seo-description: Accès à la console de configuration d'Enregistrement
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 5%

---


# Configuration du stockage {#storage-configuration}

La configuration des Enregistrements est le moyen d’identifier l’enregistrement choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC).

Ce paramètre informe le code AEM Communities de la mise en oeuvre du fournisseur de ressources d’enregistrement (SRP) à utiliser lors de l’accès au CU et doit refléter la topologie établie lors du déploiement de l’AEM.

Pour consulter les options d’enregistrement et les topologies de déploiement, visitez :

* [Communauté Content Store](working-with-srp.md)
* [Topologies recommandées](topologies.md)

## Console de configuration des Enregistrements {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Dans l’environnement d’auteur, pour accéder à la console de configuration de l’enregistrement.

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de l&#39;Enregistrement]**

Pour sélectionner une option d’enregistrement autre que le JCR par défaut :

* Sélectionner une option
* Configurer correctement

   * Voir les détails de [sélection de MSRP](msrp.md#select-msrp)
   * Voir les détails de [sélection de DSRP](dsrp.md#select-dsrp)
   * Voir les détails de [sélection de l&#39;ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**.

### À propos de l’Enregistrement JCR {#about-jcr-storage}

Sachez que si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR est *non* un magasin commun partagé par l’auteur et les environnements de publication. Le contenu de la communauté n’est visible que depuis l’environnement d’auteur ou de publication dans lequel il a été créé.

Consultez [JCR Store](jsrp.md) pour plus d’informations.

>[!NOTE]
>
>L’absence du noeud `srpc` sous `/etc/socialconfig` indique le magasin [JCR par défaut](jsrp.md).
