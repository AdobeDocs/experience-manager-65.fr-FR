---
title: Installation du pack de fonctionnalités 18912 pour la migration de ressources en bloc
description: Le pack de fonctionnalités 18912 vous permet soit d’ingérer en bloc des ressources par FTP, soit de migrer des ressources de Dynamic Media Classic vers Dynamic Media sur Adobe Experience Manager. Ce pack de fonctionnalités optionnel est fourni par l’assistance d’Adobe.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 100%

---

# Installation du pack de fonctionnalités 18912 pour la migration de ressources en bloc{#installing-feature-pack-for-bulk-asset-migration}

L’installation du pack de fonctionnalités 18912 est *facultative*.

Le pack de fonctionnalités 18912 vous permet d’ingérer des ressources en bloc directement dans Dynamic Media en mode Scene7 sur Adobe Experience Manager par FTP. Il vous permet également de migrer des ressources de Dynamic Media Classic vers Dynamic Media en mode Scene7 sur Experience Manager. Le pack de fonctionnalités est disponible à l’adresse [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>Il est possible d’utiliser le pack de fonctionnalités pour migrer en bloc des ressources de Dynamic Media Classic vers Dynamic Media en mode Scene7 dans Experience Manager. Il est également possible de migrer des ressources en bloc à l’aide de la fonction FTP dans Dynamic Media Classic. Cependant, Adobe ne recommande *pas* d’utiliser ces méthodes en raison de la complexité de la tâche.
>
>C’est pour cela que ce pack de fonctionnalités de migration est *seulement* pris en charge dans le cadre d’un projet de migration avec [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Avant d’installer le pack de fonctionnalités, créez un utilisateur de service et fournissez ses informations à l’assistance d’Adobe.

Consultez également la section [Configuration de Dynamic Media en mode Scene7](/help/assets/config-dms7.md).

**Pour installer le pack de fonctionnalités 18912 pour la migration en bloc de ressources :**

1. Dans votre instance Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]** et sélectionnez **[!UICONTROL Créer un utilisateur]**. Cet utilisateur de service doit disposer des autorisations de *lecture/écriture* sur `/content/dam.`.
1. Dans les champs **[!UICONTROL ID]** et **[!UICONTROL Mot de passe]** , saisissez un nom d’utilisateur ou d’utilisatrice et un mot de passe, par exemple : **Utilisateur FTP**. Ce nom apparaît dans la chronologie en tant qu’utilisateur ou utilisatrice ayant créé la ressource. Lorsqu’une ressource est chargée à partir du FTP, elle est considérée comme créée lorsqu’elle est chargée sur le serveur FTP et envoyée vers Experience Manager.
1. Contactez l’[assistance clientèle Adobe pour Experience Manager](https://experienceleague.adobe.com/fr?support-solution=General&amp;lang=fr#support) pour demander l’accès au pack de fonctionnalités 18912 pour le téléchargement. Vous aurez peut-être besoin des informations suivantes lorsque vous contactez l’assistance :

   * L’adresse IP du serveur de l’instance d’auteur, y compris le numéro de port (4502 par défaut)
   * Le nom d’utilisateur et le mot de passe du service Experience Manager de l’étape précédente

1. L’assistance clientèle d’Adobe pour Experience Manager vous fournit les informations d’identification au FTP et l’accès au pack de fonctionnalités 18912.
1. Une fois reçu le pack de fonctionnalités 18912, installez-le.

   Pour plus d’informations sur l’utilisation des packages et de la distribution logicielle dans Experience Manager, consultez ](/help/sites-administering/package-manager.md)Utilisation des packages[.
