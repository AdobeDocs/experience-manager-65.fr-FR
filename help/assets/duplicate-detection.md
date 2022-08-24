---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources en double dans Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 27%

---

# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous tentez de charger une ressource qui existe dans [!DNL Adobe Experience Manager Assets], la fonction de détection des doublons l’identifie comme un doublon. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez le [!DNL Experience Manager] page de configuration de la console web en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Modification de la configuration de la servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Sélectionnez la **[!UICONTROL détecter les doublons]** puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option Détecter les doublons dans le servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. Lorsqu’un utilisateur tente de charger une ressource qui existe dans [!DNL Experience Manager], le système recherche les conflits et les indique. Les ressources sont identifiées à l’aide du hachage SHA-1 stocké à l’adresse `jcr:content/metadata/dam:sha1`, ce qui signifie que les ressources en double sont détectées quel que soit le nom de fichier.

>[!MORELIKETHIS]
>
>* [Duplication de ressources dans le référentiel existant (un tutoriel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

