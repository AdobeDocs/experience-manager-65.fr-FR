---
title: Configuration d’une page pour la modification en masse des propriétés de page
seo-title: Configuration d’une page pour la modification en masse des propriétés de page
description: La modification des propriétés de page vous permet de modifier les propriétés de plusieurs pages à la fois
seo-description: La modification des propriétés de page vous permet de modifier les propriétés de plusieurs pages à la fois
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration d’une page pour la modification en masse des propriétés de page {#configuring-your-page-for-bulk-editing-of-page-properties}

La [modification des propriétés de page](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) vous permet de modifier les propriétés de plusieurs pages à la fois.

En raison de la possibilité de valeurs différentes, les propriétés de page ne sont, par défaut, pas activées pour la modification en masse. Elles doivent être explicitement ajoutées à la liste blanche (activé). Lorsque vous définissez les propriétés de page disponibles pour la modification en masse, vous devez prendre en compte certaines répercussions, par exemple :

* Certains champs sont généralement uniques, par exemple un titre de page. Vous devez décider s’il est utile d’activer ces champs pour la modification en masse, lorsqu’une valeur sera appliquée.
* Certains champs peuvent posséder plusieurs valeurs, ce qui nécessite une représentation significative lors du rendu.

   Par exemple, une case à cocher indiquant « Prêt pour publication ». Il peut y avoir plusieurs valeurs avant la modification en bloc (par exemple, prêt, en révision, en cours).

>[!CAUTION]
>
>La modification en masse des propriétés de la page est :
>
>* Indisponible dans l’IU classique.
>* Indisponible pour les pages d’une live copy.
>* Uniquement disponible pour les pages ayant le même type de ressource.
>



>[!NOTE]
>
>La modification en masse est également disponible pour les actifs. Elle est très similaire, mais diffère en quelques points. Pour plus d’informations, voir [Modification des propriétés de plusieurs actifs.](/help/assets/managing-multiple-assets.md) You can customize the fields in the Bulk Metadata editor for Assets using the [Schema editor](/help/assets/metadata-schemas.md).

## Activation d’un champ {#enabling-a-field}

>[!NOTE]
>
>Certains champs peuvent posséder plusieurs valeurs, ce qui nécessite une représentation significative lors du rendu. Pour cette raison, vous devez activer uniquement les types de champs suivants :
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>



Les champs sont activés sur le composant de page (et *non* sur le modèle) :

1. En utilisant CRXDE Lite (ou une méthode équivalente), ouvrez votre composant de page.

   Par exemple: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Cet exemple suppose que les composants de base ont été installés sur l’instance, ce qui est le cas si l’instance est exécutée avec un exemple de contenu We.Retail. Pour plus d’informations, voir la [documentation relative aux composants de base](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html).

1. Navigate to the required field within the `cq:dialog` definition.
1. Définissez la propriété suivante sur le nœud de champ :

   * **Nom**: `allowBulkEdit`
   * **Type**: `Boolean`
   * **Valeur**: `true`
   Par exemple, pour le [composant de base](/help/sites-authoring/default-components-foundation.md) de page standard :

   `/libs/foundation/components/page`

   La propriété serait définie sur :

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >You ***must*** not change anything in the `/libs` path.
   >
   >This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
   >
   >La méthode recommandée pour la configuration et d’autres modifications est la suivante :
   >
   >    1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
   >    1. Make any changes within `/apps`


1. Sélectionnez **Enregistrer tout** pour conserver vos mises à jour.

