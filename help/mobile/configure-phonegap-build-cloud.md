---
title: 'Configurer le service cloud Adobe PhoneGap Build '
seo-title: 'Configurer le service cloud Adobe PhoneGap Build '
description: Consultez cette page pour configurer les services cloud et créer votre application avec PhoneGap Build.
seo-description: Consultez cette page pour configurer les services cloud et créer votre application avec PhoneGap Build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 19%

---

# Configurer le service cloud Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

La **mosaïque PhoneGap Build** du tableau de bord de l’application permet de créer et de distribuer votre application mobile PhoneGap via le service Adobe PhoneGap Build.

Toutes les plateformes prises en charge définies dans la mosaïque **Gérer l’application** seront créées avec le PhoneGap Build lors de la publication d’une version distante avec la mosaïque **PhoneGap Build**.

Vous pouvez envoyer une version distante vers [https://build.phonegap.com](https://build.phonegap.com) ou télécharger la source à créer localement avec [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![Mosaïque PhoneGap Build](assets/chlimage_1-60.png)

## Configuration du service cloud {#configuring-the-cloud-service}

Pour exploiter pleinement PhoneGap Build, vous devez configurer le service cloud PhoneGap Build d’AEM à l’aide de vos informations de compte PhoneGap Build.

Si vous ne possédez pas encore de compte, accédez à [https://build.phonegap.com](https://build.phonegap.com) et inscrivez-vous ! Si vous disposez d’un abonnement Adobe Creative Cloud, vous pouvez prendre en charge jusqu’à 25 applications privées (applications non open source).

Une fois que vous avez vérifié que votre compte PhoneGap Build est principal, accédez à votre console de gestion du cloud AEM, en particulier au [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Utilisez la mosaïque **Gérer les Cloud Services** pour configurer une nouvelle configuration de service cloud.

### Utilisation de la mosaïque Gérer les Cloud Services {#using-manage-cloud-services-tile}

Avant de commencer à créer votre application à l’aide de la mosaïque **PhoneGap Build** , vous devez configurer vos services cloud à l’aide de la mosaïque **Gérer les Cloud Services** du tableau de bord AEM Mobile.

Pour configurer les services cloud pour votre application, procédez comme suit :

1. Cliquez sur dans le coin supérieur droit de la mosaïque **Gérer les Cloud Services** .

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Sélectionnez l’option **PhoneGap Build** dans l’écran **Ajouter ou modifier le Cloud Service**.

   Cliquez sur **Suivant**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Saisissez vos informations d’identification pour créer une configuration cloud.

   Une fois la vérification effectuée, cliquez sur **Submit**. Cette configuration de cloud configurée s’affiche désormais dans la mosaïque **Gérer les Cloud Services** .

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Développement d’une application avec PhoneGap Build {#building-your-application-with-phonegap-build}

Une fois que vous avez configuré les services cloud, vous pouvez créer votre application avec la mosaïque **PhoneGap Build**. Cliquez sur le coin supérieur droit pour choisir parmi les options **Créer à distance** ou **Télécharger la source** .

![chlimage_1-64](assets/chlimage_1-64.png)

Pour appeler une version distante avec Adobe PhoneGap Build, cliquez sur **Créer à distance**.

>[!NOTE]
>
>Si la compilation échoue pour une raison quelconque (l’icône iOS rouge ci-dessous indique que la plateforme a échoué), vous pouvez survoler l’icône à l’aide du pointeur pour voir le message d’erreur. Vous pouvez également cliquer sur le point triple &quot;...&quot;. au bas de la mosaïque pour accéder directement à https://build.phonegap.com (vous devez vous authentifier) et regarder et gérer votre version directement.

### Création de votre application avec l’interface de ligne de commande PhoneGap {#building-your-application-with-phonegap-cli}

PhoneGap fournit une interface de ligne de commande pour créer votre application localement.

Compilez l’application PhoneGap sur votre ordinateur à l’aide de l’interface de ligne de commande PhoneGap (CLI). Pour inclure le contenu AEM dans votre application, AEM crée un fichier ZIP qui contient le contenu de votre application mobile, les configurations de synchronisation de contenu et d’autres ressources requises. Téléchargez le fichier ZIP et incluez-le dans votre version.

Pour tirer parti de l’interface de ligne de commande de PhoneGap, vous devez configurer votre environnement local afin d’inclure :

1. Le SDK spécifique à la plateforme (iOS, Android, WindowsPhone, etc.) et,
1. La ligne de commande de PhoneGap

Vous pouvez en lire plus [ici](https://docs.phonegap.com/references/phonegap-cli/).

Une fois que vous avez installé les conditions préalables requises, effectuez un test simple en créant une application simple et en l’exécutant dans votre simulateur ou mieux encore sur votre appareil, à partir d’une tentative de terminal :

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add —emulate à la fin de cette ligne si vous ne souhaitez pas l’exécuter sur votre appareil connecté.

Une fois que vous avez vérifié que les éléments ci-dessus fonctionnent, utilisez la mosaïque **PhoneGap Build** pour **Télécharger la source**. Enregistrez et décompressez le fichier ZIP sur le système local. Une fois cette opération effectuée :

* accéder à ce fichier enregistré (dossier) ;
* run &#39;phonegap run ios&#39; (ou android, etc.)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un auteur et d’un développeur, consultez les ressources ci-dessous :

* [Développement pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/developing-in-phonegap.md)
* [Création pour Adobe PhoneGap Enterprise dans AEM](/help/mobile/phonegap.md)
