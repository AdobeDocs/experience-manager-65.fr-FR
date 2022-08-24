---
title: Suivi des performances de l’application avec Adobe Mobile Analytics
seo-title: Track App Performance with Adobe Mobile Analytics
description: Avec Adobe Mobile Services, vous pouvez mieux comprendre comment vos utilisateurs utilisent vos applications mobiles en suivant l’utilisation, les blocages d’applications, les détails du périphérique et tant d’autres mesures critiques pour vos applications mobiles. Consultez cette page pour en savoir plus.
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 10%

---

# Suivi des performances de l’application avec Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous souhaitez augmenter les conversions et la fidélité des clients.

Vous souhaitez offrir à vos clients des expériences pertinentes et attrayantes.

Que fait votre application AEM Mobile pour vos campagnes marketing ?

Comment optimiser vos applications mobiles pour offrir une expérience optimale à vos utilisateurs ?

Avec Adobe Mobile Services, vous pouvez mieux comprendre comment vos utilisateurs utilisent vos applications mobiles en suivant l’utilisation, les blocages d’applications, les détails du périphérique et tant d’autres mesures critiques pour vos applications mobiles.

Adobe Experience Manager Mobile donne un aperçu des détails de vos analyses mobiles directement depuis le tableau de bord de l’application AEM Mobile. Le **Mosaïque Mesures mobiles** dans le tableau de bord fournit des analyses en temps réel pour votre application mobile, ce qui permet aux développeurs, aux auteurs et aux administrateurs d’avoir un aperçu rapide de l’intégrité de votre application mobile. Sous les couvertures, l’option [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. Le SDK Adobe Mobile Analytics peut être connecté nativement à vos applications ou par le biais d’un module externe PhoneGap Bridge pour les vues web. Les mesures sont collectées et mises en cache sur l’appareil jusqu’à ce que l’appareil soit connecté, au moment où les données sont transmises à Adobe Mobile Services Cloud pour création de rapports et analyse.

Le SDK Adobe Mobile Analytics fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** : collectez des données complètes pour vos sites web et applications mobiles sur tous les grands systèmes d’exploitation.
1. **Analyse de l&#39;engagement mobile** - Comprendre l’engagement des utilisateurs dans votre application mobile, votre site web ou votre vidéo, notamment la fréquence à laquelle les clients lancent le canal, s’ils effectuent des achats sur celui-ci, etc.
1. **Tableaux de bord et rapports d’applications mobiles** - Obtenez des rapports d’utilisation qui contiennent des mesures de cycle de vie pour vos applications et des mesures de boutique d’applications. Consultez les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse de campagne mobile** - Quantifiez l’efficacité des campagnes spécifiques aux mobiles telles que les SMS, les annonces de recherche mobile, les annonces d’affichage mobile et les codes QR.
1. **Analyse de géolocalisation** - Déterminez où les utilisateurs de votre application lancent vos expériences mobiles et interagissent avec celles-ci par emplacement GPS ou points ciblés.
1. **Analyse du cheminement** - Découvrez comment les utilisateurs naviguent dans votre application pour déterminer les écrans et les éléments de l’interface utilisateur qui attirent les utilisateurs et qui provoquent l’abandon des utilisateurs.

Cette section décrit comment [AEM développeurs](#developers) peuvent ensuite apprendre à instrumenter les applications AEM Mobile avec le suivi analytics.

Enfin, [Administrateurs AEM](#administrators) apprenez à :

* créer un service cloud pour Adobe Mobile Services ;
* créer une configuration de service mobile et associer une suite de rapports ;
* associer la configuration du service mobile à une application mobile ;
* Affichage des mesures via le Centre de commandes des applications AEM
* Affectez la configuration du SDK AMS à votre application mobile.

## Pour les développeurs : intégrez Analytics à votre application {#for-developers-integrate-analytics-into-your-app}

**Condition requise :** AEM administrateurs doivent configurer la configuration cloud d’Adobe Mobile Services, [comme décrit ci-dessous](#amscloudserviceconfig).

Les développeurs sont responsables des [ajout d’analytics à une application AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) si nécessaire, vous pouvez suivre, créer des rapports et comprendre la manière dont vos utilisateurs interagissent avec le contenu de votre application mobile, ainsi que mesurer les mesures clés de cycle de vie, telles que les lancements, le temps passé dans l’application et le taux de plantage.

## Pour les administrateurs - Configuration du Cloud Service Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Pour tirer parti d’Adobe Mobile Services, vous devez configurer le Cloud Service Adobe Mobile Services d’AEM avec les informations de votre compte Adobe Analytics. Le Centre de commandes des applications fournit un **Analyse des mesures** dans laquelle vous pouvez créer et associer le service cloud à votre application mobile.

Configurez le service cloud sur votre application mobile en commençant par cliquer sur l’icône d’engrenage située sur la mosaïque Analyser les mesures .

![chlimage_1-125](assets/chlimage_1-125.png)

Cliquez sur l’icône d’engrenage dans la mosaïque Analyser les mesures pour ouvrir la boîte de dialogue modale &quot;Configurer Mobile Services Analytics&quot;. Sélectionnez votre configuration dans la liste déroulante &quot;Sélectionner une configuration de service mobile&quot;. Si vous devez créer une nouvelle configuration, cliquez sur l’icône en forme de clé.

Pour créer un service cloud Adobe Mobile Service, deux étapes sont impliquées : la connexion au service et la sélection de la suite de rapports à affecter à la configuration.

Pour commencer, cliquez sur le bouton &quot;+&quot; sur la mosaïque Gérer les Cloud Services du tableau de bord.

![chlimage_1-126](assets/chlimage_1-126.png)

Lorsque vous cliquez sur &quot;&quot;**+**&quot;, le bouton **Ajouter un Cloud Service** s’affiche.

![chlimage_1-127](assets/chlimage_1-127.png)

Sélectionnez ou créez une configuration de service mobile en remplissant les champs requis comme illustré ci-dessous. Votre administrateur AEM aura besoin de ces informations pour créer correctement la connexion à Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Une fois que vous avez terminé les paramètres du compte Mobile Services, vous êtes invité à sélectionner une application. Cela permet de connecter la création de rapports d’analyse Adobe Mobile Service à cette application.

Sélectionnez le service mobile souhaité, puis cliquez sur &quot;Mettre à jour&quot; pour attribuer la configuration du service mobile et fermer la boîte de dialogue.

Maintenant que vous avez associé la configuration du service mobile à l’application AEM Mobile, la mosaïque commence à récupérer les données de mesure et à commencer à créer des rapports.

![chlimage_1-129](assets/chlimage_1-129.png)

### Fichier de configuration du SDK Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

À ce stade, votre application mobile est associée à un service cloud, mais l’application mobile ne sait pas encore comment transmettre les mesures mobiles collectées à Adobe Analytics. Pour connecter l’application mobile à Adobe Analytics, le fichier de configuration du SDK Mobile Services Adobe doit être ajouté à Adobe Experience Manager.

Dans la mosaïque Analyser les mesures , cliquez sur l’icône en forme de flèche pour afficher les entrées du menu Télécharger/charger la configuration du SDK AMS .

![chlimage_1-130](assets/chlimage_1-130.png)

La première étape consiste à obtenir la configuration du SDK à partir d’Adobe Mobile Services. Cliquez sur &quot;Télécharger la configuration du SDK AMS&quot; pour vous rediriger vers le site web d’Adobe Mobile Services à partir duquel vous pouvez télécharger le fichier de configuration. Une fois que vous avez obtenu le fichier ADBMobileConfig.json, cliquez sur &quot;Télécharger la configuration du SDK AMS&quot; pour charger le fichier de configuration dans AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Cliquez sur le bouton &quot;Télécharger la configuration de l’application Adobe Mobile Services&quot;, recherchez le fichier ADBMobileConfig.json, puis cliquez sur &quot;Télécharger&quot;.

Maintenant que l’application mobile a accès au fichier ADBMobileConfig.json, elle dispose des connaissances nécessaires pour communiquer à Adobe Analytics et commencer à créer des rapports sur les valeurs de mesures importantes qui vont contribuer à la réussite de vos applications.

## Prochaines étapes? {#what-s-next}

1. [Expérimenter le développement d’une application AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gérer le contenu d’une application mobile](/help/mobile/phonegap-manage-app-content.md)
1. [Développer une application mobile](/help/mobile/building-app-mobile-phonegap.md)
1. [Suivre les performances d’une application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Offrir une expérience personnalisée dans une application mobile grâce à Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Diffuser des messages importants à l’intention des utilisateurs](/help/mobile/phonegap-push-notifications.md)
