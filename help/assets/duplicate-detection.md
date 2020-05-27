---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources de duplicata dans Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 26%

---


# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous tentez de télécharger une ressource qui existe dans les ressources d’Adobe Experience Manager, la fonction de détection de duplicata l’identifie comme duplicata. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez la page Configuration de la console Web Experience Manager en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click **[!UICONTROL Save]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option Détecter le duplicata dans la servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans  Assets. Lorsqu’un utilisateur tente de télécharger une ressource qui existe dans Experience Manager, le système recherche un conflit et l’indique. The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [Duplicata de ressources dans le référentiel existant (didacticiel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

