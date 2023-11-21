---
title: Éditeur de texte enrichi
description: L’éditeur de texte enrichi est un bloc de création de base permettant de saisir du contenu texte dans AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 88%

---

# Éditeur de texte enrichi {#rich-text-editor}

L’éditeur de texte enrichi est un bloc de création de base permettant de saisir du contenu texte dans AEM. Il constitue la base de divers composants, notamment :

* Texte
* Image du texte
* Tableau

## Éditeur de texte enrichi {#rich-text-editor-1}

La boîte de dialogue de modification WYSIWYG offre un large éventail de fonctionnalités :

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>Les fonctions disponibles peuvent être configurées pour chaque projet ; elles peuvent donc varier pour votre installation.

## Édition statique {#in-place-editing}

Outre le mode de modification de texte enrichi basé sur la boîte de dialogue, AEM propose un mode de modification intégré qui permet la modification directe du texte tel qu’il est affiché dans la disposition de la page.

Cliquez deux fois sur un paragraphe (double-clic lent) pour passer en mode de modification intégré (la bordure du composant devient orange).

Vous pourrez modifier directement le texte sur la page, plutôt que dans une boîte de dialogue. Il vous suffit d’apporter vos modifications qui seront automatiquement enregistrées.

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>Si l’outil de recherche de contenu est ouvert, une barre d’outils avec les options de mise en forme de l’éditeur de texte enrichi s’affiche en haut de l’onglet (comme ci-dessus).
>
>Si l’outil de recherche de contenu n’est pas ouvert, la barre d’outils ne s’affiche pas.

Actuellement, le mode de modification intégré est activé pour les éléments de page générés par les composants **Texte** et **Titre**.

>[!NOTE]
>
>Le composant [!UICONTROL Titre] est conçu pour contenir un texte court sans sauts de ligne. Lorsque vous modifiez un titre en mode d’édition statique, la saisie d’un saut de ligne ouvre une nouvelle **Texte** sous le titre.

## Fonctionnalités de l’éditeur de texte enrichi {#features-of-the-rich-text-editor}

L’éditeur de texte enrichi fournit diverses fonctions, [selon la configuration](/help/sites-administering/rich-text-editor.md) du composant. Ces fonctions sont disponibles dans les deux interfaces utilisateur (classique et optimisée pour les écrans tactiles).

### Formats de caractères de base {#basic-character-formats}

![Barre d’outils Format de caractère](do-not-localize/cq55_rte_basicchars.png)

Vous pouvez y appliquer une mise en forme aux caractères que vous avez sélectionnés (mis en surbrillance). Certaines options comportent également des raccourcis clavier :

* Gras (Ctrl+B)
* Italique (Ctrl+I)
* Souligné (Ctrl-U)
* Indice
* Exposant

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

Tous fonctionnent comme un bouton bascule. La résélection supprime donc le format.

### Styles et formats prédéfinis {#predefined-styles-and-formats}

![cq55_rte_stylesparagraph](assets/cq55_rte_stylesparagraph.png)

Votre installation peut inclure des styles et des formats prédéfinis. Ils sont disponibles avec la fonction **[!UICONTROL Style]** et **[!UICONTROL Format]** liste déroulante et peut être appliqué au texte que vous avez sélectionné.

Un style peut être appliqué à une chaîne spécifique (un style correspond à CSS) :

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

Tandis qu’une disposition est appliquée à l’intégralité d’un paragraphe texte (une mise en forme est basée sur le langage HTML) :

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

Seul un format spécifique peut être modifié (la valeur par défaut est **[!UICONTROL Paragraphe]**).

Un style peut être supprimé. Placez le curseur dans le texte auquel le style a été appliqué, puis cliquez sur l’icône Supprimer :

>[!CAUTION]
>
>Ne sélectionnez pas à nouveau le texte auquel le style a été appliqué ou l’icône sera désactivée.

### Couper, Copier, Coller {#cut-copy-paste}

