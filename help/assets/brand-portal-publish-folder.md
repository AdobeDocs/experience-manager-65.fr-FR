---
title: Publication de dossiers sur Brand Portal
description: Découvrez comment publier et annuler la publication de dossiers sur Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '565'
ht-degree: 100%

---

# Publication de dossiers sur Brand Portal{#publish-folders-to-brand-portal}

En tant qu’administrateur d’Adobe Experience Manager (AEM) Assets, vous pouvez publier des ressources et des dossiers sur l’instance AEM Assets Brand Portal (ou planifier le workflow de publication à une date/heure ultérieure) pour votre organisation. Cependant, vous devez d’abord intégrer AEM Assets à Brand Portal. Pour plus de détails, consultez [Configuration d’AEM Assets avec Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Une fois que vous avez publié une ressource ou un dossier, il est disponible dans Brand Portal.

Si vous apportez des modifications ultérieures à la ressource ou au dossier d’origine dans AEM Assets, les changements ne sont reflétés dans Brand Portal que lorsque vous republiez la ressource ou le dossier. Cette fonction assure que les modifications en cours ne sont pas disponibles dans Brand Portal. Seules les modifications approuvées publiées par un administrateur sont disponibles dans Brand Portal.

## Publication de dossiers sur Brand Portal {#publish-folders-to-brand-portal-1}

1. Dans l’interface d’AEM Assets, placez le curseur au-dessus du dossier désiré et sélectionnez l’option **Publier** parmi les actions rapides.

   Vous pouvez aussi sélectionner le dossier souhaité et suivre les étapes supplémentaires.

   ![publish2bp](assets/publish2bp.png)

1. **Publier immédiatement des dossiers**

   Pour publier les dossiers sélectionnés sur Brand Portal, effectuez l’une des opérations suivantes :

   * Dans la barre d’outils, sélectionnez **Publication rapide**. Ensuite, sélectionnez **Publier sur Brand Portal** dans le menu.

   * Dans la barre d’outils, sélectionnez **Gérer la publication**.

   1. Dans **Action**, sélectionnez **Publication sur Brand Portal**, depuis **Planification** sélectionnez **Maintenant**, puis cliquez sur **Suivant.**
   1. Confirmez votre sélection dans **Portée** et cliquez sur **Publier sur Brand Portal**.

   Un message indique que le dossier a été placé en file d’attente pour publication sur Brand Portal. Connectez-vous à l’interface Brand Portal pour voir le dossier publié.

   **Publication ultérieure de dossiers**

   Pour planifier le workflow de publication sur Brand Portal de dossiers de ressources à une date ou à une heure ultérieure :

   1. Une fois que vous avez sélectionné les ressources/dossiers à publier, sélectionnez **Gérer la publication** dans la barre d’outils supérieure.
   1. Dans **Action**, sélectionnez **Publier sur Brand Portal** et dans **Planification**, sélectionnez **Plus tard**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Sélectionnez une **Date d’activation** et spécifiez l’heure. Cliquez sur **Suivant**.
   1. Confirmez votre sélection dans **Portée**. Cliquez sur **Suivant**.
   1. Spécifiez un titre de workflow sous **Processus**. Cliquez sur **Publier ultérieurement**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Dépublication de dossiers sur Brand Portal {#unpublish-folders-from-brand-portal}

Vous pouvez supprimer n’importe quel dossier de ressources publié sur Brand Portal en la dépubliant à partir de l’instance d’auteur AEM. Une fois que vous avez dépublié le dossier d’origine, sa copie n’est plus disponible pour les utilisateurs de Brand Portal.

Vous avez la possibilité d’annuler rapidement la publication de dossiers à partir de Brand Portal ou de la planifier pour une date et une heure ultérieures. Pour dépublier des dossiers de ressources de Brand Portal :

1. Depuis l’interface d’AEM Assets de l’instance d’auteur AEM, sélectionnez le dossier que vous souhaitez dépublier.

   ![publish2bp-1](assets/publish2bp.png)

1. Dans la barre d’outils, cliquez sur **Gérer la publication**.

1. **Annuler immédiatement la publication sur Brand Portal**

   Pour annuler rapidement la publication du dossier souhaité dans Brand Portal :

   1. Dans la barre d’outils, sélectionnez **Gérer la publication**.
   1. Dans **Action**, sélectionnez **Dépublier sur Brand Portal**, depuis **Planification** sélectionnez **Maintenant**, puis cliquez sur **Suivant.**
   1. Confirmez votre sélection dans **Portée** et cliquez sur **Dépublier sur Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Dépublication ultérieure sur Brand Portal**

   Pour planifier l’annulation de la publication d’un dossier sur Brand Portal à une date et à une heure ultérieures :

   1. Dans la barre d’outils, sélectionnez **Gérer la publication**.
   1. Dans **Action**, sélectionnez **Dépublier sur Brand Portal** et sélectionnez **Plus tard** dans **Planification**.
   1. Sélectionnez une **Date d’activation** et spécifiez l’heure. Cliquez sur **Suivant**.
   1. Confirmez votre sélection dans **Portée** et cliquez sur **Suivant**.
   1. Spécifiez un **Titre de workflow** sous **Processus**. Cliquez sur **Dépublier ultérieurement**.

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>La procédure de publication/de dépublication vers/depuis Brand Portal est identique à la procédure correspondante pour les dossiers.
