---
title: Détecter le type MIME des ressources à l’aide d’Apache Tika
description: Activez Apache Tika pour aider [!DNL Experience Manager Assets] à détecter le type MIME des ressources du flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.
contentOwner: AG
role: Administrator, Architect
feature: Métadonnées,Outils de développement,Gestion des ressources
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 11%

---

# Détectez le type MIME des ressources à l’aide de [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

En règle générale, [!DNL Adobe Experience Manager Assets] détecte le type MIME des ressources que vous chargez à partir de leur extension de fichier.

Si vous utilisez [!DNL Apache Tika] pour charger des ressources, [!DNL Assets] détecte leur type MIME dans le flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.

Cette fonction est désactivée par défaut. Pour activer la fonction, configurez le service **[!UICONTROL Day CQ DAM Mime Type]** à partir de [!UICONTROL Configuration Manager].

>[!NOTE]
>
>La détection de type MIME à l’aide de la bibliothèque [!DNL Apache Tika] est une opération gourmande en ressources.

1. Pour ouvrir la console web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, recherchez **[!UICONTROL Day CQ DAM Mime Type Service]** et cliquez sur **[!UICONTROL Modifier]**.

1. Sélectionnez l’option **[!UICONTROL Détecter MIME à partir du contenu]** pour permettre l’analyse des ressources chargées afin de déterminer leur type MIME tout en ignorant les extensions de fichier. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
