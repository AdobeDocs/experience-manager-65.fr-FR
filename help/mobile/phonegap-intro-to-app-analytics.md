---
title: Suivi des performances des applications avec Adobe Mobile Analytics
description: Avec Adobe Mobile Services, vous pouvez obtenir des informations sur la manière dont vos utilisateurs utilisent vos applications mobiles en suivant l'utilisation, les blocages d'applications, les détails d'appareils et de nombreuses autres mesures critiques de vos applications mobiles. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# Suivi des performances des applications avec Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

{{ue-over-mobile}}

Vous souhaitez augmenter les conversions et la fidélité des clients.

Vous souhaitez offrir à vos clients des expériences pertinentes et attrayantes.

Que fait votre application AEM Mobile pour vos campagnes marketing ?

Comment pouvez-vous affiner vos applications mobiles pour offrir la meilleure expérience à vos utilisateurs ?

Avec Adobe Mobile Services, vous pouvez obtenir des informations sur la manière dont vos utilisateurs utilisent vos applications mobiles en suivant l&#39;utilisation, les blocages d&#39;applications, les détails d&#39;appareils et de nombreuses autres mesures critiques de vos applications mobiles.

Adobe Experience Manager Mobile offre un aperçu des détails de votre analyse mobile directement depuis le tableau de bord de l’application AEM Mobile. La **Mosaïque Mesures mobiles** du tableau de bord fournit Real-Time Analytics pour votre application mobile, ce qui permet aux développeurs, aux auteurs et aux administrateurs d’avoir un aperçu rapide de l’intégrité de votre application mobile. Sous cet écran, l’analytics est alimenté par le SDK [Adobe Mobile Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html). Le SDK Adobe Mobile Analytics peut être connecté à vos applications en mode natif ou par le biais d’un plug-in PhoneGap Bridge pour les webviews. Les mesures sont collectées et mises en cache sur l’appareil jusqu’à la connexion de celui-ci. Les données sont ensuite transmises au cloud Mobile Services d’Adobe pour rapport et analyse.

Adobe Mobile Analytics SDK fournit les éléments suivants :

1. **Collecte de données pour les canaux mobiles** - Collectez des données complètes pour vos sites web et applications mobiles sur tous les principaux systèmes d’exploitation.
1. **Analyse de l’engagement mobile** - Comprenez l’engagement des utilisateurs dans votre application mobile, votre site web ou votre vidéo, y compris la fréquence à laquelle les consommateurs lancent le canal, s’ils y effectuent des achats, etc.
1. **Tableaux de bord et rapports des applications mobiles** - Obtenez des rapports d’utilisation qui incluent des mesures de cycle de vie pour vos applications et des mesures d’app store. Consultez les tendances pour les utilisateurs, les lancements, la durée de session moyenne, la durée de rétention et les blocages.
1. **Analyse des campagnes mobiles** - Quantifiez l’efficacité des campagnes spécifiques aux appareils mobiles telles que les SMS, les annonces de recherches mobiles, les annonces pour appareils mobiles et les codes QR.
1. **Analyse de géolocalisation** - Trouvez où les utilisateurs de votre application lancent et interagissent avec vos expériences mobiles par localisation GPS ou points ciblés.
1. **Analyse du cheminement** - Découvrez comment les utilisateurs naviguent dans votre application pour déterminer quels écrans et éléments d’interface interagissent avec les utilisateurs et lesquels provoquent le décrochage de ces derniers.

