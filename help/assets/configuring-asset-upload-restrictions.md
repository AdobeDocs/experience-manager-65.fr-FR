---
title: Configuration des restrictions de chargement des ressources
description: 'Limitation du type de ressources (fichiers) que les utilisateurs peuvent charger '
contentOwner: AG
role: Developer, Administrator, Architect
feature: Gestion des ressources,Télécharger
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 54%

---

# Configuration des restrictions de chargement des ressources {#configuring-asset-upload-restrictions}

Vous pouvez configurer [!DNL Adobe Experience Manager Assets] pour restreindre le type de ressources que les utilisateurs peuvent charger. Cela permet d’éviter les chargements accidentels de fichiers au format indésirable. Le service `Day CQ DAM Asset Upload Restriction` (Restriction de chargement des ressources de la gestion des ressources numériques Day CQ) permet de contrôler le type de fichiers que les utilisateurs peuvent charger. Par défaut, [!DNL Assets] permet aux utilisateurs de charger des ressources de tous les types MIME. Cependant, vous pouvez configurer le service pour empêcher les utilisateurs de charger des fichiers disposant de types MIME spécifiques.

1. Ouvrez la console web Configuration Manager. Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en mode d’édition. Par défaut, la case **Autoriser tous les MIME** est cochée, ce qui permet aux utilisateurs de charger des fichiers quel que soit leur type MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Pour empêcher les utilisateurs de charger des fichiers de certains types MIME uniquement, désélectionnez l’option **[!UICONTROL Autoriser tous les types MIME]** et spécifiez les types MIME autorisés dans les champs **[!UICONTROL Allowed Asset MIMEs (regex)]** à l’aide d’expressions régulières.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications. Si vous spécifiez des chaînes MIME pour les types MIME autorisés, l’opération de chargement échoue pour toute ressource de type MIME qui ne correspond pas aux chaînes MIME configurées dans ces champs.
