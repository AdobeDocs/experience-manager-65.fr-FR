---
title: Ressources liées
description: Découvrez comment relier des ressources numériques qui partagent certains attributs communs. Créez également des relations dérivées de la source entre les ressources numériques.
contentOwner: AG
role: Professionnel
feature: Collaboration, gestion des ressources
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 47%

---


# Ressources liées{#related-assets}

[!DNL Adobe Experience Manager Assets] vous permet de relier manuellement des ressources en fonction des besoins de votre organisation à l’aide de la fonction d’éléments connexes. Par exemple, vous pouvez mettre en relation un fichier de licence avec une ressource ou une image/vidéo portant sur un sujet similaire. Vous pouvez mettre en relation des ressources qui partagent certains attributs communs. Vous pouvez également utiliser cette fonctionnalité pour créer des relations source/dérivés entre des ressources. Par exemple, si un fichier PDF est généré à partir d’un fichier INDD, vous pouvez mettre en relation le fichier PDF avec son fichier INDD source.

Cette fonctionnalité vous permet de partager un fichier PDF ou JPG basse résolution avec des fournisseurs ou des agences et de rendre le fichier INDD haute résolution disponible uniquement sur demande.

>[!NOTE]
>
>Seuls les utilisateurs disposant d’autorisations de modification sur les ressources peuvent établir une relation et établir une relation entre les ressources.

## Lier les ressources {#relating-assets}

1. Dans l&#39;interface [!DNL Experience Manager], ouvrez la page **[!UICONTROL Propriétés]** pour une ressource à relier.

   ![ouvrir la page Propriétés d’une ressource pour établir une relation avec la ressource](assets/asset-properties-relate-assets.png)

   *Figure :  [!DNL Assets]  Propriétés pour associer des ressources.*

   Vous pouvez également sélectionner la ressource en mode Liste.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Sinon, sélectionnez la ressource à partir d’une collection.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Pour établir une relation entre un autre fichier et le fichier sélectionné, cliquez sur **[!UICONTROL Reler]** ![relier les ressources](assets/do-not-localize/link-relate.png) dans la barre d’outils.
1. Utilisez l’une des méthodes suivantes :

   * Pour mettre en relation le fichier source avec la ressource, sélectionnez **[!UICONTROL Source]** dans la liste.
   * Pour mettre en relation un fichier dérivé avec la ressource, sélectionnez **[!UICONTROL Dérivés]** dans la liste.
   * Pour créer une relation réciproque entre les ressources, sélectionnez **[!UICONTROL Autres]** dans la liste.

1. Sur l’écran **[!UICONTROL Sélectionner une ressource]**, accédez à l’emplacement de la ressource que vous souhaitez mettre en relation et sélectionnez-la.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez sur **[!UICONTROL Confirmer]**.
1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. En fonction de la relation que vous avez choisie à l’étape 3, la ressource associée apparaît sous une catégorie appropriée dans la section **[!UICONTROL En relation]**. Par exemple, si la ressource que vous avez mise en relation est le fichier source de la ressource actuelle, elle apparaît sous **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Pour annuler la relation entre un élément, cliquez sur **[!UICONTROL Annuler la relation]** ![dissocier les éléments](assets/do-not-localize/link-unrelate-icon.png) dans la barre d’outils.

1. Sélectionnez les ressources que vous souhaitez annuler la relation dans la boîte de dialogue **[!UICONTROL Supprimer les relations]**, puis cliquez sur **[!UICONTROL Annuler la relation]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. Les ressources pour lesquelles vous avez supprimé des relations sont supprimées de la liste des ressources mises en relation dans la section **[!UICONTROL En relation]**.

## Traduire les éléments connexes {#translating-related-assets}

La création de relations source/dérivée entre les ressources à l’aide de la fonction ressources connexes s’avère également utile dans les workflows de traduction. Lorsque vous exécutez un processus de traduction sur une ressource dérivée, [!DNL Experience Manager Assets] récupère automatiquement toute ressource référencée par le fichier source et l’inclut pour la traduction. De cette manière, la ressource référencée par la ressource source est traduite avec les ressources source et dérivées. Par exemple, supposons que votre copie de langue anglaise inclut une ressource dérivée et son fichier source, comme indiqué sur l’image ci-dessous.

![chlimage_1-281](assets/chlimage_1-281.png)

Si le fichier source est associé à un autre fichier, [!DNL Experience Manager Assets] récupère l’actif référencé et l’inclut pour traduction.

![la page Propriétés du fichier affiche le fichier source du fichier associé à inclure pour la traduction.](assets/asset-properties-source-asset.png)

*Figure : Fichier source des éléments connexes à inclure pour la traduction.*

1. Traduisez les ressources du dossier source dans une langue cible en suivant les étapes de la section [Créer un projet de traduction](translation-projects.md#create-a-new-translation-project). Par exemple, dans ce cas, traduisez vos ressources en français.

1. Dans la page [!UICONTROL Projets], ouvrez le dossier de traduction.

1. Cliquez sur la mosaïque du projet pour ouvrir la page de détails.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Cliquez sur les points de suspension sous la carte Tâche de traduction pour vue l’état de la traduction.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Sélectionnez la ressource, puis cliquez sur **[!UICONTROL Afficher dans les ressources]** dans la barre d’outils pour vue l’état de traduction de la ressource.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Pour vérifier si les fichiers associés à la source ont été traduits, cliquez sur le fichier source.

1. Sélectionnez la ressource associée à la source, puis cliquez sur **[!UICONTROL Afficher dans les ressources]**. La ressource associée traduite s’affiche.
