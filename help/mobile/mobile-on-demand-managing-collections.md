---
title: Gestion des collections
description: Les collections représentent un compartiment bien défini rempli de contenu tel que des articles ou des bannières qui convient au thème de la couverture. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 2%

---

# Gestion des collections{#managing-collections}

{{ue-over-mobile}}

Les actions de gestion de contenu sont les blocs de création qui permettent de créer et de gérer du contenu dans une application. Les actions suivantes sont effectuées sur le contenu de l’application.

## Présentation des collections {#collections-overview}

Les collections représentent un *compartiment* bien défini, rempli d’un contenu tel que des articles ou des bannières qui convient au thème de la couverture.

>[!NOTE]
>
>Consultez les ressources suivantes de l’aide en ligne pour en savoir plus sur les rubriques suivantes des applications AEM Mobile :
>
>* [Considérations de conception](https://helpx.adobe.com/fr/digital-publishing-solution/help/design-app.html)
>
>* [Gestion des collections](https://helpx.adobe.com/fr/digital-publishing-solution/help/creating-collections.html)
>

## Création d’une collection {#creating-a-collection}

Le workflow général de création d’une collection est le suivant :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Dans Mobile, choisissez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gérer les collections**.
1. Parcourez chaque étape de l’assistant pour continuer à créer votre article.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvel article s’affiche dans la mosaïque **Gérer les collections**.

![chlimage_1-1](assets/chlimage_1-1.gif)

## Importer une nouvelle collection {#importing-a-new-collection}

Le contenu Mobile On-Demand existant peut être téléchargé (importé) depuis Mobile On-Demand vers AEM. Cela permet la modification et l’affichage de contenu local.

>[!NOTE]
>
>L’importation n’inclut pas les images.

Workflow d’importation d’une nouvelle collection

1. Dans Mobile, choisissez l’application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gestion des collections** et sélectionnez Importer des collections.
1. Cliquez sur **Importer des collections** dans la boîte de dialogue, puis sur Fermer.
1. Vos collections On-Demand mobiles apparaissent désormais dans la mosaïque **Gérer les collections**.

>[!CAUTION]
>
>Associez d’abord une connexion Mobile On-Demand.

## Modification d’une collection {#editing-a-collection}

Utilisez l’éditeur AEM intégré par glisser-déposer pour ajouter ou modifier un article. Il est possible d’ajouter ou de supprimer des composants tels que du texte et des images. Vous pouvez insérer des images depuis DAM Assets.

Workflow de modification d’une collection :

1. Dans Mobile, choisissez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article d’origine AEM dans la mosaïque **Gérer les collections**.
1. Cliquez sur la collection en surbrillance dans la vue Liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser le contenu de la collection (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans une collection {#viewing-and-editing-the-metadata-within-a-collection}

Les collections possèdent de nombreuses propriétés telles que des titres, des descriptions, des images. Cette action permet d’afficher et de modifier ces propriétés. Ces modifications peuvent éventuellement être chargées sur Mobile On-Demand lors de l’enregistrement.

Workflow général d’affichage/de modification d’une collection :

1. Dans Mobile, choisissez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une collection dans la mosaïque **Gérer les collections**.

1. Sélectionnez **Propriétés** dans la barre d’actions.
1. Affichez toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si vous le souhaitez et cliquez sur **Enregistrer** lorsque vous avez terminé.
1. Vous pouvez éventuellement charger immédiatement les modifications dans Mobile On-Demand.

## Chargement d’une collection {#uploading-a-collection}

L’action de chargement copie le contenu sélectionné et l’ajoute à un projet Mobile On-Demand. Le contenu Mobile On-Demand existant est remplacé par la nouvelle version.

Workflow général de chargement d’une collection :

1. Dans **Mobile**, choisissez l’application Mobile On-Demand dans le catalogue.
1. Dans la mosaïque **Gérer les collections**, sélectionnez un article à charger sur Mobile On-Demand.
1. Ajoutez d’autres collections si nécessaire à partir de la vue Liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Votre ou vos collections sont maintenant chargées sur Mobile On-Demand.

## Suppression d’une collection {#deleting-a-collection}

Cette opération supprime la collection sélectionnée de Mobile On-Demand et, éventuellement, de l&#39;instance AEM locale.

Workflow général de suppression d’une collection :

1. Dans Mobile, choisissez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez l’article à supprimer dans la mosaïque **Gérer les collections**.
1. Assurez-vous qu’il est sélectionné dans la liste. Sélectionnez d’autres éléments à supprimer selon vos besoins.
1. Cliquez sur **Supprimer** dans la barre d’actions.
1. Cochez cette case si vous souhaitez supprimer d’AEM et Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre collection est maintenant supprimée de la liste.

## Ajout de contenu aux collections {#adding-content-to-collections}

Les collections sont essentiellement une catégorie de contenu associé. Ils rassemblent le contenu tel que des articles et des bannières dans des packages qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

>[!NOTE]
>
>Le contenu doit être chargé sur Mobile On-Demand avant de pouvoir être ajouté à une collection.

Les collections sont essentiellement une catégorie de contenu associé : elles rassemblent du contenu tel que des articles ou des bannières dans des packages qui définissent la structure de navigation de votre application. Les collections peuvent être imbriquées.

1. Dans Mobile, choisissez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez un article précédemment téléchargé (ou une bannière/collection).
1. Sélectionnez Ajouter à dans la barre d’actions.
1. Sélectionnez une collection précédemment chargée dans la boîte de dialogue.
1. Cliquez sur **Mettre à jour** pour ajouter du contenu à la collection.

![chlimage_1-2](assets/chlimage_1-2.gif)

### Les étapes suivantes {#the-next-steps}

Une fois que vous en savez plus sur la gestion des collections, consultez

* [Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)
* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Chargement des ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/dépublication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
