---
title: Gérer la mosaïque d’application
description: Apprenez-en davantage sur la mosaïque « Gérer l’application » du tableau de bord de l’application qui vous permet de modifier des détails sur l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 2%

---

# Gérer la mosaïque d’application{#manage-app-tile}

{{ue-over-mobile}}

La mosaïque **`Manage App`** du tableau de bord de l’application permet d’en modifier les détails. Pour ouvrir la page Détails, cliquez sur le lien Détails de la mosaïque **`Manage App`**. Dans la page **`Manage App`**, vous pouvez modifier les paramètres Configuration de l’application PhoneGap (config.xml) et préparer votre application pour l’envoi aux différents magasins d’applications.

![chlimage_1-116](assets/chlimage_1-116.png)

## Comprendre la mosaïque `Manage App` {#understanding-the-manage-app-tile}

Vous pouvez explorer chaque mosaïque de la mosaïque **`Manage App`** pour afficher ou modifier des détails en cliquant sur le signe « ... » dans le coin inférieur droit.

### Onglet De base {#the-basic-tab}

Vous pouvez modifier les **Nom**, **Auteur**, **Description courte** et **Description** pour votre application à partir de cet onglet.

![chlimage_1-117](assets/chlimage_1-117.png)

### Onglet Avancé {#the-advanced-tab}

Chaque plateforme d’applications mobiles décrit les données collectées, en ciblant spécifiquement chaque boutique d’applications.

Les plateformes affichées sont pilotées par le contenu PhoneGap config.xml :

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Chaque boutique d’applications fournisseur, par exemple Apple App Store ou Google Play Store, nécessite une ou plusieurs captures d’écran de votre application mobile pour afficher les détails de votre application aux clients. Ces captures d’écran peuvent avoir des exigences strictes en matière de dimensions et de contenu (en fait, elles doivent vraiment représenter l’application). AEM Apps prend en charge la sélection et la gestion de ces captures d’écran pour les plateformes prises en charge, ainsi que l’affichage des dimensions de port en fonction des besoins du magasin d’applications de chaque fournisseur.

>[!NOTE]
>
>L’application AEM Verify vous permet d’envoyer des captures d’écran directement aux détails de votre application dans AEM.
>
>Voir [Démarrage rapide mobile pour AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) pour plus d’informations.

![chlimage_1-118](assets/chlimage_1-118.png)

### Métadonnées {#metadata}

>[!NOTE]
>
>Une fois que vous connaissez la mosaïque **`Manage App`**, reportez-vous à la section [ Modification des métadonnées d’application ](/help/mobile/phonegap-editmetadata.md) pour afficher et modifier les métadonnées.

#### Métadonnées courantes {#common-metadata}

Chaque application doit être associée à des métadonnées qui aident à configurer différents aspects de l&#39;application. La page Gérer l’application est séparée en deux zones différentes liées à la collecte des métadonnées. Métadonnées spécifiques à Platform et métadonnées communes.

Il existe une configuration et des métadonnées communes à toutes les plateformes.

Dans cette section, vous définissez l’URL du serveur de mise à jour de contenu, la page de destination de votre application mobile, la version PhoneGap pour la compilation, la version de votre application, le nom, la description, etc.

**Version de l’application** est la version de travail de votre application. La bonne pratique courante consiste à utiliser une notation à 3 décimales et à commencer sous la version 1.0.0 avant votre première version.

**PhoneGap Version** est la version dans laquelle vous souhaitez compiler votre application avec PhoneGap. Il est recommandé de suivre la version actuelle pour vous assurer d’obtenir les dernières fonctionnalités et les correctifs de bugs les plus performants.

**URL du serveur de mise à jour de contenu** est l’URL que votre application utilise pour appeler les mises à jour de ContentSync. Elle doit être définie sur votre URL Dispatcher ou, si vous n’utilisez pas de Dispatcher, sur l’une de vos instances de publication utilisées pour diffuser les mises à jour ContentSync dans votre application.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Cette section peut sembler vide à moins que des données ne soient renseignées dans les champs.
>
>En haut de la vue des détails, vous voyez Version de l’application, Version de PhoneGap et URL de mise à jour. Chacune de ces valeurs peut être définie dans la section Métadonnées communes . Cependant, l’ID d’application ne peut pas être modifié.

#### Métadonnées de plateforme {#platform-metadata}

Chaque plateforme définie dans PhoneGap config.xml peut contenir des propriétés de plateforme personnalisées. Un développeur AEM doit apporter sa contribution à la structure de contenu pour capturer ces propriétés. Vous trouverez un exemple fourni de propriétés spécifiques à une plateforme pour iOS.

Les métadonnées de toutes les plateformes configurées s’affichent désormais en même temps dans l’onglet Avancé de la mosaïque `Manage App`.

>[!NOTE]
>
>Les sections de métadonnées de plateforme ne sont pas utilisées par PhoneGap lors d&#39;une interface de ligne de commande ou d&#39;une version de PhoneGap distant. Au lieu de cela, AEM tente de capturer des métadonnées pour les plateformes afin qu’elles puissent être utilisées ultérieurement lors de l’envoi au magasin d’applications du fournisseur ciblé.

