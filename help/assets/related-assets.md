---
title: Ressources liées
description: Découvrez comment mettre en relation des ressources numériques qui partagent certains attributs communs. Créez également des relations dérivées de la source entre les ressources numériques.
contentOwner: AG
role: Business Practitioner
feature: Collaboration, Gestion des ressources
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 46%

---

# Ressources liées{#related-assets}

[!DNL Adobe Experience Manager Assets] vous permet de mettre en relation manuellement des ressources en fonction des besoins de votre entreprise à l’aide de la fonction ressources associée. Par exemple, vous pouvez mettre en relation un fichier de licence avec une ressource ou une image/vidéo portant sur un sujet similaire. Vous pouvez mettre en relation des ressources qui partagent certains attributs communs. Vous pouvez également utiliser cette fonctionnalité pour créer des relations source/dérivés entre des ressources. Par exemple, si un fichier PDF est généré à partir d’un fichier INDD, vous pouvez mettre en relation le fichier PDF avec son fichier INDD source.

Grâce à cette fonctionnalité, vous avez la possibilité de partager un fichier PDF ou JPG basse résolution avec des fournisseurs ou des agences et de rendre le fichier INDD haute résolution disponible uniquement sur demande.

>[!NOTE]
>
>Seuls les utilisateurs disposant d’autorisations de modification des ressources peuvent mettre en relation et dissocier ces dernières.

## Lier les ressources {#relating-assets}

1. Dans l’interface [!DNL Experience Manager], ouvrez la page **[!UICONTROL Propriétés]** d’une ressource que vous souhaitez mettre en relation.

   ![ouvrir la page Propriétés d’une ressource pour mettre celle-ci en relation.](assets/asset-properties-relate-assets.png)

   *Figure :  [!DNL Assets]  Propriétés permettant de mettre en relation des ressources.*

   Vous pouvez également sélectionner la ressource en mode Liste.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Sinon, sélectionnez la ressource à partir d’une collection.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Pour mettre en relation une autre ressource avec la ressource sélectionnée, cliquez sur **[!UICONTROL Lier]** ![mettre en relation les ressources](assets/do-not-localize/link-relate.png) dans la barre d’outils.
1. Utilisez l’une des méthodes suivantes :

   * Pour mettre en relation le fichier source avec la ressource, sélectionnez **[!UICONTROL Source]** dans la liste.
   * Pour mettre en relation un fichier dérivé avec la ressource, sélectionnez **[!UICONTROL Dérivés]** dans la liste.
   * Pour créer une relation réciproque entre les ressources, sélectionnez **[!UICONTROL Autres]** dans la liste.

1. Sur l’écran **[!UICONTROL Sélectionner une ressource]**, accédez à l’emplacement de la ressource que vous souhaitez mettre en relation et sélectionnez-la.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez sur **[!UICONTROL Confirmer]**.
1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. En fonction de la relation que vous avez choisie à l’étape 3, la ressource associée apparaît sous une catégorie appropriée dans la section **[!UICONTROL En relation]**. Par exemple, si la ressource que vous avez mise en relation est le fichier source de la ressource actuelle, elle apparaît sous **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Pour annuler la relation entre une ressource, cliquez sur **[!UICONTROL Ne plus mettre en relation]** ![Ressources ](assets/do-not-localize/link-unrelate-icon.png) dans la barre d’outils.

1. Sélectionnez la ou les ressources dont vous souhaitez annuler la relation dans la boîte de dialogue **[!UICONTROL Supprimer les relations]**, puis cliquez sur **[!UICONTROL Ne plus mettre en relation]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. Les ressources pour lesquelles vous avez supprimé des relations sont supprimées de la liste des ressources mises en relation dans la section **[!UICONTROL En relation]**.

## Traduire les éléments connexes {#translating-related-assets}

La création de relations source/dérivées entre les ressources à l’aide de la fonction Ressources connexes s’avère également utile dans les processus de traduction. Lorsque vous exécutez un workflow de traduction sur une ressource dérivée, [!DNL Experience Manager Assets] récupère automatiquement toute ressource référencée par le fichier source et l’inclut pour traduction. De cette manière, la ressource référencée par la ressource source est traduite avec les ressources source et dérivées. Par exemple, supposons que votre copie de langue anglaise inclut une ressource dérivée et son fichier source, comme indiqué sur l’image ci-dessous.

![chlimage_1-281](assets/chlimage_1-281.png)

Si le fichier source est associé à une autre ressource, [!DNL Experience Manager Assets] récupère la ressource référencée et l’inclut pour traduction.

![la page Propriétés de la ressource affiche le fichier source de la ressource associée à inclure pour traduction.](assets/asset-properties-source-asset.png)

*Figure : Ressource des ressources connexes à inclure pour traduction.*

1. Traduisez les ressources du dossier source dans une langue cible en suivant les étapes de la section [Créer un projet de traduction](translation-projects.md#create-a-new-translation-project). Par exemple, dans ce cas, traduisez vos ressources en français.

1. Sur la page [!UICONTROL Projets], ouvrez le dossier de traduction.

1. Cliquez sur la mosaïque du projet pour ouvrir la page de détails.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Cliquez sur les points de suspension situés sous la carte Tâche de traduction pour afficher l’état de traduction.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Sélectionnez la ressource, puis cliquez sur **[!UICONTROL Afficher dans Assets]** dans la barre d’outils pour afficher l’état de traduction de la ressource.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Pour vérifier si les ressources liées à la source ont été traduites, cliquez sur la ressource source.

1. Sélectionnez la ressource liée à la source, puis cliquez sur **[!UICONTROL Afficher dans Assets]**. La ressource associée traduite s’affiche.
