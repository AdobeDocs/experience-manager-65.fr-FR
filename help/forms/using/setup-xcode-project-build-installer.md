---
title: Configuration du projet Xcode et génération de l’application iOS
seo-title: Configuration du projet Xcode et génération de l’application iOS
description: Explique comment générer une application AEM Forms standard pour iOS.
seo-description: Explique comment générer une application AEM Forms standard pour iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# Configuration du projet Xcode et génération de l’application iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms fournit le code source complet de l’application AEM Forms. La source contient tous les composants nécessaires pour créer l’application personnalisée AEM Forms. The source code archive, `adobe-lc-mobileworkspace-src-<version>.zip` is a part of the `adobe-aemfd-forms-app-src-pkg-<version>.zip` package on package share.

Pour obtenir le code source de l’application AEM Forms, suivez les étapes ci-après :

1. Accédez au package shareURL : `https://<server>:<port>/crx/packageshare`.

1. Téléchargez le package source. Lorsque vous téléchargez le package, il est ajouté au gestionnaire de package AEM Forms.
1. Une fois téléchargé, accédez à : `https://<server>:<port>/crx/packmgr/index.jsp`, puis installez `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Pour télécharger l’archive du code source, ouvrez `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` dans votre navigateur.
Le package source est téléchargé sur votre périphérique.

L&#39;image suivante affiche le contenu extrait du fichier`adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

The following table details contents of the `adobe-lc-mobileworkspace-src-[version]/ios` folder.

<table>
 <tbody>
  <tr>
   <th><p>Répertoire</p> </th>
   <th><p>Contenu</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Ressources, modules externes PhoneGap et module principal de l’application</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Projet Xcode pour l’application AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>Fichiers HTML, CSS, images et JavaScript pour le projet de l’application AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Pour avoir des informations détaillées sur la signature de code et l’ajout de périphériques au portail d’approvisionnement iOS, consultez [Signature de code iOS : configuration, traitement et dépannage](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

1. Effectuez les étapes suivantes pour configurer un projet dans Xcode et fournir une identité de signature :

   Connectez-vous à votre ordinateur Mac sur lequel Xcode et le SDK iOS sont installés et configurés.

1. Copy the `adobe-lc-mobileworkspace-src-<version>.zip` archive from the downloads folder to `[User_Home]/Projects/`.
1. Extract the archive in the `[User_Home]/Projects/[your-project]`directory.
1. Accédez au répertoire ` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Ouvrez le projet `AEM Forms.xcodeproj` dans Xcode.
1. Cliquez sur **AEM Forms**, sous **TARGETS**, sélectionnez **AEM Forms**. Select the **Build Settings** tab, locate the **Code Signing Entitlement** section, and in Debug and Release fields do one of the following:

   * Laisser les champs non spécifiés pour créer une application Mobile Workspace standard
   * Specify the fields to as explained in [Building a Secure AEM Forms app for iOS](/help/forms/using/building-secure-mobile-workspace-app.md) to build a secure AEM Forms app.

1. Sous l’onglet **Paramètres de génération**, cliquez sur **Tous**, puis sur **Combiné**.
1. Dans la liste des **Paramètres**, développez **Signature de code**. 
1. Pour **Identité de signature de code**, sélectionnez la signature appropriée. For detailed information about, creating new signatures, see [Creating and Downloading Development Provisioning Profiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Vérifiez que la même signature est sélectionnée pour **Débogage**, **Version finale** et **N’importe quel SDK iOS**.
1. Replace the following code in the `AEM Forms-info.plist` file:

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   par ce qui suit si vous remplacez `yourserver.com`   par un nom d’hôte approprié pour votre serveur.

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >Cette étape est requise uniquement si l’application AEM Forms doit se connecter à un serveur qui ne respecte pas les exigences de sécurité du transport des applications.

1. Under **PROJECT**, select **AEM Forms** and ensure that the appropriate signature is selected for **Code Signing Identity**, **Debug**, **Release** and **Any iOS SDK**.
1. Connectez un iPad muni d’un profil d’approvisionnement à un ordinateur Mac.
1. Select the provisioned device for the **AEM Forms** project.

   ![ipad](assets/ipad.png)

   Un périphérique muni d’un profil d’approvisionnement, iPad Air 2, est sélectionné.

1. Sélectionnez **Produit** > **Nettoyer**.
1. Sélectionnez **Produit** > **Générer**.

## Générer le programme d’installation de l’application AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Vous devez archiver le projet Xcode pour générer le programme d’installation (un fichier .ipa) et une liste de propriétés (un fichier .plist). Le fichier de liste de propriétés contient les informations de configuration de l’application interne hébergée, telles que le nom de l’application et l’emplacement où elle est hébergée. Pour en savoir plus sur le fichier de liste de propriétés, consultez [A propos des fichiers de liste de propriétés d’informations](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Connectez un iPad muni d’un profil d’approvisionnement à un ordinateur Mac. For detailed information about provisioning an iPad, see [Creating and Downloading Development Provisioning Profiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Select the provisioned device for the **AEM Forms** project.

   ![ipad-1](assets/ipad-1.png)

   Un périphérique muni d’un profil d’approvisionnement, iPad Air 2, est sélectionné.

1. Sélectionnez **Produit** > **Nettoyer**.
1. Sélectionnez **Produit** > **Générer**.
1. Sélectionnez **Produit** > **Archiver**.
1. Dans Organisateur - Archives, sélectionnez la dernière archive de votre projet et cliquez sur **Distribuer**.
1. Sélectionnez **Enregistrer pour déploiement en entreprise ou ad hoc** comme méthode de distribution et cliquez sur **Suivant**.
1. Sélectionnez l’identité de signature qui convient dans le champ **Code Signing Identity** et cliquez sur **Next**. Cliquez sur **Allow** (Autoriser) pour appliquer la signature.
1. Indiquez le nom de l’application et sélectionnez **Enregistrer pour distribution en entreprise**.
1. Indiquez l’URL de l’application dans le champ **Application URL**. Par exemple, pour héberger l’application sur un serveur CRX, indiquez l’URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. Dans le champ **Titre**, indiquez AEM Forms.
1. Cliquez sur **Enregistrer** et fermez Xcode.

   Un fichier de programme d’installation, `AEM Forms.ipa`, et un fichier de liste de propriétés, `AEM Forms-info.plist`, sont alors créés à l’emplacement spécifié.

1. Ouvrez le `AEM Forms-info.plist` fichier dans un éditeur.
1. Remplacez tous les espaces dans l’URL de votre fichier .ipa par %20. 
1. Save and close the `AEM Forms-info.plist` file.