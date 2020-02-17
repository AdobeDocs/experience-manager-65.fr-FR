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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration du stockage {#storage-configuration}

La configuration du stockage permet d’identifier le stockage choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC).

Ce paramètre informe le code des communautés AEM sur l’implémentation du fournisseur de ressources de stockage (SRP) à utiliser lors de l’accès au contenu UGC et doit refléter la topologie établie lors du déploiement d’AEM.

Pour consulter les options de stockage et les topologies de déploiement, rendez-vous sur la page

* [Community Content Store](working-with-srp.md)
* [Topologies recommandées](topologies.md)

## Console de configuration de stockage {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

Dans l’environnement de création, pour accéder à la console de configuration du stockage

* A partir de la navigation globale : **[!UICONTROL Outils > Communautés > Configuration du stockage]**

Pour sélectionner une option de stockage autre que le JCR par défaut :

* sélectionner une option
* Configurer correctement

   * Voir les détails de la [sélection du MSRP](msrp.md#select-msrp)
   * Voir les détails de la [sélection de DSRP](dsrp.md#select-dsrp)
   * Voir les détails de la [sélection d’ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**

### A propos du stockage JCR {#about-jcr-storage}

Sachez que si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR *n’est pas* un magasin commun partagé par les environnements d’auteur et de publication. Le contenu de la communauté n’est visible que depuis l’environnement d’auteur ou de publication dans lequel il a été créé.

Consultez le magasin [](jsrp.md) JCR pour plus d’informations.

>[!NOTE]
>
>L’absence du noeud `srpc`sous `/etc/socialconfig` indique le magasin [](jsrp.md)JCR par défaut.

