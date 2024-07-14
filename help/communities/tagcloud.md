---
title: Utilisation de Social Tag Cloud
description: Découvrez comment ajouter un composant Nuage de balises sociales à une page qui permet aux membres de la communauté connectés d’identifier rapidement les rubriques de tendance et de localiser le contenu balisé.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 4%

---

# Utilisation de Social Tag Cloud {#using-social-tag-cloud}

## Présentation {#introduction}

Le composant `Social Tag Cloud` met en évidence les balises appliquées par les membres de la communauté lors de la publication de contenu. Il permet d’identifier les sujets de tendance et de permettre aux visiteurs du site de localiser rapidement le contenu balisé.

Pour un autre moyen d’identifier les tendances actuelles, consultez la page [Tendances d’activité](trends.md).

Cette page documente les paramètres de la boîte de dialogue du composant `Social Tag Cloud` et décrit l’expérience utilisateur.

Pour plus d’informations à l’intention des développeurs, voir [Notions fondamentales sur les balises](tag.md).

Voir [Administration des balises](../../help/sites-administering/tags.md) pour plus d’informations sur la création et la gestion des balises et sur la façon de déterminer à quel contenu elles ont été appliquées.

## Ajout d’un nuage de balises sociales {#adding-a-social-tag-cloud}

Pour ajouter un composant `Social Tag Cloud` à une page en mode création, utilisez l’explorateur de composants pour localiser `Communities / Social Tag Cloud` et le faire glisser sur une page où le nuage de balises doit apparaître.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](tag.md#essentials-for-client-side) sont incluses, voici comment le composant `Social Tag Cloud` apparaît :

![social-tag](assets/social-tag.png)

## Configuration du cloud de balises sociales {#configuring-social-tag-cloud}

Sélectionnez le composant `Social Tag Cloud` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Nuage de balises sociales]** , spécifiez les balises à afficher et, si les balises sont des liens actifs, l’emplacement de la page pour les résultats de la recherche :

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Balises sociales à afficher]**
Identifiez les balises UGC à afficher. Les options de la liste déroulante sont les suivantes :

   * `From page and child pages`
   * `All tags`

  La valeur par défaut est `From page and child pages`, où &quot;page&quot; fait référence au paramètre **Page** ci-dessous.

* **[!UICONTROL Page]**

  (Obligatoire si non `All tags)` Chemin d’accès au contenu généré par l’utilisateur pour une page. La valeur par défaut est la page active si rien n’est indiqué.

* **[!UICONTROL Aucun lien sur les balises]**

  Si cette case est cochée, les balises s’affichent dans le nuage de balises sous forme de texte brut. Si cette option n’est pas cochée, les balises s’affichent sous forme de liens actifs qui effectuent une recherche sur tout le contenu auquel cette balise est appliquée. La valeur par défaut n’est pas cochée et requiert la définition du **[!UICONTROL Chemin d’accès aux résultats de recherche]**.

* **[!UICONTROL Chemin du résultat de la recherche]**

  Le chemin d’accès à une page sur laquelle un composant `Search Result` a été placé, configuré pour référencer le contenu généré par l’utilisateur, qui inclut le chemin d’accès spécifié par le paramètre **Page** .

## Modification de l’affichage du Nuage de balises sociales {#change-display-of-social-tag-cloud}

Pour modifier l’affichage de **Social Tag Cloud**, saisissez [Mode de conception](../../help/sites-authoring/default-components-designmode.md) et double-cliquez sur le composant `Social Tag Cloud` inséré pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

À l’aide de l’onglet **[!UICONTROL Nuage de balises sociales (Conception)]**, spécifiez le mode d’affichage des balises. Une balise peut être une balise simple, un seul mot dans l’espace de noms par défaut ou une taxonomie hiérarchique :

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Afficher les chemins complets de titre]**

  Si cette case est cochée, les titres des balises parentes et de l’espace de noms de chaque balise appliquée s’affichent.

  Par exemple :

   * Vérifié : `Geometrixx Media: Gadgets / Cars`
   * Non coché : `Cars`

  Il n’y a aucune différence pour une balise simple.

  La case par défaut est décochée.

* **[!UICONTROL Afficher uniquement les balises terminales]**

  Si cette case est cochée, seules les balises appliquées ne contiennent aucune autre balise.

  Par exemple, étant donné l’ID de balise :

  `Geometrixx Media: Gadgets / Cars`

  Trois balises peuvent être appliquées :

  `Geometrixx Media (the namespace)`, `Gadgets` et `Cars`

   * Cochée : `Cars` uniquement s’affiche, le cas échéant.
   * Non coché : `Geometrixx Media`, `Gadgets` et `Cars` sont affichés, le cas échéant.

  Une balise simple est une balise terminale.

  La case par défaut est décochée.

* **[!UICONTROL Modèle de lien]**

  Modèle, autre qu’un modèle par défaut, utilisé pour afficher les liens dans un nuage de balises, lorsque les liens sont activés par le biais de la boîte de dialogue de modification des composants.

* **[!UICONTROL Même taille pour toutes les balises]**

  Si cette case est cochée, tous les mots du nuage de balises sont stylisés de la même manière. Si cette option n’est pas cochée, le style des mots varie en fonction de leur utilisation. La case par défaut est décochée.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Notions fondamentales sur les balises](tag.md) pour les développeurs.

Pour plus d’informations sur la création et la gestion des balises, voir [Balisage de contenu généré par l’utilisateur](tag-ugc.md) .
