---
title: Stockage   Configuration
seo-title: Stockage   Configuration
description: 'Accès à la console de configuration  '
seo-description: 'Accès à la console de configuration  '
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Configuration du stockage {#storage-configuration}

 configuration  est le moyen d’identifier le  choisi pour le contenu de la communauté, également appelé contenu généré par l’utilisateur (UGC).

Ce paramètre informe le code des communautés AEM du choix de l’implémentation du fournisseur de ressources  (SRP) à utiliser lors de l’accès au contenu UGC et doit refléter la topologie établie lors du déploiement d’AEM.

Pour une discussion sur les options de   et les topologies de déploiement, visitez :

* [Community Content Store](working-with-srp.md)
* [Topologies recommandées](topologies.md)

##  Console de configuration {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

Dans le  de l&#39;auteur , pour accéder à la console de configuration du .

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL configuration]**

Pour sélectionner une option  de autre que le JCR par défaut :

* Sélectionner une option
* Configurer correctement

   * Voir les détails de la [sélection du MSRP](msrp.md#select-msrp)
   * Voir les détails de la [sélection de DSRP](dsrp.md#select-dsrp)
   * Voir les détails de la [sélection d’ASRP](asrp.md#select-asrp)

* Sélectionnez **[!UICONTROL Envoyer]**.

### A propos du  JCR {#about-jcr-storage}

Sachez que si aucune sélection n’est effectuée, la valeur par défaut est le référentiel AEM, JCR.

JCR *n’est pas* un magasin commun partagé par l’auteur et publie  . Le contenu de la communauté n’est visible que depuis l’auteur ou la publication  le  dans lequel il a été créé.

Consultez le magasin [](jsrp.md) JCR pour plus d’informations.

>[!NOTE]
>
>L’absence du noeud `srpc` sous `/etc/socialconfig` indique le magasin [](jsrp.md)JCR par défaut.