![Barre d’outils Couper, Copier, Coller](do-not-localize/cq55_rte_cutcopypaste.png)

Les fonctionnalités standard **[!UICONTROL Couper]** et **[!UICONTROL Copier]** sont disponibles. Plusieurs versions de **[!UICONTROL Coller]** sont fournies pour prendre en charge différents formats.

* Couper (Ctrl-X)
* Copier (Ctrl-C)
* Coller
Mécanisme de collage par défaut (Ctrl-V) pour le composant ; dans le cas d’une installation standard, il est configuré sur [!UICONTROL Coller à partir de Word].

* Coller en tant que texte : supprime tous les styles et options de mise en forme afin de ne coller que le texte brut.

* Coller à partir de Word : cette option colle le contenu au format HTML (avec la remise en forme nécessaire).

### Annuler, rétablir {#undo-redo}

![Annuler, rétablir la barre d’outils](do-not-localize/cq55_rte_undoredo.png)

AEM conserve un enregistrement de vos 50 dernières actions dans le composant actuel, dans l’ordre chronologique. Au besoin, ces actions peuvent être annulées (puis rétablies) dans un ordre strict.

>[!CAUTION]
>
>L’historique n’est conservé que pour la session de modification actuelle. Il est redémarré chaque fois que vous ouvrez le composant en vue de le modifier.

>[!NOTE]
>
>Le nombre de tâches par défaut est de cinquante. Cela peut être différent pour votre installation.

### Alignement {#alignment}

![Barre d’outils d’alignement](do-not-localize/cq55_rte_alignment.png)

Votre texte peut être aligné à gauche, au centre ou à droite.

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### Indentation {#indentation}

![Barre d’outils de mise en retrait](do-not-localize/cq55_rte_indent.png)

La mise en retrait d’un paragraphe peut être augmentée ou réduite. Le paragraphe sélectionné est mis en retrait, tout nouveau texte saisi conserve le niveau de mise en retrait actuel.

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### Listes {#lists}

![Barre d’outils des listes](do-not-localize/cq55_rte_lists.png)

Vous pouvez créer des listes à puces et numérotées dans votre texte. Sélectionnez le type de liste et commencez à saisir ou mettez en surbrillance le texte à convertir. Dans les deux cas, un changement de ligne lance un nouvel élément de liste.

Vous pouvez créer des listes imbriquées en mettant en retrait un ou plusieurs éléments de liste.

Vous pouvez modifier le style d’une liste en positionnant simplement le curseur dans la liste, puis en sélectionnant l’autre style. Une sous-liste peut également avoir un style différent de la liste de contenu. Vous pouvez l’appliquer une fois la sous-liste créée (par mise en retrait).

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### Liens {#links}

![Barre d’outils de liens](do-not-localize/cq55_rte_links.png)

Un lien vers une URL (que ce soit dans votre site web ou un emplacement externe) est généré en mettant en surbrillance le texte requis, puis en cliquant sur l’icône de lien hypertexte :

![Icône Lien hypertexte](do-not-localize/chlimage_1-9.png)

Une boîte de dialogue vous permet de spécifier l’URL cible, mais aussi de spécifier si elle doit être ouverte dans une nouvelle fenêtre.

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

Vous pouvez :

* saisir directement une URI ;
* utiliser un plan de site (sitemap) pour sélectionner une page de votre site Web ;
* Saisissez l’URI, puis ajoutez l’ancre cible ; par exemple, `www.TargetUri.org#AnchorName`
* saisir une ancre seule (pour faire référence à la « page en cours »), `#anchor`#, par exemple ;
* rechercher une page dans l’outil de recherche de contenu, puis faire glisser son icône dans la boîte de dialogue Lien hypertexte.

>[!NOTE]
>
>Vous pouvez faire précéder l’URI de l’un des protocoles configurés pour votre installation. Dans une installation standard, ces protocoles sont `https://`, `ftp://` et `mailto:`. Les protocoles non configurés pour votre installation seront rejetés et marqués comme non valides.

