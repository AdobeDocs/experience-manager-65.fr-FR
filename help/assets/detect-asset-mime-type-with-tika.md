---
title: Détection du type MIME des ressources à l’aide d’Apache Tika
description: Activez Apache Tika afin d’aider  [!DNL Experience Manager Assets]  à détecter le type MIME des ressources à partir du flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 100%

---

# Détection du type MIME des ressources à l’aide d’[!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalement, [!DNL Adobe Experience Manager Assets] détecte le type MIME des ressources que vous chargez à partir de leur extension de fichier.

Si vous utilisez [!DNL Apache Tika] pour charger des ressources, [!DNL Assets] détecte leur type MIME à partir du flux de contenu au cours de l’opération de chargement plutôt que de l’extension de fichier.

Cette fonction est désactivée par défaut. Pour activer la fonction, configurez le service **[!UICONTROL Type MIME de gestion des ressources numériques Day CQ]** à partir du [!UICONTROL gestionnaire de configuration].

>[!NOTE]
>
>La détection du type MIME à l’aide de la bibliothèque [!DNL Apache Tika] est une opération qui nécessite de nombreuses ressources.

1. Pour ouvrir la console Web du gestionnaire de configuration, accédez à `https://[aem_server]:[port]/system/console/configMgr`.

1. Dans la liste des services, localisez le **[!UICONTROL service de type MIME de gestion des ressources numériques Day CQ]** et cliquez sur **[!UICONTROL Modifier]**.

1. Sélectionnez l’option **[!UICONTROL Détecter le type MIME à partir du contenu]** pour permettre à l’analyse des ressources chargées de déterminer leur type MIME, tout en ignorant les extensions de fichier. Par défaut, cette option n’est pas sélectionnée.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications.
