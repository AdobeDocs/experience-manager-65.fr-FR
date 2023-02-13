---
title: Installer le projet Android Studio et générer l’application Android
seo-title: Set up the Android studio project and build the Android app
description: Procédure d’installation du projet Android Studio et de génération du programme d’installation pour l’application AEM Forms
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# Configuration du projet Android Studio et génération de l’application Android {#set-up-the-android-studio-project-and-build-the-android-app}

Cet article permet de créer l’application AEM Forms 6.3.1.1 et versions ultérieures. Pour créer une application à partir du code source AEM Forms App 6.3, voir [Configurer le projet Eclipse et génération de l’application Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms fournit le code source complet de l’application AEM Forms. La source contient tous les composants nécessaires pour générer une application AEM Forms personnalisée. L’archive du code source, `adobe-lc-mobileworkspace-src-<version>.zip`, fait partie du package `adobe-aemfd-forms-app-src-pkg-<version>.zip` dans Distribution de logiciels.

Pour obtenir le code source de l’application AEM Forms, procédez comme suit :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Formulaires]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Appuyez sur le nom applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les conditions du CLUF]**, puis appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package, puis cliquez sur **[!UICONTROL Installer]**.

L’image suivante affiche le contenu extrait du fichier`adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenu extrait de la source Android™ compressée](assets/mws-content-1.png)

L’image suivante affiche la structure du répertoire du dossier `android` dans le dossier `src`.

![Structure des répertoires du dossier Android dans la source](assets/android-folder.png)

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

1. Effectuez les étapes suivantes pour configurer un projet dans Android™ Studio et fournir une identité de signature :

   Ouvrez une session sur un ordinateur sur lequel Android™ Studio est installé et configuré.

1. Copiez l’archive `adobe-lc-mobileworkspace-src-<version>.zip` téléchargée sous :

   **Pour les utilisateurs de Mac** : `[User_Home]/Projects`

   **Pour les utilisateurs de Windows®** : `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Pour Windows®, il est recommandé de conserver le projet Android dans le lecteur système.

1. Extrayez l’archive dans le répertoire suivant :

   **Pour les utilisateurs de Mac** : `[User_Home]/Projects/[your-project]`

   **Pour les utilisateurs de Windows®** : `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Il est recommandé de conserver le projet Android extrait dans le lecteur système avant d’importer le projet dans Android Studio.

1. Lancez Android™ Studio.

   **Pour les utilisateurs de MAC** : mettez à jour le fichier `local.properties` situé dans le dossier `[User_Home]/Projects/[your-project]/android` et pointez la variable `sdk.dir` vers l’emplacement `SDK` sur votre bureau.

   **Pour les utilisateurs de Windows®** : mettez à jour le fichier `local.properties` situé dans le dossier `%HOMEPATH%\Projects\[your-project]\android` et pointez la variable `sdk.dir` vers l’emplacement `SDK` de votre ordinateur.

1. Cliquez sur **[!UICONTROL Terminer]** pour créer le projet.

   Le projet est disponible dans l’explorateur de projets ADT.

   ![projet eclipse après la création de l’application](assets/eclipsebuildmws.png)

1. Dans Android™ Studio, sélectionnez **[!UICONTROL Importer un projet (Eclipse ADT, Gradle, etc.)]**.
1. Dans l’explorateur de projets, sélectionnez le répertoire racine du projet que vous souhaitez créer dans la zone de texte **Répertoire racine** :

   **Pour les utilisateurs de Mac :** [User_Home]/Projects/MobileWorkspace/src/android

   **Pour les utilisateurs de Windows® :** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Une fois le projet importé, une fenêtre contextuelle s’affiche avec une option permettant de mettre à jour le module externe Android™ Gradle. Cliquez sur le bouton approprié selon vos exigences.

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. Une fois Gradle généré, l’écran suivant s’affiche. Connectez le périphérique ou l’émulateur approprié au système et cliquez sur **[!UICONTROL Exécuter Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio affiche les périphériques connectés et les émulateurs disponibles. Sélectionnez le périphérique sur lequel vous souhaitez exécuter l’application, puis cliquez sur **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Après avoir créé le projet, vous pouvez choisir d’installer l’application à l’aide d’Android™ Debug Bridge ou d’Android™ Studio.

### À l’aide d’Android™ Debug Bridge {#andriod-debug-bridge}

Vous pouvez installer l’application sur un périphérique Android™ via [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) avec la commande suivante :

**Pour les utilisateurs de Mac** : `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Pour les utilisateurs de Windows®** : `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