Pour rompre le lien, placez le curseur n’importe où dans le texte du lien et cliquez sur l’icône [!UICONTROL Dissocier] :

![Icône Dissocier](do-not-localize/chlimage_1-10.png)

### Ancres {#anchors}

![Barre d’outils des ancres](do-not-localize/cq55_rte_anchor.png)

Vous pouvez créer une ancre n’importe où dans le texte en positionnant le curseur ou en sélectionnant du texte. Cliquez ensuite sur l’icône **Ancre** pour ouvrir la boîte de dialogue.

Saisissez le nom de l’ancre, puis cliquez sur **OK** pour enregistrer.

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

L’ancre s’affiche lorsque le composant est en cours d’édition ; elle peut désormais être utilisée dans une cible pour les liens.

![chlimage_1-104](assets/chlimage_1-104.png)

### Rechercher et remplacer {#find-and-replace}

![Barre d’outils Rechercher et remplacer](do-not-localize/cq55_rte_findreplace.png)

AEM fournit à la fois une fonction **Rechercher** et **Remplacer** (rechercher et remplacer).

Les deux ont un bouton **Rechercher suivant** pour rechercher le texte spécifié dans le composant ouvert. Vous pouvez également indiquer si la casse (majuscule/minuscule) doit être mise en correspondance.

La recherche commence toujours à partir de la position actuelle du curseur dans le texte. Lorsque la fin du composant est atteinte, un message vous informe que la prochaine opération de recherche démarre à partir du haut.

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

La variable **Remplacer** permet de **Rechercher**, puis **Remplacer** une instance individuelle avec le texte spécifié, ou **Remplacer tout** dans le composant actif.

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### Images {#images}

Vous pouvez faire glisser des images à partir de l’outil de recherche de contenu pour les ajouter au texte.

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM propose également des composants spécialisés permettant une configuration d’image plus détaillée ; Par exemple, la variable **Image** et **Image texte** sont disponibles.

### Vérificateur orthographique {#spelling-checker}

![Vérificateur orthographique](do-not-localize/cq55_rte_spellchecker.png)

Le vérificateur orthographique vérifie l’intégralité du texte dans le composant actif.

Toute faute d’orthographe est mise en surbrillance :

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>Le correcteur orthographique fonctionne dans la langue du site Web soit en prenant la propriété de langue de la sous-arborescence, soit en extrayant la langue de l’URL ;  Par exemple, la variable `en` la branche est vérifiée pour l’anglais et la variable `de` branche pour l’allemand.

### Tableaux {#tables}

Les tableaux sont disponibles dans les deux cas :

* Comme composant **Tableau**

  ![Composant Tableau](assets/chlimage_1-105.png)

* À l’intérieur du composant **Texte**

  ![Barre d’outils Texte](do-not-localize/chlimage_1-11.png)

  >[!NOTE]
  >
  >Bien que les tableaux soient disponibles dans l’éditeur de texte enrichi, il est conseillé d’utiliser le composant **Tableau** lors de leur création.

Dans les composants **Texte** et **Tableau**, la fonctionnalité de tableau est accessible par le biais du menu contextuel (qui s’ouvre généralement à l’aide du bouton droit de la souris) ; par exemple :

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>Dans le composant **Tableau**, une barre d’outils spécialisée est également disponible comprenant diverses fonctions standards d’éditeur de texte enrichi, ainsi qu’un sous-ensemble de fonctions spécifiques au tableau.

Les fonctions spécifiques au tableau sont les suivantes :

