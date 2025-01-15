---
title: Création d’une configuration d’exportation de ressources partagées
description: Consultez cette page pour en savoir plus sur l’exportation de ressources partagées depuis Adobe Experience Manager (AEM) en vue de les charger vers AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Création d’une configuration d’exportation de ressources partagées{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**Prérequis** :
>
>Avant d’en savoir plus sur la création et la modification des ressources partagées, consultez [Synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md) pour comprendre les concepts de base.

Adobe Experience Manager (AEM) Les utilisateurs mobiles utilisent la synchronisation de contenu pour exporter du contenu en direct vers du contenu statique à utiliser dans les applications mobiles. Cette exportation a lieu lorsque le contenu est chargé sur les services Mobile On-Demand depuis AEM Mobile.

La propriété ***dps-exportTemplate*** mentionnée dans le tableau ci-dessus, définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l’exportation de ressources partagées depuis AEM pour chargement vers AEM Mobile.

Les ressources d’HTML partagées permettent aux articles de partager des ressources d’HTML qui seraient autrement dupliquées pour tous les articles. Elles peuvent inclure des icônes, des polices, des JavaScript et des feuilles css.

La configuration de la synchronisation de contenu disponible dans **&lt;dps-exportTemplate>/dps-HTMLResources>** doit être configurée pour exporter tout le contenu et l’article requis pour le rendu statique des propriétés sur l’appareil.

>[!CAUTION]
>
>Vous pouvez effectuer les étapes ci-dessous pour afficher des exemples de ressources partagées, uniquement si vous disposez des éléments suivants :
>
>* a installé l’exemple de contenu .
>* exécution de l’instance AEM
>* aucun contexte personnalisé configuré ou port différent
>

Pour afficher un exemple de ressource partagée, procédez comme suit :

1. Ouvrez CRXDE Lite sur votre serveur AEM.
1. Accédez à ce chemin *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* pour afficher les exemples de ressources partagées.

   Vous pouvez afficher toutes les propriétés requises pour créer vos ressources partagées, comme illustré dans la figure ci-dessous :

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Les ressources partagées doivent être chargées ou exportées vers AEM Mobile On-demand Services en cas de modification de l’une d’elles.
