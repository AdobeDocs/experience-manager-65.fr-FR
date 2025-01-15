---
title: Développement d’applications avec l’interface de ligne de commande PhoneGap
description: Découvrez comment développer des applications mobiles avec l’interface de ligne de commande PhoneGap à l’aide d’un environnement de développement amorcé.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Développement d’applications avec l’interface de ligne de commande PhoneGap{#developing-apps-with-phonegap-cli}

{{ue-over-mobile}}

En tant que développeur ou développeuse, vous pouvez à tout moment exécuter votre application sur un appareil ou dans un émulateur, à condition que vous ayez configuré votre environnement de développement.

Pour exécuter les exemples ci-dessous, vous avez besoin d’un système qui exécute macOS X avec Xcode ou d’un système Mac/Win/Linux sur lequel Android™ SDK est installé.

## Bootstrap de votre environnement de développement {#bootstrap-your-development-environment}

Configurer l’interface de ligne de commande PhoneGap (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

Pour iOS : pour développer sur iPhone et iPad, vous avez besoin de l’IDE Xcode d’Apple.

* Téléchargez-le gratuitement [ici](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* Guide de la plateforme PhoneGap iOS (`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

Pour Android™ : pour développer sur iPhone et iPad, vous avez besoin de l’IDE Android™ Studio de Google.

* Téléchargez-le gratuitement [ici](https://developer.android.com/studio).
* Guide de la plateforme PhoneGap Android™ (`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## Télécharger le Source {#download-the-source}

Une fois votre environnement de développement amorcé, téléchargez la source à partir de la mosaïque de build de l’application AEM :

* Cliquez sur le chevron de liste déroulante de la mosaïque PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Cliquez sur Télécharger Source.
* Sélectionnez la source souhaitée dans la boîte de dialogue modale Télécharger Source .

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>La source de développement contient le dernier état de votre application, tout en incluant des modifications non intermédiaires. Utilisez la source d’évaluation pour créer des versions candidates à envoyer aux fournisseurs d’App Store.
>
>Si vous n’évaluez jamais votre application, sélectionner Évaluation déclenche le workflow d’évaluation (conseil : s’affiche en tant qu’application évaluée dans l’application PhoneGap Enterprise Viewer disponible dans AppStore et Google PlayStore).

* Cliquez sur Télécharger et enregistrez le fichier ZIP sur votre ordinateur.
* Extrayez le fichier zip téléchargé dans votre espace de travail.

## Créer et charger l’application (à partir de la source) {#build-and-load-the-app-from-source}

L’interface de ligne de commande PhoneGap peut créer un projet de plateforme, compiler la source et déployer l’application dans une seule commande.

>[!NOTE]
>
>Vous pouvez effectuer toutes ces étapes séparément, voir Documents d’interface de ligne de commande PhoneGap (`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`).

1. Vérifiez que vous avez installé PhoneGap CLI, voir ci-dessus.
1. Dans une fenêtre de console (ou de terminal), accédez au répertoire racine de la source extraite.
1. Saisissez la commande suivante :

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>Si vous rencontrez des problèmes à ce stade, revenez aux principes de base pour résoudre les problèmes -
>
>1. Création d’un dossier (test mkdir)
>1. Accédez à ce nouveau dossier (test cd).
>1. Exécutez `phonegap create helloWorld`.
>1. Accéder à helloWorld (cd helloWorld)
>1. Exécutez `phonegap run android` (ou remplacez Android™ par iOS comme ci-dessus).
>1. L’émulateur s’ouvre et exécute l’application PhoneGap que vous venez de créer, en indiquant « Device Ready » (Prêt pour l’appareil) si le Bridge JavaScript natif est opérationnel.
>
>Ce dépannage vérifie que votre environnement de développement PhoneGap CLI s’exécute correctement.

## Déboguer JavaScript avec débogage Safari et IOS {#debug-javascripts-with-safari-and-ios-debug}

Vous pouvez déboguer le JavaScript de votre application à l’aide des outils de développement de Safari, comme vous le feriez avec une application web.

## Activer les outils de développement Safari {#enable-safari-developer-tools}

Pour activer les outils de développement :

* Ouvrir les préférences de Safari

   * Cliquez sur Safari dans la barre de menus
   * Cliquer sur les préférences

* Cliquez sur Avancé dans la fenêtre Préférence

![chlimage_1-47](assets/chlimage_1-47.png)

* Cochez « Afficher le menu Développer dans la barre de menus ».
* Fermer la fenêtre Préférences

## Connecter Safari à iOS {#connect-safari-to-ios}

Vous pouvez connecter Safari à un appareil ou à un émulateur iOS.

* Dans une fenêtre de console, accédez au répertoire racine de la source extraite.
* Saisissez la commande suivante afin de lancer votre application sur votre appareil ou émulateur.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Ouvrir Safari
* Cliquez sur Développer dans la barre de menus
* Sélectionner le sous-menu iOS Simulator
* Cliquez sur home.html .

![chlimage_1-48](assets/chlimage_1-48.png)

## Déboguer JavaScript avec l’inspecteur web de Safari {#debug-javascript-with-safari-s-web-inspector}

Vous pouvez définir des points d’arrêt n’importe où dans votre source. Lorsque vous interagissez avec votre émulateur ou appareil, l’exécution de votre application s’arrête à ces points d’arrêt. Vous pouvez parcourir et inspecter les valeurs dans les variables.

* Cliquez sur Ressources dans la fenêtre Inspecteur Web
* Parcourez l’arborescence source et cliquez sur le fichier source souhaité
* Cliquez sur le numéro de ligne en regard de pour ajouter un point d’arrêt
* Interaction avec un appareil ou un émulateur

![chlimage_1-49](assets/chlimage_1-49.png)

* Utilisez les boutons de contrôle pour poursuivre l’exécution, passer à une autre étape, entrer et sortir de méthodes :

![Cinq boutons de commande de fonctionnement différents alignés sur une ligne horizontale.](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Pour afficher les valeurs des variables dans la méthode actuelle, passez la souris.

## Les étapes suivantes {#the-next-steps}

Après avoir appris à développer des applications avec l’interface de ligne de commande PhoneGap, consultez [Accès aux fonctionnalités de l’appareil](/help/mobile/phonegap-access-device-features.md).
