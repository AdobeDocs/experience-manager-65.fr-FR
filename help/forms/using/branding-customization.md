---
title: Personnaliser l’identité graphique
description: Personnalisez l’icône de l’application, le nom de l’application, les images de lancement et la page de connexion afin de donner à l’application AEM Forms une apparence spécifique à l’entreprise.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 54%

---

# Personnaliser l’identité graphique {#branding-customization}

Vous pouvez personnaliser l’icône et le nom de l’application, les images de lancement et la page de connexion pour donner à l’application AEM Forms une apparence différente et spécifique de l’entreprise. Vous avez, par exemple, la possibilité de remplacer les images par des logos de votre société. L’application AEM Forms prend en charge les personnalisations suivantes :

* Personnalisation de l’icône de l’application et des images de lancement
* Personnalisation du nom de l’application
* Personnalisation des images sur la page de connexion
* Personnalisation du logo dans le menu de l’application

## Personnalisation de l’icône et des images de lancement {#customizing-icon-and-launch-images}

Exécutez les étapes suivantes pour personnaliser l’icône par défaut et l’image de lancement de l’application AEM Forms :

>[!NOTE]
>
>Pour toutes les icônes et images, utilisez le format PNG non entrelacé.

### Personnalisation de l’icône et des images de lancement {#to-customize-icon-and-launch-images}

#### Pour iOS {#for-ios}

1. Ouvrez le projet `Capture.xcodeproj` dans Xcode.
1. (***Pour la personnalisation des icônes***) En mode navigateur de Capture, accédez à **[!UICONTROL Capturer > Capture > Fichiers pris en charge > Capture-info.plist]**. Cliquez sur la liste déroulante à côté des fichiers d’icônes. Spécifiez le nom du fichier d’icône (.png) et chargez le fichier sur **[!UICONTROL Capturer > Capture > Ressources > icônes]**. Les dimensions actuellement prises en charge sont : 29x29, 50x50, 58x58, 72x72, 100x100 et 144x144.
1. (***Pour la personnalisation des images de lancement***) Vérifiez que les noms de fichiers de vos images sont les suivantes :

   * Pour lʼorientation portrait : `Default-Portrait~ipad.png` et `Default-Portrait@2x~ipad.png`
   * Pour lʼorientation paysage : `Default-Landscape~ipad.png` et `Default-Landscape@2x~ipad.png`

   Chargez-les dans le projet Capture pour remplacer les fichiers existants du projet.

   >[!NOTE]
   >
   >Assurez-vous que le nom et la résolution de votre image correspondent à l’image que vous remplacez dans le projet.

1. Générez et exécutez l’application AEM Forms sur un appareil ou un simulateur iOS.

#### Pour Android {#for-android}

1. Nommez les fichiers d’icône de l’application comme suit :

   `ic_launcher.png`

1. Placez les fichiers d’icône correspondants dans les répertoires suivants :

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Assurez-vous que le nom et la résolution de votre image correspondent à l’image que vous remplacez dans le projet.

1. Recréez l’application AEM Forms.

### Pour Windows {#for-windows}

1. Remplacez les icônes du chemin d’accès :

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Remplacez l’image de lancement dans le chemin d’accès :

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Assurez-vous que le nom et la résolution de votre image correspondent à l’image que vous remplacez dans le projet.

1. Recréez l’application AEM Forms.

## Personnalisation du nom de l’application {#customize-the-app-name}

### Pour iOS {#for-ios-1}

1. Ouvrez le projet `Capture.xcodeproj` dans Xcode.
1. Dans la vue Navigateur de Capture, accédez à **[!UICONTROL Capture > Capture > Fichiers pris en charge > InfoPlist.strings]**.

   Mettez à jour la valeur de l’attribut `CFBundleDisplayName` avec un nom que vous souhaitez afficher pour l’application.

