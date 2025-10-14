---
title: Création d’applications mobiles
description: Cette page contient un article détaillé complet sur la création d’une application mobile à l’aide du code disponible dans GitHub. Créez votre application pour l’installer sur un appareil ou un simulateur à des fins de test ou de publication sur des boutiques d’applications. Vous pouvez créer des applications localement à l’aide de l’interface de ligne de commande PhoneGap ou dans le cloud à l’aide de PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# Création d’applications mobiles{#building-mobile-applications}

{{ue-over-mobile}}

Créez votre application pour l’installer sur un appareil ou un simulateur à des fins de test ou de publication sur des boutiques d’applications. Vous pouvez créer des applications localement à l’aide de l’interface de ligne de commande PhoneGap ou dans le cloud à l’aide de PhoneGap Build.

Un article détaillé complet sur la création d’une application mobile à l’aide du code disponible dans GitHub est disponible [ici](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Déplacement de l’application vers l’instance Publish {#moving-the-application-to-the-publish-instance}

Déplacez les fichiers d’application vers l’instance de publication afin de fournir des mises à jour de contenu aux instances installées de l’application mobile et de créer l’application à l’aide du contenu publié. Les applications se composent de deux branches de nœud dans le référentiel :

* `/content/phonegap/apps/<application name>` : pages web créées et activées par les auteurs.
* `/content/phonegap/content/<application name>` : fichiers de configuration de l’application et configurations de synchronisation du contenu.

>[!NOTE]
>
>Si vous ne déplacez pas les fichiers d’application vers l’instance de publication, les auteurs de contenu ne peuvent pas mettre à jour le cache de synchronisation de contenu.

Il vous suffit de déplacer les fichiers de la branche `/content/phonegap/content/<application name>` vers l’instance de publication. Les fichiers de la branche `/content/phonegap/apps/<application name>` sont déplacés lorsque l’auteur active les pages.

AEM propose deux méthodes pour déplacer du contenu en bloc vers l’instance de publication :

* [Utilisez la commande Activer l’arborescence](/help/sites-authoring/publishing-pages.md) sur la console de réplication.
* [Créez un package](/help/sites-administering/package-manager.md) qui contient le contenu et réplique le package.

Par exemple, une application mobile nommée phonegapapp est créée. Le nœud suivant doit être déplacé vers l’instance de publication : /content/phonegap/content/phonegapapp.

**Conseil :** pour déplacer un package de l’instance d’auteur vers l’instance de publication, utilisez la commande Répliquer sur le package.

![chlimage_1-16](assets/chlimage_1-16.png)

## Création à l’aide de l’interface de ligne de commande PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilez l’application PhoneGap sur votre ordinateur à l’aide de l’interface de ligne de commande PhoneGap. Pour inclure le contenu AEM dans votre application, AEM crée un fichier ZIP contenant le contenu de votre application mobile, les configurations de synchronisation de contenu et d’autres ressources requises. Téléchargez le fichier ZIP et incluez-le dans votre version.

### Préparation de votre environnement de génération {#preparing-your-build-environment}

Pour créer à l’aide de l’interface de ligne de commande PhoneGap, vous devez installer Node.js et l’utilitaire client PhoneGap. Une connexion Internet est nécessaire pour effectuer la procédure suivante.

1. Téléchargez et installez [Node.js](https://nodejs.org/fr).
1. Ouvrez un terminal ou une invite de commande et saisissez la commande de nœud suivante pour installer l’utilitaire PhoneGap :

   ```shell
   npm install -g phonegap
   ```

   Sur un système UNIX® ou Linux®, vous devrez peut-être ajouter le préfixe `sudo` à la commande.

   Le terminal affiche les résultats d’une série de commandes de GET HTTP. Lorsque l’installation est réussie, le terminal affiche l’emplacement d’installation des bibliothèques comme dans l’exemple suivant :

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

   * Pour créer des applications pour la plateforme iOS, installez la dernière version de [Xcode](https://developer.apple.com/xcode/).
   * Pour créer des applications Android™, installez [Android™ SDK](https://developer.android.com/).

### Téléchargement du fichier ZIP de contenu {#downloading-the-content-zip-file}

Déplacez le contenu de votre application mobile vers votre système de fichiers.

1. Sur la page Applications mobiles, sélectionnez votre application.
1. (Facultatif) Pour créer l’application pour des installations complètes, dans la barre d’outils, cliquez sur l’icône Effacer le cache .

   ![Icône Effacer le cache signalée par un symbole de lien rompu.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >Le cache contient les mises à jour de contenu pour les applications installées. L’effacement du cache annule toutes les mises à jour mises en cache.

1. Dans la barre d’outils, cliquez sur l’icône Télécharger l’interface de ligne de commande Assets .

   ![Icône Télécharger l’interface de ligne de commande d’Assets indiquée par le symbole de tablette superposé.](do-not-localize/chlimage_1-1.png)

1. Après avoir enregistré le fichier ZIP, cliquez sur Fermer dans la boîte de dialogue Succès.
1. Extrayez le contenu du fichier ZIP.

### Utilisation de l’interface de ligne de commande PhoneGap pour créer {#using-the-phonegap-cli-to-build}

Utilisez l’interface de ligne de commande PhoneGap pour compiler et installer l’application. Pour plus d’informations sur l’utilisation de l’interface de ligne de commande PhoneGap, consultez la documentation de l’interface de ligne de commande PhoneGap (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`) .

1. Ouvrez un terminal ou une invite de commande et remplacez le répertoire actuel par le fichier ZIP de l’application téléchargé. Par exemple, le code suivant modifie le répertoire en fichier ng-app-cli.1392137825303.zip :

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Saisissez la commande phonegap pour la plateforme que vous ciblez. Par exemple, la commande suivante crée l’application pour Android ™ :

   ```shell
   phonegap build android
   ```

## Création À L’Aide De PhoneGap Build {#building-using-phonegap-build}

Utilisez le service cloud PhoneGap pour créer votre application. Pour effectuer cette procédure, vous devez d’abord créer une configuration de PhoneGap Build.

### Connexion à PhoneGap Build {#connecting-to-phonegap-build}

Créez une configuration de PhoneGap Build afin de pouvoir utiliser les services de PhoneGap Build depuis AEM. Indiquez le nom d&#39;utilisateur et le mot de passe du compte PhoneGap Build que vous utiliserez pour créer vos applications mobiles.

1. Ouvrez la page Outils . ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Dans la zone Opérations CQ, cliquez sur Cloud Service.
1. Cliquez sur le lien Configurer maintenant pour PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Dans la boîte de dialogue Créer une configuration , saisissez une valeur pour la propriété Titre . Par défaut, la valeur de la propriété Nom est dérivée du titre, mais vous pouvez saisir un nom. Cliquez sur Créer.
1. Dans la boîte de dialogue Configuration de PhoneGap Build, saisissez votre nom d’utilisateur et votre mot de passe PhoneGap Build, puis cliquez sur OK.

### Utilisation de PhoneGap Build {#using-phonegap-build}

Envoyez vos ressources applicatives à PhoneGap Build pour compiler pour les différentes plateformes mobiles.

1. Sur la page Applications mobiles, ouvrez votre application mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facultatif) Pour créer l’application pour des installations complètes, sélectionnez l’application et cliquez sur l’icône Effacer le cache .

   ![Icône Effacer le cache signalée par un symbole de lien rompu.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >Le cache contient les mises à jour de contenu pour les applications installées. L’effacement du cache annule toutes les mises à jour mises en cache.

1. Sélectionnez la page de démarrage, puis cliquez sur l’icône Créer à distance .

   ![Icône Créer la télécommande indiquée par deux engrenages ronds.](do-not-localize/chlimage_1-3.png)

   **Remarque :** la version Beta d’AEM Beta ne génère pas de notification de boîte de réception une fois la création terminée.

1. Dans la boîte de dialogue Succès , cliquez sur PhoneGap Build pour ouvrir la page Adobe PhoneGap Build à l’adresse `https://build.phonegap.com/apps`. Si vous attendez que votre application apparaisse, vous pouvez vérifier le Statut du PhoneGap Build à l’adresse `https://status.build.phonegap.com/`.

   Pour plus d&#39;informations sur l&#39;installation de la version, consultez la [Documentation de PhoneGap Build &#x200B;](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Les comptes de PhoneGap Build gratuits sont autorisés une application privée. Les builds PhoneGap échouent si vous créez une application privée supplémentaire.

### Les étapes suivantes {#the-next-steps}

L’étape suivante du processus de création consiste à en savoir plus sur la [structure d’une application](/help/mobile/phonegap-structure-an-app.md).
