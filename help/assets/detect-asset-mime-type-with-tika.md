---
title: Détecter le type MIME des fichiers à l’aide d’Apache Tika
description: Activez Apache Tika afin d’aider AEM Assets à détecter le type MIME des ressources à partir du flux de contenu pendant l’opération de téléchargement au lieu de l’extension de fichier.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, AEM (Adobe Experience Manager) Assets détecte le type MIME des fichiers que vous transférez en fonction de leur extension.

Si vous utilisez Apache Tika pour transférer des ressources, AEM Assets détecte leur type MIME à partir du flux de contenu au cours de l’opération de transfert plutôt que de l’extension de fichier.

Cette fonction est désactivée par défaut. To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La détection de type MIME à l’aide de la bibliothèque Apache Tika est une opération gourmande en ressources.

1. Pour ouvrir la console Web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. From the list of services, locate **[!UICONTROL Day CQ DAM Mime Type Service]** and tap **[!UICONTROL Edit]** beside it to open it in Edit mode.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click/tap **[!UICONTROL Save]** to save the changes.
