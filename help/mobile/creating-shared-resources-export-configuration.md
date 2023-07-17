---
title: Création de la configuration de l'export des ressources partagées
description: Consultez cette page pour en savoir plus sur l’exportation de ressources partagées à partir d’Adobe Experience Manager (AEM) en vue de leur chargement vers AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Création de la configuration de l&#39;export des ressources partagées{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Prérequis**:
>
>Avant d’en savoir plus sur la création et la modification de ressources partagées, voir [Synchronisation du contenu](/help/mobile/mobile-ondemand-contentsync.md) pour comprendre les concepts de base.

Adobe Experience Manager (AEM) Les utilisateurs mobiles utilisent la synchronisation de contenu pour exporter du contenu en direct vers du contenu statique en vue de l’utiliser dans les applications mobiles. Cet export se produit lorsque le contenu est téléchargé vers Mobile On-Demand Services à partir d’AEM Mobile.

La propriété ***dps-exportTemplate*** mentionné dans le tableau ci-dessus, définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l’exportation de ressources partagées depuis AEM pour chargement vers AEM Mobile.

Les ressources de HTML partagées permettent aux articles de partager des ressources de HTML qui seraient sinon dupliquées pour tous les articles et qui peuvent inclure des icônes, des polices, du code JavaScript et des feuilles CSS.

La configuration de synchronisation de contenu se trouve à l’adresse **&lt;dps-exporttemplate>/dps-HTMLResources>** doit être configuré pour exporter tout le contenu nécessaire au rendu statique des propriétés sur l’appareil.

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
1. Parcourir vers ce chemin *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, pour afficher les exemples de ressources partagées.

   Vous pouvez afficher toutes les propriétés requises pour créer vos ressources partagées, comme illustré dans la figure ci-dessous :

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Les ressources partagées doivent être chargées ou exportées vers AEM Mobile On-demand Services lorsque l’une des ressources partagées change.
