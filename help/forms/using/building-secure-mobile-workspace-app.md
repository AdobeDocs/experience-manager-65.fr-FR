---
title: Création d’AEM sécurisé forme l’application pour iOS
seo-title: Création d’une application AEM Forms sécurisée pour iOS
description: Etapes de création d’une application AEM Forms sécurisée
seo-description: Etapes de création d’une application AEM Forms sécurisée
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Création d’une application AEM Forms sécurisée pour iOS {#building-a-secure-aem-forms-app-for-ios}

Vous devez archiver le projet Xcode pour l’application AEM Forms afin de générer le programme d’installation (un fichier .ipa) et une liste de propriétés (un fichier .plist). Le fichier de liste de propriétés contient les informations de configuration de l’application interne hébergée, telles que le nom de l’application et l’emplacement où elle est hébergée. Pour en savoir plus sur le fichier de liste de propriétés, consultez [A propos des fichiers de liste de propriétés d’informations](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Connectez-vous au site Web suivant :

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Créez un identifiant d’application. Pour avoir des instructions détaillées sur la création d’un identifiant d’application, consultez [Création et configuration des identifiants d’application](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Pour configurer l’identifiant de lot de votre application iOS, cliquez sur **[!UICONTROL Configurer un identifiant d’application]**.
1. Dans la partie inférieure de la page Web, sélectionnez **[!UICONTROL Enable for Data Protection]** (Activer pour la protection des données). Spécifiez les options de protection des données.

   Cliquez sur **[!UICONTROL Terminé]**.

1. Accédez à Provisioning (Approvisionnement) >Distribution et créez un profil en utilisant l’identifiant d’application configuré à l’étape 3.
1. Téléchargez le profil d’approvisionnement et ajoutez-le à Xcode et à l’iPad.
1. Ouvrez une session sur l’ordinateur Mac sur lequel Xcode et le SDK iOS sont installés et configurés.
1. Ouvrez le projet `AEM Forms.xcodeproj` dans Xcode.
1. Cliquez sur **[!UICONTROL AEM Forms]**, sous **[!UICONTROL TARGETS]**, sélectionnez **[!UICONTROL AEM Forms]**. Select the **[!UICONTROL Build Settings]** tab, locate the **[!UICONTROL Code Signing Entitlement]** section and in the Entitlements dropdown, select the **[!UICONTROL LC Enterprise]** option.
1. Trouvez et ouvrez le fichier `LC Enterprise.entitlements` dans Xcode pour le modifier. Under the **XCode entitlements**, add the same key-value pair as present in your provisioning profile.
1. Sous l’onglet **[!UICONTROL Paramètres de génération]**, cliquez sur **[!UICONTROL Tous]**, puis sur **[!UICONTROL Combiné]**.
1. Dans la liste des **[!UICONTROL Paramètres]**, développez **[!UICONTROL Signature de code]**. 
1. Pour **[!UICONTROL Identité de signature de code]**, sélectionnez la signature appropriée. Vérifiez que la même signature est sélectionnée pour **[!UICONTROL Débogage]**, **[!UICONTROL Version finale]** et **[!UICONTROL N’importe quel SDK iOS]**.
1. Under **[!UICONTROL PROJECT]**, select **[!UICONTROL AEM Forms]** and ensure that the appropriate signature is selected for **[!UICONTROL Code Signing Identity]**, **[!UICONTROL Debug]**, **[!UICONTROL Release]** and **[!UICONTROL Any iOS SDK]**.
1. Générer et distribuer une application AEM Forms. Pour obtenir des instructions détaillées sur la génération et la distribution d’une application AEM Forms, consultez [Générer le programme d’installation de l’application AEM Forms](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12).
