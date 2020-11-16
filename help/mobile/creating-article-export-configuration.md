---
title: Création de la configuration d’exportation d’article
seo-title: Création de la configuration d’exportation d’article
description: Suivez cette page pour en savoir plus sur l’exportation de contenu à partir de Adobe Experience Manager (AEM) en vue d’un téléchargement vers AEM Mobile.
seo-description: Suivez cette page pour en savoir plus sur l’exportation de contenu à partir de Adobe Experience Manager (AEM) en vue d’un téléchargement vers AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 6%

---


# Création de la configuration d’exportation d’article{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Condition requise**:
>
>Avant d’en savoir plus sur la création et la modification de ressources partagées, voir Synchronisation [du](/help/mobile/mobile-ondemand-contentsync.md) contenu pour comprendre les concepts de base.

Les utilisateurs AEM Mobile utilisent la synchronisation de contenu pour exporter du contenu en direct vers du contenu statique en vue de l’utiliser dans les applications mobiles. Cette exportation survient lorsque le contenu est téléchargé vers Mobile On-Demand Services à partir d’AEM Mobile.

La propriété ***dps-exportTemplate*** mentionnée dans le tableau ci-dessus définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l’exportation de contenu à partir de Adobe Experience Manager (AEM) en vue d’un transfert vers AEM Mobile.

Les articles comportent un contenu qui doit être exporté et téléchargé. Une partie de ce contenu peut être partagée entre les articles.

Utilisez [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) pour rassembler le contenu et créer un package de ressources ****** partagées.

La configuration ContentSync trouvée dans **&lt;dps-exportTemplate>/dps-article>** doit être configurée pour exporter tout le contenu et l’article requis pour le rendu statique des propriétés sur le périphérique.

>[!CAUTION]
>
>Vous pouvez effectuer les étapes ci-dessous pour vue des exemples de ressources partagées, uniquement si vous avez :
>
>* installation de l’exemple de contenu
>* exécution de l’instance AEM
>* aucun contexte personnalisé configuré ou port différent

>



Pour vue des exemples de ressources partagées, procédez comme suit :

1. Ouvrez le CRXDE Lite sur votre serveur AEM.
1. Accédez à ce chemin d’accès [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), pour vue aux exemples de ressources partagées.

   Vous pouvez vue toutes les propriétés requises pour la création de vos ressources partagées, comme le montre la figure ci-dessous :

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Les articles doivent être téléchargés ou exportés en AEM Mobile On-demand Services lorsqu’un contenu d’article change.

