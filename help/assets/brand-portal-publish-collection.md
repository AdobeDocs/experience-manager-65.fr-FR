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
feature: Brand Portal
role: Business Practitioner
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 69%

---

# Publication de collections sur Brand Portal {#publish-collections-to-brand-portal}

En tant qu’administrateur Adobe Experience Manager (AEM) Assets, vous pouvez publier des collections dans l’instance AEM Assets Brand Portal de votre organisation. Cependant, vous devez d’abord intégrer AEM Assets à Brand Portal. Pour plus de détails, voir [Configuration d’AEM Assets avec Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Si vous apportez des modifications ultérieures à la collection d’origine dans AEM Assets, les modifications ne sont pas répercutées dans Brand Portal tant que vous n’avez pas republié la collection. Cette caractéristique permet de s’assurer que les modifications en cours ne sont pas disponibles dans Brand Portal. Seules les modifications approuvées publiées par un administrateur sont disponibles dans Brand Portal.

>[!NOTE]
>
>Les fragments de contenu ne peuvent pas être publiés sur Brand Portal. Par conséquent, si vous sélectionnez un ou plusieurs fragments de contenu sur l’auteur AEM, l’action **Publier sur Brand Portal** n’est pas disponible.
>
>Si des collections contenant des fragments de contenu sont publiées sur Brand Portal à partir de l’auteur AEM, alors tout le contenu du dossier, excepté les fragments de contenu, est répliqué sur l’interface Brand Portal.

## Publication d’une collection dans Brand Portal {#publish-a-collection-to-brand-portal}

1. Dans l’interface utilisateur AEM Assets, cliquez sur le logo AEM.
1. Dans la console **Navigation**, accédez à **Ressources > Collections**.
1. Dans la console Collections, sélectionnez la collection que vous souhaitez publier dans Brand Portal.

   ![select_collection](assets/select_collection.png)

1. Dans la barre d’outils, cliquez sur **Publier sur Brand Portal**.
1. Dans la boîte de dialogue de confirmation, cliquez sur **Publier**.
1. Fermez le message de confirmation.
1. Connectez-vous à Brand Portal en tant qu’administrateur. La collection publiée est disponible dans la console Collections.

   ![collection publiée](assets/published_collection.png)

## Annulation de la publication de collections {#unpublish-collections}

Vous pouvez annuler la publication de collections que vous publiez d’AEM Assets vers Brand Portal. Une fois la publication de la collection d’origine annulée, sa copie n’est plus disponible pour les utilisateurs de Brand Portal.

1. Dans la console Collections de votre instance AEM Assets, sélectionnez la collection dont vous souhaitez annuler la publication.

   ![select_collection-1](assets/select_collection-1.png)

1. Dans la barre d’outils, cliquez sur l’icône **Supprimer de Brand Portal**.
1. Dans la boîte de dialogue, cliquez sur **Annuler la publication**.
1. Fermez le message de confirmation. La collection est supprimée de l’interface de Brand Portal.
