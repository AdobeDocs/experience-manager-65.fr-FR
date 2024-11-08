---
title: Configuration de votre Cloud Service Mobile Services Adobe
description: Consultez cette page pour configurer votre Cloud Service Mobile Services Adobe.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 7%

---

# Configuration de votre Cloud Service Mobile Services Adobe {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

La **mosaïque Mesures mobiles** du centre de commande fournit des analyses en temps réel pour votre application mobile.

Le SDK [ Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) est disponible via un module externe PhoneGap. Les mesures sont collectées et mises en cache sur l’appareil jusqu’à ce que l’appareil soit connecté. Les données sont alors transmises à Adobe Mobile Services Cloud pour création de rapports et analyse.

Le SDK Adobe Mobile Analytics fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** - Collectez des données complètes pour vos sites web et applications mobiles sur tous les principaux systèmes d’exploitation.
1. **Analyse de l’engagement mobile** - Comprendre l’engagement des utilisateurs dans votre application mobile, votre site web ou votre vidéo, y compris la fréquence à laquelle les clients lancent le canal, s’ils effectuent des achats sur celui-ci, etc.
1. **Tableaux de bord et rapports d’applications mobiles** - Obtenez des rapports d’utilisation qui incluent des mesures de cycle de vie pour vos applications et mesures de boutique d’applications. Consultez les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse de campagne mobile** - Quantifiez l’efficacité des campagnes spécifiques aux mobiles telles que les SMS, les annonces de recherche mobile, les annonces d’affichage mobile et les codes QR.
1. **Analyse de géolocalisation** : découvrez où les utilisateurs de votre application lancent vos expériences mobiles et interagissent avec celles-ci par emplacement GPS ou points ciblés.
1. **Analyse du cheminement** - Découvrez comment les utilisateurs naviguent dans votre application pour déterminer les écrans et les éléments de l’interface utilisateur qui attirent les utilisateurs et qui provoquent le abandon des utilisateurs.

>[!CAUTION]
>
>La mosaïque **Analyser les mesures** s’affiche dans le tableau de bord, uniquement si vous avez configuré les services cloud.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM mosaïque Mesures du centre de commandes

## Configuration du Cloud Service {#configuring-the-cloud-service}

Pour tirer parti d’Adobe Mobile Services Analytics, vous devez configurer le service AEM Mobile Analytics Cloud avec les informations de votre compte Adobe Analytics.

1. Cliquez sur l’icône en haut à droite pour ajouter ou modifier les Cloud Service à partir de la mosaïque **Gérer les Cloud Service** du tableau de bord de l’application.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. L’écran **Ajouter ou Modifier des Cloud Service** s’affiche. Sélectionnez **Adobe Mobile Services** et cliquez sur **Suivant**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Choisissez une configuration existante dans les **Mobile Services** ou sélectionnez **Créer une configuration** pour en créer une.

   Pour une nouvelle configuration, saisissez les **propriétés Mobile Services** et cliquez sur **Vérifier.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si les informations d’identification sont vérifiées, le bouton **Vérifier** devient **Vérifié**. Vous pouvez choisir une application de service mobile dans **Sélectionner un service d’application mobile**.

   Cliquez sur **Submit** pour configurer votre configuration.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Une fois que vous avez configuré une configuration cloud, vous pouvez en afficher une dans votre tableau de bord.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Une fois la configuration cloud configurée, vous pouvez afficher la mosaïque **Analyser les mesures** dans le tableau de bord de votre application.

   ![chlimage_1-28](assets/chlimage_1-28.png)
