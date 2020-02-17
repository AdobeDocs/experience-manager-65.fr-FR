---
title: Configuration des restrictions de transfert de fichier
description: 'Restreindre le type de fichiers (fichiers) que les utilisateurs peuvent télécharger '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configuration des restrictions de transfert de fichier {#configuring-asset-upload-restrictions}

Vous pouvez configurer Adobe Experience Manager (AEM) Assets de sorte que le type de ressources (fichiers) que les utilisateurs peuvent charger soit limité. Cette fonctionnalité permet d’éviter que les utilisateurs ne chargent des ressources dans un format indésirable ou qu’ils ne chargent des fichiers malveillants. The `Day CQ DAM Asset Upload Restriction` service enables you to control the type of files that users can upload. Par défaut, AEM Assets permet aux utilisateurs de charger des ressources quel que soit leur type MIME. Cependant, vous pouvez configurer le service pour empêcher les utilisateurs de charger des fichiers disposant de types MIME spécifiques.

1. Ouvrez la console Web Configuration Manager. Accès `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Asset Upload Restriction]** service in Edit mode. By default, the **Allow all MIME** option is selected, which allows users to upload files of all MIME types.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click/tap **[!UICONTROL Save]** to save the changes. Si vous spécifiez des chaînes MIME pour les types MIME autorisés, l’opération de chargement échoue pour toute ressource de type MIME qui ne correspond pas aux chaînes MIME configurées dans ces champs.
