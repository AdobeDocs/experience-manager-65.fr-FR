---
title: Détecter le type de fichier MIME à l’aide d’Apache Tika
description: Activez Apache Tika pour aider Experience Manager Assets à détecter le type MIME de ressources du flux de contenu pendant l’opération de téléchargement au lieu de l’extension de fichier.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 10%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, Adobe Experience Manager Assets détecte le type MIME de ressources que vous téléchargez à partir de leur extension de fichier.

Si vous utilisez Apache Tika pour télécharger des fichiers, Assets détecte leur type MIME dans le flux de contenu au cours de l’opération de téléchargement et non dans l’extension de fichier.

Cette fonction est désactivée par défaut. To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La détection de type MIME à l&#39;aide de la bibliothèque Apache Tika est une opération gourmande en ressources.

1. Pour ouvrir la console Web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, recherchez **[!UICONTROL Day CQ DAM Mime Type Service]** et cliquez sur **[!UICONTROL Modifier]**.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
