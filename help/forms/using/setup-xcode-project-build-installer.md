---
title: Configurer le projet Xcode et générer l’application iOS
seo-title: Set up the Xcode project and build the iOS app
description: Explique comment créer une application AEM Forms standard pour iOS.
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 72%

---

# Configurer le projet Xcode et générer l’application iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms fournit le code source complet de l’application AEM Forms. La source contient tous les composants nécessaires à la création d’une application AEM Forms personnalisée. L’archive du code source `adobe-lc-mobileworkspace-src-<version>.zip` fait partie du package `adobe-aemfd-forms-app-src-pkg-<version>.zip` dans la Distribution de logiciels.

Pour obtenir le code source de l’application AEM Forms, procédez comme suit :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Sélectionner **[!UICONTROL Adobe Experience Manager]** disponibles dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Sélectionnez le nom du package correspondant à votre système d’exploitation, puis sélectionnez **[!UICONTROL Accepter les termes du contrat de licence de l’utilisateur]**, puis sélectionnez **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour télécharger l’archive du code source, ouvrez `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` dans votre navigateur.
Le package source est téléchargé sur votre appareil.

L’image suivante affiche le contenu extrait du fichier`adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

Le tableau suivant détaille le contenu du dossier `adobe-lc-mobileworkspace-src-[version]/ios`.

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

Pour avoir des informations détaillées sur la signature de code et l’ajout d’appareils au portail d’approvisionnement iOS, consultez [Signature de code iOS : configuration, traitement et dépannage](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Génération d’une application AEM Forms standard {#set-up-the-xcode-project}

1. Effectuez les étapes suivantes pour configurer un projet dans Xcode et fournir une identité de signature :

   Ouvrez une session sur l’ordinateur Mac sur lequel Xcode et le SDK iOS sont installés et configurés.

1. Copiez l’archive `adobe-lc-mobileworkspace-src-<version>.zip` depuis le dossier des téléchargements vers `[User_Home]/Projects/`.
1. Extrayez l’archive dans le répertoire `[User_Home]/Projects/[your-project]`.
1. Accédez au répertoire ` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`.
1. Ouvrez le projet `AEM Forms.xcodeproj` dans Xcode.
1. Cliquez sur **AEM Forms**, sous **TARGETS**, sélectionnez **AEM Forms**. Sélectionnez l’onglet **Paramètres de construction**, recherchez la section **Droit de signature du code** et, dans les champs Débogage et Version finale, effectuez l’une des opérations suivantes :

   * Laisser les champs non spécifiés pour créer une application Mobile Workspace standard
   * Remplissez les champs comme indiqué dans [Créer une application AEM Forms sécurisée pour iOS](/help/forms/using/building-secure-mobile-workspace-app.md) pour créer une application AEM Forms sécurisée.

1. Dans le **Paramètres de création** , cliquez sur **Tous** puis cliquez sur **Combiné**.
1. Dans la **Paramètres** list, expand **Signature de code**.
1. Pour **Identité de signature de code**, sélectionnez la signature appropriée. Pour avoir des informations détaillées sur la création de nouvelles signatures, consultez [Créer et télécharger des profils d’approvisionnement de développement](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Vérifiez que la même signature est sélectionnée pour **Débogage**, **Version finale** et **N’importe quel SDK iOS**.
1. Remplacez le code suivant dans le fichier `AEM Forms-info.plist` :

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   par ce qui suit si vous remplacez `yourserver.com` par un nom d’hôte approprié pour votre serveur.

   ```xml
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
   >Cette étape est exigée seulement si l’application AEM Forms doit se connecter à un serveur qui ne suit pas les exigences de sécurité de transport des applications.

1. Dans **PROJET**, sélectionnez **AEM Forms** et vérifiez que la signature adéquate est sélectionnée pour **Identité de signature de code**, **Débogage**, **Version** et **N’importe quel SDK iOS**.
1. Connectez un iPad muni d’un profil d’approvisionnement à un ordinateur Mac.
1. Sélectionnez l’appareil muni d’un profil d’approvisionnement pour le projet **AEM Forms**.

   ![ipad](assets/ipad.png)

   Un appareil muni d’un profil d’approvisionnement, iPad Air 2, est sélectionné.

1. Sélectionner **Produit** > **Nettoyer**.
1. Sélectionner **Produit** > **Build**.

## Générer le programme d’installation de l’application AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Vous devez archiver le projet Xcode pour créer le programme d’installation (un fichier .ipa) et une liste de propriétés (un fichier .plist). Le fichier de liste de propriétés contient des informations de configuration de l’application interne hébergée, telles que le nom et l’emplacement d’hébergement de l’application. Pour plus d’informations sur le fichier de liste de propriétés, voir [À propos des fichiers de liste de propriétés d’informations](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Connectez un iPad muni d’un profil d’approvisionnement à un ordinateur Mac. Pour avoir des informations détaillées sur l’approvisionnement d’un iPad, consultez [Créer et télécharger des profils d’approvisionnement de développement](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Sélectionnez l’appareil muni d’un profil d’approvisionnement pour le projet **AEM Forms**.

   ![ipad-1](assets/ipad-1.png)

   Un appareil muni d’un profil d’approvisionnement, iPad Air 2, est sélectionné.

1. Sélectionner **Produit** > **Nettoyer**.
1. Sélectionner **Produit** > **Build**.
1. Sélectionner **Produit** > **Archiver**.
1. Dans Organisateur - Archives, sélectionnez la dernière archive de votre projet et cliquez sur **Distribuer**.
1. Sélectionner **Enregistrer pour le déploiement en entreprise ou ad hoc** comme méthode de distribution et cliquez sur **Suivant**.
1. Sélectionnez l’identité de signature qui convient dans le champ **Code Signing Identity** et cliquez sur **Next**. Cliquez sur **Autoriser** pour appliquer la signature.
1. Indiquez le nom de l’application et sélectionnez **Enregistrer pour distribution d’entreprise**.
1. Indiquez l’URL de l’application dans le champ **Application URL**. Par exemple, pour héberger l’application sur un serveur CRX, fournissez une URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. Dans le **Titre** , spécifiez AEM Forms.
1. Cliquez sur **Enregistrer** et fermez Xcode.

   Un fichier de programme d’installation, `AEM Forms.ipa`, et un fichier de liste de propriétés, `AEM Forms-info.plist`, sont alors créés à l’emplacement spécifié.

1. Ouvrez le fichier `AEM Forms-info.plist` dans un éditeur.
1. Remplacez tous les espaces dans l’URL de votre fichier .ipa par %20. 
1. Enregistrez et fermez le fichier `AEM Forms-info.plist`.
