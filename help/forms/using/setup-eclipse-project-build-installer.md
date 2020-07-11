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
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 55%

---


# Générez l’application Android AEM Forms.{#build-the-aem-forms-android-app}

Effectuez les étapes suivantes dans l’ordre recommandé pour créer l’application Android pour AEM Forms.

1. [Téléchargement du package de code source de l’application AEM Forms](#download-android-zip)
1. [Définition des variables d’environnement](#set-environment-variable-android)
1. [Génération d’une application AEM Forms standard](#set-up-the-xcode-project)

## Téléchargement du package de code source de l’application AEM Forms {#download-android-zip}

AEM Forms App Source Code Package refers to the `adobe-lc-mobileworkspace-src-<version>.zip` archive. Cette archive comprend le code source requis pour créer une application AEM Forms personnalisée. L&#39;archive est incluse dans le `adobe-aemfd-forms-app-src-pkg-<version>.zip`package disponible sur la distribution de logiciels.

Perform the following steps to download the `adobe-aemfd-forms-app-src-pkg-<version>.zip` file:

1. Distribution [](https://experience.adobe.com/downloads)de logiciels ouverts. Vous avez besoin d&#39;un Adobe ID pour vous connecter à la distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. In the **[!UICONTROL Filters]** section:
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]** .
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option Téléchargements **[!UICONTROL de]** recherche pour filtrer les résultats.
1. Appuyez sur le nom du pack applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les termes]** du contrat de licence de l’utilisateur final et appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://docs.adobe.com/content/help/fr-FR/experience-manager-65/administering/contentmanagement/package-manager.html) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Select the package and click **[!UICONTROL Install]**.
1. To download the source-code archive, open **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** in your browser. Le fichier .zip de l’application Android est téléchargé sur votre appareil.
1. Extrayez le contenu du fichier .zip dans un dossier de votre système de fichiers local. For example, *C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

The following image displays the structure of the `adobe-lc-mobileworkspace-src-<version>.zip\android`folder.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Définition des variables d’environnement {#set-environment-variable-android}

Définissez les variables d’environnement suivantes avant de démarrer le processus de génération pour l’application AEM Forms :

* Définissez la variable d’environnement JAVA_HOME sur l’emplacement du logiciel JDK sur le système de fichiers local. Par exemple, C:\Program Files\Java\jdk1.8.0_181
* Set the `ANDROID_SDK_ROOT` system environment variable to the SDK location for Android. Par exemple, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Définissez la variable d’environnement système `Path` pour inclure les outils de la plate-forme et les emplacements de dossier d’outils pour Android. Par exemple, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

Après avoir enregistré le fichier adobe-lc-mobileworkspace-src-&lt;version>.zip sur le système de fichiers local et défini les variables d’environnement, créez une application Android AEM Forms standard à l’aide de l’une des options suivantes :

* [Génération de l’application AEM Forms à l’aide d’Android Studio](#using-android-studio)
* [Génération du fichier .apk à l’aide d’Android Studio](#generate-apk-android-studio)

### Génération de l’application AEM Forms à l’aide d’Android Studio {#using-android-studio}

Procédez comme suit pour générer l’application AEM Forms à l’aide d’Android Studio :

1. Lancez l’application Android Studio sur votre ordinateur.
1. Cliquez sur **Ouvrir un projet Android Studio existant**. Si la boîte de dialogue pour ouvrir un projet existant ne s’affiche pas automatiquement, sélectionnez **Fichier**>**Ouvrir**.
1. Accédez à *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* sur le système de fichiers local et cliquez sur **OK**.

   L’option **android** s’affiche dans le volet de gauche.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Select **android** from the left pane and click **Run** > **Run &#39;android&#39;**.
1. Sélectionnez le périphérique Android dans la section Appareils connectés de la boîte de dialogue Sélectionner la Cible de déploiement, puis cliquez sur OK.

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
