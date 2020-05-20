---
title: Configuration des restrictions de transfert de ressources
description: 'Limiter le type de fichiers (fichiers) que les utilisateurs peuvent télécharger '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 55%

---


# Configuration des restrictions de transfert de ressources {#configuring-asset-upload-restrictions}

You can configure [!DNL Adobe Experience Manager Assets] to restrict the type of assets that users can upload. Elle permet d’éviter les téléchargements accidentels de formats non désirés et de fichiers malveillants. Le service `Day CQ DAM Asset Upload Restriction` (Restriction de chargement des ressources de la gestion des ressources numériques Day CQ) permet de contrôler le type de fichiers que les utilisateurs peuvent charger. By default, [!DNL Assets] allows users to upload assets of all MIME types. Cependant, vous pouvez configurer le service pour empêcher les utilisateurs de charger des fichiers disposant de types MIME spécifiques.

1. Ouvrez la console web Configuration Manager. Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en mode d’édition. Par défaut, la case **Autoriser tous les MIME** est cochée, ce qui permet aux utilisateurs de charger des fichiers quel que soit leur type MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications. Si vous spécifiez des chaînes MIME pour les types MIME autorisés, l’opération de chargement échoue pour toute ressource de type MIME qui ne correspond pas aux chaînes MIME configurées dans ces champs.