Pour les plateformes qu’AEM ne comprend pas, il est toujours possible pour un développeur ou une développeuse AEM d’étendre l’interface utilisateur afin de capturer ces métadonnées qui peuvent ensuite être exportées et utilisées pendant le processus d’envoi de la demande.

#### Métadonnées iOS {#ios-metadata}

L’AppStore d’Apple nécessite des métadonnées supplémentaires pour envoyer votre application en vue de sa distribution. La section des métadonnées d’iOS tente de collecter les informations requises qui peuvent être utilisées par l’outil iTMSTransporter d’Apple pour publier les métadonnées sur le compte du développeur ou de la développeuse Apple associé.

Pour obtenir les métadonnées spécifiques à Apple, créez votre application sur [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Lors de la création de votre application, Apple génère les métadonnées qui sont requises par la section des métadonnées d’iOS si vous souhaitez utiliser l’outil iTMSTransporter d’Apple pour valider et charger les métadonnées dans itunesconnect.apple.com. Si vous souhaitez obtenir les métadonnées à collecter, vous n’avez pas à renseigner les métadonnées spécifiques à iOS. Vous pouvez toujours exporter les métadonnées qui fusionnent les métadonnées iOS et les métadonnées communes et collecter toutes les captures d’écran dans un fichier zip qui peut être téléchargé à tout moment.

Le fichier zip téléchargé contient un fichier itmsp qui peut être inspecté pour le fichier metadata.xml. Le fichier itmsp contient les métadonnées exportées (dans le fichier metadata.xml), ainsi que toutes les captures d’écran associées.

La fonctionnalité d’exportation est utilisée pour fournir un moyen pratique de collecter les captures d’écran et les métadonnées qui peuvent être transmises à l’éditeur de l’application pour saisie dans le magasin d’applications spécifique au fournisseur.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Métadonnées Android™ {#android-metadata}

Lors de la sélection de la plateforme Android™, aucune métadonnée personnalisée ne peut être définie à ce stade. Lorsque vous cliquez sur le bouton de téléchargement, un fichier zip est généré avec un fichier de propriétés qui contient toutes les métadonnées et les captures d’écran associées.

La fonctionnalité d’exportation est utilisée pour fournir un moyen pratique de collecter les captures d’écran et les métadonnées qui peuvent être transmises à l’éditeur de l’application pour saisie dans le magasin d’applications spécifique au fournisseur.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL du serveur de mise à jour du contenu {#content-update-server-url}

L’une des fonctionnalités essentielles des applications AEM est la possibilité pour une application mobile de demander du nouveau contenu via ContentSync, où le contenu peut être du contenu HTML sous forme de ressources, de pages, de vidéos, d’images, de texte, etc. Une fois qu’un auteur de contenu a mis à jour du contenu, puis publie ce contenu, le serveur rend la mise à jour de contenu disponible pour le téléchargement de l’application mobile.

La propriété URL du serveur de mise à jour de contenu est l’URL qui doit pointer vers une instance de publication, directement ou via le Dispatcher ou le réseau CDN. Le format de l’URL est simple :

`https://[hostname]:[port]`

>[!NOTE]
>
>Si votre instance de serveur de création effectue une réplication sur de nombreuses instances de serveur de publication (architecture commune pour AEM), chaque serveur de publication possède le même contenu de mise à jour. En effet, la mise à jour est créée sur l’instance de création et répliquée sur toutes les instances de publication. L&#39;équilibrage de charge et le basculement sont entièrement pris en charge.

### Onglet Modules externes {#the-plugins-tab}

L’onglet **Modules externes** décrit les modules externes associés à votre application. Ces informations sont utilisées pour récupérer le module externe approprié au cours d’une génération.

![chlimage_1-122](assets/chlimage_1-122.png)

### Onglet Captures d’écran {#the-screenshots-tab}

L’onglet **Captures d’écran** affiche les résolutions de capture d’écran prises en charge sur différentes plateformes.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Pour ajouter et supprimer des captures d’écran, consultez [Modification des métadonnées d’application](/help/mobile/phonegap-editmetadata.md).

### Onglet Authentification {#the-authentication-tab}

L’onglet **Authentification** vous permet de sélectionner un client OAuth à associer à votre application et permet à un développeur ou une développeuse d’utiliser l’authentification OAuth de Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez appris comment gérer la mosaïque d’application dans le tableau de bord de l’application, reportez-vous aux ressources suivantes pour d’autres rôles de création :

* [Modification Des Métadonnées De L’Application](/help/mobile/phonegap-editmetadata.md)
* [Définitions d’application](/help/mobile/phonegap-app-definitions.md)
* [Création d’une application à l’aide de l’assistant Créer une application](/help/mobile/phonegap-create-new-app.md)
* [Importer une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Autres ressources {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
