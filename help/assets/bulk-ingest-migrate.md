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
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Installing feature pack 18912 for bulk asset migration{#installing-feature-pack-for-bulk-asset-migration}

The installation of feature pack 18912 is *optional*.

Feature Pack 18912 vous permet soit d’assimiler des fichiers en masse directement dans le mode Contenu multimédia dynamique - Scene7 sur AEM par FTP, soit de migrer des fichiers de Contenu multimédia dynamique vers le mode Contenu multimédia dynamique - Scene7 sur AEM. Le Feature Pack est disponible auprès des Services [professionnels](https://www.adobe.com/fr/experience-cloud/consulting-services.html)Adobe.

>[!NOTE]
>
>Bien qu’il soit possible d’utiliser Feature Pack pour migrer en masse des fichiers vous-même de Contenu multimédia dynamique vers Contenu multimédia dynamique - Scene7 dans AEM ou pour migrer en masse des fichiers à l’aide de la fonctionnalité FTP dans Contenu multimédia dynamique classique, Adobe *ne recommande pas* cette méthode en raison de la complexité de la procédure.
>
>Par conséquent, les packs de fonctionnalités de migration, comme celui-ci, sont *uniquement* pris en charge dans le cadre d’un projet de migration lorsqu’ils sont effectués par le biais des services [professionnels](https://www.adobe.com/fr/experience-cloud/consulting-services.html)Adobe.

Avant d’installer Feature Pack, vous devez d’abord créer un utilisateur du service et fournir ces informations au support Adobe.

See also [Configuring Dynamic Media - Scene7 mode](/help/assets/config-dms7.md).

**Pour installer Feature Pack 18912 pour la migration des ressources en vrac**

1. Dans votre instance AEM, sélectionnez **[!UICONTROL Outils > Sécurité > Utilisateurs]** et sélectionnez **[!UICONTROL Créer un utilisateur]**. Cet utilisateur du service doit disposer des autorisations de *lecture/écriture* sur `/content/dam.`
1. Dans les champs **[!UICONTROL ID]** et **[!UICONTROL Mot de passe]**, saisissez un nom d’utilisateur et un mot de passe ; par exemple, **Utilisateur FTP**. Ce nom apparaît dans la chronologie en tant qu’utilisateur qui a créé cette ressource. Lorsqu’une ressource est transférée à partir du FTP, elle est considérée créée lorsqu’elle est transférée sur le serveur FTP et envoyée vers AEM.
1. Contactez le service à la clientèle [Adobe Enterprise pour Experience Manager](https://helpx.adobe.com/fr/contact/enterprise-support.ec.html) pour demander l’accès à Feature Pack 18912 en vue du téléchargement. Vous pouvez avoir besoin des informations suivantes lorsque vous contactez l’assistance :

   * Adresse IP du serveur de votre instance d’auteur, y compris le numéro de port (par défaut, le numéro de port est 4502).
   * Nom d’utilisateur et mot de passe du service AEM de l’étape précédente.

1. Le service à la clientèle d’Adobe Enterprise pour AEM vous fournit les informations d’identification FTP et l’accès à Feature Pack 18912.
1. Lorsque vous recevez Feature Pack 18912, installez-le.

   See [How to Work with Packages](/help/sites-administering/package-manager.md) for more information on using Package Share and packages in AEM.
