---
title: Nuage de balises sociales
seo-title: Using Social Tag Cloud
description: Ajout d’un composant Nuage de balises sociales à une page
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 31%

---

# Nuage de balises sociales {#using-social-tag-cloud}

## Présentation  {#introduction}

Le `Social Tag Cloud` Le composant met en surbrillance les balises appliquées par les membres de la communauté lors de la publication de contenu. Il permet d’identifier les tendances et de permettre aux visiteurs de localiser rapidement du contenu balisé.

Pour connaître les autres moyens d’identifier les tendances actuelles, reportez-vous à la section [Tendances d’activité](trends.md).

Cette page documente les `Social Tag Cloud` paramètres de la boîte de dialogue du composant et décrit l’expérience utilisateur.

Pour plus d’informations pour le développeur, reportez-vous à la section [Notions fondamentales sur les balises](tag.md). 

Voir [Administration des balises](../../help/sites-administering/tags.md) pour plus d’informations sur la création et la gestion des balises, ainsi que sur les balises de contenu qui ont été appliquées.

## Ajout d’un composant Nuage de balises sociales {#adding-a-social-tag-cloud}

Pour ajouter une `Social Tag Cloud` sur une page en mode création, utilisez l’explorateur de composants pour accéder à `Communities / Social Tag Cloud` et faites-le glisser sur la page où le nuage de balises doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](tag.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Social Tag Cloud` apparaît :

![social-tag](assets/social-tag.png)

## Configuration du composant Nuage de balises sociales {#configuring-social-tag-cloud}

Sélectionnez le `Social Tag Cloud` pour accéder au composant et le sélectionner. `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous , **[!UICONTROL Nuage de balises sociales]** , spécifiez les balises à afficher et, si les balises sont des liens principaux, l’emplacement de la page pour les résultats de la recherche :

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Balises sociales à afficher]** Identifie les balises UGC à afficher. Les options de la liste déroulante sont les suivantes :

   * `From page and child pages`
   * `All tags`

   La valeur par défaut est `From page and child pages`, où &quot;page&quot; fait référence à la variable **Page** ci-dessous.

* **[!UICONTROL Page]**

   (Obligatoire si non `All tags)` Chemin d’accès au contenu généré par l’utilisateur pour une page. Par défaut, la page actuelle est laissée vide.

* **[!UICONTROL Aucun lien sur les balises]**

   Si cette case est cochée, les balises s’affichent dans le nuage de balises sous forme de texte brut. Si cette option n’est pas sélectionnée, les balises s’affichent sous forme de liens actifs qui effectuent une recherche sur tout le contenu auquel la balise est appliquée. Par défaut, l’option n’est pas sélectionnée et nécessite que **[!UICONTROL Chemin d’accès aux résultats de recherche]** soit défini.

* **[!UICONTROL Chemin d&#39;accès aux résultats de recherche]**

   Chemin d’accès à une page sur laquelle un `Search Result` Le composant a été placé, configuré pour référencer le contenu généré par l’utilisateur qui inclut le chemin d’accès créé par l’utilisateur spécifié par la variable **Page** .

## Modification de l’affichage du nuage de balises sociales {#change-display-of-social-tag-cloud}

Pour modifier l’affichage de la variable **Nuage de balises sociales**, saisissez [Mode de conception](../../help/sites-authoring/default-components-designmode.md) et double-cliquez sur le `Social Tag Cloud` pour ouvrir une boîte de dialogue avec un onglet supplémentaire.

En utilisant la variable **[!UICONTROL Nuage de balises sociales (conception)]** , indiquez le mode d’affichage des balises. Une balise peut être une balise simple, un seul mot dans l’espace de noms par défaut ou une taxonomie hiérarchique :

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Afficher les chemins des titres entiers]**

   Si cette case est cochée, les titres des balises parentes et de l’espace de noms de chaque balise appliquée s’affichent.

   Par exemple :

   * Cochée: `Geometrixx Media: Gadgets / Cars`
   * Non cochée: `Cars`

   Il n’y a aucune différence pour une balise unique.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Afficher uniquement les balises terminales]**

   Si cette case est cochée, seules les balises appliquées ne contiennent aucune autre balise.

   Par exemple, étant donné l’ID de balise :

   `Geometrixx Media: Gadgets / Cars`

   Trois balises peuvent être appliquées :

   `Geometrixx Media (the namespace)`, `Gadgets`, et `Cars`

   * Cochée : Uniquement `Cars` s’affiche, le cas échéant.
   * Non coché : `Geometrixx Media` et `Gadgets`ainsi que `Cars` s’affiche, le cas échéant.

   Une balise unique est une balise terminale.

   Cette option n’est pas cochée par défaut.

* **[!UICONTROL Modèle de lien]**

   Modèle, autre qu’un modèle par défaut, utilisé pour afficher les liens dans un nuage de balises, lorsque les liens sont activés par le biais de la boîte de dialogue de modification des composants.

* **[!UICONTROL Taille identique pour toutes les balises]**

   Si cette case est cochée, tous les mots du nuage de balises sont stylisés de la même manière. Si cette option n’est pas cochée, les mots sont stylisés différemment selon leur utilisation. Cette option n’est pas cochée par défaut.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur les balises](tag.md) pour les développeurs.

Voir [Balisage du contenu généré par l’utilisateur](tag-ugc.md) (contenu généré par l’utilisateur) pour plus d’informations sur la création et la gestion des balises.
