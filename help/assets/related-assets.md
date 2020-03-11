---
title: Ressources connexes
description: Découvrez comment mettre en relation des ressources qui partagent des attributs communs. Vous pouvez également utiliser cette fonctionnalité pour créer des relations source/dérivés entre des ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4fc656948e4c5cb4a3e927c25d3afd29102b7ab4

---


# Related assets {#related-assets}

Les ressources d’Adobe Experience Manager (AEM) vous permettent de lier manuellement des ressources en fonction des besoins de votre entreprise à l’aide de la fonctionnalité des ressources connexes. Par exemple, vous pouvez mettre en relation un fichier de licence avec une ressource ou une image/vidéo portant sur un sujet similaire. Vous pouvez mettre en relation des ressources qui partagent certains attributs communs. Vous pouvez également utiliser cette fonctionnalité pour créer des relations source/dérivés entre des ressources. Par exemple, si un fichier PDF est généré à partir d’un fichier INDD, vous pouvez mettre en relation le fichier PDF avec son fichier INDD source.

Grâce à cette fonctionnalité, vous pouvez partager un fichier PDF ou JPG basse résolution avec des fournisseurs ou des agences et rendre le fichier INDD haute résolution disponible uniquement sur demande.

>[!NOTE] Seuls les utilisateurs disposant d’autorisations de modification peuvent établir des relations avec des fichiers et les dissocier.
>

## Relate assets {#relating-assets}

1. From the AEM interface, open the [!UICONTROL Properties] page for an asset that you want to relate.

   ![chlimage_1-272](assets/chlimage_1-272.png)

   Vous pouvez également sélectionner la ressource en mode Liste.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Sinon, sélectionnez la ressource à partir d’une collection.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Pour mettre en relation une autre ressource avec celle que vous avez sélectionnée, cliquez/appuyez sur l’icône **[!UICONTROL Mettre en relation]** dans la barre d’outils.

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. Utilisez l’une des méthodes suivantes :

   * Pour mettre en relation le fichier source avec la ressource, sélectionnez **[!UICONTROL Source]** dans la liste.
   * To relate a derived file, select **[!UICONTROL Derived]** from the list.
   * Pour créer une relation réciproque entre les ressources, sélectionnez **[!UICONTROL Autres]** dans la liste.
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. Sur l’écran **[!UICONTROL Sélectionner une ressource]**, accédez à l’emplacement de la ressource que vous souhaitez mettre en relation et sélectionnez-la.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez/appuyez sur l’icône **[!UICONTROL Confirmer]**.
1. Click/tap **[!UICONTROL OK]** to close the dialog. En fonction de la relation que vous avez choisie à l’étape 3, la ressource associée apparaît sous une catégorie appropriée dans la section **[!UICONTROL En relation]**. Par exemple, si la ressource que vous avez mise en relation est le fichier source de la ressource actuelle, elle apparaît sous **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. To un-relate an asset, click/tap **[!UICONTROL Unrelate]** from the toolbar.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Select the asset(s) you want to un-relate from the **[!UICONTROL Remove Relations]** dialog, and the click/tap **[!UICONTROL Unrelate]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Cliquez/appuyez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. Les ressources pour lesquelles vous avez supprimé des relations sont supprimées de la liste des ressources mises en relation dans la section **[!UICONTROL En relation]**.

## Traduction de ressources associées {#translating-related-assets}

La création de relations source/dérivés entre des ressources à l’aide de la fonctionnalité Ressources mises en relation est également utile dans les processus de traduction. Lorsque vous exécutez un processus de traduction sur une ressource dérivée, AEM Assets récupère automatiquement toute ressource référencée par le fichier source et la soumet pour traduction. De cette manière, la ressource référencée par la ressource source est traduite avec les ressources source et dérivées. Par exemple, supposons que votre copie de langue anglaise inclut une ressource dérivée et son fichier source, comme indiqué sur l’image ci-dessous.

![chlimage_1-281](assets/chlimage_1-281.png)

Si le fichier source est lié à un autre fichier, AEM Assets récupère l’élément référencé et l’inclut pour traduction.

![chlimage_1-282](assets/chlimage_1-282.png)

1. Traduisez les ressources du dossier source dans une langue cible en suivant les étapes de la section [Créer un projet de traduction](translation-projects.md#create-a-new-translation-project). Par exemple, dans ce cas, traduisez vos ressources en français.
1. From the [!UICONTROL Projects] page, open the translation folder.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Cliquez/appuyez sur la mosaïque du projet pour ouvrir la page de détails.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Cliquez/appuyez sur les points de suspension en dessous de la carte Tâche de traduction pour afficher l’état de la traduction.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Sélectionnez la ressource, puis cliquez/appuyez sur **[!UICONTROL Afficher dans Assets]** dans la barre d’outils pour afficher l’état de la traduction de la ressource.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Pour vérifier si les ressources mises en relation avec la source ont été traduites, cliquez/appuyez sur la ressource source.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Select the asset that is related to the source, and then click/tap **[!UICONTROL Reveal in Assets]**. La ressource associée traduite s’affiche.

   ![chlimage_1-288](assets/chlimage_1-288.png)
