---
title: Configuration de votre service cloud Adobe Mobile Services
seo-title: Configuration de votre service cloud Adobe Mobile Services
description: Consultez cette page pour configurer votre Cloud Service Mobile Services Adobe.
seo-description: Consultez cette page pour configurer votre Cloud Service Mobile Services Adobe.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 32%

---

# Configuration de votre service cloud Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La **mosaïque Mesures mobiles** du centre de commande fournit des analyses en temps réel pour votre application mobile.

Le SDK [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) est disponible via un plug-in PhoneGap. Les mesures sont collectées et mises en cache sur le périphérique jusqu’à ce que ce dernier soit connecté, moment auquel les données sont transférées vers le service cloud Adobe Mobile Services à des fins de rapports et d’analyses.

Le SDK Adobe Mobile Analytics fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** : collectez des données complètes pour vos sites web et applications mobiles sur tous les grands systèmes d’exploitation.
1. **Analyse de l’engagement mobile**  : comprenez l’engagement des utilisateurs au sein de votre application mobile, de votre site web ou de votre vidéo, notamment la fréquence à laquelle les clients lancent le canal, s’ils effectuent des achats sur celui-ci, etc.
1. **Tableaux de bord et rapports d’applications mobiles**  - Obtenez des rapports d’utilisation qui incluent des mesures de cycle de vie pour vos applications et des mesures de boutique d’applications. Consultez les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse de campagne mobile**  : mesurez l’efficacité des campagnes spécifiques aux mobiles telles que les SMS, les annonces de recherche mobile, les annonces d’affichage mobile et les codes QR.
1. **Analyse de géolocalisation**  : découvrez où les utilisateurs de votre application lancent vos expériences mobiles et interagissent avec celles-ci par emplacement GPS ou points ciblés.
1. **Analyse du cheminement**  : découvrez comment les utilisateurs naviguent dans votre application pour déterminer les écrans et les éléments de l’interface utilisateur qui attirent les utilisateurs et qui provoquent le abandon des utilisateurs.

>[!CAUTION]
>
>La mosaïque **Analyser les mesures** s’affiche dans le tableau de bord, uniquement si vous avez configuré les services cloud.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaïque Mesures du centre de commande AEM

## Configuration du service cloud {#configuring-the-cloud-service}

Pour exploiter pleinement Adobe Mobile Services Analytics, vous devez configurer le service cloud AEM Mobile Analytics avec les informations de votre compte Adobe Analytics.

1. Cliquez sur l’icône en haut à droite pour ajouter ou modifier les Cloud Services à partir de la mosaïque **Gérer les Cloud Services** dans le tableau de bord de l’application.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. L’écran **Ajouter ou modifier des Cloud Services** s’affiche. Sélectionnez **Adobe Mobile Services** et cliquez sur **Suivant**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Choisissez une configuration existante dans **Mobile Services** ou sélectionnez **Créer une configuration** pour en créer une.

   Pour une nouvelle configuration, saisissez **Propriétés Mobile Services** et cliquez sur **Vérifier.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si les informations d’identification sont vérifiées, le bouton **Vérifier** passe à **Vérifié**. Vous pouvez choisir une application de service mobile à partir de **Sélectionnez un service d’application mobile**.

   Cliquez sur **Submit** pour configurer votre configuration.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Une fois que vous avez configuré une configuration cloud, vous pouvez en afficher une dans votre tableau de bord.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Une fois la configuration cloud configurée, vous pouvez afficher la mosaïque **Analyser les mesures** dans le tableau de bord de l’application.

   ![chlimage_1-28](assets/chlimage_1-28.png)
