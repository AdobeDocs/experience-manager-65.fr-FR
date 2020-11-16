---
title: Nuage de balises sociales
seo-title: Nuage de balises sociales
description: Ajouter un composant Social Tag Cloud à une page
seo-description: Ajouter un composant Social Tag Cloud à une page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 30%

---


# Nuage de balises sociales {#using-social-tag-cloud}

## Présentation {#introduction}

The `Social Tag Cloud` component highlights tags applied by community members when posting content. Il permet d’identifier les tendances et de permettre aux visiteurs de localiser rapidement du contenu balisé.

Pour connaître les autres moyens d’identifier les tendances actuelles, reportez-vous à la section [Tendances d’activité](trends.md).

This page documents the `Social Tag Cloud` component dialog settings and describes the user experience.

Pour plus d’informations pour le développeur, reportez-vous à la section [Notions fondamentales sur les balises](tag.md). 

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Ajout d’un composant Nuage de balises sociales {#adding-a-social-tag-cloud}

Pour ajouter un `Social Tag Cloud` composant à une page en mode création, utilisez l’explorateur de composants pour le localiser `Communities / Social Tag Cloud` et faites-le glisser sur une page sur laquelle le nuage de balises doit apparaître.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](tag.md#essentials-for-client-side) are included, this is how the `Social Tag Cloud` component will appear:

![social-tag](assets/social-tag.png)

## Configuration du composant Nuage de balises sociales {#configuring-social-tag-cloud}

Select the placed `Social Tag Cloud` component to access and select the `Configure` icon which opens the edit dialog.

![configurer](assets/configure-new.png)

Under the **[!UICONTROL Social Tag Cloud]** tab, specify which tags to display and, if the tags are active links, the location of the page for search results:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Balises sociales à afficher]** Identifie les balises UGC à afficher. Les options de la liste déroulante sont les suivantes :

   * `From page and child pages`
   * `All tags`

   La valeur par défaut est `From page and child pages`, où &quot;page&quot; fait référence au paramètre **Page** ci-dessous.

* **[!UICONTROL Page]**

   (Required if not `All tags)` The path to the UGC for a page. Par défaut, la page actuelle est laissée vide.

* **[!UICONTROL Aucun lien sur les balises]**

   Si cette case est cochée, les balises s’affichent dans le nuage de balises sous forme de texte brut. Si cette option n’est pas sélectionnée, les balises s’affichent sous forme de liens actifs qui effectuent une recherche sur tout le contenu auquel la balise est appliquée. Par défaut, l’option n’est pas sélectionnée et nécessite que **[!UICONTROL Chemin d’accès aux résultats de recherche]** soit défini.

* **[!UICONTROL Chemin d&#39;accès aux résultats de recherche]**

   The path to a page on which a `Search Result` component has been placed, configured to reference UGC which includes the UGC path specified by the **Page** setting.

## Modification de l’affichage du nuage de balises sociales {#change-display-of-social-tag-cloud}

To edit the display of the **Social Tag Cloud**, enter [Design Mode](../../help/sites-authoring/default-components-designmode.md) and double click on the placed `Social Tag Cloud` component to open a dialog with an additional tab.

Using the **[!UICONTROL Social Tag Cloud (Design)]** tab, specify how tags are displayed. Une balise peut être une balise simple, un mot unique dans l’espace de nommage par défaut ou une taxonomie hiérarchique :

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Afficher les chemins des titres entiers]**

   Si cette case est cochée, affiche les titres des balises parentes et l’espace de nommage de chaque balise appliquée.

   Par exemple :

   * Cochée: `Geometrixx Media: Gadgets / Cars`
   * Non cochée: `Cars`

   Il n’y a aucune différence pour une balise unique.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Afficher uniquement les balises terminales]**

   Si cette case est cochée, affiche uniquement les balises appliquées qui ne contiennent aucune autre balise.

   Par exemple, à partir de l’ID de balise de :

   `Geometrixx Media: Gadgets / Cars`

   Trois balises peuvent être appliquées :

   `Geometrixx Media (the namespace)`, `Gadgets`, et `Cars`

   * Checked: Only `Cars` will display, if applied.
   * Unchecked: `Geometrixx Media` and `Gadgets`as well as `Cars` will display, if applied.

   Une balise unique est une balise terminale.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Modèle de lien]**

   Modèle, autre qu’un modèle par défaut, utilisé pour afficher les liens dans un nuage de balises, lorsque les liens sont activés via la boîte de dialogue de modification des composants.

* **[!UICONTROL Taille identique pour toutes les balises]**

   Si cette case est cochée, tous les mots du nuage de balises sont mis dans le même style. Si cette option n’est pas cochée, les mots sont stylisés différemment selon leur utilisation. Cette option n’est pas cochée par défaut.

## Informations supplémentaires {#additional-information}

More information may be found on the [Tag Essentials](tag.md) page for developers.

See [Tagging User Generated Content](tag-ugc.md) (UGC) for information about creating and managing tags.
