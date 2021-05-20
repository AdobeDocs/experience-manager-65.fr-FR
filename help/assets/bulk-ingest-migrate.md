---
title: Installation du Feature Pack 18912 pour la migration de ressources en masse
description: Le Feature Pack 18912 vous permet soit d’ingérer des ressources par FTP en masse, soit de migrer des ressources de Dynamic Media Classic vers Dynamic Media sur AEM. Ce Feature Pack optionnel est fourni par le support Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Gestion des ressources
role: Business Practitioner, Administrator
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 23%

---

# Installation du Feature Pack 18912 pour la migration en masse des ressources{#installing-feature-pack-for-bulk-asset-migration}

L’installation du Feature Pack 18912 est *optionnel*.

Le Feature Pack 18912 vous permet soit d’ingérer des ressources en masse directement dans Dynamic Media - mode Scene7 sur AEM par FTP, soit de migrer des ressources de Dynamic Media Classic vers le mode Dynamic Media - mode Scene7 sur AEM. Le Feature Pack est disponible à partir de [Adobe Professional Services](https://www.adobe.com/fr/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Bien qu’il soit possible d’utiliser le Feature Pack pour migrer en masse des ressources de Dynamic Media Classic vers Dynamic Media - mode Scene 7 dans AEM ou migrer en masse des ressources à l’aide de la fonctionnalité FTP dans Dynamic Media Classic, Adobe ne recommande *pas* cette méthode en raison de la complexité impliquée.
>
>Par conséquent, les packs de fonctionnalités de migration, comme celui-ci, sont *uniquement* pris en charge dans le cadre d’un projet de migration lorsqu’ils sont réalisés via [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Avant de pouvoir installer le Feature Pack, vous devez d’abord créer un utilisateur du service et fournir ces informations à la prise en charge de l’Adobe.

Voir aussi [Configuration de Dynamic Media - mode Scene7](/help/assets/config-dms7.md).

**Pour installer le Feature Pack 18912 pour la migration des ressources en masse**

1. Dans votre instance AEM, sélectionnez **[!UICONTROL Outils > Sécurité > Utilisateurs]** et sélectionnez **[!UICONTROL Créer un utilisateur]**. Cet utilisateur du service doit disposer des autorisations de *lecture/écriture* sur `/content/dam.`
1. Dans les champs **[!UICONTROL ID]** et **[!UICONTROL Mot de passe]**, saisissez un nom d’utilisateur et un mot de passe ; par exemple, **Utilisateur FTP**. Ce nom apparaît dans la chronologie en tant qu’utilisateur qui a créé cette ressource. Lorsqu’une ressource est transférée à partir du FTP, elle est considérée créée lorsqu’elle est transférée sur le serveur FTP et envoyée vers AEM.
1. Contactez [l’Assistance clientèle d’Adobe Enterprise pour Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) pour demander l’accès au Feature Pack 18912 pour le téléchargement. Vous aurez peut-être besoin des informations suivantes lorsque vous contactez l’assistance :

   * Adresse IP du serveur pour votre instance d’auteur, y compris le numéro de port (par défaut, le numéro de port est 4502).
   * AEM nom d’utilisateur et mot de passe de l’utilisateur du service de l’étape précédente.

1. Adobe Enterprise Customer Care pour AEM vous fournit les informations d’identification FTP et l’accès au Feature Pack 18912.
1. Lorsque vous recevez le Feature Pack 18912, installez-le.

   Voir [Utilisation des packages](/help/sites-administering/package-manager.md) pour plus d’informations sur l’utilisation de la distribution logicielle et des packages dans AEM.
