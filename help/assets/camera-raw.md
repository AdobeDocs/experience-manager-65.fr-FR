---
title: « Prise en charge d’[!DNL Adobe Camera Raw] pour le traitement des ressources numériques »
description: Découvrez comment activer la prise en charge d’ [!DNL Adobe Camera Raw]  dans  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 91%

---

# Traitement des images à l’aide d’[!DNL Adobe Camera Raw] {#camera-raw-support}

Vous pouvez activer la prise en charge d’[!DNL Adobe Camera Raw] pour le traitement des formats de fichiers bruts, tels que CR2, NEF et RAF, et du rendu des images au format JPEG. Cette fonctionnalité est prise en charge dans [!DNL Adobe Experience Manager Assets] en utilisant le [package Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponible à partir dans la distribution logicielle.

>[!NOTE]
>
>La fonctionnalité ne prend en charge que les rendus JPEG. Elle est prise en charge sous Windows 64 bits, Mac OS et RHEL 7.x.

Pour activer la prise en charge de [!DNL Camera Raw] dans [!DNL Experience Manager Assets], procédez comme suit :

1. Téléchargez le package [[!DNL Camera Raw] ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) à partir de la [!DNL Software Distribution].
1. Accédez à l’adresse `https://[aem_server]:[port]/workflow`. Ouvrez le workflow **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]**.
1. Modifier l’étape **[!UICONTROL Miniatures des processus]**.
1. Indiquez la configuration suivante dans l’onglet **[!UICONTROL Miniatures]** :

   * **[!UICONTROL Miniatures]** : `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Types MIME ignorés]** : `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Dans l’onglet **[!UICONTROL Image activée pour le web]**, dans le champ **[!UICONTROL Liste à ignorer]**, spécifiez `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Dans le panneau latéral, ajoutez l’étape **[!UICONTROL Camera Raw / DNG Handler]** sous l’étape **[!UICONTROL Miniatures des processus]**.
1. Dans l’étape **[!UICONTROL Camera Raw / DNG Handler]**, ajoutez la configuration suivante dans l’onglet **[!UICONTROL Arguments]** :

   * **[!UICONTROL Types MIME]** : `image/dng` et `image/x-raw-(.*)`
   * **[!UICONTROL Commande]** :

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Vérifiez que la configuration ci-dessus est identique à la configuration de l’**[!UICONTROL exemple de ressource de mise à jour de la gestion des ressources numériques avec l’étape de Camera RAW et DNG Handler]**.

Vous pouvez désormais importer des fichiers Camera Raw dans Assets. Une fois que vous avez installé le package Camera Raw et configuré le workflow requis, l’option **[!UICONTROL Réglage de l’image]** apparaît dans la liste des volets latéraux.

![chlimage_1-131](assets/chlimage_1-337.png)

*Image : options dans le volet latéral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Image : utilisez cette option pour apporter des modifications légères à vos images.*

Après avoir enregistré les modifications apportées à une image [!DNL Camera Raw], un nouveau rendu `AdjustedPreview.jpg` est généré pour cette image. Pour les types d’images autres que [!DNL Camera Raw], les modifications sont répercutées dans tous les rendus.

## Bonnes pratiques, problèmes connus et limites {#best-practices}

La fonctionnalité présente les limites suivantes :

* La fonctionnalité ne prend en charge que les rendus JPEG. Il est pris en charge sur Windows 64 bits, Mac OS et RHEL 7.x.
* L’écriture différée des métadonnées n’est pas prise en charge pour les formats RAW et DNG.
* La bibliothèque [!DNL Camera Raw] présente des limitations quant au nombre total de pixels qu’elle peut traiter à la fois. Actuellement, il peut traiter un fichier de maximum 65 000 pixels de long, ou de maximum 512 MP, quel que soit la limite rencontrée en premier.
