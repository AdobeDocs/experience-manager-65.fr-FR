---
title: Gestion des bannières
seo-title: Gestion des bannières
description: Les bannières représentent généralement des liens promotionnels graphiques. Consultez cette page pour en savoir plus.
seo-description: Les bannières représentent généralement des liens promotionnels graphiques. Consultez cette page pour en savoir plus.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 7%

---


# Gestion des bannières{#managing-banners}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les actions de gestion de contenu sont les blocs de création qui aident à créer et à gérer du contenu dans une application. Les actions suivantes sont exécutées sur le contenu de l’application.

## Présentation des bannières {#banners-overview}

Les bannières représentent généralement des liens promotionnels graphiques.

>[!NOTE]
>
>Reportez-vous aux ressources suivantes de l’aide en ligne pour en savoir plus sur les rubriques suivantes dans les applications AEM Mobile :
>
>* [Observations relatives à la conception](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
   >
   >
* [Création de bannières](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)

>



## Création d’une bannière {#creating-a-banner}

La procédure générale de création d’un article est la suivante :

1. Sélectionnez **Mobile** dans le rail latéral.
1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gérer les bannières** .
1. Parcourez chaque étape de l’assistant pour continuer à créer votre nouvelle bannière.
1. Une fois prêt, cliquez sur **Créer**.
1. Votre nouvelle bannière s’affiche dans la mosaïque **Gérer les bannières** .

![chlimage_1-6](assets/chlimage_1-6.gif)

## Importation d’une nouvelle bannière {#importing-a-new-banner}

Le contenu Mobile On-Demand existant peut être téléchargé (importé) de Mobile On-Demand à AEM. Cela permet la modification et l’affichage du contenu local.

>[!NOTE]
>
>L’importation n’inclut pas les images.

Flux de travail pour importer un nouvel article

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Cliquez sur la flèche vers le bas située dans le coin supérieur droit de la mosaïque **Gérer les bannières** et sélectionnez Importer des bannières.
1. Cliquez sur **Importer une bannière** dans la boîte de dialogue, puis sur Fermer.
1. Vos articles Mobile On-Demand apparaissent désormais dans la mosaïque **Gérer les bannières** .

>[!CAUTION]
>
>Vous devez d&#39;abord associer une connexion Mobile On-Demand.

## Modification d’une bannière {#editing-a-banner}

Utilisez l’éditeur de glisser-déplacer d’AEM intégré pour ajouter ou modifier un article. Des composants tels que du texte et des images peuvent être ajoutés/supprimés. Vous pouvez insérer des images à partir de ressources DAM.

>[!CAUTION]
>
>Seules les bannières créées dans AEM peuvent être ouvertes dans l’éditeur.

Flux de travail pour modifier un article :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une bannière d’AEM source dans la mosaïque** Gérer les bannières**.
1. Cliquez sur la bannière mise en surbrillance dans la vue de liste pour l’ouvrir dans l’éditeur de contenu.
1. Utilisez l’éditeur de contenu pour faire glisser le contenu de la bannière (manuscrits, images, texte, etc.).

### Affichage et modification des métadonnées dans une bannière {#viewing-and-editing-the-metadata-within-a-banner}

Les bannières ont de nombreuses propriétés, telles que des titres, des descriptions, des images. Cette action est utilisée pour vue et modifier ces propriétés. Ces modifications peuvent éventuellement être téléchargées sur Mobile On-Demand lors de l’enregistrement.

Processus général de vue/modification d’un article :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez une bannière dans la mosaïque **Gérer les bannières** .

1. Sélectionnez **Propriétés** dans la barre d’actions.
1. Vue de toutes les métadonnées disponibles pour cet article.
1. Modifiez les métadonnées si nécessaire et cliquez sur **Enregistrer** lorsque vous avez terminé.
1. Si vous le souhaitez, téléchargez immédiatement les modifications sur Mobile On-Demand.

## Téléchargement d’une bannière {#uploading-a-banner}

L&#39;action de téléchargement copie le contenu sélectionné et l&#39;ajoute à un projet Mobile On-Demand. Le contenu Mobile On-Demand existant est déjà remplacé par la nouvelle version.

Processus général de téléchargement d’une bannière :

1. Dans **Mobile**, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Dans la mosaïque **Gérer les bannières** , sélectionnez une bannière à télécharger sur Mobile On-Demand.
1. Si nécessaire, Ajoutez d&#39;autres bannières à partir de la vue de liste.
1. Sélectionnez **Télécharger** dans la barre d’actions, puis cliquez sur Télécharger dans la boîte de dialogue.
1. Vos bannières sont maintenant chargées sur Mobile On-Demand.

![chlimage_1-7](assets/chlimage_1-7.gif)

## Suppression d’une bannière {#deleting-a-banner}

Cette opération supprime la bannière sélectionnée de Mobile On-Demand et éventuellement de l’instance d’AEM locale.

Processus général de suppression d&#39;une bannière :

1. Dans Mobile, sélectionnez votre application Mobile On-Demand dans le catalogue.
1. Sélectionnez la bannière à supprimer dans la mosaïque **Gérer les bannières** .
1. Assurez-vous qu’elle est sélectionnée dans la liste (sélectionnez d’autres options à supprimer si nécessaire).
1. Click **Delete** from the action bar.
1. Vérifiez si vous souhaitez supprimer des AEM ainsi que des services Mobile On-Demand.
1. Cliquez sur **Supprimer**.
1. Votre bannière est maintenant supprimée de la liste.

### Étapes suivantes {#the-next-steps}

Vous en apprendrez plus sur la gestion des bannières à la section

* [Gestion des articles](/help/mobile/mobile-on-demand-managing-articles.md)
* [Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)
* [Chargement des ressources partagées](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publication/annulation de publication du contenu](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
