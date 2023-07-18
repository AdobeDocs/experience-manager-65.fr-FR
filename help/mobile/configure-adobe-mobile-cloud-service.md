---
title: Configuration de votre Cloud Service Mobile Services Adobe
seo-title: Configure your Adobe Mobile Services Cloud Service
description: Consultez cette page pour configurer votre Cloud Service Mobile Services Adobe.
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Configuration de votre Cloud Service Mobile Services Adobe {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le **Mosaïque Mesures mobiles** sur le centre de commande fournit des analyses en temps réel pour votre application mobile.

Le [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) Le SDK est rendu disponible par le biais d’un module externe PhoneGap. Les mesures sont collectées et mises en cache sur l’appareil jusqu’à ce que l’appareil soit connecté. Les données sont alors transmises à Adobe Mobile Services Cloud pour création de rapports et analyse.

Le SDK Adobe Mobile Analytics fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** - Collectez des données complètes pour vos sites web et applications mobiles sur tous les principaux systèmes d’exploitation.
1. **Analyse de l&#39;engagement mobile** - Comprendre l’engagement des utilisateurs dans votre application mobile, votre site web ou votre vidéo, notamment la fréquence à laquelle les clients lancent le canal, s’ils effectuent des achats sur celui-ci, etc.
1. **Tableaux de bord et rapports d’applications mobiles** - Obtenez des rapports d’utilisation qui contiennent des mesures de cycle de vie pour vos applications et des mesures de boutique d’applications. Consultez les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse de campagne mobile** - Quantifiez l’efficacité des campagnes spécifiques aux mobiles telles que les SMS, les annonces de recherche mobile, les annonces d’affichage mobile et les codes QR.
1. **Analyse de géolocalisation** - Déterminez où les utilisateurs de votre application lancent vos expériences mobiles et interagissent avec celles-ci par emplacement GPS ou points ciblés.
1. **Analyse du cheminement** - Découvrez comment les utilisateurs naviguent dans votre application pour déterminer les écrans et les éléments de l’interface utilisateur qui attirent les utilisateurs et qui provoquent l’abandon des utilisateurs.

>[!CAUTION]
>
>Le **Analyse des mesures** La mosaïque s’affiche dans le tableau de bord, uniquement si vous avez configuré les services cloud.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM mosaïque Mesures du centre de commandes

## Configuration du Cloud Service {#configuring-the-cloud-service}

Pour tirer parti d’Adobe Mobile Services Analytics, vous devez configurer le service AEM Mobile Analytics Cloud avec les informations de votre compte Adobe Analytics.

1. Cliquez sur l’icône en haut à droite pour ajouter ou modifier les Cloud Services à partir du **Gestion des Cloud Services** à partir du tableau de bord de l’application.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Le **Ajout ou modification de Cloud Services** s’affiche. Sélectionner **Adobe Mobile Services** et cliquez sur **Suivant**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Sélectionnez une configuration existante dans le **Mobile Services** ou choisissez **Créer une configuration** pour en créer un.

   Pour une nouvelle configuration, saisissez la variable **Propriétés Mobile Services** et cliquez sur **Vérifiez.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si les informations d’identification sont vérifiées, la variable **Vérifier** modification du bouton **Vérifié**. Vous pouvez choisir une application de service mobile parmi **Sélection d’un service d’applications mobiles**.

   Cliquez sur **Envoyer** pour configurer votre configuration.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Une fois que vous avez configuré une configuration cloud, vous pouvez en afficher une dans votre tableau de bord.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Une fois la configuration du cloud configurée, vous pouvez afficher la variable **Analyse des mesures** Mosaïque dans le tableau de bord de votre application.

   ![chlimage_1-28](assets/chlimage_1-28.png)
