---
title: Mosaïque Gérer l’application
description: Consultez cette page pour en savoir plus sur la mosaïque Gérer l’application du tableau de bord de l’application qui permet de modifier les détails de l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 2%

---

# Mosaïque Gérer l’application{#manage-app-tile}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Le **Gérer l’application** La mosaïque du tableau de bord de l’application permet de modifier les détails de l’application. Pour ouvrir la page Détails, cliquez sur le lien Détails de la mosaïque Gérer l’application . Dans la page Gérer l’application , vous pouvez modifier les paramètres Configuration de l’application PhoneGap (config.xml) et préparer votre application à l’envoi aux différents magasins d’applications.

![chlimage_1-116](assets/chlimage_1-116.png)

## Présentation de la mosaïque Gérer l’application {#understanding-the-manage-app-tile}

Vous pouvez explorer chaque mosaïque de la **Gérer l’application** pour afficher ou modifier les détails en cliquant sur &quot;...&quot;. dans le coin inférieur droit.

### Onglet De base {#the-basic-tab}

Vous pouvez modifier la variable **Nom**, **Auteur**, **Description courte**, et la variable **Description** pour votre application depuis cet onglet.

![chlimage_1-117](assets/chlimage_1-117.png)

### Onglet Avancé {#the-advanced-tab}

Chaque plateforme d’applications mobiles décrit les données collectées, ciblant spécifiquement chaque boutique d’applications.

Les plateformes affichées sont pilotées par le contenu du fichier de configuration.xml PhoneGap :

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Chaque boutique d’applications de fournisseur (Apple App Store ou Google Play Store, par exemple) nécessite une ou plusieurs captures d’écran de votre application mobile pour afficher les détails de votre application aux clients. Ces captures d’écran peuvent avoir des exigences strictes concernant les dimensions et le contenu (en fait, elles doivent représenter fidèlement l’application). Les applications d’AEM prennent en charge la sélection et la gestion de ces captures d’écran pour les plateformes prises en charge et les dimensions de port requises par la boutique d’applications de chaque fournisseur.

>[!NOTE]
>
>L’application AEM Vérifier permet d’envoyer des captures d’écran directement aux détails de votre application dans AEM.
>
>Voir [Démarrage rapide mobile pour la vérification AEM](/help/mobile/phonegap-mobile-quickstart.md) pour plus d’informations.

![chlimage_1-118](assets/chlimage_1-118.png)

### Métadonnées {#metadata}

>[!NOTE]
>
>Une fois que vous connaissez le **Gérer l’application** mosaïque, voir [Modification des métadonnées d’application](/help/mobile/phonegap-editmetadata.md) pour afficher et modifier les métadonnées.

#### Métadonnées courantes {#common-metadata}

Chaque application doit être associée à des métadonnées qui facilitent la configuration de différents aspects de l’application. La page Gérer l’application est divisée en deux zones distinctes liées à la collecte de métadonnées. Métadonnées spécifiques à la plateforme et métadonnées communes.

Il existe une configuration et des métadonnées communes à toutes les plateformes.

Dans cette section, vous définissez l’URL du serveur de mise à jour de contenu, la page d’entrée de votre application mobile, la version de PhoneGap à des fins de compilation, la version de votre application, le nom, la description, etc.

**Version de l’application** est la version opérationnelle de votre application. Il est recommandé d’utiliser une notation à 3 décimales et de commencer sous 1.0.0 avant la première version.

**Version de PhoneGap** est la version dans laquelle vous souhaitez compiler votre application avec PhoneGap. La bonne pratique consiste à suivre la version actuelle afin de vous assurer d’obtenir les fonctionnalités et correctifs les plus récents et les plus performants.

**URL du serveur de mise à jour de contenu** est l’URL que votre application utilisera pour appeler les mises à jour ContentSync. Il doit être défini sur votre URL de Dispatcher ou, si vous n’utilisez pas un Dispatcher, sur l’une de vos instances de publication qui sera utilisée pour diffuser les mises à jour ContentSync à votre application.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Cette section peut apparaître vide, sauf si des données sont renseignées dans les champs.
>
>Dans la partie supérieure de la vue détaillée, vous verrez la version de l’application, la version PhoneGap et l’URL de mise à jour. Chacune de ces valeurs peut être définie dans la section Métadonnées courantes . Toutefois, l’ID de l’application ne peut pas être modifié.

#### Métadonnées de plateforme {#platform-metadata}

Chaque plateforme définie dans le fichier de configuration PhoneGap config.xml peut contenir des propriétés de plateforme personnalisées. Un développeur AEM doit contribuer à la structure de contenu pour capturer ces propriétés. Vous trouverez un exemple de propriétés spécifiques à la plateforme pour iOS.

Les métadonnées pour toutes les plateformes configurées s’affichent désormais en même temps dans l’onglet Avancé de la mosaïque Gérer l’application .

