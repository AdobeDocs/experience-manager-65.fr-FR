---
title: Détecter le type MIME de fichiers à l’aide d’Apache Tika
description: Activez Apache Tika pour aider [!DNL Experience Manager Assets] à détecter le type MIME des ressources du flux de contenu pendant l’opération de téléchargement au lieu de l’extension de fichier.
contentOwner: AG
role: Administrateur, architecte
feature: Métadonnées, Outils de développement, Gestion des ressources
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 11%

---


# Détecter le type MIME de fichiers à l’aide de [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, [!DNL Adobe Experience Manager Assets] détecte le type MIME de ressources que vous téléchargez à partir de leur extension de fichier.

Si vous utilisez [!DNL Apache Tika] pour télécharger des fichiers, [!DNL Assets] détecte leur type MIME dans le flux de contenu pendant l’opération de téléchargement au lieu de l’extension de fichier.

Cette fonction est désactivée par défaut. Pour activer la fonction, configurez le service **[!UICONTROL Day CQ DAM Mime Type]** à partir de [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La détection de type MIME à l&#39;aide de la bibliothèque [!DNL Apache Tika] est une opération gourmande en ressources.

1. Pour ouvrir la console Web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, recherchez **[!UICONTROL Day CQ MIM Type Service]** et cliquez sur **[!UICONTROL Modifier]**.

1. Sélectionnez l&#39;option **[!UICONTROL Détecter MIME du contenu]** pour permettre l&#39;analyse des fichiers téléchargés afin de déterminer leur type MIME tout en ignorant les extensions de fichier. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
