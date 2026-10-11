---
title: Activer la détection des ressources en double
description: Découvrez comment activer la détection des ressources en double dans Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%
---
# Activer la détection des ressources en double {#enable-detection-of-duplicate-assets}

Si vous essayez de charger une ressource qui existe dans [!DNL Adobe Experience Manager Assets], la fonctionnalité de détection des doublons l’identifie comme un doublon. Par défaut, la détection des doublons est désactivée. Pour activer la fonctionnalité, procédez comme suit :

1. Ouvrez la page d’[!DNL Experience Manager] de configuration de la console Web en accédant à `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifiez la configuration du servlet **[!UICONTROL Ressource de création de gestion des ressources numériques Day CQ]**.
1. Sélectionnez l’option **[!UICONTROL Détecter les doublons]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Sélection de l’option de détection des doublons dans le servlet](assets/chlimage_1-377.png)

   * : sélection de l’option de détection des doublons dans le servlet.*

La fonctionnalité de détection des doublons est maintenant activée dans [!DNL Assets]. Lorsqu’un utilisateur tente de charger un fichier qui existe dans [!DNL Experience Manager], le système recherche un éventuel conflit et le signale. Les ressources sont identifiées à l’aide du hachage SHA-1 stocké dans `jcr:content/metadata/dam:sha1`, ce qui signifie que les ressources en double sont détectées quels que soient les noms de fichiers.

>[!MORELIKETHIS]
>
>* [Duplication de ressources dans un référentiel existant (tutoriel d’un membre de la communauté)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Détection des ressources en double dans AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=fr)
