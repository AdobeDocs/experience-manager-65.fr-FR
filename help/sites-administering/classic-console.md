---
title: Console Balisage de l’interface utilisateur (IU) classique
description: Découvrez la console de balisage de l’interface utilisateur de Adobe Experience Manager Classic.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 48%

---


# Console Balisage de l’interface utilisateur (IU) classique{#classic-ui-tagging-console}

Cette section concerne la console de balisage de l’interface utilisateur classique.

La console de balisage de l’interface utilisateur optimisée pour les écrans tactiles est [here](/help/sites-administering/tags.md#tagging-console).

Pour accéder à la console Balisage de l’interface utilisateur classique :

* en mode de création
* connexion avec droits d’administrateur
* Accédez à la console par exemple, [https://localhost:4502/tagging](https://localhost:4502/tagging).

![Fenêtre de console classique](assets/managing_tags_usingthetagasministrationconsole.png)

## Création de balises et d’espaces de noms {#creating-tags-and-namespaces}

1. Selon le niveau à partir duquel vous commencez, vous pouvez créer une balise ou un espace de noms à l’aide de **Nouveau**:

   Si vous sélectionnez **Balises** vous pouvez créer un espace de noms :

   ![Création d’un espace de noms](assets/creating_tags_andnamespaces.png)

   Si vous sélectionnez un espace de noms (par exemple : **Démonstration**) vous pouvez créer une balise dans cet espace de noms :

   ![Création d’une boîte de dialogue de balise](assets/creating_tags_andnamespacesinnewnamespace.png)

1. Dans les deux cas, saisissez

   * **Titre**
(*Obligatoire*) Titre affiché pour la balise. Même s’il est possible d’utiliser n’importe quel caractère, il est recommandé de ne pas utiliser ces caractères spéciaux :

      * `colon (:)` - Délimiteur d’espace de noms
      * `forward slash (/)` - Délimiteur de sous-balises

     Si vous saisissez ces caractères, ils ne s’affichent pas.

   * **Nom**
(*Obligatoire*) Nom du nœud pour la balise.

   * **Description**
(*Facultatif*) Description de la balise.

   * select **Créer**

## Modification des balises {#editing-tags}

1. Dans le volet de droite, sélectionnez la balise à modifier.
1. Cliquez sur **Modifier**.
1. Vous pouvez modifier le **Titre** et la variable **Description**.
1. Cliquez sur **Enregistrer** pour fermer la boîte de dialogue.

## Suppression des balises {#deleting-tags}

1. Dans le volet de droite, sélectionnez la balise à supprimer.
1. Cliquez sur **Supprimer**.
1. Cliquez sur **Oui** pour fermer la boîte de dialogue.

   La balise ne doit plus être répertoriée.

## Activation et désactivation des balises {#activating-and-deactivating-tags}

1. Dans le volet de droite, sélectionnez l’espace de noms ou la balise à activer (publier) ou désactiver (annuler la publication).
1. Cliquez sur **Activer** ou **Désactiver** selon les besoins.

## Liste : indique l’emplacement de référence des balises. {#list-showing-where-tags-are-referenced}

**Liste** ouvre une nouvelle fenêtre affichant les chemins de toutes les pages à l’aide de la balise mise en surbrillance :

![Recherche de l’emplacement où les balises sont référencées](assets/list_showing_wheretagsarereferenced.png)

## Déplacement des balises {#moving-tags}

Pour aider les administrateurs et les développeurs de balises à nettoyer la taxonomie ou à renommer un ID de balise, il est possible de déplacer une balise vers un nouvel emplacement :

1. Ouvrez le **Balisage** console.
1. Sélectionnez la balise et cliquez sur **Déplacer..** dans la barre d’outils supérieure (ou dans le menu contextuel).
1. Dans le **Déplacer la balise** dialog, définissez :

   * **to**, le noeud de destination.
   * **Renommer en**, le nouveau nom du noeud.

1. Cliquez sur **Déplacer**.

La variable **Déplacer la balise** dialog se présente comme suit :

![Déplacement d’une balise](assets/move_tag.png)

>[!NOTE]
>
>Les créateurs ne doivent pas déplacer les balises ou renommer l’ID de balise. Lorsque cela est nécessaire, les créateurs doivent seulement [modifier le titre des balises](#editing-tags).

## Fusion de balises {#merging-tags}

Il est également possible de recourir à la fusion de balises lorsqu’une taxonomie comporte des doublons. Lorsque la balise A est fusionnée dans la balise B, toutes les pages balisées avec la balise A sont balisées avec la balise B et la balise A n’est plus disponible pour les auteurs.

Pour fusionner une balise dans une autre balise :

1. Ouvrez le **Balisage** console.
1. Sélectionnez la balise et cliquez sur **Fusionner..** dans la barre d’outils supérieure (ou dans le menu contextuel).
1. Dans le **Fusionner la balise** dialog, définissez :

   * **into**, le noeud de destination.

1. Cliquez sur **Fusion**.

La boîte de dialogue **Fusionner la balise** se présente de la manière suivante :

![Fusion d’une balise](assets/mergetag.png)

## Comptage de l’utilisation des balises {#counting-usage-of-tags}

Pour savoir combien de fois une balise est utilisée :

1. Ouvrez le **Balisage** console.
1. Cliquez sur **Utilisation des nombres** dans la barre d’outils supérieure : la colonne Nombre affiche le résultat.

## Gestion des balises dans différentes langues {#managing-tags-in-different-languages}

La propriété facultative `title` d’une balise peut être traduite en plusieurs langues. Les `titles` de balises peuvent s’afficher soit dans la langue de l’utilisateur, soit dans la langue de la page.

### Définition de titres de balises dans plusieurs langues {#defining-tag-titles-in-multiple-languages}

La procédure ci-dessous indique comment traduire le `title` de la balise **Animals** en anglais, en allemand et en français :

1. Accédez à la console **Balisage**.
1. Modifiez la balise **Animals** située sous **Balises** > **Images de photothèque**.
1. Ajoutez les traductions dans les langues suivantes :

   * **Anglais**: animaux
   * **Allemand**: Tiere
   * **Français**: Animaux

1. Enregistrez les modifications.

La boîte de dialogue se présente comme suit :

![Modification d’une balise](assets/edit_tag.png)

La console Balisage utilise la langue du créateur, dès lors, pour la balise « Animals », « Animaux » s’affiche si l’utilisateur définit la langue sur Français dans les propriétés de l’utilisateur.

Pour ajouter une nouvelle langue à la boîte de dialogue, voir la section [Ajout d’une nouvelle langue à la boîte de dialogue Modifier la balise](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) dans le **Balisage pour les développeurs** .

### Affichage des titres des balises dans les propriétés de page dans une langue spécifiée {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Par défaut, les `titles` des balises dans les propriétés de page sont affichés dans la langue de la page. La boîte de dialogue de balise dans les propriétés de page comporte un champ Langue, qui permet d’afficher le `titles` des balises dans une autre langue. La procédure ci-dessous décrit comment afficher les `titles` des balises en français :

1. Reportez-vous à la section précédente pour ajouter la traduction française au mot-clé **Animals** en sélectionnant **Balises** > **Images de photothèque**.
1. Ouvrez les propriétés de la page **Produits** dans la branche English (Anglais) du site **Geometrixx**.
1. Ouvrez la boîte de dialogue **Balises/Mots-clés** (en sélectionnant le menu déroulant à droite de la zone d’affichage Balises/Mots-clés) et sélectionnez la langue **Français** dans le menu déroulant dans le coin inférieur droit.
1. Faites défiler la page à l’aide des flèches gauche-droite jusqu’à ce que vous puissiez sélectionner l’onglet **Images de photothèque**.

   Sélectionnez la balise **Animals** (**Animaux**) et cliquez en dehors de la boîte de dialogue pour la fermer et ajouter la balise aux propriétés de la page.

   ![Modifier une autre balise](assets/french_tag.png)

Par défaut, la boîte de dialogue Propriétés de page affiche le `titles` des balises en fonction de la langue de la page.

En général, la langue de la balise est celle de la page si elle est disponible. Lorsque la variable [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) est utilisé dans d’autres cas (dans les formulaires ou les boîtes de dialogue, par exemple), la langue de la balise dépend du contexte.

>[!NOTE]
>
>Le nuage de balises et les éléments « meta keyword » du composant Page standard utilisent les `titles` des balises localisées en fonction de la langue de la page (si elle est disponible).
