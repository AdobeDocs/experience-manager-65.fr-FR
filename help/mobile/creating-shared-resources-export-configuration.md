---
title: Création de la configuration de l'export des ressources partagées
seo-title: Création de la configuration de l'export des ressources partagées
description: Consultez cette page pour en savoir plus sur l’exportation de ressources partagées à partir d’Adobe Experience Manager (AEM) en vue de leur chargement vers AEM Mobile.
seo-description: Consultez cette page pour en savoir plus sur l’exportation de ressources partagées à partir d’Adobe Experience Manager (AEM) en vue de leur chargement vers AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 6%

---

# Création de la configuration de l’exportation des ressources partagées{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prérequis**:
>
>Avant d’en savoir plus sur la création et la modification de ressources partagées, voir [Synchronisation du contenu](/help/mobile/mobile-ondemand-contentsync.md) pour comprendre les concepts de base.

Les utilisateurs d’AEM Mobile utilisent la synchronisation de contenu pour exporter du contenu en direct vers du contenu statique en vue de l’utiliser dans les applications mobiles. Cet export se produit lorsque le contenu est chargé vers Mobile On Demand Services à partir d’AEM Mobile.

La propriété ***dps-exportTemplate*** mentionnée dans le tableau ci-dessus définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l’exportation de ressources partagées à partir d’Adobe Experience Manager (AEM) pour chargement vers AEM Mobile.

Les ressources HTML partagées permettent aux articles de partager des ressources HTML qui auraient sinon besoin d’être dupliquées pour tous les articles et peuvent inclure des icônes, des polices, du code JavaScript et des feuilles CSS.

La configuration de synchronisation de contenu disponible à l’adresse **&lt;dps-exportTemplate>/dps-HTMLResources>** doit être configurée pour exporter tout le contenu et un article requis pour le rendu statique des propriétés sur l’appareil.

>[!CAUTION]
>
>Vous pouvez effectuer les étapes ci-dessous pour afficher les exemples de ressources partagées, uniquement si vous disposez des éléments suivants :
>
>* installation de l’exemple de contenu
>* exécution de l’instance AEM
>* aucun contexte personnalisé configuré ou port différent

>



Pour afficher un exemple de ressource partagée, procédez comme suit :

1. Ouvrez le CRXDE Lite sur votre serveur AEM.
1. Accédez à ce chemin *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* pour afficher les exemples de ressources partagées.

   Vous pouvez afficher toutes les propriétés requises pour créer vos ressources partagées, comme illustré dans la figure ci-dessous :

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Les ressources partagées doivent être chargées ou exportées vers AEM Mobile On-demand Services lorsque l’une des ressources partagées change.