Cette section décrit comment les [développeurs AEM](#developers) peuvent ensuite apprendre à instrumenter les applications AEM Mobile avec le suivi Analytics.

Enfin, [les administrateurs AEM](#administrators) apprennent à :

* créer un service cloud pour Adobe Mobile Services
* créer une configuration de service mobile et associer une suite de rapports
* associer la configuration de mobile service à une application mobile
* affichage des mesures via le centre de commande des applications AEM
* affectez la configuration AMS SDK à votre application mobile.

## Pour les développeurs - Intégrer Analytics à votre application {#for-developers-integrate-analytics-into-your-app}

**Prérequis :** les administrateurs AEM doivent configurer la configuration cloud d’Adobe Mobile Services, [comme décrit ci-dessous](#amscloudserviceconfig).

Les développeurs sont chargés d’[ajouter des analyses à une application AEM Mobile](/help/mobile/phonegap-add-analytics-to-apps.md) si nécessaire, pour suivre, générer des rapports et comprendre comment vos utilisateurs interagissent avec le contenu de votre application mobile et pour mesurer les mesures de cycle de vie clés telles que les lancements, le temps passé dans l’application et le taux de plantage.

## Pour les administrateurs : configuration du Cloud Service Mobile Services d’Adobe {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Pour tirer parti d’Adobe Mobile Services, vous devez configurer le Cloud Service AEM Adobe Mobile Services à l’aide des informations de votre compte Adobe Analytics. Le Centre de commande des applications fournit une mosaïque **Analyser les mesures** dans laquelle vous pouvez créer et associer le service cloud à votre application mobile.

Configurer le service cloud sur votre application mobile commence par cliquer sur l’icône d’engrenage sur la mosaïque Analyser les mesures .

![chlimage_1-125](assets/chlimage_1-125.png)

Cliquez sur l’icône en forme d’engrenage dans la mosaïque Analyser les mesures pour ouvrir la boîte de dialogue modale Configurer Mobile Services Analytics. Sélectionnez votre configuration dans le menu déroulant « Sélectionner une configuration de service mobile ». Si vous devez créer une configuration, cliquez sur le bouton Clé à molette.

Pour créer un service cloud Adobe Mobile Service, deux étapes sont nécessaires : la connexion au service et la sélection de la suite de rapports à affecter à la configuration.

Pour commencer, cliquez sur le bouton « + » sur la mosaïque Gérer les Cloud Service du tableau de bord.

![chlimage_1-126](assets/chlimage_1-126.png)

Après avoir cliqué sur le bouton « **+** », l’assistant **Ajouter un Cloud Service** s’affiche.

![chlimage_1-127](assets/chlimage_1-127.png)

Sélectionnez ou créez une configuration de service mobile en remplissant les champs obligatoires comme illustré ci-dessous. Votre administrateur AEM a besoin de ces informations pour établir la connexion à Adobe Mobile Services.

![chlimage_1-128](assets/chlimage_1-128.png)

Une fois que vous avez terminé les paramètres du compte Mobile Services, vous êtes invité à sélectionner une application. Cela connecte les rapports d’analyse Adobe Mobile Service à cette application.

Sélectionnez le service mobile souhaité, puis cliquez sur « Mettre à jour » pour attribuer la configuration du service mobile et fermer la boîte de dialogue.

Maintenant que vous avez associé la configuration du service mobile à l’application AEM Mobile, la mosaïque commence à récupérer les données de mesure et à créer des rapports.

![chlimage_1-129](assets/chlimage_1-129.png)

### Fichier de configuration SDK Adobe Mobile Services {#adobe-mobile-services-sdk-config-file}

À ce stade, votre application mobile est associée à un service cloud, mais l’application mobile ne sait pas encore comment communiquer les mesures mobiles collectées à Adobe Analytics. Pour connecter l’application mobile à Adobe Analytics, le fichier de configuration SDK Adobe Mobile Services doit être ajouté à Adobe Experience Manager.

Dans la mosaïque Analyser les mesures , cliquez sur l’icône de flèche pour afficher les entrées du menu Télécharger/charger la configuration SDK AMS .

![chlimage_1-130](assets/chlimage_1-130.png)

La première étape consiste à obtenir la configuration SDK à partir d’Adobe Mobile Services. Cliquez sur Télécharger la configuration SDK d’AMS pour être redirigé vers le site web d’Adobe Mobile Services à partir duquel vous pouvez télécharger le fichier de configuration. Une fois que vous avez obtenu le fichier ADBMobileConfig.json, cliquez sur « Télécharger la configuration SDK d’AMS » pour télécharger le fichier de configuration dans AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Cliquez sur le bouton « Charger la configuration de l’application Mobile Services Adobe » et recherchez le fichier ADBMobileConfig.json, puis cliquez sur « Charger ».

Maintenant que l’application mobile a accès au fichier ADBMobileConfig.json, elle sait comment communiquer avec Adobe Analytics et commencer à créer des rapports sur ces valeurs de mesures importantes qui contribuent au succès de vos applications.

## Quelle est la suite ? {#what-s-next}

1. [Démarrer mon expérience d’application AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gérer le contenu de mon application](/help/mobile/phonegap-manage-app-content.md)
1. [Créer mon application](/help/mobile/building-app-mobile-phonegap.md)
1. [Suivre les performances de mon application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Offrir une expérience d’application personnalisée avec Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Envoyer des messages importants à mes utilisateurs](/help/mobile/phonegap-push-notifications.md)
