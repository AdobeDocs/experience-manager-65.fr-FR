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

Le composant `Social Tag Cloud` met en évidence les balises appliquées par les membres de la communauté lors de la publication de contenu. Il permet d’identifier les tendances et de permettre aux visiteurs de localiser rapidement du contenu balisé.

Pour connaître les autres moyens d’identifier les tendances actuelles, reportez-vous à la section [Tendances d’activité](trends.md).

Cette page documents les paramètres de la boîte de dialogue du composant `Social Tag Cloud` et décrit l&#39;expérience de l&#39;utilisateur.

Pour plus d’informations pour le développeur, reportez-vous à la section [Notions fondamentales sur les balises](tag.md). 

Voir [Administration des balises](../../help/sites-administering/tags.md) pour plus d&#39;informations sur la création et la gestion des balises, ainsi que sur les balises de contenu qui ont été appliquées.

## Ajout d’un composant Nuage de balises sociales {#adding-a-social-tag-cloud}

Pour ajouter un composant `Social Tag Cloud` à une page en mode création, utilisez l’explorateur de composants pour localiser `Communities / Social Tag Cloud` et faites-le glisser sur une page sur laquelle le nuage de balises doit apparaître.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](tag.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Social Tag Cloud` apparaîtra :

![social-tag](assets/social-tag.png)

## Configuration du composant Nuage de balises sociales {#configuring-social-tag-cloud}

Sélectionnez le composant `Social Tag Cloud` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Cloud de balises sociales]**, spécifiez les balises à afficher et, si les balises sont des liens principaux, l’emplacement de la page pour les résultats de la recherche :

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Balises sociales à afficher]** Identifie les balises UGC à afficher. Les options de la liste déroulante sont les suivantes :

   * `From page and child pages`
   * `All tags`

   La valeur par défaut est `From page and child pages`, où &quot;page&quot; fait référence au paramètre **Page** ci-dessous.

* **[!UICONTROL Page]**

   (Obligatoire si non `All tags)` Chemin d’accès à l’UGC pour une page. Par défaut, la page actuelle est laissée vide.

* **[!UICONTROL Aucun lien sur les balises]**

   Si cette case est cochée, les balises s’affichent dans le nuage de balises sous forme de texte brut. Si cette option n’est pas sélectionnée, les balises s’affichent sous forme de liens actifs qui effectuent une recherche sur tout le contenu auquel la balise est appliquée. Par défaut, l’option n’est pas sélectionnée et nécessite que **[!UICONTROL Chemin d’accès aux résultats de recherche]** soit défini.

* **[!UICONTROL Chemin d&#39;accès aux résultats de recherche]**

   Chemin d&#39;accès à une page sur laquelle un composant `Search Result` a été placé, configuré pour référencer l&#39;UGC qui inclut le chemin UGC spécifié par le paramètre **Page**.

## Modification de l’affichage du nuage de balises sociales {#change-display-of-social-tag-cloud}

Pour modifier l’affichage du **nuage de balises sociales**, saisissez [Mode de conception](../../help/sites-authoring/default-components-designmode.md) et cliquez sur le composant `Social Tag Cloud` placé pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

A l’aide de l’onglet **[!UICONTROL Cloud de balises sociales (Conception)]**, spécifiez le mode d’affichage des balises. Une balise peut être une balise simple, un mot unique dans l’espace de nommage par défaut ou une taxonomie hiérarchique :

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

   * Cochée : Seul `Cars` s’affiche, s’il est appliqué.
   * Non coché : `Geometrixx Media` et `Gadgets`ainsi que `Cars` s&#39;affichent, le cas échéant.

   Une balise unique est une balise terminale.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Modèle de lien]**

   Modèle, autre qu’un modèle par défaut, utilisé pour afficher les liens dans un nuage de balises, lorsque les liens sont activés via la boîte de dialogue de modification des composants.

* **[!UICONTROL Taille identique pour toutes les balises]**

   Si cette case est cochée, tous les mots du nuage de balises sont mis dans le même style. Si cette option n’est pas cochée, les mots sont stylisés différemment selon leur utilisation. Cette option n’est pas cochée par défaut.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Tag Essentials](tag.md) destinée aux développeurs.

Voir [Balisage du contenu généré par l’utilisateur](tag-ugc.md) (UGC) pour plus d’informations sur la création et la gestion des balises.
