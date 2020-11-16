---
title: Configuration de votre service cloud Adobe Mobile Services
seo-title: Configuration de votre service cloud Adobe Mobile Services
description: Suivez cette page pour configurer votre Cloud Service Adobe Mobile Services.
seo-description: Suivez cette page pour configurer votre Cloud Service Adobe Mobile Services.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 32%

---


# Configuration de votre service cloud Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

The **Mobile Metrics Tile** on the command center provides real-time analytics for your mobile application.

Le SDK [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) est disponible via un plug-in PhoneGap. Les mesures sont collectées et mises en cache sur le périphérique jusqu’à ce que ce dernier soit connecté, moment auquel les données sont transférées vers le service cloud Adobe Mobile Services à des fins de rapports et d’analyses.

Le SDK Adobe Mobile Analytics fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** : collectez des données complètes pour vos sites web et applications mobiles sur tous les grands systèmes d’exploitation.
1. **Analyse** d’engagement mobile - Comprenez l’engagement des utilisateurs au sein de votre application mobile, de votre site Web ou de votre vidéo, notamment la fréquence de lancement du canal par les clients, la fréquence à laquelle ils effectuent des achats, etc.
1. **Tableaux de bord et rapports** d&#39;applications mobiles - Obtenez des rapports d&#39;utilisation qui incluent des mesures de cycle de vie pour vos applications et des mesures de boutique d&#39;applications — afficher les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse** des campagnes mobiles : quantifiez l&#39;efficacité des campagnes spécifiques aux mobiles telles que les SMS, les publicités de recherche mobile, les publicités d&#39;affichage mobile et les codes QR.
1. **Analyse** de géolocalisation - Recherchez où les utilisateurs de votre application lancent et interagissent avec vos expériences mobiles par localisation GPS ou points ciblés.
1. **Analyse** du cheminement : déterminez comment les utilisateurs naviguent dans votre application afin de déterminer quels écrans et éléments de l’interface utilisateur attirent les utilisateurs et ce qui les pousse à abandonner.

>[!CAUTION]
>
>La mosaïque **Analyser les mesures** s’affiche dans le tableau de bord, uniquement si vous avez configuré les services Cloud.

![chlimage_1-22](assets/chlimage_1-22.png)

Mosaïque Mesures du centre de commande AEM

## Configuration du service cloud {#configuring-the-cloud-service}

Pour exploiter pleinement Adobe Mobile Services Analytics, vous devez configurer le service cloud AEM Mobile Analytics avec les informations de votre compte Adobe Analytics.

1. Cliquez sur l’icône en haut à droite de l’écran pour ajouter ou modifier les Cloud Services à partir de la mosaïque **Gérer les Cloud Services** à partir du tableau de bord de l’application.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. L’écran **Ajouter ou Modifier les Cloud Services** s’affiche. Sélectionnez **Adobe Mobile Services** et cliquez sur **Suivant**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Choisissez une configuration existante dans **Mobile Services** ou sélectionnez **Créer une configuration** pour en créer une nouvelle.

   Pour la nouvelle configuration, saisissez les propriétés de **Mobile Services** et cliquez sur **Vérifier.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Si les informations d’identification sont vérifiées, le bouton **Vérifier** devient **Vérifié**. Vous pouvez choisir une application de service mobile dans **Sélectionner un service** d’application mobile.

   Cliquez sur **Envoyer** pour configurer votre configuration.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. Une fois que vous avez configuré une configuration de cloud, vous pouvez en vue la même dans votre tableau de bord.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >Une fois que vous avez configuré la configuration du cloud, vous pouvez vue la mosaïque **Analyser les mesures** dans votre tableau de bord d’application.

   ![chlimage_1-28](assets/chlimage_1-28.png)

