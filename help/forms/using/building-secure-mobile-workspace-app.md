---
title: Création d’AEM Forms sécurisé l’application pour iOS
seo-title: Building a secure AEM Forms app for iOS
description: Etapes de création d’une application AEM Forms sécurisée
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# Création d’AEM Forms sécurisé l’application pour iOS {#building-a-secure-aem-forms-app-for-ios}

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
1. Cliquez sur **[!UICONTROL AEM Forms]**, sous **[!UICONTROL TARGETS]**, sélectionnez **[!UICONTROL AEM Forms]**. Sélectionnez l’onglet **[!UICONTROL Paramètres de construction]**, recherchez la section **[!UICONTROL Droit de signature du code]**, puis dans la liste déroulante Droits, sélectionnez l’option **[!UICONTROL LC Enterprise]**.
1. Trouvez et ouvrez le fichier `LC Enterprise.entitlements` dans Xcode pour le modifier. Dans l’onglet **Droits XCode**, ajoutez la même paire de valeurs clés que dans vos profils d’approvisionnement.
1. Sous l’onglet **[!UICONTROL Paramètres de génération]**, cliquez sur **[!UICONTROL Tous]**, puis sur **[!UICONTROL Combiné]**.
1. Dans la liste des **[!UICONTROL Paramètres]**, développez **[!UICONTROL Signature de code]**. 
1. Pour **[!UICONTROL Identité de signature de code]**, sélectionnez la signature appropriée. Vérifiez que la même signature est sélectionnée pour **[!UICONTROL Débogage]**, **[!UICONTROL Version finale]** et **[!UICONTROL N’importe quel SDK iOS]**.
1. Dans la liste **[!UICONTROL PROJET]**, sélectionnez **[!UICONTROL AEM Forms]** et vérifiez que la signature adéquate est sélectionnée pour **[!UICONTROL Identité de signature de code]**, **[!UICONTROL Débogage]**, **[!UICONTROL Version]** et **[!UICONTROL N’importe quel SDK iOS]**.
1. Générer et distribuer une application AEM Forms. Pour obtenir des instructions détaillées sur la génération et la distribution d’une application AEM Forms, consultez [Générer le programme d’installation de l’application AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
