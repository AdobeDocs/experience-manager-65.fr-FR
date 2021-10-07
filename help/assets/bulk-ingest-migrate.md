---
title: Installer le Feature Pack 18912 pour la migration de ressources en masse
description: Le Feature Pack 18912 vous permet soit d’ingérer des ressources par FTP en masse, soit de migrer des ressources de Dynamic Media Classic vers Dynamic Media sur Adobe Experience Manager. Ce Feature Pack optionnel est fourni par le support Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 13%

---

# Installer le Feature Pack 18912 pour la migration de ressources en masse{#installing-feature-pack-for-bulk-asset-migration}

L’installation du Feature Pack 18912 est *optionnel*.

Le Feature Pack 18912 vous permet d’ingérer des ressources en masse directement dans Dynamic Media - mode Scene7 sur Adobe Experience Manager par FTP. Il vous permet également de migrer des ressources de Dynamic Media Classic vers le mode Dynamic Media - Scene7 sur Experience Manager. Le Feature Pack est disponible à partir de [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>Il est possible d’utiliser le Feature Pack pour migrer en masse des ressources de Dynamic Media Classic vers Dynamic Media - mode Scene7 en Experience Manager. Il est également possible de migrer des ressources en masse à l’aide de la fonction FTP dans Dynamic Media Classic. Cependant, Adobe ne vous recommande *pas* d’utiliser l’une de ces méthodes en raison de la complexité de la tâche.
>
>Par conséquent, ce Feature Pack de migration est *uniquement* pris en charge dans le cadre d’un projet de migration lorsqu’il est effectué via [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Avant d’installer le Feature Pack, créez un utilisateur de service et fournissez ces informations à la prise en charge des Adobes.

Voir aussi [Configuration de Dynamic Media - mode Scene7](/help/assets/config-dms7.md).

**Pour installer le Feature Pack 18912 pour la migration en masse de ressources :**

1. Dans votre instance de Experience Manager, accédez à **[!UICONTROL Outil]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]** et sélectionnez **[!UICONTROL Créer un utilisateur]**. Cet utilisateur du service doit disposer des autorisations de *lecture/écriture* sur `/content/dam.`
1. Dans les champs **[!UICONTROL ID]** et **[!UICONTROL Mot de passe]**, saisissez un nom d’utilisateur et un mot de passe ; par exemple, **Utilisateur FTP**. Ce nom apparaît dans la chronologie en tant qu’utilisateur qui a créé cette ressource. Lorsqu’une ressource est téléchargée à partir du FTP, elle est considérée comme créée lorsqu’elle est téléchargée sur le serveur FTP et envoyée au Experience Manager.
1. Contactez le [service clientèle Adobe pour Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) pour demander l’accès au Feature Pack 18912 pour le téléchargement. Vous aurez peut-être besoin des informations suivantes lorsque vous contactez l’assistance :

   * Adresse IP du serveur pour votre instance d’auteur, y compris le numéro de port (par défaut, le numéro de port est 4502).
   * Nom d’utilisateur et mot de passe du service Experience Manager de l’étape précédente.

1. Le service clientèle d’Adobe pour Experience Manager vous fournit les informations d’identification FTP et l’accès au Feature Pack 18912.
1. Lorsque vous recevez le Feature Pack 18912, installez-le.

   Voir [Utilisation des modules](/help/sites-administering/package-manager.md) pour plus d’informations sur l’utilisation de la distribution logicielle et des modules en Experience Manager.
