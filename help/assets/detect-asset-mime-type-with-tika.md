---
title: Détecter le type MIME des ressources à l’aide d’Apache Tika
description: Activation d’Apache Tika pour obtenir de l’aide [!DNL Experience Manager Assets] détectez le type MIME des ressources du flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 11%

---

# Détecter le type MIME des ressources à l’aide de [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalement, [!DNL Adobe Experience Manager Assets] détecte le type MIME des ressources que vous chargez à partir de leur extension de fichier.

Si vous utilisez [!DNL Apache Tika] pour charger des ressources, [!DNL Assets] détecte leur type MIME dans le flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.

Cette fonction est désactivée par défaut. Pour activer la fonction, configurez la variable **[!UICONTROL Type MIME DAM Day CQ]** service à partir de [!UICONTROL Configuration Manager].

>[!NOTE]
>
>Détection du type MIME à l’aide de la fonction [!DNL Apache Tika] La bibliothèque est une opération gourmande en ressources.

1. Pour ouvrir la console web de Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, localisez **[!UICONTROL Service Day CQ DAM Mime Type]** et cliquez sur **[!UICONTROL Modifier]**.

1. Sélectionnez la **[!UICONTROL Détecter MIME du contenu]** pour activer l’analyse des ressources chargées afin de déterminer leur type MIME tout en ignorant les extensions de fichier. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
