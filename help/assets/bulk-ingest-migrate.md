---
title: Installation de Feature Pack 18912 pour la migration des ressources en vrac
description: Feature Pack 18912 vous permet soit d’assimiler des fichiers en masse par FTP, soit de migrer des fichiers de Dynamic Media Classic vers Dynamic Media sur AEM. Ce Feature Pack optionnel est fourni par le support Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 24%

---


# Installation de Feature Pack 18912 pour la migration des ressources en vrac{#installing-feature-pack-for-bulk-asset-migration}

L&#39;installation de Feature Pack 18912 est *optionnelle*.

Feature Pack 18912 vous permet soit d’assimiler des ressources en vrac directement en mode Dynamic Media - Scene7 sur AEM par FTP, soit de migrer des ressources de Dynamic Media Classic vers le mode Dynamic Media sur AEM. Le Feature Pack est disponible à partir de [Adobe Professional Services](https://www.adobe.com/fr/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Bien qu’il soit possible d’utiliser Feature Pack pour migrer en masse des fichiers vous-même de Dynamic Media Classic vers Dynamic Media - Scene 7 en mode AEM ou migrer en masse des fichiers à l’aide de la fonctionnalité FTP de Dynamic Media Classic, l’Adobe ne recommande *pas* cette méthode en raison de la complexité impliquée.
>
>Par conséquent, les packs de fonctionnalités de migration, tels que celui-ci, sont *uniquement* pris en charge dans le cadre d’un projet de migration lorsqu’ils sont exécutés via [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Avant d’installer Feature Pack, vous devez d’abord créer un utilisateur de service et fournir ces informations à l’assistance Adobe.

Voir aussi [Configuration du mode Dynamic Media - Scene7](/help/assets/config-dms7.md).

**Pour installer Feature Pack 18912 pour la migration des ressources en vrac**

1. Dans votre instance AEM, sélectionnez **[!UICONTROL Outils > Sécurité > Utilisateurs]** et sélectionnez **[!UICONTROL Créer un utilisateur]**. Cet utilisateur du service doit disposer des autorisations de *lecture/écriture* sur `/content/dam.`
1. Dans les champs **[!UICONTROL ID]** et **[!UICONTROL Mot de passe]**, saisissez un nom d’utilisateur et un mot de passe ; par exemple, **Utilisateur FTP**. Ce nom apparaît dans la chronologie en tant qu’utilisateur qui a créé cette ressource. Lorsqu’une ressource est transférée à partir du FTP, elle est considérée créée lorsqu’elle est transférée sur le serveur FTP et envoyée vers AEM.
1. Contactez le service à la clientèle [Adobe Enterprise ](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) pour demander l’accès à Feature Pack 18912 pour le téléchargement. Vous aurez peut-être besoin des informations suivantes lorsque vous contactez l&#39;assistance :

   * Adresse IP du serveur de votre instance d’auteur, y compris le numéro de port (par défaut, le numéro de port est 4502).
   * AEM nom d’utilisateur et mot de passe du service de maintenance de l’étape précédente.

1. L’assistance clientèle d’Adobe Entreprise pour AEM vous fournit les informations d’identification FTP et l’accès à Feature Pack 18912.
1. Lorsque vous recevez Feature Pack 18912, installez-le.

   Pour plus d&#39;informations sur l&#39;utilisation de la distribution de logiciels et des packages dans AEM, consultez la section [Comment utiliser des packages](/help/sites-administering/package-manager.md).
