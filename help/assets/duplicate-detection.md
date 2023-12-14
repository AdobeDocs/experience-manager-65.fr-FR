---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources en double dans Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
source-git-commit: 477c62b857ab98d8617c7bd8ba226019d42d330d
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 85%

---

# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous essayez de charger une ressource qui existe dans [!DNL Adobe Experience Manager Assets], la fonctionnalité de détection des doublons l’identifie comme un doublon. La détection des doublons est désactivée par défaut. Pour activer la fonction, procédez comme suit :

1. Ouvrez la page d’[!DNL Experience Manager] de configuration de la console Web en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration du servlet **[!UICONTROL Ressource de création de gestion des ressources numériques Day CQ]**.
1. Sélectionnez l’option **[!UICONTROL Détecter les doublons]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   * : sélection de l’option de détection des doublons dans le servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. Lorsqu’un utilisateur tente de charger un fichier qui existe dans [!DNL Experience Manager], le système recherche un éventuel conflit et le signale. Les ressources sont identifiées à l’aide du hachage SHA-1 stocké dans `jcr:content/metadata/dam:sha1`, ce qui signifie que les ressources en double sont détectées quels que soient les noms de fichiers.

>[!MORELIKETHIS]
>
>* [Duplication de ressources dans un référentiel existant (tutoriel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Détecter les ressources en double dans AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
