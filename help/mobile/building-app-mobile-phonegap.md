---
title: Création d’applications mobiles
seo-title: Création d’applications mobiles
description: Cette page fournit un article détaillé sur la création d'une application mobile à l'aide du code disponible sur GitHub. Vous trouverez ci-dessous un article détaillé sur la création d'une application mobile. Créez votre application pour l'installer sur un périphérique ou un simulateur à des fins de test ou pour la publication dans les boutiques d'applications. Vous pouvez créer des applications localement à l'aide de l'interface de ligne de commande PhoneGap ou dans le cloud à l'aide du PhoneGap Build.
seo-description: Cette page fournit un article détaillé sur la création d'une application mobile à l'aide du code disponible sur GitHub. Vous trouverez ci-dessous un article détaillé sur la création d'une application mobile. Créez votre application pour l'installer sur un périphérique ou un simulateur à des fins de test ou pour la publication dans les boutiques d'applications. Vous pouvez créer des applications localement à l'aide de l'interface de ligne de commande PhoneGap ou dans le cloud à l'aide du PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 4%

---


# Création d’applications mobiles{#building-mobile-applications}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Générez votre application à installer sur un périphérique ou un simulateur à des fins de test ou de publication dans des boutiques d’applications. Vous pouvez créer des applications localement à l&#39;aide de l&#39;interface de ligne de commande PhoneGap ou dans le cloud à l&#39;aide du PhoneGap Build.

Un article détaillé sur la création d&#39;une application mobile à l&#39;aide du code disponible sur GitHub est disponible [ici](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Déplacement de l’application vers l’instance de publication {#moving-the-application-to-the-publish-instance}

Déplacez les fichiers d’application vers l’instance de publication afin de pouvoir fournir des mises à jour de contenu aux instances installées de l’application mobile et de créer l’application à l’aide du contenu publié. Les applications se composent de deux branches de noeud dans le référentiel :

* `/content/phonegap/apps/<application name>`: Pages Web que les auteurs créent et activent.
* `/content/phonegap/content/<application name>`: Fichiers de configuration d’application et configurations Content Sync.

>[!NOTE]
>
>Si vous ne déplacez pas les fichiers de l’application vers l’instance de publication, les auteurs de contenu ne peuvent pas mettre à jour le cache de synchronisation de contenu.

Il vous suffit de déplacer les fichiers de la `/content/phonegap/content/<application name>` branche vers l’instance de publication. Les fichiers de la `/content/phonegap/apps/<application name>` branche sont déplacés lorsque l&#39;auteur active les pages.

aem fournit deux méthodes pour déplacer du contenu en vrac vers l’instance de publication :

* [Utilisez la commande](/help/sites-authoring/publishing-pages.md) Activer l&#39;arborescence de la console de réplication.
* [Créez un package](/help/sites-administering/package-manager.md) qui contient le contenu et réplique le package.

Par exemple, une application mobile appelée phonegapapp est créée. Le noeud suivant doit être déplacé vers l’instance de publication : /content/phonegap/content/phonegapapp.

**Conseil :** Pour déplacer un package de l’instance d’auteur vers l’instance de publication, utilisez la commande Répliquer du package.

![chlimage_1-16](assets/chlimage_1-16.png)

## Création à l&#39;aide de l&#39;interface de ligne de commande PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilez l&#39;application PhoneGap sur votre ordinateur à l&#39;aide de l&#39;interface de ligne de commande PhoneGap (CLI). Pour inclure le contenu AEM dans votre application, AEM crée un fichier ZIP qui contient le contenu de votre application mobile, les configurations de synchronisation de contenu et d’autres ressources requises. Téléchargez le fichier ZIP et incluez-le dans votre compilation.

### Préparation de votre Environnement de création {#preparing-your-build-environment}

Pour créer à l’aide de l’interface de ligne de commande PhoneGap, vous devez installer Node.js et l’utilitaire client PhoneGap. Vous avez besoin d’une connexion Internet pour effectuer la procédure suivante.

