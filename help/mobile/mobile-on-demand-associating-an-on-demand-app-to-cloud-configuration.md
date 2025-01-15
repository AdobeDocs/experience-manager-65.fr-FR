---
title: Configuration du cloud
description: L’association d’une application à la demande à une configuration cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant une liaison bidirectionnelle. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 6%

---

# Configuration du cloud{#cloud-configuration}

{{ue-over-mobile}}

L’association d’une application à la demande à une configuration cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant une liaison bidirectionnelle. En liant votre application à un projet Mobile On-Demand, vous pouvez créer du contenu, tel que des articles, des bannières et des collections au sein d’AEM, mais également diffuser ce contenu sur Mobile On-Demand.

De là, la publication, la prévisualisation et la gestion du contenu deviennent possibles. Vous pouvez également importer du contenu Mobile On-Demand existant dans AEM et effectuer des modifications de contenu.

## Configuration du cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Avant de commencer à configurer la configuration cloud pour votre application à la demande, vous devez connaître l’approvisionnement d’AEM Mobile et la configuration du client AEM Mobile On-demand Services.
>
>Pour plus d’informations, consultez la section [Configuration d’AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) dans la section Administration .

Pour configurer les Cloud Service On-Demand mobiles, cliquez sur l’engrenage supérieur dans le coin supérieur droit de la mosaïque **Gérer la connexion** depuis le tableau de bord de l’application.

Vous devriez vous familiariser avec le tableau de bord de l’application et les vignettes disponibles. Voir [Tableau de bord de l’application AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md) pour plus d’informations.

### Configuration d’un lien vers une configuration cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Vérifiez que vous disposez d’une configuration cloud et d’un client On-Demand existante.
>
>Pour plus d’informations, consultez la section [Configuration d’AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) dans la section Administration .

Les étapes suivantes décrivent la configuration d’un lien vers la configuration cloud :

1. Dans **Mobile**, choisissez **Applications**, puis votre application mobile à la demande dans le catalogue.
1. Cliquez sur l’icône en forme d’engrenage sur la mosaïque **Gérer la connexion**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Saisissez la configuration existante ou créez-en une en saisissant les **Titre de la configuration**, **ID de l’appareil** et **Jeton de l’appareil**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Une fois votre **ID d’appareil** et **Jeton d’appareil** vérifiés, choisissez votre projet à la demande dans la liste.

   Cliquez sur **Envoyer**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   La mosaïque **Gérer la connexion** affiche votre configuration cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Si vous essayez de modifier le projet auquel cette application est associée, lors du changement de projet dans le tableau de bord, vous recevrez un avertissement pour les problèmes d’intégrité du contenu, comme illustré dans la figure ci-dessous :

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez configuré la configuration cloud de votre application, consultez les ressources suivantes pour gérer le contenu :

* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement des ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/dépublication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
