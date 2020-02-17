---
title: Configuration du cloud
seo-title: Configuration du cloud
description: L’association d’une application à la demande à une configuration Cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant un lien bidirectionnel. Consultez cette page pour en savoir plus.
seo-description: L’association d’une application à la demande à une configuration Cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant un lien bidirectionnel. Consultez cette page pour en savoir plus.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration du cloud{#cloud-configuration}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

L’association d’une application à la demande à une configuration Cloud permet à Adobe Experience Manager (AEM) de communiquer directement avec un projet hébergé sur Mobile On-Demand en établissant un lien bidirectionnel. En liant votre application à un projet Mobile On-Demand, vous pourrez créer du contenu, tel que des articles, des bannières et des collections dans AEM, mais aussi diffuser ce contenu à Mobile On-Demand.

A partir de là, la publication, la prévisualisation et la gestion du contenu deviennent possibles. Vous pouvez également importer du contenu Mobile On-Demand existant dans AEM et modifier le contenu.

## Configuration de Cloud {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Avant de commencer à configurer la configuration du cloud pour votre application à la demande, vous devez connaître les fonctions de configuration et de configuration d&#39;AEM Mobile On-Demand Services Client.
>
>Pour plus d&#39;informations, reportez-vous à la section [Configuration des services](/help/mobile/aem-mobile-setup.md) à la demande AEM Mobile dans la section Administration.

Pour configurer Mobile On-Demand Cloud Services, cliquez sur l’engrenage supérieur dans le coin supérieur droit du volet **Gérer la connexion** depuis le tableau de bord de votre application.

Vous devez connaître le tableau de bord de l’application et les mosaïques disponibles. Pour plus d&#39;informations, reportez-vous au tableau de bord [des applications](/help/mobile/mobile-apps-ondemand-application-dashboard.md) AEM Mobile.

### Configuration du lien vers la configuration de Cloud {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Vérifiez que vous disposez d’un client à la demande et d’une configuration de cloud existants.
>
>Pour plus d&#39;informations, reportez-vous à la section [Configuration des services](/help/mobile/aem-mobile-setup.md) à la demande AEM Mobile dans la section Administration.

La procédure suivante décrit la configuration d’un lien vers la configuration du cloud :

1. Dans **Mobile**, sélectionnez **Applications** , puis votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur l’icône d’engrenage dans la mosaïque **Gérer la connexion** .

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Entrez la configuration existante ou créez-en une nouvelle en saisissant le titre **de la** configuration, l’ID **de** périphérique et le jeton **de** périphérique.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Une fois l&#39;ID **de votre** périphérique et le jeton **de votre** périphérique vérifiés, sélectionnez votre projet à la demande dans la liste.

   Cliquez sur **Envoyer**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   Le volet **Gérer la connexion** affiche votre configuration Cloud.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Si vous essayez de modifier le projet auquel cette application est associée, tout en changeant de projet dans le tableau de bord, vous recevrez un avertissement pour les problèmes d’intégrité du contenu, comme illustré dans la figure ci-dessous :

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Étapes suivantes {#the-next-steps}

Une fois que vous avez configuré la configuration Cloud pour votre application, consultez les ressources suivantes pour la gestion du contenu :

* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Téléchargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
