---
title: Configuration du stockage
description: Découvrez la console Configuration du stockage comme moyen d’identifier le stockage choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# Configuration du stockage {#storage-configuration}

La configuration du stockage est le moyen d’identifier le stockage choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC).

Ce paramètre informe le code AEM Communities sur l’implémentation du fournisseur de ressources de stockage (SRP) utilisée lors de l’accès au contenu généré par l’utilisateur. Elle doit refléter la topologie définie lors du déploiement de Adobe Experience Manager (AEM).

Pour une discussion sur les options de stockage et les topologies de déploiement, consultez :

* [Community Content Store](working-with-srp.md)
* [Topologies recommandées](topologies.md)

## Console de configuration de stockage {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Dans l’environnement de création, pour accéder à la console de configuration du stockage.

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de stockage]**

Pour sélectionner une option de stockage autre que le JCR par défaut :

* Sélectionner une option
* Configurez les

   * Voir les détails de la [sélection de MSRP](msrp.md#select-msrp)
   * Voir les détails de la [sélection de DSRP](dsrp.md#select-dsrp)
   * Voir les détails de la [sélection de l’ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**.

### À propos du stockage JCR {#about-jcr-storage}

Si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR n’est *pas* un magasin commun partagé par les environnements Auteur et Publish. Le contenu de la communauté n’est visible que dans l’environnement de création ou de Publish dans lequel il a été créé.

Pour plus d’informations, consultez la [boutique JCR](jsrp.md) .

>[!NOTE]
>
>L’absence du noeud `srpc` sous `/etc/socialconfig` indique le [magasin JCR](jsrp.md) par défaut.
