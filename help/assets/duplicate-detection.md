---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources de duplicata dans le Experience Manager.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Management,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 28%

---


# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous tentez de télécharger une ressource qui existe dans [!DNL Adobe Experience Manager Assets], la fonction de détection de duplicata l’identifie comme duplicata. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez la page de configuration de la console Web [!DNL Experience Manager] en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de la servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Sélectionnez l&#39;option **[!UICONTROL détecter le duplicata]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option Détecter le duplicata dans la servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. Lorsqu’un utilisateur tente de télécharger une ressource qui existe dans [!DNL Experience Manager], le système recherche un conflit et l’indique. Les ressources sont identifiées à l’aide du hachage SHA-1 stocké à `jcr:content/metadata/dam:sha1`, ce qui signifie que les ressources de duplicata sont détectées indépendamment des noms de fichier.

>[!MORELIKETHIS]
>
>* [Duplicata de ressources dans le référentiel existant (didacticiel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

