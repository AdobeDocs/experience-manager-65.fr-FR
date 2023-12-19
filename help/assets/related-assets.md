---
title: Ressources liées
description: Découvrez comment mettre en relation des ressources numériques qui partagent certains attributs communs. Créez également des relations dérivées de la source entre les ressources numériques.
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 96%

---

# Ressources liées {#related-assets}

[!DNL Adobe Experience Manager Assets] vous permet de mettre en relation manuellement des ressources en fonction des besoins de votre organisation à l’aide de la fonctionnalité Ressources associées. Vous pouvez, par exemple, associer un fichier de licence à une ressource ou à une image/vidéo sur une rubrique similaire. Vous pouvez mettre en relation des ressources qui partagent certains attributs communs. Vous pouvez également utiliser la fonction pour créer des relations sources/dérivées entre les ressources. Par exemple, si vous disposez d’un fichier PDF généré à partir d’un fichier INDD, vous pouvez associer le fichier PDF à son fichier INDD source.

Grâce à cette fonctionnalité, vous avez la possibilité de partager un fichier PDF ou JPG basse résolution avec des fournisseurs ou des agences et de rendre le fichier INDD haute résolution disponible uniquement sur demande.

>[!NOTE]
>
>Seuls les utilisateurs disposant d’autorisations de modification des ressources peuvent mettre en relation et dissocier ces dernières.

## Lier les ressources {#relating-assets}

1. À partir de l’interface d’[!DNL Experience Manager], ouvrez la page **[!UICONTROL Propriétés]** d’une ressource que vous souhaitez mettre en relation.

   ![ouvrir la page Propriétés d’une ressource pour mettre celle-ci en relation](assets/asset-properties-relate-assets.png)

   *Image : page [!UICONTROL Propriétés] d’[!DNL Assets] pour mettre en relation des ressources.*

   Vous pouvez également sélectionner la ressource dans la vue Liste.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Sinon, sélectionnez la ressource à partir d’une collection.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Pour mettre en relation une autre ressource avec celle que vous avez sélectionnée, cliquez sur **[!UICONTROL Mettre en relation]** ](assets/do-not-localize/link-relate.png)lier des ressources![ dans la barre d’outils.
1. Utilisez l’une des méthodes suivantes :

   * Pour associer le fichier source de la ressource, sélectionnez **[!UICONTROL Source]** dans la liste.
   * Pour mettre en relation un fichier dérivé avec la ressource, sélectionnez **[!UICONTROL Dérivés]** dans la liste.
   * Pour créer une relation bidirectionnelle entre les ressources, sélectionnez **[!UICONTROL Autres]** dans la liste.

1. À l&#39;écran **[!UICONTROL Sélectionner une ressource]**, accédez à l’emplacement de la ressource à associer puis sélectionnez-la.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez sur **[!UICONTROL Confirmer]**.
1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. Selon la relation que vous avez choisie à l’étape 3, la ressource associée est répertoriée sous une catégorie appropriée dans la section **[!UICONTROL Associé]** . Par exemple, si la ressource que vous avez associée est le fichier source de la ressource actuelle, elle est répertoriée sous **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Pour annuler la relation avec une ressource, cliquez sur **[!UICONTROL Dissocier]** ![dissociation des ressources](assets/do-not-localize/link-unrelate-icon.png) dans la barre d’outils.

1. Sélectionnez la ou les ressources que vous souhaitez dissocier dans la boîte de dialogue **[!UICONTROL Supprimer les relations]**, puis cliquez sur **[!UICONTROL Dissocier]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Cliquez sur **[!UICONTROL OK]** pour fermer la boîte de dialogue. Les ressources pour lesquelles vous avez supprimé des relations sont supprimées de la liste des ressources mises en relation dans la section **[!UICONTROL En relation]**.

## Traduire les ressources liées {#translating-related-assets}

La création de relations source/dérivés entre des ressources à l’aide de la fonctionnalité Ressources mises en relation est également utile dans les workflows de traduction. Lorsque vous exécutez un workflow de traduction sur une ressource dérivée, [!DNL Experience Manager Assets] récupère automatiquement toute ressource référencée par le fichier source et la soumet pour traduction. Ainsi, la ressource référencée par la ressource source est traduite avec les ressources source et dérivées. Supposons, par exemple, que votre copie en anglais inclue une ressource dérivée et son fichier source, comme illustré ci-dessous.

![chlimage_1-281](assets/chlimage_1-281.png)

Si le fichier source est mis en relation avec une autre ressource, [!DNL Experience Manager Assets] récupère la ressource référencée et la soumet pour traduction.

![page Propriétés de la ressource qui affiche le fichier source de la ressource associée à inclure pour la traduction](assets/asset-properties-source-asset.png)

*Image : ressource source des ressources connexes à inclure pour la traduction*

1. Traduisez les ressources du dossier source dans une langue cible en suivant les étapes décrites dans la section [Création d’un projet de traduction](translation-projects.md#create-a-new-translation-project). Par exemple, ici, traduisez vos ressources en français.

1. Sur la page [!UICONTROL Projets], ouvrez le dossier de traduction.

1. Cliquez sur la mosaïque du projet pour ouvrir la page de détails.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Cliquez sur les points de suspension en dessous de la carte Tâche de traduction pour afficher le statut de la traduction.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Sélectionnez la ressource, puis cliquez sur **[!UICONTROL Afficher dans Assets]** dans la barre d’outils pour afficher le statut de la traduction de la ressource.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Pour vérifier si les ressources mises en relation avec la source ont été traduites, cliquez sur la ressource source.

1. Sélectionnez la ressource mise en relation avec la source, puis cliquez sur **[!UICONTROL Afficher dans Assets]**. La ressource associée traduite s’affiche.
