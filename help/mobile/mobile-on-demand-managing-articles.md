---
title: Gestion des articles
seo-title: Gestion des articles
description: Suivez cette page pour en savoir plus sur la création et la gestion des articles.
seo-description: Suivez cette page pour en savoir plus sur la création et la gestion des articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 4%

---


# Gestion des articles{#managing-articles}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui permettent de créer et de gérer des articles au sein d’une application. Les actions suivantes sont exécutées sur des articles de l’application.

## Présentation des articles {#articles-overview}

Les articles représentent le texte basé sur l&#39;art pour transmettre des informations.

>[!NOTE]
>
>Reportez-vous aux ressources suivantes de l’aide en ligne pour en savoir plus sur les rubriques suivantes dans les applications AEM Mobile :
>
>* [Observations relatives à la conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Gestion des articles](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)

>



## Création d’un article {#creating-an-article}

La procédure générale de création d’un article est la suivante :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gérer les articles** .
1. Choisissez un modèle d’article et cliquez sur **Suivant**.
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvel article.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvel article s’affiche dans le volet **Gérer les articles** .

## Importation d’un nouvel article {#importing-a-new-article}

Le contenu Mobile On-Demand existant peut être téléchargé (importé) de Mobile On-Demand à AEM. Cela permet la modification et l’affichage du contenu local.

>[!NOTE]
>
>L’importation n’inclut pas les images.

Flux de travail pour importer un nouvel article

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit du volet **Gérer les articles** et sélectionnez Importer des articles.
1. Cliquez sur **Importer des articles** dans la boîte de dialogue, puis sur Fermer.
1. Vos articles Mobile On-Demand apparaissent désormais dans le volet **Gérer les articles** .

>[!CAUTION]
>
>Vous devez d&#39;abord associer une connexion Mobile On-Demand.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Modification d’un article {#editing-an-article}

Utilisez l’éditeur de glisser-déplacer d’AEM intégré pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Vous pouvez insérer des images à partir de ressources DAM.

>[!CAUTION]
>
>Seuls les articles créés dans AEM peuvent être ouverts dans l’éditeur.

Flux de travail pour modifier un article :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article d’origine AEM dans le volet **Gérer les articles** .
1. Cliquez sur l’article en surbrillance de la vue de liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser le contenu de l’article (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans un article {#viewing-and-editing-the-metadata-within-an-article}

Les contenus tels que les articles, les bannières, etc, ont de nombreuses propriétés telles que les titres, descriptions, images. Cette action est utilisée pour vue et modifier ces propriétés. Ces modifications peuvent éventuellement être téléchargées sur Mobile On-Demand lors de l’enregistrement.

Processus général de vue/modification d’un article :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article dans le volet **Gérer les articles** .

1. Select **View Properties** from the action bar.
1. Vue de toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si nécessaire et cliquez sur **Enregistrer** lorsque vous avez terminé.
1. Si vous le souhaitez, téléchargez immédiatement les modifications sur Mobile On-Demand.

## Téléchargement d’un article {#uploading-an-article}

L&#39;action de téléchargement copie le contenu sélectionné et l&#39;ajoute à un projet Mobile On-Demand. Le contenu Mobile On-Demand existant est déjà remplacé par la nouvelle version.

Processus général de téléchargement d’un article :

1. Dans **Mobile**, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Dans le volet **Gérer les articles** , sélectionnez un article à télécharger sur Mobile On-Demand.
1. Si nécessaire, Ajoutez d’autres articles à partir de la vue de liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos articles sont maintenant chargés sur Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Suppression d’un article {#deleting-an-article}

Cette opération supprime le contenu sélectionné de Mobile On-Demand et éventuellement de l’instance d’AEM locale.

Processus général de suppression d’un article :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez l’article à supprimer dans le volet **Gérer les articles** .
1. Assurez-vous qu’elle est sélectionnée dans la liste (sélectionnez d’autres options à supprimer si nécessaire).
1. Click **Delete** from the action bar.
1. Vérifiez si vous souhaitez supprimer des AEM ainsi que des services Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre article est maintenant supprimé de la liste.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Étapes suivantes {#the-next-steps}

Une fois que vous avez appris sur la gestion des articles, reportez-vous à la section

* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement des ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
