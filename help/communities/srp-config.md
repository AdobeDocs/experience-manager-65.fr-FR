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
source-wordcount: '213'
ht-degree: 4%
---
# Configuration du stockage {#storage-configuration}

La configuration de stockage permet d’identifier le stockage choisi pour le contenu de la communauté. Elle est également appelée contenu créé par l’utilisateur.

Ce paramètre informe le code AEM Communities quant à l’implémentation du fournisseur de ressources de stockage (SRP) utilisée lors de l’accès au contenu créé par l’utilisateur. Elle doit refléter la topologie établie lors du déploiement de Adobe Experience Manager (AEM).

Pour plus d’informations sur les options de stockage et les topologies de déploiement, consultez :

* [Stockage de contenu de la communauté](working-with-srp.md)
* [Topologies recommandées](topologies.md)

## Console de configuration du stockage {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Dans l’environnement de création, pour accéder à la console de configuration du stockage.

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Configuration de stockage]**

Pour sélectionner une option de stockage autre que le JCR par défaut :

* Sélectionner une option
* Configurer correctement

  * Voir les détails pour [sélectionner MSRP](msrp.md#select-msrp)
  * Voir les détails pour [sélectionner DSRP](dsrp.md#select-dsrp)
  * Voir les détails pour [sélectionner ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**.

### À propos du stockage JCR {#about-jcr-storage}

Si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR n’est *pas* un magasin commun partagé par les environnements de création et de publication. Le contenu de la communauté est visible uniquement à partir de l’environnement de création ou de publication dans lequel il a été créé.

Consultez [Magasin JCR](jsrp.md) pour plus d’informations.

>[!NOTE]
>
>L’absence du nœud `srpc` sous `/etc/socialconfig` indique le [magasin JCR](jsrp.md) par défaut.
