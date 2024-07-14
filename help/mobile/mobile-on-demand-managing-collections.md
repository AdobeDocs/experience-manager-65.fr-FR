---
title: Gestion des collections
description: Les collections représentent un compartiment bien défini contenant du contenu tel que des articles ou des bannières qui correspondent au thème de la couverture. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 5%

---

# Gestion des collections{#managing-collections}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui permettent de créer et de gérer du contenu dans une application. Les actions suivantes sont effectuées sur le contenu de l’application.

## Présentation des collections {#collections-overview}

Les collections représentent un *compartiment* bien défini avec du contenu tel que des articles ou des bannières qui s’adapte au thème de la couverture.

>[!NOTE]
>
>Pour en savoir plus sur les rubriques suivantes des applications AEM Mobile, reportez-vous aux ressources suivantes de l’aide en ligne :
>
>* [Considérations de conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Gestion des collections](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## Création d’une collection {#creating-a-collection}

Le workflow général pour créer une collection est le suivant :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas dans le coin supérieur droit de la mosaïque **Gérer les collections** .
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvel article.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvel article apparaît dans la mosaïque **Gérer les collections**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importation d’une nouvelle collection {#importing-a-new-collection}

Le contenu Mobile On Demand existant peut être téléchargé (importé) de Mobile On-Demand vers AEM. Cela permet l’édition et l’affichage de contenu local.

>[!NOTE]
>
>L’importation ne comprend pas d’images.

Workflow d’importation d’une nouvelle collection

1. Depuis Mobile, sélectionnez votre application mobile à la demande dans le catalogue.
1. Cliquez sur la flèche vers le bas dans le coin supérieur droit de la mosaïque **Gérer les collections** et sélectionnez Importer des collections.
1. Cliquez sur **Importer des collections** dans la boîte de dialogue, puis sur Fermer.
1. Vos collections Mobile On-Demand apparaissent désormais dans la mosaïque **Gérer les collections**.

>[!CAUTION]
>
>Associez d’abord une connexion Mobile On-Demand.

## Modification d’une collection {#editing-a-collection}

Utilisez l’éditeur de glisser-déplacer intégré AEM pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Les images de DAM Assets peuvent être insérées.

Le workflow pour modifier une collection :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article AEM issu de la mosaïque **Gérer les collections**.
1. Cliquez sur la collection mise en surbrillance en mode Liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser du contenu de collection (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans une collection {#viewing-and-editing-the-metadata-within-a-collection}

Les collections comportent de nombreuses propriétés telles que des titres, des descriptions, des images. Cette action est utilisée pour afficher et modifier ces propriétés. Vous pouvez éventuellement charger ces modifications dans Mobile On-Demand lors de l’enregistrement.

Le workflow général pour afficher/modifier une collection :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une collection dans la mosaïque **Gérer les collections**.

1. Sélectionnez **Propriétés** dans la barre d’actions.
1. Affichez toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si vous le souhaitez et cliquez sur **Enregistrer** une fois terminé.
1. Vous pouvez éventuellement charger immédiatement les modifications dans Mobile On-Demand.

## Téléchargement d’une collection {#uploading-a-collection}

L’action de téléchargement copie le contenu sélectionné et l’ajoute à un projet Mobile On-Demand. Le contenu existant de Mobile On Demand est déjà remplacé par la nouvelle version.

Workflow général de téléchargement d’une collection :

1. Depuis **Mobile**, sélectionnez votre application mobile à la demande dans le catalogue.
1. Dans la mosaïque **Gérer les collections**, sélectionnez un article à charger vers Mobile On-Demand.
1. Ajoutez d’autres collections si nécessaire à partir du mode Liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos collections sont désormais chargées vers Mobile On-Demand.

## Suppression d’une collection {#deleting-a-collection}

Cette opération supprime la collection sélectionnée de Mobile On-Demand, et éventuellement de l’instance d’AEM locale.

Workflow général de suppression d’une collection :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez l’article à supprimer dans la mosaïque **Gérer les collections**.
1. Assurez-vous qu’il est sélectionné dans la liste et sélectionnez d’autres options à supprimer.
1. Cliquez sur **Supprimer** dans la barre d’actions.
1. Vérifiez si vous souhaitez supprimer de AEM et de Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre collection est maintenant supprimée de la liste.

## Ajout de contenu aux collections {#adding-content-to-collections}

Les collections sont essentiellement une catégorie de contenu associé. Ils rassemblent du contenu, tel que des articles, des bannières, dans des modules qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

>[!NOTE]
>
>Le contenu doit être chargé sur Mobile On-Demand avant de pouvoir être ajouté à une collection.

Les collections sont essentiellement une catégorie de contenu associé : elles rassemblent le contenu tel que des articles, des bannières dans des packages qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionner un article précédemment chargé (ou bannière/collection)
1. Sélectionnez Ajouter à dans la barre d’actions.
1. Sélectionnez une collection précédemment chargée dans la boîte de dialogue.
1. Cliquez sur **Mettre à jour** pour ajouter du contenu à la collection.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Les étapes suivantes {#the-next-steps}

Pour en savoir plus sur la gestion des collections, voir

* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Chargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de la publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
