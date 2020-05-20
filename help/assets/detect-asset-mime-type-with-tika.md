---
title: Détecter le type de fichier MIME à l’aide d’Apache Tika
description: Activez Apache Tika afin d’aider AEM Assets à détecter le type MIME des ressources à partir du flux de contenu pendant l’opération de téléchargement au lieu de l’extension de fichier.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 50%

---


# Detect MIME type of assets using Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, AEM (Adobe Experience Manager) Assets détecte le type MIME des fichiers que vous transférez en fonction de leur extension.

Si vous utilisez Apache Tika pour transférer des ressources, AEM Assets détecte leur type MIME à partir du flux de contenu au cours de l’opération de transfert plutôt que de l’extension de fichier.

Cette fonction est désactivée par défaut. To enable the feature, configure the **[!UICONTROL Day CQ DAM Mime Type]** service from [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La détection de type MIME à l&#39;aide de la bibliothèque Apache Tika est une opération gourmande en ressources.

1. Pour ouvrir la console Web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, recherchez **[!UICONTROL Day CQ DAM Mime Type Service]** et cliquez sur **[!UICONTROL Modifier]**.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
