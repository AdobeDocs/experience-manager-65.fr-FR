---
title: Gestion des collections
seo-title: Gestion des collections
description: Les collections représentent un compartiment bien défini rempli de contenu tel que des articles ou des bannières qui s’adapte au thème de la couverture. Consultez cette page pour en savoir plus.
seo-description: Les collections représentent un compartiment bien défini rempli de contenu tel que des articles ou des bannières qui s’adapte au thème de la couverture. Consultez cette page pour en savoir plus.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gestion des collections{#managing-collections}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui aident à créer et à gérer le contenu dans une application. Les actions suivantes sont exécutées sur le contenu de l’application.

## Présentation des collections {#collections-overview}

Les collections représentent un *compartiment bien défini* rempli de contenu tel que des articles ou des bannières qui s’adaptent au thème de la couverture.

>[!NOTE]
>
>Reportez-vous aux ressources suivantes dans l&#39;aide en ligne pour en savoir plus sur les rubriques suivantes dans les applications AEM Mobile :
>
>* [Observations relatives à la conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gestion des collections](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>



## Création d’une collection {#creating-a-collection}

La procédure générale de création d’une collection est la suivante :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas dans le coin supérieur droit du volet **Gérer les collections** .
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvel article.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvel article s’affiche dans le volet **Gérer les collections** .

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importation d’une nouvelle collection {#importing-a-new-collection}

Le contenu Mobile On-Demand existant peut être téléchargé (importé) de Mobile On-Demand vers AEM. Cela permet la modification et l’affichage du contenu local.

>[!NOTE]
>
>L’importation n’inclut pas les images.

Processus d’importation d’une nouvelle collection

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas dans le coin supérieur droit du volet **Gérer les collections** et sélectionnez Importer des collections.
1. Cliquez sur **Importer des collections** dans la boîte de dialogue, puis sur Fermer.
1. Vos collections Mobile On-Demand apparaissent désormais dans le volet **Gérer les collections** .

>[!CAUTION]
>
>Vous devez d&#39;abord associer une connexion Mobile On-Demand.

## Modification d’une collection {#editing-a-collection}

Utilisez l’éditeur de glisser-déplacer intégré à AEM pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Vous pouvez insérer des images à partir de ressources DAM.

Processus de modification d’une collection :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article d’origine AEM dans le volet **Gérer les collections** .
1. Cliquez sur la collection mise en surbrillance dans la vue Liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser le contenu de la collection (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans une collection {#viewing-and-editing-the-metadata-within-a-collection}

Les collections ont de nombreuses propriétés telles que des titres, des descriptions, des images. Cette action est utilisée pour afficher et modifier ces propriétés. Ces modifications peuvent éventuellement être téléchargées sur Mobile On-Demand lors de l’enregistrement.

Processus général d’affichage/de modification d’une collection :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une collection dans le volet **Gérer les collections** .

1. Sélectionnez **Propriétés** dans la barre d’actions.
1. Afficher toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées, le cas échéant, puis cliquez sur **Enregistrer** lorsque vous avez terminé.
1. Si vous le souhaitez, téléchargez les modifications immédiatement vers Mobile On-Demand.

## Téléchargement d’une collection {#uploading-a-collection}

L’action de téléchargement copie le contenu sélectionné et l’ajoute à un projet Mobile On-Demand. Le contenu Mobile On-Demand existant est déjà remplacé par la nouvelle version.

Processus général de téléchargement d’une collection :

1. Dans **Mobile**, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Dans le volet **Gérer les collections** , sélectionnez un article à télécharger vers Mobile On-Demand.
1. Ajoutez d’autres collections si nécessaire dans la vue Liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos collections sont maintenant transférées vers Mobile On-Demand.

## Suppression d’une collection {#deleting-a-collection}

Cette opération supprime la collection sélectionnée de Mobile On-Demand et éventuellement de l’instance locale AEM.

Processus général de suppression d’une collection :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez l’article à supprimer dans le volet **Gérer les collections** .
1. Assurez-vous qu’elle est sélectionnée dans la liste (sélectionnez d’autres options à supprimer, le cas échéant).
1. Click **Delete** from the action bar.
1. Vérifiez si vous souhaitez supprimer des fichiers d&#39;AEM et de Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre collection est maintenant supprimée de la liste.

## Ajout de contenu aux collections {#adding-content-to-collections}

Les collections sont essentiellement une catégorie de contenu associé. Ils rassemblent du contenu, tel que des articles, des bannières, dans des packages qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

>[!NOTE]
>
>Le contenu doit être téléchargé sur Mobile On-Demand pour pouvoir être ajouté à une collection.

Les collections sont essentiellement une catégorie de contenu associé :Ils rassemblent du contenu, tel que des articles, des bannières, dans des packages qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionner un article précédemment téléchargé (ou bannière/collection)
1. Choisissez Ajouter à dans la barre d’actions.
1. Sélectionnez une collection précédemment chargée dans la boîte de dialogue.
1. Cliquez sur **Mettre à jour** pour ajouter du contenu à la collection.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Étapes suivantes {#the-next-steps}

Une fois que vous avez appris sur la gestion des collections, reportez-vous à la section

* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Téléchargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
