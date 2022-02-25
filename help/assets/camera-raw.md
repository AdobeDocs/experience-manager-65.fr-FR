---
title: '"[!DNL Adobe Camera Raw] prise en charge du traitement des ressources numériques"'
description: Découvrez comment activer [!DNL Adobe Camera Raw] assistance dans [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 29%

---

# Traitement des images à l’aide de [!DNL Adobe Camera Raw] {#camera-raw-support}

Vous pouvez activer la variable [!DNL Adobe Camera Raw] prise en charge du traitement des formats de fichiers bruts, tels que CR2, NEF et RAF, et du rendu des images au format JPEG. Cette fonctionnalité est prise en charge dans [!DNL Adobe Experience Manager Assets] en utilisant la variable [Package Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponible à partir de Distribution logicielle.

>[!NOTE]
>
>La fonctionnalité ne prend en charge que les rendus JPEG. Il est pris en charge sur Windows 64 bits, Mac OS et RHEL 7.x.

Pour activer [!DNL Camera Raw] assistance dans [!DNL Experience Manager Assets], procédez comme suit :

1. Téléchargez la [[!DNL Camera Raw] package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) de [!DNL Software Distribution].
1. Accédez à l’adresse `https://[aem_server]:[port]/workflow`. Ouvrez le **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** workflow.
1. Modifiez la variable **[!UICONTROL Miniatures des processus]** étape .
1. Fournissez la configuration suivante dans la section **[!UICONTROL Miniatures]** tab :

   * **[!UICONTROL Miniatures]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Types MIME ignorés]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Dans le **[!UICONTROL Image web]** , dans le **[!UICONTROL Ignorer la liste]** champ, spécifiez `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dans le panneau latéral, ajoutez le **[!UICONTROL Gestionnaire Camera Raw/DNG]** étape sous **[!UICONTROL Miniatures des processus]** étape .
1. Dans le **[!UICONTROL Gestionnaire Camera Raw/DNG]** ajoutez la configuration suivante dans la **[!UICONTROL Arguments]** tab :

   * **[!UICONTROL Types MIME]**: `image/dng` et `image/x-raw-(.*)`
   * **[!UICONTROL Commande]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Vérifiez que la configuration ci-dessus est identique à la configuration **[!UICONTROL Exemple de ressources de mise à jour de gestion des actifs numériques avec l&#39;étape de manipulation Camera RAW et DNG]**.

Vous pouvez désormais importer des fichiers Camera Raw dans Assets. Après avoir installé le package Camera Raw et configuré le workflow requis, **[!UICONTROL Réglage de l’image]** s’affiche dans la liste des panneaux latéraux.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figure : Options dans le volet latéral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figure : Utilisez cette option pour apporter des modifications légères à vos images.*

Après avoir enregistré les modifications dans une [!DNL Camera Raw] image, nouveau rendu `AdjustedPreview.jpg` est généré pour l’image. Pour les autres types d’image, sauf [!DNL Camera Raw], les modifications sont répercutées dans tous les rendus.

## Bonnes pratiques, problèmes connus et limites {#best-practices}

La fonctionnalité présente les limites suivantes :

* La fonctionnalité ne prend en charge que les rendus JPEG. Elle est prise en charge sous Windows 64 bits, Mac OS et RHEL 7.x.
* L’écriture différée des métadonnées n’est pas prise en charge pour les formats RAW et DNG.
* Le [!DNL Camera Raw] bibliothèque présente des limites relatives au nombre total de pixels qu’elle peut traiter à la fois. Actuellement, il peut traiter un maximum de 6 500 pixels sur le long du côté d’un fichier ou 512 MP, quels que soient les critères rencontrés en premier.
