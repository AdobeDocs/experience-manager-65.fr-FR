---
title: Configuration du cloud
description: L’association d’une application On-Demand à une configuration cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant un lien bidirectionnel. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 11%

---

# Configuration du cloud{#cloud-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

L’association d’une application On-Demand à une configuration cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant un lien bidirectionnel. En liant votre application à un projet Mobile On-Demand, vous pouvez créer du contenu, tel que des articles, des bannières et des collections dans AEM, mais également diffuser ce contenu à Mobile On-Demand.

A partir de là, la publication, la prévisualisation et la gestion du contenu deviennent possibles. Vous pouvez également importer du contenu Mobile On Demand existant dans AEM et effectuer l’édition du contenu.

## Configuration du cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Avant de commencer à configurer la configuration du cloud pour votre application On-Demand, vous devez maîtriser l’approvisionnement AEM Mobile et la configuration du client AEM Mobile On-demand Services.
>
>Pour plus d’informations, voir [Configuration d’AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) dans la section Administration.

Pour configurer les Cloud Service mobiles à la demande, cliquez sur l’engrenage supérieur dans le coin supérieur droit de la mosaïque **Gérer la connexion** depuis le tableau de bord de votre application.

Vous devez connaître le tableau de bord de l’application et les mosaïques disponibles. Pour plus d’informations, voir [Tableau de bord des applications AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) .

### Configuration d’un lien vers la configuration du cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Vérifiez que vous disposez d’une configuration de cloud et d’un client On-Demand existante.
>
>Pour plus d’informations, voir [Configuration d’AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) dans la section Administration.

Les étapes suivantes décrivent la configuration d’un lien vers la configuration cloud :

1. Depuis **Mobile**, sélectionnez **Applications** , puis votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur l’icône d’engrenage sur la mosaïque **Gérer la connexion** .

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Saisissez la configuration existante ou créez-en une en saisissant les **Titre de configuration**, **Id de périphérique** et **Jeton de périphérique**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Une fois que votre **ID de périphérique** et votre **Jeton de périphérique** sont vérifiés, sélectionnez votre projet On-Demand dans la liste.

   Cliquez sur **Envoyer**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   La mosaïque **Gérer la connexion** affiche votre configuration du cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Si vous essayez de modifier le projet auquel cette application est associée, lors du changement de projet dans le tableau de bord, vous recevrez un avertissement pour les problèmes d’intégrité du contenu, comme illustré dans la figure ci-dessous :

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez configuré la configuration cloud pour votre application, reportez-vous aux ressources suivantes pour gérer le contenu :

* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de la publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
