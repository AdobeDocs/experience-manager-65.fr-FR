---
title: Console Balisage de l’interface utilisateur (IU) classique
seo-title: Console Balisage de l’interface utilisateur (IU) classique
description: Découvrez la console Balisage de l’interface utilisateur classique.
seo-description: Découvrez la console Balisage de l’interface utilisateur classique.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 69%

---


# Console Balisage de l’interface utilisateur (IU) classique{#classic-ui-tagging-console}

Cette section est réservée à la console Balisage de l’interface utilisateur classique.

La console Balisage de l’interface utilisateur optimisée pour les écrans tactiles se trouve [ici](/help/sites-administering/tags.md#tagging-console).

Pour accéder à la console Balisage de l’interface utilisateur classique :

* en mode de création
* Connectez-vous avec des droits d’administrateur.
* accéder à la console
par exemple, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Créations de balises et d’espaces de noms {#creating-tags-and-namespaces}

1. En fonction du niveau de départ, vous pouvez créer une balise ou un espace de noms à l’aide de l’option **Nouveau** :

   Si vous sélectionnez **Balises**, vous pouvez créer un espace de noms :

   ![](assets/creating_tags_andnamespaces.png)

   Si vous sélectionnez un espace de noms (**Demo**, par exemple), vous pouvez y créer une balise :

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. Dans les deux cas, saisissez

   * **Titre**
(
*Obligatoire*) Titre d’affichage de la balise. Même s’il est possible d’utiliser n’importe quel caractère, il est recommandé de ne pas utiliser ces caractères spéciaux :

      * `colon (:)` - Délimiteur d&#39;espace de nommage
      * `forward slash (/)` - délimiteur de sous-balises

      Si vous saisissez ces caractères, ils ne s’affichent pas.

   * **Nom**
(
*Obligatoire*) Nom du noeud pour la balise .

   * **Description**
(
*facultatif*) Description de la balise.

   * Sélectionnez **Créer**.


## Modification de balises {#editing-tags}

1. Dans le volet de droite, sélectionnez la balise à modifier.
1. Cliquez sur **Modifier**.
1. Vous pouvez modifier le **Titre** et la **Description**.
1. Cliquez sur **Enregistrer** pour fermer la boîte de dialogue.

## Suppression des balises {#deleting-tags}

1. Dans le volet de droite, sélectionnez la balise à supprimer.
1. Cliquez sur **Supprimer**.
1. Cliquez sur **Oui** pour fermer la boîte de dialogue.

   La balise ne doit plus être répertoriée.

## Activation et désactivation de balises {#activating-and-deactivating-tags}

1. Dans le volet de droite, sélectionnez l’espace de noms ou la balise à activer (publication) ou à désactiver (annulation de la publication).
1. Cliquez sur **Activer** ou **Désactiver**, suivant les besoins.

## Liste : indiquant où les balises sont référencées  {#list-showing-where-tags-are-referenced}

L’option **Liste** ouvre une nouvelle fenêtre qui présente les chemins d’accès de toutes les pages utilisant la balise mise en surbrillance :

![](assets/list_showing_wheretagsarereferenced.png)

## Déplacement des balises  {#moving-tags}

Pour aider les administrateurs et les développeurs de balises à nettoyer la taxonomie ou à renommer un ID de balise, il est possible de déplacer une balise vers un nouvel emplacement :

1. Ouvrez la console **Tagging**.
1. Sélectionnez le tag et cliquez sur **Déplacer...** dans la barre d’outils supérieure (ou dans le menu contextuel).
1. Dans la boîte de dialogue **Déplacer le tag**, définissez :

   * **vers**, le nœud de destination.
   * **Renommer en**, le nouveau nom du nœud.

1. Cliquez sur **Déplacer**.

La boîte de dialogue **Déplacer le tag** se présente comme suit :

![](assets/move_tag.png)

>[!NOTE]
>
>Les créateurs ne doivent pas déplacer les balises ou renommer l’ID de balise. Si nécessaire, les auteurs doivent uniquement [modifier les titres des balises](#editing-tags).

## Fusion des balises {#merging-tags}

Il est également possible de recourir à la fusion de balises lorsqu’une taxonomie comporte des doublons. Lorsque la balise A est fusionnée dans la balise B, toutes les pages balisées avec la balise A sont balisées avec la balise B, et la balise A n’est plus disponible pour les auteurs.

Pour fusionner un tag dans un autre :

1. Ouvrez la console **Tagging**.
1. Sélectionnez le tag et cliquez sur **Fusionner...** dans la barre d’outils supérieure (ou dans le menu contextuel).
1. Dans la boîte de dialogue **Fusionner le tag**, définissez :

   * **en**, le nœud de destination.

1. Cliquez sur **Fusionner**.

La boîte de dialogue **Fusionner la balise** se présente comme suit :

![](assets/mergetag.png)

## Compte d’utilisation des balises {#counting-usage-of-tags}

Pour afficher le nombre d’utilisations d’un tag :

1. Ouvrez la console **Tagging**.
1. Cliquez sur **Compteur d’utilisations** dans la barre d’outils supérieure : la colonne Décompte affiche le résultat.

## Gestion de tags dans diverses langues  {#managing-tags-in-different-languages}

La propriété facultative `title`   d’une balise peut être traduite en plusieurs langues. La balise `titles` peut ensuite être affichée en fonction de la langue de l’utilisateur ou de la langue de la page.

### Définition de titres de balises dans plusieurs langues {#defining-tag-titles-in-multiple-languages}

La procédure suivante montre comment traduire la balise `title`Animals **en anglais, allemand et français :**

1. Accédez à la console **Balisage**.
1. Modifiez la balise **Animaux** ci-dessous **Balises** > **Images photographiques**.
1. Ajoutez les traductions dans les langues suivantes :

   * **Anglais** : Animals
   * **Allemand** : Tiere
   * **Français** : Animaux

1. Enregistrez les modifications.

La boîte de dialogue se présente comme suit :

![](assets/edit_tag.png)

La console Balisage utilise la langue du créateur, dès lors, pour la balise « Animals », « Animaux » s’affiche si l’utilisateur définit la langue sur Français dans les propriétés de l’utilisateur.

Pour ajouter une nouvelle langue à la boîte de dialogue, reportez-vous à la section [Ajout d’une langue à la boîte de dialogue Modifier la balise](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) dans la section **Balisage pour les développeurs**.

### Affichage des titres des balises dans les propriétés de page dans une langue spécifiée {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Par défaut, la balise `titles`dans les propriétés de la page s’affiche dans la langue de la page. La boîte de dialogue des balises dans les propriétés de la page comporte un champ de langue qui permet l’affichage de la balise `titles`dans une autre langue. La procédure suivante décrit comment afficher la balise `titles`en français :

1. Reportez-vous à la section précédente pour ajouter la traduction française aux **Animaux** ci-dessous **Balises** > **Images photographiques**.
1. Ouvrez les propriétés de la page **Produits** dans la branche English (Anglais) du site **Geometrixx**.
1. Ouvrez la boîte de dialogue **Balises/Mots-clés** (en sélectionnant le menu déroulant à droite de la zone d&#39;affichage Balises/Mots-clés) et sélectionnez la langue **française** dans le menu déroulant dans le coin inférieur droit.
1. Faites défiler la page à l’aide des flèches gauche et droite jusqu’à ce que vous puissiez sélectionner l’onglet **Images photographiques**.

   Sélectionnez la balise **Animaux** (**Animaux**) et sélectionnez-la en dehors de la boîte de dialogue pour la fermer et ajouter la balise aux propriétés de la page.

   ![](assets/french_tag.png)

Par défaut, la boîte de dialogue Propriétés de la page affiche la balise `titles`selon la langue de la page.

En général, la langue de la balise est celle de la page si elle est disponible. Si le widget [`tag` est utilisé dans d’autres cas (dans des formulaires ou des boîtes de dialogue, par exemple), la langue du tag dépend du contexte.](/help/sites-developing/building.md#tagging-on-the-client-side)

>[!NOTE]
>
>Le nuage de balises et les mots-clés de métadonnées dans le composant de page standard utilisent la balise localisée `titles`en fonction de la langue de page, le cas échéant.