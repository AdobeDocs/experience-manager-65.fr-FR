---
title: Détection du type MIME des ressources à l’aide d’Apache Tika
description: Activez Apache Tika pour [!DNL Experience Manager Assets] aider à détecter le type MIME des ressources à partir du flux de contenu pendant l’opération de chargement au lieu de l’extension de fichier.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 85%
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
