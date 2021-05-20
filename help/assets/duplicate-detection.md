---
title: Activation de la détection des ressources en double
description: Découvrez comment activer la détection des ressources en double dans Experience Manager.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Gestion des ressources, rapports sur les ressources
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 26%

---

# Activation de la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous tentez de charger une ressource qui existe dans [!DNL Adobe Experience Manager Assets], la fonction de détection des doublons l’identifie comme un doublon. La fonctionnalité de détection des doublons est désactivée par défaut. Pour l’activer, procédez comme suit :

1. Ouvrez la page de configuration de la console Web [!DNL Experience Manager] en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration de la servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Sélectionnez l’option **[!UICONTROL Détecter les doublons]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   *Figure : Sélectionnez l’option Détecter les doublons dans le servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. Lorsqu’un utilisateur tente de charger une ressource qui existe dans [!DNL Experience Manager], le système recherche un conflit et l’indique. Les ressources sont identifiées à l’aide du hachage SHA-1 stocké à l’adresse `jcr:content/metadata/dam:sha1`, ce qui signifie que les ressources en double sont détectées quel que soit le nom de fichier.

>[!MORELIKETHIS]
>
>* [Duplication de ressources dans le référentiel existant (un tutoriel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

