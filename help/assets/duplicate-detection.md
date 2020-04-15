---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources en double dans AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous essayez de transférer une ressource qui existe dans Adobe Experience Manager (AEM) Assets, la fonctionnalité de détection des doublons l’identifie comme un doublon. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez la page de configuration de la console Web AEM en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option de détection  dans la servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans AEM Assets. Lorsqu’un utilisateur tente de télécharger un fichier qui existe dans AEM, le système recherche un éventuel conflit et le signale. The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [de ressources dans le référentiel existant (didacticiel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

