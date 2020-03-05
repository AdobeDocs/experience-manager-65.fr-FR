---
title: Publication de collections sur Brand Portal
seo-title: Publication de collections sur Brand Portal
description: Découvrez comment publier et annuler la publication de collections dans Brand Portal.
seo-description: Découvrez comment publier et annuler la publication de collections dans Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publication de collections sur Brand Portal {#publish-collections-to-brand-portal}

En tant qu’administrateur Adobe Experience Manager (AEM) Assets, vous pouvez publier des collections dans l’instance AEM Assets Brand Portal de votre organisation. Cependant, vous devez d’abord intégrer AEM Assets à Brand Portal. For details, see [Configure AEM Assets with Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Si vous apportez des modifications ultérieures à la collection d’origine dans AEM Assets, les modifications ne sont pas répercutées dans Brand Portal tant que vous n’avez pas publié à nouveau la collection. Cette caractéristique garantit que les modifications en cours ne sont pas disponibles dans le portail de marque. Seules les modifications approuvées publiées par un administrateur sont disponibles dans le portail des marques.

>[!NOTE]
>
>Les fragments de contenu ne peuvent pas être publiés sur Brand Portal. Therefore, if you select content fragment(s) on AEM Author, then **Publish to Brand Portal** action is not available.
>
>Si des collections contenant des fragments de contenu sont publiées sur Brand Portal à partir de l’auteur AEM, alors tout le contenu du dossier, excepté les fragments de contenu, est répliqué sur l’interface Brand Portal.

## Publication d’une collection dans Brand Portal {#publish-a-collection-to-brand-portal}

1. Dans l’interface utilisateur d’AEM Assets, cliquez sur le logo AEM.
1. From **Navigation** page, go to **Assets > Collections**.
1. Dans la console Collections, sélectionnez la collection que vous souhaitez publier sur le portail de marques.

   ![select_collection](assets/select_collection.png)

1. From the toolbar, click **Publish to Brand Portal**.
1. In the confirmation dialog, click **Publish**.
1. Fermez le message de confirmation.
1. Connectez-vous à Brand Portal en tant qu’administrateur. La collection publiée est disponible dans la console Collections.

   ![collection publiée](assets/published_collection.png)

## Annulation de la publication de collections {#unpublish-collections}

Vous pouvez annuler la publication des collections que vous publiez depuis AEM Assets sur le portail de marques. Une fois la collection d’origine dépubliée, sa copie n’est plus disponible pour les utilisateurs du portail de marque.

1. Dans la console Collections de votre instance AEM Assets, sélectionnez la collection dont vous souhaitez annuler la publication.

   ![select_collection-1](assets/select_collection-1.png)

1. From the toolbar, click **Remove from Brand Portal** icon.
1. In the dialog, click **Unpublish**.
1. Fermez le message de confirmation. La collection est supprimée de l’interface de Brand Portal.

