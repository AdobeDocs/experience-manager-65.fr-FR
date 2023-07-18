---
title: Configurer votre page pour la modification en bloc des propriétés de page
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: La modification en masse des propriétés de page permet de modifier les propriétés de plusieurs pages à la fois.
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 67%

---

# Configurer votre page pour la modification en bloc des propriétés de page {#configuring-your-page-for-bulk-editing-of-page-properties}

[Modification en masse des propriétés de page](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) permet de modifier les propriétés de plusieurs pages à la fois.

En raison de la possibilité de valeurs différentes, les propriétés de page ne sont, par défaut, pas activées pour la modification en masse. Elles doivent être explicitement autorisées (activées). Lors de la définition des propriétés de page à mettre à disposition pour la modification en masse, vous devez tenir compte de certaines implications, telles que :

* Certains champs sont généralement uniques, par exemple un titre de page. Vous devez décider s’il est utile d’activer ces champs pour la modification en masse, lorsqu’une valeur sera appliquée.
* Certains champs peuvent posséder plusieurs valeurs, ce qui nécessite une représentation significative lors du rendu.

  Par exemple, une case à cocher indiquant « Prêt pour publication ». Il peut y avoir plusieurs valeurs avant la modification en masse (par exemple, prête, en cours de révision, en cours).

>[!CAUTION]
>
>La modification en masse des propriétés de page est la suivante :
>
>* Non disponible dans l’IU classique.
>* Non disponible pour les pages d’une Live Copy.
>* Uniquement disponible pour les pages avec le même type de ressource.
>

>[!NOTE]
>
>La modification en masse est également disponible pour les actifs. Elle est très similaire, mais diffère en quelques points. Pour plus d’informations, voir [Modification des propriétés de plusieurs actifs. ](/help/assets/metadata.md) Vous pouvez personnaliser les champs dans l’éditeur de métadonnées en bloc dans Assets à l’aide de l’[éditeur de schéma](/help/assets/metadata-schemas.md).

## Activation d’un champ {#enabling-a-field}

>[!NOTE]
>
>Certains champs peuvent posséder plusieurs valeurs, ce qui nécessite une représentation significative lors du rendu. Pour cette raison, vous devez uniquement activer les types de champ suivants :
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

Les champs sont activés sur le composant de page (*not* sur le modèle) :

1. À l’aide de CRXDE Lite (ou d’une méthode équivalente), ouvrez votre composant de page.

   Par exemple : `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Cet exemple suppose que les composants de base ont été installés sur l’instance, ce qui est le cas si l’instance est exécutée avec un exemple de contenu We.Retail. Voir [Documentation des composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) pour plus d’informations.

1. Accédez au champ requis dans la définition de `cq:dialog`.
1. Définissez la propriété suivante sur le nœud de champ :

   * **Nom** : `allowBulkEdit`
   * **Type** : `Boolean`
   * **Valeur** : `true`

   Par exemple, pour le [composant de base](/help/sites-authoring/default-components-foundation.md) de page standard :

   `/libs/foundation/components/page`

   La propriété serait définie sur :

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Vous ne devez ***rien*** modifier dans le chemin `/libs`.
   >
   >En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
   >
   >La méthode recommandée pour la configuration et d’autres modifications est la suivante :
   >
   >    1. Recréez l’élément requis (tel qu’il existe dans `/libs`) sous `/apps`.
   >    1. Apportez les modifications désirées dans `/apps`.

1. Sélectionnez **Enregistrer tout** pour conserver vos mises à jour.
