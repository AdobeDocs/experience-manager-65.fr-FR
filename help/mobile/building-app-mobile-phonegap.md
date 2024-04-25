---
title: Création d’applications mobiles
description: Cette page fournit un article détaillé complet sur la création d’une application mobile à l’aide du code disponible sur GitHub. Créez votre application à installer sur un appareil ou un simulateur à des fins de test ou de publication dans les boutiques d’applications. Vous pouvez créer des applications localement à l’aide de l’interface de ligne de commande PhoneGap ou dans le cloud à l’aide de PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 3%

---

# Création d’applications mobiles{#building-mobile-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Créez votre application à installer sur un appareil ou un simulateur à des fins de test ou de publication dans les boutiques d’applications. Vous pouvez créer des applications localement à l’aide de l’interface de ligne de commande PhoneGap ou dans le cloud à l’aide de PhoneGap Build.

Un article complet détaillé sur la création d’une application mobile à l’aide du code disponible sur GitHub est disponible. [here](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Déplacement de l’application vers l’instance de publication {#moving-the-application-to-the-publish-instance}

Déplacez les fichiers d’application vers l’instance de publication afin de pouvoir fournir des mises à jour de contenu aux instances installées de l’application mobile et de créer l’application à l’aide du contenu publié. Les applications se composent de deux branches de noeud dans le référentiel :

* `/content/phonegap/apps/<application name>`: les pages web que les auteurs créent et activent.
* `/content/phonegap/content/<application name>`: fichiers de configuration de l’application et configurations de synchronisation de contenu.

>[!NOTE]
>
>Si vous ne déplacez pas les fichiers de l’application vers l’instance de publication, les auteurs de contenu ne peuvent pas mettre à jour le cache de synchronisation du contenu.

Il vous suffit de déplacer les fichiers dans la variable `/content/phonegap/content/<application name>` branche vers l’instance de publication. Les fichiers de la variable `/content/phonegap/apps/<application name>` sont déplacées lorsque l’auteur active les pages.

AEM fournit deux méthodes pour déplacer du contenu en bloc vers l’instance de publication :

* [Utilisation de la commande Activer l’arborescence](/help/sites-authoring/publishing-pages.md) sur la console de réplication.
* [Création d’un package](/help/sites-administering/package-manager.md) qui contient le contenu et réplique le module.

Par exemple, une application mobile nommée phonegapapp est créée. Le noeud suivant doit être déplacé vers l’instance de publication : /content/phonegap/content/phonegapapp.

**Conseil :** Pour déplacer un module de l’instance d’auteur vers l’instance de publication, utilisez la commande Répliquer du module.

![chlimage_1-16](assets/chlimage_1-16.png)

## Création à l’aide de l’interface de ligne de commande PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilez l’application PhoneGap sur votre ordinateur à l’aide de l’interface de ligne de commande PhoneGap (CLI). Pour inclure le contenu AEM dans votre application, AEM crée un fichier ZIP qui contient le contenu de votre application mobile, les configurations de synchronisation de contenu et d’autres ressources requises. Téléchargez le fichier ZIP et incluez-le dans votre version.

### Préparation de votre environnement de création {#preparing-your-build-environment}

Pour créer à l’aide de l’interface de ligne de commande de PhoneGap, vous devez installer Node.js et l’utilitaire client PhoneGap. Vous avez besoin d’une connexion Internet pour effectuer la procédure suivante.

1. Télécharger et installer [Node.js](https://nodejs.org/fr).
1. Ouvrez un terminal ou une invite de commande et saisissez la commande de noeud suivante pour installer l’utilitaire PhoneGap :

   ```shell
   npm install -g phonegap
   ```

   Sur un système UNIX® ou Linux®, vous devrez peut-être ajouter un préfixe à la commande `sudo`.

   Le terminal affiche les résultats d’une série de commandes de GET HTTP. Une fois l’installation terminée, le terminal indique où les bibliothèques sont installées, comme dans l’exemple suivant :

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. (Facultatif) Obtenez le SDK pour la plateforme mobile que vous ciblez :

   * Pour créer des applications pour la plateforme iOS, installez la dernière version de la [Xcode](https://developer.apple.com/xcode/).
   * Pour créer des applications Android™, installez le [SDK Android™](https://developer.android.com/).

### Téléchargement du fichier ZIP de contenu {#downloading-the-content-zip-file}

Déplacez le contenu de votre application mobile vers votre système de fichiers.

1. Sur la page Applications mobiles , sélectionnez votre application.
1. (Facultatif) Pour créer l’application pour les installations complètes, cliquez sur l’icône Effacer le cache dans la barre d’outils.

   ![Icône Effacer le cache indiquée par un symbole de lien rompu.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >Le cache contient les mises à jour de contenu pour les applications installées. L’effacement du cache empêche toutes les mises à jour mises en cache.

1. Dans la barre d’outils, cliquez sur l’icône Télécharger les ressources de l’interface de ligne de commande.

   ![Icône Télécharger les ressources en ligne de commande indiquée par le symbole de tablette qui se chevauche.](do-not-localize/chlimage_1-1.png)

1. Après avoir enregistré le fichier ZIP, cliquez sur Fermer dans la boîte de dialogue Succès.
1. Extrayez le contenu du fichier ZIP.

### Utilisation de l’interface de ligne de commande PhoneGap pour créer {#using-the-phonegap-cli-to-build}

Utilisez l’interface de ligne de commande PhoneGap pour compiler et installer l’application. Pour plus d’informations sur l’utilisation de l’interface de ligne de commande PhoneGap, voir Interface de ligne de commande PhoneGap (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`).

1. Ouvrez une invite de commande ou de terminal et remplacez le répertoire actuel par le fichier ZIP de l’application téléchargé. Par exemple, le fichier suivant remplace le répertoire par le fichier ng-app-cli.1392137825303.zip :

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Saisissez la commande phonegap de la plateforme que vous ciblez. Par exemple, la commande suivante crée l’application pour Android™ :

   ```shell
   phonegap build android
   ```

## Construire en PhoneGap Build {#building-using-phonegap-build}

Utilisez le service cloud PhoneGap pour créer votre application. Pour effectuer cette procédure, vous devez d’abord créer une configuration de PhoneGap Build.

### Connexion au PhoneGap Build {#connecting-to-phonegap-build}

Créez une configuration de PhoneGap Build afin de pouvoir utiliser les services de PhoneGap Build depuis AEM. Indiquez le nom d’utilisateur et le mot de passe du compte PhoneGap Build que vous utiliserez pour créer vos applications mobiles.

1. Ouvrez la page Outils . ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Dans la zone Opérations CQ, cliquez sur Cloud Service.
1. Cliquez sur le lien Configurer maintenant pour PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Dans la boîte de dialogue Créer une configuration, saisissez une valeur pour la propriété Titre . Par défaut, la valeur de la propriété Name est dérivée du titre, mais vous pouvez saisir un nom. Cliquez sur Créer.
1. Dans la boîte de dialogue Configuration du PhoneGap Build, saisissez votre nom d’utilisateur et votre mot de passe PhoneGap Build, puis cliquez sur OK.

### Utilisation du PhoneGap Build {#using-phonegap-build}

Envoyez vos ressources d’application en PhoneGap Build pour la compilation pour les différentes plateformes mobiles.

1. Sur la page Applications mobiles , ouvrez votre application mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facultatif) Pour créer l’application pour les installations complètes, sélectionnez l’application et cliquez sur l’icône Effacer le cache .

   ![Icône Effacer le cache indiquée par un symbole de lien rompu.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >Le cache contient les mises à jour de contenu pour les applications installées. L’effacement du cache empêche toutes les mises à jour mises en cache.

1. Sélectionnez la page de démarrage, puis cliquez sur l’icône Créer à distance .

   ![Icône Créer à distance indiquée par deux vitesses rondes.](do-not-localize/chlimage_1-3.png)

   **Remarque :** La version bêta d’AEM bêta ne crée pas de notification de boîte de réception une fois la génération terminée.

1. Dans la boîte de dialogue Succès, cliquez sur PhoneGap Build pour ouvrir la page Adobe PhoneGap Build à l’adresse `https://build.phonegap.com/apps`. Si vous attendez l’affichage de votre application, vous pouvez vérifier l’état du PhoneGap Build à l’adresse `https://status.build.phonegap.com/`.

   Pour plus d’informations sur l’installation de la version, voir [Documentation du PhoneGap Build](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Les comptes en PhoneGap Build libre sont autorisés dans une application privée. Les versions PhoneGap échouent si vous créez une application privée supplémentaire.

### Les étapes suivantes {#the-next-steps}

L’étape suivante après le processus de création consiste à en apprendre davantage sur la variable [Structure d’une application](/help/mobile/phonegap-structure-an-app.md).