* [Propriétés du tableau](#table-properties)
* [Propriétés de la cellule](#cell-properties)
* [Ajouter ou Supprimer des lignes](#add-or-delete-rows)
* [Ajouter ou Supprimer des colonnes](#add-or-delete-columns)
* [Sélectionner des lignes ou colonnes entières](#selecting-entire-rows-or-columns)
* [Fusionner des cellules](#merge-cells)
* [Diviser des cellules](#split-cells)
* [Tableaux imbriqués](#creating-nested-tables)
* [Supprimer le tableau](#remove-table)

#### Propriétés du tableau {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

Les propriétés de base du tableau peuvent être configurées avant de cliquer sur **OK** pour l’enregistrement :

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **Largeur** : largeur totale du tableau.

* **Hauteur** : hauteur totale du tableau.

* **Bordure** : taille de la bordure du tableau.

* **Marge intérieure des cellules** : définit l’espace blanc entre le contenu de la cellule et ses bordures.

* **Espacement des cellules** : définit la distance entre les cellules.

>[!NOTE]
>
>Certaines propriétés de cellule, telles que Largeur et Hauteur, peuvent être définies en pixels ou en pourcentages.

>[!CAUTION]
>
>Adobe vous recommande de définir une Largeur pour votre tableau.

#### Propriétés de la cellule {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

Les propriétés d’une cellule spécifique ou d’une série de cellules peuvent être configurées :

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **Largeur**
* **Hauteur**
* **Alignement horizontal** - Gauche, Centre ou Droite
* **Alignement vertical** - Haut, Milieu, Bas ou Ligne de base
* **Type de cellule** - Données ou En-tête
* **Appliquer à :** une seule cellule, rangée entière, colonne entière

#### Ajouter ou Supprimer des lignes {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

Vous pouvez ajouter des lignes au-dessus ou au-dessous de la ligne active.

Vous pouvez également supprimer la ligne active.

#### Ajouter ou supprimer des colonnes {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

Vous pouvez ajouter des colonnes à gauche ou à droite de la colonne active.

Vous pouvez également supprimer la colonne active.

#### Sélectionner des lignes ou colonnes entières {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

Sélectionne toute la ligne ou la colonne active. Des actions spécifiques (par exemple, fusion) sont alors disponibles.

#### Fusionner des cellules {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* Si vous avez sélectionné un groupe de cellules, vous pouvez les fusionner en une seule.
* Si vous avez sélectionné une seule cellule, vous pouvez la fusionner avec la cellule à droite ou en dessous.

#### Diviser des cellules {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

Sélectionnez une seule cellule pour la diviser :

* Diviser horizontalement une cellule génère une nouvelle cellule à droite de la cellule active, dans la colonne active.
* Diviser verticalement une cellule génère une nouvelle cellule sous la cellule active, mais dans la ligne active.

#### Création de tableaux imbriqués {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

La création d’un tableau imbriqué crée un tableau autonome dans la cellule active.

>[!NOTE]
>
>Certains comportements supplémentaires dépendent du navigateur :
>
>* Windows IE : utilisez les touches Ctrl + clic principal de la souris (généralement le gauche) pour sélectionner plusieurs cellules.
>* Firefox : faites glisser le pointeur pour sélectionner une plage de cellules.

#### Supprimer le tableau {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

Utilisez cette option pour supprimer le tableau du composant **[!UICONTROL Texte]**.

### Caractères spéciaux {#special-characters}

![Barre d’outils Caractères spéciaux](do-not-localize/cq55_rte_specialchars.png)

Des caractères spéciaux peuvent être mis à la disposition de votre éditeur de texte enrichi. Ils peuvent varier en fonction de votre installation.

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

Survolez avec la souris pour afficher une version agrandie du caractère, puis cliquez pour qu’il soit inclus à l’emplacement actuel dans votre texte.

### Mode de modification de la source {#source-editing-mode}

![Barre d’outils du mode de modification de la source](do-not-localize/cq55_rte_sourceedit.png)

Le mode d’édition source permet d’afficher et de modifier le HTML sous-jacent du composant.

Le texte suivant :

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

Se présentera comme suit dans le mode source (la source étant bien souvent plus longue, un défilement s’avérera nécessaire) :

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>Lors de la sortie du mode source, AEM effectue certaines vérifications de validation (par exemple, s’assurer que le texte est correctement contenu/imbriqué dans des blocs). Cela peut entraîner des modifications de vos modifications.
