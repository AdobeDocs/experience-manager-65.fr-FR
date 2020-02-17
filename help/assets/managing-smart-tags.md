---
title: Gestion des balises dynamiques et des recherches
description: Mettez à jour ou supprimez les balises actives inexactes pour améliorer la pertinence des balises.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gestion des balises dynamiques et des recherches {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

Vous pouvez traiter les balises intelligentes pour supprimer les balises inexactes qui ont pu être attribuées aux images de votre marque afin que seules les balises les plus pertinentes soient affichées.

La modération de balises intelligentes contribue également à affiner les résultats des recherches d’images basées sur des balises, en garantissant que votre image apparaisse dans les résultats de la recherche pour les balises les plus pertinentes. Essentiellement, cela réduit les risques que des images non pertinentes apparaissent dans les résultats de la recherche.

Vous pouvez également affecter un rang supérieur à une balise pour en accroître la pertinence par rapport à une image. La promotion d’une balise pour une image augmente les risques qu’une image apparaisse dans les résultats de la recherche lorsqu’une recherche est basée sur cette balise.

1. Dans l’encadré Omnisearch, recherchez des ressources sur la base d’une balise.
1. Examinez les résultats de la recherche pour identifier une image que vous ne trouvez pas pertinente.
1. Select the image, and then tap **[!UICONTROL Manage Tags]** from the toolbar.
1. Examinez les balises sur la page **[!UICONTROL Gérer les balises]**. If you don&#39;t want the image to be searched based on a specific tag, select the tag and then tap **[!UICONTROL Delete]** from the toolbar. Alternatively, click/tap `X` symbol that appears beside the label.
1. To assign a higher rank to a tag, select the tag and tap **[!UICONTROL Promote]** from the toolbar. La balise faisant l’objet d’une conversion est déplacée dans la section **[!UICONTROL Balises]**.
1. Click/tap **[!UICONTROL Save]**, and then click/tap **[!UICONTROL OK]** to close the Success dialog.
1. Accédez à la page Propriétés de l’image. Remarquez que la balise que vous avez convertie se voit attribuer une pertinence élevée et apparaît donc plus haut dans les résultats de la recherche.

## Comprendre les résultats de recherche AEM avec des balises dynamiques {#understandsearch}

By default, AEM search combines the search terms with an `AND` clause. L’utilisation de balises dynamiques ne modifie pas ce comportement par défaut. Using smart tags adds an additional `OR` clause to find any of the search terms in the applies smart tags. For example, consider searching for `woman running`. Assets with just `woman` or just `running` keyword in the metadata do not appear in the search results by default. However, an asset tagged with either `woman` or `running` using smart tags appears in such a search query. Les résultats de la recherche sont donc une combinaison de

* assets with `woman` and `running` keywords in the metadata.

* ressources avec balise dynamique avec l’un des mots-clés.

Les résultats de recherche qui correspondent à tous les termes de recherche dans les champs de métadonnées s’affichent en premier, suivis des résultats de recherche correspondant à l’un des termes de recherche des balises dynamiques. Dans l’exemple ci-dessus, l’ordre approximatif de l’affichage des résultats de recherche est le suivant :

1. matches of `woman running` in the various metadata fields.
1. correspondances de `woman running` dans les balises actives.
1. matches of `woman` or of `running` in smart tags.
