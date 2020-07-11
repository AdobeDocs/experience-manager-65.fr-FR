---
title: Configuration du projet Android Studio et génération de l’application Android
seo-title: Configuration du projet Android Studio et génération de l’application Android
description: Procédure d’installation du projet Android Studio et de génération du programme d’installation pour l’application AEM Forms
seo-description: Procédure d’installation du projet Android Studio et de génération du programme d’installation pour l’application AEM Forms
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 59%

---


# Configuration du projet Android Studio et génération de l’application Android {#set-up-the-android-studio-project-and-build-the-android-app}

Cet article permet de créer l’application AEM Forms 6.3.1.1 et versions ultérieures. For building an app from source code of source code of the AEM Forms App 6.3, see [Set up the Eclipse project and build the Android™ app](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms fournit le code source complet de l’application AEM Forms. La source contient tous les composants nécessaires pour générer une application AEM Forms personnalisée. L&#39;archive du code source `adobe-lc-mobileworkspace-src-<version>.zip` fait partie du `adobe-aemfd-forms-app-src-pkg-<version>.zip` paquet sur la distribution de logiciels.

Pour obtenir le code source de l’application AEM Forms, suivez les étapes ci-après :

1. Distribution [](https://experience.adobe.com/downloads)de logiciels ouverts. Vous avez besoin d&#39;un Adobe ID pour vous connecter à la distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. In the **[!UICONTROL Filters]** section:
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]** .
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option Téléchargements **[!UICONTROL de]** recherche pour filtrer les résultats.
1. Appuyez sur le nom du pack applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les termes]** du contrat de licence de l’utilisateur final et appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://docs.adobe.com/content/help/fr-FR/experience-manager-65/administering/contentmanagement/package-manager.html) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Select the package and click **[!UICONTROL Install]**.

L&#39;image suivante affiche le contenu extrait du fichier`adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenu extrait de la source Android™ compressée](assets/mws-content-1.png)

The following image displays the directory structure of the `android`folder in the `src`folder.

![Structure des répertoires du dossier Android dans la source](assets/android-folder.png)

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

1. Effectuez les étapes suivantes pour configurer un projet dans Android™ Studio et fournir une identité de signature :

   Ouvrez une session sur un ordinateur sur lequel Android™ Studio est installé et configuré.

1. Copy the downloaded `adobe-lc-mobileworkspace-src-<version>.zip` archive to:

   **Pour les utilisateurs** de Mac : `[User_Home]/Projects`

   **Pour les utilisateurs** de Windows® : `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Pour Windows®, il est recommandé de conserver le projet Android dans le lecteur système.

1. Extrayez l’archive dans le répertoire suivant :

   **Pour les utilisateurs** de Mac : `[User_Home]/Projects/[your-project]`

   **Pour les utilisateurs** de Windows® : `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Il est recommandé de conserver le projet Android extrait dans le lecteur système avant d’importer le projet dans Android Studio.

1. Lancez Android™ Studio.

   **Pour les utilisateurs** de Mac : Mettez à jour le `local.properties` fichier présent dans le `[User_Home]/Projects/[your-project]/android` dossier et pointez la `sdk.dir` variable vers `SDK` l’emplacement de votre bureau.

   **Pour les utilisateurs** de Windows® : Mettez à jour le `local.properties` fichier présent dans le `%HOMEPATH%\Projects\[your-project]\android` dossier et pointez la `sdk.dir` variable vers `SDK` l’emplacement de votre bureau.

1. Cliquez sur **[!UICONTROL Terminer]** pour créer le projet.

   Le projet est disponible dans l’explorateur de projets ADT.

   ![projet eclipse après la création de l’application](assets/eclipsebuildmws.png)

1. Dans Android™ Studio, sélectionnez **[!UICONTROL Importer un projet (Eclipse ADT, Gradle, etc.)]**.
1. In the project explorer, select the root directory of the project that you want to build in the **Root Directory** text box:

   **Pour les utilisateurs de Mac :** [User_Home]/Projects/MobileWorkspace/src/android

   **Pour les utilisateurs de Windows® :** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Une fois le projet importé, une fenêtre contextuelle s’affiche avec une option permettant de mettre à jour le module externe Android™ Gradle. Cliquez sur le bouton approprié selon vos exigences.

   ![projet dontremindmeagainimmédiatement](assets/dontremindmeagainforthisproject.png)

1. Une fois Gradle généré, l’écran suivant s’affiche. Connectez le périphérique ou l’émulateur approprié au système et cliquez sur **[!UICONTROL Exécuter Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio affiche les périphériques connectés et les émulateurs disponibles. Sélectionnez le périphérique sur lequel vous souhaitez exécuter l’application, puis cliquez sur **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Après avoir créé le projet, vous pouvez choisir d’installer l’application à l’aide d’Android™ Debug Bridge ou d’Android™ Studio.

### À l’aide d’Android™ Debug Bridge {#andriod-debug-bridge}

Vous pouvez installer l’application sur un périphérique Android™ via [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) avec la commande suivante :

**Pour les utilisateurs** de Mac : `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Pour les utilisateurs** de Windows® : `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
