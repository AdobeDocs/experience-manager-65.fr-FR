---
title: Création d’une configuration d’exportation d’article
description: Consultez cette page pour en savoir plus sur l’exportation de contenu à partir de Adobe Experience Manager (AEM) pour le transfert vers AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---

# Création d’une configuration d’exportation d’article{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Condition requise**:
>
>Avant d’en savoir plus sur la création et la modification de ressources partagées, voir [Synchronisation du contenu](/help/mobile/mobile-ondemand-contentsync.md) pour comprendre les concepts de base.

Les utilisateurs d’AEM Mobile utilisent la synchronisation de contenu pour exporter du contenu en direct vers du contenu statique en vue de l’utiliser dans les applications mobiles. Cet export se produit lorsque le contenu est chargé vers Mobile On Demand Services à partir d’AEM Mobile.

La propriété ***dps-exportTemplate*** mentionné dans le tableau ci-dessus, définit le chemin d’accès aux configurations d’exportation de l’application. Définissez cette propriété pour créer et modifier des ressources partagées.

Les ressources suivantes décrivent l’exportation de contenu à partir de Adobe Experience Manager (AEM) pour téléchargement vers AEM Mobile.

Les articles contiennent du contenu qui doit être exporté et chargé. Une partie de ce contenu peut être partagée entre les articles.

Utilisation [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) pour rassembler le contenu et créer une ***Ressources partagées*** module.

Configuration ContentSync disponible à l’adresse **&lt;dps-exporttemplate>/dps-article>** doit être configuré pour exporter tout le contenu requis pour le rendu statique des propriétés sur l’appareil.

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
1. Parcourir vers ce chemin [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), pour afficher les exemples de ressources partagées.

   Vous pouvez afficher toutes les propriétés requises pour créer vos ressources partagées, comme illustré dans la figure ci-dessous :

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Les articles doivent être transférés ou exportés vers AEM Mobile On-demand Services lorsqu’un contenu d’article change.
