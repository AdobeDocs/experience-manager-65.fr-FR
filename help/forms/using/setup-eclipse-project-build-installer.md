---
title: Générez l’application Android AEM Forms.
seo-title: Générez l’application Android AEM Forms.
description: Procédure d’installation du projet Android Studio et de génération du fichier .apk pour l’application AEM Forms pour Android
seo-description: Procédure d’installation du projet Android Studio et de génération du fichier .apk pour l’application AEM Forms pour Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Générez l’application Android AEM Forms.{#build-the-aem-forms-android-app}

Effectuez les étapes suivantes dans l’ordre recommandé pour créer l’application Android pour AEM Forms.

1. [Téléchargement du package de code source de l’application AEM Forms](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-277929160)
1. [Définition des variables d’environnement](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-111803610)
1. [Génération d’une application AEM Forms standard](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-heading-0)

## Téléchargement du package de code source de l’application AEM Forms {#download-android-zip}

AEM Forms App Source Code Package refers to the `adobe-lc-mobileworkspace-src-<version>.zip` archive. Cette archive comprend le code source requis pour créer une application AEM Forms personnalisée. The archive is included in the `adobe-aemfd-forms-app-src-pkg-<version>.zip`package available on the package share.

Perform the following steps to download the `adobe-aemfd-forms-app-src-pkg-<version>.zip` file:

1. Log in to the author instance of the [AEM server](http://localhost:4502/) as an administrator and open [package share](http://localhost:4502/crx/packageshare). Vous avez besoin d’un Adobe ID pour vous connecter au partage de package.
1. In [AEM package share](http://localhost:4502/crx/packageshare/login.html), search `adobe-aemfd-forms-app-src-pkg-<version>.zip`, click the package applicable to your operating system, and click **Download**. Lisez et acceptez l’accord de licence, puis cliquez sur **OK**. Le téléchargement démarre. Une fois le téléchargement effectué, le mot **Téléchargé** apparaît en regard du package.
1. Une fois le téléchargement terminé, cliquez sur **Téléchargé**. Vous êtes redirigé vers le gestionnaire de package. Dans le gestionnaire de packages, recherchez le package téléchargé, puis cliquez sur **Installer**.
1. To download the source-code archive, open **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** in your browser. Le fichier .zip de l’application Android est téléchargé sur votre périphérique.
1. Extrayez le contenu du fichier .zip dans un dossier de votre système de fichiers local. For example, *C:\&amp;lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

The following image displays the structure of the `adobe-lc-mobileworkspace-src-<version>.zip\android`folder.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Définition des variables d’environnement {#set-environment-variable-android}

Définissez les variables d’environnement suivantes avant de démarrer le processus de génération pour l’application AEM Forms :

* Définissez la variable d’environnement JAVA_HOME sur l’emplacement du logiciel JDK sur le système de fichiers local. Par exemple, C:\Program Files\Java\jdk1.8.0_181
* Set the `ANDROID_SDK_ROOT` system environment variable to the SDK location for Android. Par exemple, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Définissez la variable d’environnement système `Path` pour inclure les outils de la plate-forme et les emplacements de dossier d’outils pour Android. Par exemple, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

Une fois que vous avez enregistré le fichier adobe-lc-mobileworkspace-src-&lt;version>.zip sur le système de fichiers local et que vous avez défini les  variables  du, créez une application Android AEM Forms standard à l’aide de l’une des options suivantes :

* [Génération de l’application AEM Forms à l’aide d’Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-1347434739)
* [Génération du fichier .apk à l’aide d’Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-0)

### Génération de l’application AEM Forms à l’aide d’Android Studio {#using-android-studio}

Procédez comme suit pour générer l’application AEM Forms à l’aide d’Android Studio :

1. Lancez l’application Android Studio sur votre ordinateur.
1. Cliquez sur **Ouvrir un projet Android Studio existant**. Si la boîte de dialogue pour ouvrir un projet existant ne s’affiche pas automatiquement, sélectionnez **Fichier**>**Ouvrir**.
1. Accédez à *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* sur le système de fichiers local et cliquez sur **OK**.

   L’option **android** s’affiche dans le volet de gauche.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Select **android** from the left pane and click **Run** > **Run &#39;android&#39;**.
1. Sélectionnez le périphérique Android dans la section Périphériques connectés de la boîte de dialogue Sélectionner le  de déploiement, puis cliquez sur OK.

   Une fois que vous avez généré l’environnement de développement, vous pouvez maintenant appliquer des personnalisations sur l’application. Utilisez les articles suivants pour personnaliser l’application :

   * [Personnalisation de l’identité graphique](/help/forms/using/branding-customization.md)
   * [Personnalisation du thème](/help/forms/using/theme-customization.md)
   * [Personnalisation de mouvement](/help/forms/using/gesture-customization.md)
   Après avoir appliqué les personnalisations appropriées à votre application, vous pouvez générer le fichier .apk pour le distribuer.

### Génération du fichier .apk à l’aide d’Android Studio {#generate-apk-android-studio}

Exécutez les étapes suivantes pour générer le fichier .apk à l’aide d’Android Studio :

1. Lancez l’application Android Studio sur votre ordinateur.
1. Select **Open an existing Android Studio project**. Si la boîte de dialogue pour ouvrir un projet existant ne s’affiche pas automatiquement, sélectionnez **Fichier**>**Ouvrir**.
1. Accédez à *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* sur le système de fichiers local et cliquez sur **OK**.

   L’option android s’affiche dans le volet de gauche.

1. Sélectionnez **Générer** > **Générer APK** pour générer le fichier .apk.

   Optionally, Select **Build** > **Generate Signed APK** to generate a [signed version](https://developer.android.com/studio/publish/app-signing) of the .apk file.

## Utilisation d’Android Debug Bridge {#build-android-debug-bridge}

Once the .apk file has been generated, execute the following command to install the application on an Android device using the [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Utilisateurs de Windows :** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utilisateurs MAC :** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
