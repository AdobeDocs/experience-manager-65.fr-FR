---
title: Détecter le type MIME de fichiers à l’aide d’Apache Tika
description: Enable Apache Tika to help [!DNL Experience Manager Assets] detect the MIME type of assets from the content stream during the upload operation instead of the file extension.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 11%

---


# Détecter le type de fichiers MIME à l’aide de [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, [!DNL Adobe Experience Manager Assets] détecte le type MIME de ressources que vous téléchargez à partir de leur extension de fichier.

If you use [!DNL Apache Tika] to upload assets, [!DNL Assets] detects their MIME type from the content stream during the upload operation instead of the file extension.

Cette fonction est désactivée par défaut. To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME type detection using the [!DNL Apache Tika] library is a resource-intensive operation.

1. Pour ouvrir la console Web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, recherchez **[!UICONTROL Day CQ DAM Mime Type Service]** et cliquez sur **[!UICONTROL Modifier]**.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
