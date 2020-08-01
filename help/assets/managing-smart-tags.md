---
title: Gestion des balises intelligentes et des recherches
description: Mettez à jour ou supprimez les balises actives inexactes afin d’améliorer la pertinence des balises.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 75%

---


# Gestion des balises intelligentes et des recherches {#manage-smart-tags-and-searches}

<!--
TBD: This article should be merged into a new, uber article for Smart Tags. Delete this article then. Cloud service article is merged.
-->

Vous pouvez traiter les balises actives pour supprimer les balises inexactes qui ont pu être attribuées à vos images de marque afin que seules les balises les plus pertinentes s’affichent.

La modération de balises intelligentes contribue également à affiner les résultats des recherches d’images basées sur des balises, en garantissant que votre image apparaisse dans les résultats de la recherche pour les balises les plus pertinentes. Essentiellement, cela réduit les risques que des images non pertinentes apparaissent dans les résultats de la recherche.

Vous pouvez également attribuer un rang supérieur à une balise afin d’accroître son degré de pertinence par rapport à une image. La promotion d’une balise pour une image augmente les risques qu’une image apparaisse dans les résultats de la recherche lorsqu’une recherche est basée sur cette balise.

1. Dans l’encadré Omnisearch, recherchez des ressources sur la base d’une balise.
1. Examinez les résultats de la recherche pour identifier une image que vous ne trouvez pas pertinente.
1. Select the image, and click **[!UICONTROL Manage Tags]** from the toolbar.
1. Examinez les balises sur la page **[!UICONTROL Gérer les balises]**. If you don&#39;t want the image to be searched based on a specific tag, select the tag and then click **[!UICONTROL Delete]** from the toolbar. Sinon, cliquez sur le symbole `X` qui apparaît en face du libellé.
1. To assign a higher rank to a tag, select the tag and click **[!UICONTROL Promote]** from the toolbar. La balise objet d’une conversion est déplacée dans la section **[!UICONTROL Balises]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL OK]** pour fermer la boîte de dialogue de réussite.
1. Accédez à la page Propriétés de l’image. Remarquez que la balise que vous avez convertie se voit attribuer une pertinence élevée et apparaît donc plus haut dans les résultats de la recherche.

## Understand [!DNL Experience Manager] search results with smart tags {#understandsearch}

By default, [!DNL Experience Manager] search combines the search terms with an `AND` clause. L’utilisation de balises intelligentes ne modifie pas ce comportement par défaut. Elle ajoute une clause `OR` supplémentaire pour trouver l’un des termes de recherche dans les balises intelligentes. Par exemple, pour la recherche de `woman running`. Les ressources avec les mots-clés `woman` ou `running` uniquement dans les métadonnées n’apparaissent pas dans les résultats de recherche par défaut. Toutefois, une ressource balisée avec `woman` ou `running` à l’aide de balises intelligentes apparaît dans une telle requête de recherche. Les résultats de la recherche sont donc une combinaison de

* ressources avec les mots-clés `woman` et `running` dans les métadonnées.

* ressources avec balise dynamique avec l’un des mots-clés.

Les résultats de recherche qui correspondent à tous les termes de recherche dans les champs de métadonnées s’affichent en premier, suivis des résultats de recherche correspondant à l’un des termes de recherche des balises dynamiques. Dans l’exemple ci-dessus, l’ordre approximatif de l’affichage des résultats de recherche est le suivant :

1. correspondances de `woman running` dans les différents champs de métadonnées.
1. correspondances de `woman running` dans les balises intelligentes.
1. correspondances de `woman` ou de `running` dans des balises intelligentes.
