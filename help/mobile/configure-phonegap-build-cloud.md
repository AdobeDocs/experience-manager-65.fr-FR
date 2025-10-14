---
title: Configuration de votre mot de Cloud Service Adobe PhoneGap Build
description: Consultez cette page pour configurer les services cloud et créer votre application avec PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Configuration de votre mot de Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

La vignette **PhoneGap Build** sur le tableau de bord de l’application vous permet de créer et de distribuer votre application mobile PhoneGap via le service Adobe PhoneGap Build.

Toutes les plateformes prises en charge définies dans la mosaïque **Gérer l’application** sont créées avec PhoneGap Build lors de la publication d’une version distante avec la mosaïque **PhoneGap Build**.

Vous pouvez pousser une version distante à `https://build.phonegap.com` ou télécharger la source pour la créer localement avec l’interface de ligne de commande PhoneGap à l’adresse `https://docs.phonegap.com/references/phonegap-cli/`.

![Vignette PhoneGap Build &#x200B;](assets/chlimage_1-60.png)

## Configuration du Cloud Service {#configuring-the-cloud-service}

Pour tirer parti de PhoneGap Build, vous devez configurer le Cloud Service AEM PhoneGap Build à l’aide des informations de votre compte PhoneGap Build.

Si vous ne disposez pas d’un compte, accédez à `https://build.phonegap.com` et inscrivez-vous ! Si vous êtes membre de Adobe Creative Cloud, vous pouvez prendre en charge jusqu’à 25 applications privées (applications non open source).

Une fois que vous avez vérifié que votre compte PhoneGap Build est actif, accédez à la console AEM Cloud Management, en particulier au [Cloud Service PhoneGap Build &#x200B;](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Utilisez le volet **Gérer les Cloud Service** pour configurer une nouvelle configuration de service cloud.

### Utilisation de la mosaïque Gestion des Cloud Service {#using-manage-cloud-services-tile}

Avant de commencer à créer votre application à l’aide de la mosaïque **PhoneGap Build**, vous devez configurer vos services cloud à l’aide de la mosaïque **Gérer les Cloud Service** du tableau de bord AEM Mobile.

Pour configurer les services cloud pour votre application, procédez comme suit :

1. Cliquez sur le coin supérieur droit de la mosaïque **Gérer les Cloud Service**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Choisissez l&#39;option **PhoneGap Build** à partir de l&#39;écran **Ajouter ou modifier le Cloud Service**.

   Cliquez sur **Suivant**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Saisissez vos informations d’identification afin de pouvoir créer une configuration cloud.

   Une fois la vérification effectuée, cliquez sur **Envoyer**. Cette configuration cloud s’affiche désormais dans la mosaïque **Gérer les Cloud Service**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Création de votre application avec PhoneGap Build {#building-your-application-with-phonegap-build}

Une fois que vous avez configuré les services cloud, vous pouvez créer votre application avec la mosaïque **PhoneGap Build**. Cliquez sur le coin supérieur droit pour effectuer votre choix parmi les options **Créer à distance** ou **Télécharger Source**.

![chlimage_1-64](assets/chlimage_1-64.png)

Pour appeler une version distante avec Adobe PhoneGap Build, cliquez sur **Créer à distance**.

>[!NOTE]
>
>Si la création échoue pour une raison quelconque (l’icône rouge d’iOS ci-dessous indique que la plateforme a échoué), vous pouvez pointer sur l’icône pour obtenir le message d’erreur. Vous pouvez également cliquer sur le triple point, « ... » au bas de la mosaïque pour accéder directement à `https://build.phonegap.com` (vous devez vous authentifier) et regarder et gérer directement votre version.

### Création de votre application avec l’interface de ligne de commande PhoneGap {#building-your-application-with-phonegap-cli}

PhoneGap fournit une interface de ligne de commande pour créer votre application localement.

Compilez l’application PhoneGap sur votre ordinateur à l’aide de l’interface de ligne de commande PhoneGap. Pour inclure le contenu AEM dans votre application, AEM crée un fichier ZIP contenant le contenu de votre application mobile, les configurations de synchronisation de contenu et d’autres ressources requises. Téléchargez le fichier ZIP et incluez-le dans votre version.

Pour tirer parti de l’interface de ligne de commande de PhoneGap, vous devez configurer votre environnement local pour inclure les éléments suivants :

1. Platform SDK (iOS, Android™, WindowsPhone, ...) et,
1. Interface de ligne de commande PhoneGap

Pour en savoir plus, rendez-vous sur `https://docs.phonegap.com/references/phonegap-cli/`.

Une fois les prérequis installés, testez-les simplement en créant une application simple et en la faisant fonctionner dans votre simulateur ou, mieux encore, sur votre appareil, à partir d’un terminal. Essayez :

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>Ajouter : émulez à la fin de cette ligne si vous ne souhaitez pas l’exécuter sur votre appareil connecté.

Une fois que vous avez vérifié que ce qui précède fonctionne, utilisez la mosaïque **PhoneGap Build** pour **Télécharger Source**. Enregistrez et décompressez le fichier sur votre système local. Une fois cette opération effectuée :

* accédez à ce fichier enregistré (dossier)
* exécutez « phonegap run ios » (ou android, etc.)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un auteur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Création pour Adobe PhoneGap Enterprise dans AEM](/help/mobile/phonegap.md)
