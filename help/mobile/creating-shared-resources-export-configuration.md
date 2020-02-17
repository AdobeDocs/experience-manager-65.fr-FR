---
title: Création de la configuration d'exportation des ressources partagées
seo-title: Création de la configuration d'exportation des ressources partagées
description: Suivez cette page pour en savoir plus sur l'exportation de ressources partagées à partir d'Adobe Experience Manager (AEM) en vue de leur téléchargement vers AEM Mobile.
seo-description: Suivez cette page pour en savoir plus sur l'exportation de ressources partagées à partir d'Adobe Experience Manager (AEM) en vue de leur téléchargement vers AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Création de la configuration d&#39;exportation des ressources partagées{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Condition requise**:
>
>Avant d’en savoir plus sur la création et la modification de ressources partagées, voir Synchronisation [du](/help/mobile/mobile-ondemand-contentsync.md) contenu pour comprendre les concepts de base.

Les utilisateurs d&#39;AEM Mobile utilisent Content Sync pour exporter du contenu en direct vers du contenu statique en vue de l&#39;utiliser dans les applications mobiles. Cette exportation survient lorsque le contenu est téléchargé vers Mobile On-Demand Services à partir d&#39;AEM Mobile.

La propriété ***dps-exportTemplate*** mentionnée dans le tableau ci-dessus définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l&#39;exportation de ressources partagées à partir d&#39;Adobe Experience Manager (AEM) en vue d&#39;un téléchargement vers AEM Mobile.

Les ressources HTML partagées permettent aux articles de partager des ressources HTML qui, autrement, auraient besoin d’être dupliquées pour tous les articles et peuvent inclure des icônes, des polices, du code JavaScript et des fichiers CSS.

La configuration de synchronisation de contenu trouvée dans **&lt;dps-exportTemplate>/dps-HTMLResources>** doit être configurée pour exporter tout le contenu et l’article requis pour le rendu statique des propriétés sur le périphérique.

>[!CAUTION]
>
>Vous pouvez exécuter les étapes ci-dessous pour afficher des exemples de ressources partagées, uniquement si vous avez :
>
>* installation du contenu d’exemple
>* exécution de l’instance AEM
>* aucun contexte personnalisé configuré ou port différent
>



Pour consulter un exemple de ressource partagée, procédez comme suit :

1. Ouvrez CRXDE Lite sur votre serveur AEM.
1. Accédez à ce chemin d’accès *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*pour afficher les exemples de ressources partagées.

   Vous pouvez afficher toutes les propriétés requises pour créer vos ressources partagées, comme illustré dans la figure ci-dessous :

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Les ressources partagées doivent être transférées ou exportées vers AEM Mobile On-Demand Services lorsque l&#39;une des ressources partagées change.