>[!NOTE]
>
>Les sections de métadonnées de la plateforme ne sont pas utilisées par PhoneGap lors d’une version d’interface de ligne de commande ou de PhoneGap à distance, mais plutôt AEM tentatives de capture des métadonnées pour les plateformes afin qu’elles puissent être utilisées ultérieurement lors de l’envoi à la boutique d’applications du fournisseur ciblé.

Pour les plateformes qui ne sont pas comprises par AEM, il est toujours possible pour un développeur AEM d’étendre l’interface utilisateur afin de capturer ces métadonnées qui pourront ensuite être exportées et utilisées pendant le processus d’envoi de l’application.

#### Métadonnées iOS {#ios-metadata}

L’AppStore Apple requiert des métadonnées supplémentaires pour envoyer votre application en vue de sa distribution. La section Métadonnées iOS tente de collecter les informations requises qui peuvent être utilisées par l’outil Apple TMSTransporter pour publier les métadonnées sur le compte de développeur Apple associé.

Pour obtenir les métadonnées spécifiques à Apple, vous devez d’abord créer votre application sur [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Lors de la création de votre application, Apple génère les métadonnées requises par la section Métadonnées iOS si vous souhaitez utiliser l’outil Apple iTMSTransporter pour valider et charger les métadonnées sur itunesconnect.apple.com. Si vous souhaitez simplement obtenir les métadonnées à collecter, il n’est pas nécessaire de renseigner les métadonnées spécifiques à iOS. Vous pouvez toujours exporter les métadonnées qui fusionneront iOS et les métadonnées communes et collecteront toutes les captures d’écran dans un fichier zip qui peut être téléchargé à tout moment.

Le fichier zip téléchargé contient un fichier itmsp qui peut être inspecté pour le fichier metadata.xml. Le fichier itmsp contient les métadonnées exportées (dans le fichier metadata.xml ), ainsi que toutes les captures d’écran associées.

La fonctionnalité d’exportation permet de collecter facilement les captures d’écran et les métadonnées qui peuvent être transmises à l’éditeur de l’application pour saisie dans la boutique d’applications spécifique au fournisseur.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Métadonnées Android™ {#android-metadata}

Lors de la sélection de la plateforme Android™, aucune métadonnée personnalisée ne peut être définie à ce stade. Lorsque vous cliquez sur le bouton de téléchargement, un fichier zip est généré avec un fichier de propriétés qui contient toutes les métadonnées et les captures d’écran associées.

La fonctionnalité d’exportation permet de collecter facilement les captures d’écran et les métadonnées qui peuvent être transmises à l’éditeur de l’application pour saisie dans la boutique d’applications spécifique au fournisseur.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL du serveur de mise à jour du contenu {#content-update-server-url}

L’une des fonctionnalités clés des applications AEM est la possibilité de demander un nouveau contenu à une application mobile via ContentSync, où le contenu peut être des ressources html, des pages, des vidéos, des images, du texte, etc. Une fois qu’un auteur de contenu a mis à jour le contenu, puis le publie, le serveur met à disposition la mise à jour de contenu pour que l’application mobile puisse la télécharger.

La propriété URL du serveur de mise à jour de contenu est l’URL qui doit pointer vers une instance de publication ; directement ou par le biais du Dispatcher ou du réseau de diffusion de contenu. Le format de l’URL est simple :

`https://[hostname]:[port]`

>[!NOTE]
>
>Si votre instance de serveur de création effectue une réplication sur plusieurs instances de serveur de publication (architecture commune pour AEM), chaque serveur de publication aura le même contenu de mise à jour, car la mise à jour est créée sur l’auteur et répliquée sur toutes les instances de publication. Fondamentalement, l’équilibrage de charge et le basculement sont entièrement pris en charge.

### Onglet Plugins {#the-plugins-tab}

Le **Modules externes** Cette section décrit les modules externes associés à votre application. Ces informations seront utilisées pour récupérer le module externe approprié pendant une génération.

![chlimage_1-122](assets/chlimage_1-122.png)

### Onglet Captures d’écran {#the-screenshots-tab}

Le **Captures d’écran** affiche les résolutions d’écran prises en charge sur différentes plateformes.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Pour ajouter et supprimer des captures d’écran, voir [Modification des métadonnées d’application](/help/mobile/phonegap-editmetadata.md).

### Onglet Authentification {#the-authentication-tab}

Le **Authentification** Cet onglet vous permet de sélectionner un client OAuth à associer à votre application et permet à un développeur d’utiliser l’authentification OAuth de Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Les étapes suivantes {#the-next-steps}

Une fois que vous avez appris la procédure de gestion de la mosaïque d’application dans le tableau de bord de l’application, consultez les ressources suivantes pour d’autres rôles de création :

* [Modification des métadonnées d’application](/help/mobile/phonegap-editmetadata.md)
* [Définitions des applications](/help/mobile/phonegap-app-definitions.md)
* [Création d’une application à l’aide de l’assistant Créer une application](/help/mobile/phonegap-create-new-app.md)
* [Importation d’une application hybride existante](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
