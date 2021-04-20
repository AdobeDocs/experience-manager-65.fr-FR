---
title: Configuration des restrictions de transfert de ressources
description: 'Limiter le type de fichiers (fichiers) que les utilisateurs peuvent télécharger '
contentOwner: AG
role: Developer, Administrator, Architect
feature: Asset Management,Upload
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 53%

---


# Configuration des restrictions de transfert de ressources {#configuring-asset-upload-restrictions}

Vous pouvez configurer [!DNL Adobe Experience Manager Assets] pour limiter le type de fichiers que les utilisateurs peuvent télécharger. Elle permet d’éviter les téléchargements accidentels de formats non désirés et de fichiers malveillants. Le service `Day CQ DAM Asset Upload Restriction` (Restriction de chargement des ressources de la gestion des ressources numériques Day CQ) permet de contrôler le type de fichiers que les utilisateurs peuvent charger. Par défaut, [!DNL Assets] permet aux utilisateurs de télécharger des fichiers de tous les types MIME. Cependant, vous pouvez configurer le service pour empêcher les utilisateurs de charger des fichiers disposant de types MIME spécifiques.

1. Ouvrez la console web Configuration Manager. Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en mode d’édition. Par défaut, la case **Autoriser tous les MIME** est cochée, ce qui permet aux utilisateurs de charger des fichiers quel que soit leur type MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Pour limiter le téléchargement des fichiers de certains types MIME uniquement, désélectionnez l’option **[!UICONTROL Autoriser tous les types MIME]** et spécifiez les types MIME autorisés dans les champs **[!UICONTROL MIME d’actifs autorisés (regex)]** à l’aide d’expressions régulières.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications. Si vous spécifiez des chaînes MIME pour les types MIME autorisés, l’opération de chargement échoue pour toute ressource de type MIME qui ne correspond pas aux chaînes MIME configurées dans ces champs.