1. Download and install [Node.js](https://nodejs.org/).
1. Ouvrez un terminal ou une invite de commande et saisissez la commande de noeud suivante pour installer l&#39;utilitaire PhoneGap :

   ```shell
   npm install -g phonegap
   ```

   Sur un système Unix ou Linux, vous devrez peut-être préfixer la commande par `sudo`.

   Le terminal affiche les résultats d&#39;une série de commandes de GET HTTP. Une fois l&#39;installation terminée, le terminal indique où les bibliothèques sont installées, comme dans l&#39;exemple suivant :

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

1. (Facultatif) Procurez-vous le SDK de la plateforme mobile que vous ciblez :

   * Pour créer des applications pour la plate-forme iOS, installez la dernière version de [Xcode](https://developer.apple.com/xcode/).
   * Pour créer des applications Android, installez le SDK [](https://developer.android.com/)Android.

### Téléchargement du fichier ZIP de contenu {#downloading-the-content-zip-file}

Déplacez le contenu de votre application mobile vers votre système de fichiers.

1. Dans la page Applications mobiles, sélectionnez votre application.
1. (Facultatif) Pour créer l’application pour des installations complètes, sur la barre d’outils, cliquez ou appuyez sur l’icône Effacer le cache.

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >Le cache contient des mises à jour de contenu pour les applications installées. L’effacement du cache annule toutes les mises à jour mises en cache.

1. Sur la barre d’outils, cliquez ou appuyez sur l’icône Télécharger les actifs de l’interface de ligne de commande.

   ![](do-not-localize/chlimage_1-1.png)

1. Après avoir enregistré le fichier ZIP, cliquez sur Fermer dans la boîte de dialogue Réussite.
1. Extrayez le contenu du fichier ZIP.

### Utilisation de l’interface de ligne de commande PhoneGap pour la création {#using-the-phonegap-cli-to-build}

Utilisez l’interface de ligne de commande PhoneGap pour compiler et installer l’application. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;interface de ligne de commande PhoneGap, consultez la documentation de l&#39;interface [de ligne de](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) commande PhoneGap.

1. Ouvrez une invite de terminal ou de commande et remplacez le répertoire actuel par le fichier ZIP de l’application téléchargé. Par exemple, le fichier suivant remplace le répertoire ng-app-cli.1392137825303.zip :

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Saisissez la commande phonegap pour la plateforme que vous ciblez. Par exemple, la commande suivante crée l’application pour Android :

   ```shell
   phonegap build android
   ```

## Création à l’aide du PhoneGap Build {#building-using-phonegap-build}

Utilisez le service PhoneGap cloud pour créer votre application. Pour effectuer cette procédure, vous devez d’abord créer une configuration de PhoneGap Build.

### Connexion à PhoneGap Build {#connecting-to-phonegap-build}

Créez une configuration de PhoneGap Build afin de pouvoir utiliser les services de PhoneGap Build depuis AEM. Indiquez le nom d’utilisateur et le mot de passe du compte PhoneGap Build que vous utiliserez pour créer vos applications mobiles.

1. Ouvrez la page Outils. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Dans la zone Opérations CQ, cliquez sur Cloud Services.
1. Cliquez sur le lien Configurer maintenant pour le PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Dans la boîte de dialogue Créer une configuration, entrez une valeur pour la propriété Title. Par défaut, la valeur de la propriété Name est dérivée du titre, mais vous pouvez saisir un nom. Cliquez sur Créer.
1. Dans la boîte de dialogue Configuration du PhoneGap Build, saisissez votre nom d’utilisateur et votre mot de passe de PhoneGap Build, puis cliquez sur OK.

### Utilisation du PhoneGap Build {#using-phonegap-build}

Envoyez vos ressources d’application en PhoneGap Build pour la compilation pour les différentes plateformes mobiles.

1. Sur la page Applications mobiles, ouvrez votre application mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facultatif) Pour créer l’application pour des installations complètes, sélectionnez l’application et cliquez sur l’icône Effacer le cache.

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >Le cache contient des mises à jour de contenu pour les applications installées. L’effacement du cache annule toutes les mises à jour mises en cache.

1. Sélectionnez la page de démarrage, puis cliquez sur l’icône Créer à distance.

   ![](do-not-localize/chlimage_1-3.png)

   **Remarque :** La version bêta de AEM version bêta ne crée pas de notification de boîte de réception une fois la compilation terminée.

1. Dans la boîte de dialogue Succès, cliquez sur PhoneGap Build pour ouvrir la page Adobe PhoneGap Build à l’adresse [https://build.phonegap.com/apps](https://build.phonegap.com/apps). Si vous attendez l’affichage de votre application, vous pouvez vérifier la page État [du](https://status.build.phonegap.com/) PhoneGap Build.

   Pour plus d’informations sur l’installation de la compilation, voir la Documentation [](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29)PhoneGap Build.

   >[!NOTE]
   >
   >Les comptes en PhoneGap Build libre sont autorisés dans une seule application privée. Les versions PhoneGap échouent si vous créez une application privée supplémentaire.

### Étapes suivantes {#the-next-steps}

L’étape suivante après le processus de création consiste à découvrir la [structure d’une application](/help/mobile/phonegap-structure-an-app.md).
