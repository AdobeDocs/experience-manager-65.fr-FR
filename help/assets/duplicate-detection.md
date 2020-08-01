---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources de duplicata dans le Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 27%

---


# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

If you attempt to upload an asset that exists in [!DNL Adobe Experience Manager Assets], the duplicate detection feature identifies it as duplicate. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez la page de configuration de la console [!DNL Experience Manager] Web en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option Détecter le duplicata dans la servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. When a user attempts to upload an asset that exists in [!DNL Experience Manager], the system checks for conflict and indicates it. The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [Duplicata de ressources dans le référentiel existant (didacticiel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

