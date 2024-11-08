---
title: Gestion des bannières
description: Les bannières représentent des liens promotionnels typiquement graphiques. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 6%

---

# Gestion des bannières{#managing-banners}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui permettent de créer et de gérer du contenu dans une application. Les actions suivantes sont effectuées sur le contenu de l’application.

## Présentation des bannières {#banners-overview}

Les bannières représentent des liens promotionnels typiquement graphiques.

>[!NOTE]
>
>Pour en savoir plus sur les rubriques suivantes des applications AEM Mobile, reportez-vous aux ressources suivantes de l’aide en ligne :
>
>* [Considérations de conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [Création de bannières](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## Création d’une bannière {#creating-a-banner}

Le workflow général pour créer un article est le suivant :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas dans le coin supérieur droit de la mosaïque **Gérer les bannières** .
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvelle bannière.
1. Une fois prêt, cliquez sur **Créer**.
1. La nouvelle bannière apparaît dans la mosaïque **Gérer les bannières** .

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importation d’une nouvelle bannière {#importing-a-new-banner}

Le contenu Mobile On Demand existant peut être téléchargé (importé) de Mobile On-Demand vers AEM. Cela permet l’édition et l’affichage de contenu local.

>[!NOTE]
>
>L’importation ne comprend pas d’images.

Workflow d’import d’un nouvel article

1. Depuis Mobile, sélectionnez votre application mobile à la demande dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gérer les bannières** et sélectionnez Importer des bannières.
1. Cliquez sur **Importer la bannière** dans la boîte de dialogue, puis sur Fermer.
1. Vos articles Mobile On-Demand apparaissent désormais dans la mosaïque **Gérer les bannières** .

>[!CAUTION]
>
>Associez d’abord une connexion Mobile On-Demand.

## Modification d’une bannière {#editing-a-banner}

Utilisez l’éditeur de glisser-déplacer intégré AEM pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Les images de DAM Assets peuvent être insérées.

>[!CAUTION]
>
>Seules les bannières créées dans AEM peuvent être ouvertes dans l’éditeur.

Workflow de modification d’un article :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une bannière d’AEM source dans la mosaïque **Gérer les bannières**.
1. Cliquez sur la bannière mise en surbrillance en mode Liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser le contenu de la bannière (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans une bannière {#viewing-and-editing-the-metadata-within-a-banner}

Les bannières présentent de nombreuses propriétés, telles que des titres, des descriptions et des images. Cette action est utilisée pour afficher et modifier ces propriétés. Vous pouvez éventuellement charger ces modifications dans Mobile On-Demand lors de l’enregistrement.

Processus général d’affichage/de modification d’un article :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une bannière dans la mosaïque **Gérer les bannières** .

1. Sélectionnez **Propriétés** dans la barre d’actions.
1. Affichez toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si vous le souhaitez et cliquez sur **Enregistrer** une fois terminé.
1. Vous pouvez éventuellement charger immédiatement les modifications dans Mobile On-Demand.

## Chargement d’une bannière {#uploading-a-banner}

L’action de téléchargement copie le contenu sélectionné et l’ajoute à un projet Mobile On-Demand. Le contenu existant de Mobile On Demand est déjà remplacé par la nouvelle version.

Processus général de téléchargement d’une bannière :

1. Depuis **Mobile**, sélectionnez votre application mobile à la demande dans le catalogue.
1. Dans la mosaïque **Gérer les bannières**, sélectionnez une bannière à charger vers Mobile On-Demand.
1. Ajoutez d’autres bannières si nécessaire à partir du mode Liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos bannières sont maintenant chargées vers Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Suppression d’une bannière {#deleting-a-banner}

Cette opération supprime la bannière sélectionnée de Mobile On-Demand, et éventuellement de l’instance d’AEM locale.

Workflow général de suppression d’une bannière :

1. Depuis Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez la bannière à supprimer dans la mosaïque **Gérer les bannières** .
1. Assurez-vous qu’il est sélectionné dans la liste (sélectionnez d’autres éléments à supprimer, si nécessaire).
1. Cliquez sur **Supprimer** dans la barre d’actions.
1. Vérifiez si vous souhaitez supprimer de AEM et de Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre bannière est maintenant supprimée de la liste.

### Les étapes suivantes {#the-next-steps}

Pour en savoir plus sur la gestion des bannières, voir

* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement de ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de la publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