1. Générez et exécutez l’application AEM Forms sur un appareil ou un simulateur iOS.

   Pour en savoir plus sur la création de l’application pour iOS, consultez la section [Configurer le projet Xcode et créer l’application iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Pour Android {#for-android-1}

1. Ouvrez le fichier XML suivant dans un éditeur de texte ou XML quelconque :

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Mettez à jour la valeur pour la clé `app_name`.
1. Recréez l’application AEM Forms.

   Pour plus d’informations sur la création de l’application pour Android, voir [Configuration du projet Eclipse et création de l’application Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Pour Windows {#for-windows-1}

1. Ouvrez le fichier XML suivant dans n’importe quel éditeur de texte :

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Mettez à jour la valeur dans la balise `<name>...</name>`.
1. Recréez l’application AEM Forms.

   Pour plus d’informations sur la création de l’application pour Windows, voir [Configuration du projet Visual Studio et création de l’application Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personnalisation des images sur la page de connexion {#customizing-images-on-the-login-page}

La page de connexion de l’application AEM Forms dispose d’un logo et d’images d’arrière-plan. Le logo se trouve au-dessus de la boîte de dialogue de connexion et l’image d’arrière-plan se trouve sous la boîte de dialogue de connexion. Effectuez les étapes suivantes pour personnaliser l’image par défaut sur la page de connexion :

**Avant de commencer**

Vérifiez que vous disposez des images suivantes :

<table>
 <tbody>
  <tr>
   <th><p>Description</p> </th>
   <th><p>Taille</p> </th>
   <th><p>Nom de fichier</p> </th>
  </tr>
  <tr>
   <td><p>Logo</p> </td>
   <td><p>72 x 72 pixels</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Image d’arrière-plan (portrait)</p> </td>
   <td><p>1 280 x 989 pixels</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Personnalisation des images sur la page de connexion à l’aide de Xcode**

1. Ouvrez le projet `Capture.xcodeproj` dans Xcode.

1. Accédez au dossier `www/wsmobile/images`. 
1. Pour changer le logo, remplacez le fichier `LC-logo.png` par défaut par le fichier `LC-logo.png` personnalisé.
1. Pour changer l’arrière-plan, remplacez le fichier par défaut `Landing_bg.jpeg` par le fichier personnalisé `Landing_bg.jpeg`.
1. Générez et exécutez l’application AEM Forms sur un appareil ou un simulateur iOS.

### Personnalisation des images sur les pages de connexion à l’aide d’Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Ouvrez le projet Android dans Eclipse.

1. Accédez au dossier `assets/www/wsmobile/images`. 
1. Pour changer le logo, remplacez le fichier `LC-logo.png` par défaut par le fichier `LC-logo.png` personnalisé.
1. Pour changer l’arrière-plan, remplacez le fichier par défaut `Landing_bg.jpeg` par le fichier personnalisé `Landing_bg.jpeg`.
1. Créez et exécutez l’application AEM Forms sur un appareil Android.

### Personnalisation des images sur les pages de connexion à l’aide de Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Ouvrez le projet `MWSWindows.sln` dans Visual Studio.

1. Accédez au dossier `MWSWindows\www\wsmobile\images`. 
1. Pour changer le logo, remplacez le fichier `LC-logo.png` par défaut par le fichier `LC-logo.png` personnalisé.
1. Pour changer l’arrière-plan, remplacez le fichier par défaut `Landing_bg.jpeg` par le fichier personnalisé `Landing_bg.jpeg`.
1. Générez et exécutez l’application AEM Forms sur un appareil Windows.

## Personnalisation du logo dans le menu de l’application {#customizing_images_on_the_login_page-1}

Une fois que vous êtes connecté à l’application AEM Forms et que vous avez sélectionné le bouton de menu, le logo s’affiche au-dessus du menu. Effectuez les étapes suivantes pour personnaliser le logo par défaut :

**Avant de commencer**

Vérifiez que vous disposez de l’image suivante :

<table>
 <tbody>
  <tr>
   <th><p>Description</p> </th>
   <th><p>Taille</p> </th>
   <th><p>Nom de fichier</p> </th>
  </tr>
  <tr>
   <td><p>Logo</p> </td>
   <td><p>72 x 72 pixels</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Personnalisation des images sur la page de connexion à l’aide de Xcode**

1. Ouvrez le projet `Capture.xcodeproj` dans Xcode.

1. Accédez au dossier `www/wsmobile/images`. 
1. Pour changer le logo, remplacez le fichier par défaut `aem_icon.png` par le fichier personnalisé `aem_icon.png`.
1. Générez et exécutez l’application AEM Forms sur un appareil ou un simulateur iOS.

### Personnalisation des images sur les pages de connexion à l’aide d’Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Ouvrez le projet Android dans Eclipse.

1. Accédez au dossier `assets/www/wsmobile/images`. 
1. Pour changer le logo, remplacez le fichier par défaut `aem_icon.png` par le fichier `aem_icon.png` personnalisé.
1. Créez et exécutez l’application AEM Forms sur un appareil Android.

### Personnalisation des images sur les pages de connexion à l’aide de Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Ouvrez le projet `MWSWindows.sln` dans Visual Studio.

1. Accédez au dossier `MWSWindows\www\wsmobile\images`. 
1. Pour changer le logo, remplacez le fichier par défaut `aem_icon.png` par le fichier personnalisé `aem_icon.png`.
1. Générez et exécutez l’application AEM Forms sur un appareil Windows.
