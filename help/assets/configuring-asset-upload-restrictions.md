---
title: Configuration des restrictions de chargement des ressources
description: Restrictions en matière de type de ressources (fichiers) que les utilisateurs peuvent charger
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 84%
---
# Configuration des restrictions de chargement des ressources {#configuring-asset-upload-restrictions}

Vous pouvez configurer [!DNL Adobe Experience Manager Assets] de sorte à limiter le type de ressources que les utilisateurs peuvent charger. Cela permet d’éviter les chargements accidentels de fichiers à un format indésirable ou malveillants. Le service `Day CQ DAM Asset Upload Restriction` permet de contrôler le type de fichiers que les utilisateurs peuvent charger. Par défaut, [!DNL Assets] permet aux utilisateurs de charger des ressources quel que soit leur type MIME. Cependant, vous pouvez configurer le service pour empêcher les utilisateurs de charger des fichiers disposant de types MIME spécifiques.

1. Ouvrez la console web Configuration Manager. Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez le service **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en mode d’édition. Par défaut, la case **Autoriser tous les MIME** est cochée, ce qui permet aux utilisateurs de charger des fichiers quel que soit leur type MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Pour empêcher les utilisateurs de charger des fichiers de certains types MIME uniquement, désélectionnez l’option **[!UICONTROL Autoriser tous les types MIME]** et spécifiez les types MIME autorisés dans les champs **[!UICONTROL Types MIME autorisés pour les ressources (regex)]** à l’aide d’expressions régulières.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer les modifications. Si vous spécifiez des chaînes MIME pour les types MIME autorisés, l’opération de chargement échoue pour toute ressource de type MIME qui ne correspond pas aux chaînes MIME configurées dans ces champs.
