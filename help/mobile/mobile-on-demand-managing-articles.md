---
title: Gestion des articles
seo-title: Managing Articles
description: Consultez cette page pour en savoir plus sur la création et la gestion des articles.
seo-description: Follow this page to learn about creating and managing Articles.
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---

# Gestion des articles{#managing-articles}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui permettent de créer et de gérer des articles au sein d’une application. Les actions suivantes sont effectuées sur des articles de l’application.

## Présentation des articles {#articles-overview}

Les articles représentent le texte fondé sur l’art pour véhiculer l’information.

>[!NOTE]
>
>Pour en savoir plus sur les rubriques suivantes des applications AEM Mobile, reportez-vous aux ressources suivantes de l’aide en ligne :
>
>* [Considérations relatives à la conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Gestion des articles](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>

## Création d’un article {#creating-an-article}

Le workflow général pour créer un article est le suivant :

1. Sélectionner **Mobile** à partir du rail latéral.
1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de l’objet **Gestion des articles** mosaïque.
1. Choisissez un modèle d’article et cliquez sur **Suivant**.
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvel article.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvel article apparaît dans la section **Gestion des articles** mosaïque.

## Importation d’un nouvel article {#importing-a-new-article}

Le contenu Mobile On Demand existant peut être téléchargé (importé) de Mobile On-Demand vers AEM. Cela permet l’édition et l’affichage de contenu local.

>[!NOTE]
>
>L’importation ne comprend pas d’images.

Workflow d’import d’un nouvel article

1. Depuis Mobile, sélectionnez votre application mobile à la demande dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de l’objet **Gestion des articles** et sélectionnez Importer des articles.
1. Cliquez sur **Importation d’articles** dans la boîte de dialogue, puis cliquez sur Fermer.
1. Vos articles Mobile On Demand apparaissent désormais dans le **Gestion des articles** mosaïque.

>[!CAUTION]
>
>Vous devez d&#39;abord associer une connexion Mobile On-Demand.

![chlimage_1-3](assets/chlimage_1-3.gif)

## Modification d’un article {#editing-an-article}

Utilisez l’éditeur de glisser-déplacer intégré AEM pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Les images des ressources de gestion des actifs numériques peuvent être insérées.

>[!CAUTION]
>
>Seuls les articles créés dans AEM peuvent être ouverts dans l’éditeur.

Workflow de modification d’un article :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un AEM article d’origine dans la **Gestion des articles** mosaïque.
1. Cliquez sur l’article en surbrillance dans la vue Liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l&#39;éditeur de contenu pour faire glisser le contenu de l&#39;article (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans un article {#viewing-and-editing-the-metadata-within-an-article}

Le contenu comme les articles, les bannières, etc., possède de nombreuses propriétés telles que les titres, descriptions, images. Cette action est utilisée pour afficher et modifier ces propriétés. Vous pouvez éventuellement charger ces modifications dans Mobile On-Demand lors de l’enregistrement.

Processus général d’affichage/de modification d’un article :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Choisissez un article dans la **Gestion des articles** mosaïque.

1. Sélectionner **Afficher les propriétés** dans la barre d’actions.
1. Affichez toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si vous le souhaitez, puis cliquez sur **Enregistrer** une fois terminé.
1. Vous pouvez éventuellement charger immédiatement les modifications dans Mobile On-Demand.

## Téléchargement d’un article {#uploading-an-article}

L’action de téléchargement copie le contenu sélectionné et l’ajoute à un projet Mobile On-Demand. Le contenu existant de Mobile On Demand est déjà remplacé par la nouvelle version.

Processus général de téléchargement d’un article :

1. De **Mobile**, sélectionnez votre application mobile à la demande dans le catalogue.
1. Dans le **Gestion des articles** , sélectionnez un article à charger vers Mobile On-Demand.
1. Ajoutez d’autres articles si nécessaire en mode Liste.
1. Sélectionner **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos articles sont maintenant chargés sur Mobile On-Demand.

![chlimage_1-4](assets/chlimage_1-4.gif)

## Suppression d’un article {#deleting-an-article}

Cette opération supprime le contenu sélectionné de Mobile On-Demand, et éventuellement de l’instance d’AEM locale.

Workflow général de suppression d’un article :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez l’article à supprimer dans le **Gestion des articles** mosaïque.
1. Assurez-vous qu’elle est sélectionnée dans la liste (sélectionnez d’autres options à supprimer, si nécessaire).
1. Cliquez sur **Supprimer** dans la barre d’actions.
1. Vérifiez si vous souhaitez supprimer de AEM ainsi que de Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre article est maintenant retiré de la liste.

![chlimage_1-5](assets/chlimage_1-5.gif)

### Les étapes suivantes {#the-next-steps}

Pour en savoir plus sur la gestion des articles, voir

* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de la publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
