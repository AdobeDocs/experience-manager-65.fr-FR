---
title: Conditions dans les communications interactives
description: Création et modification de fragments de condition à utiliser dans les communications interactives - la condition est l’un des quatre types de fragments de document utilisés pour créer des communications interactives. Les trois autres sont les fragments de texte, de liste et de disposition.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1494'
ht-degree: 100%

---

# Conditions dans les communications interactives{#conditions-in-interactive-communications}

Création et modification de fragments de condition à utiliser dans les communications interactives - la condition est l’un des quatre types de fragments de document utilisés pour créer des communications interactives. Les trois autres sont les fragments de texte, de liste et de disposition.

## Présentation {#overview}

La condition est un fragment de document que vous pouvez inclure dans une communication interactive. Les autres fragments de document sont [texte](../../forms/using/texts-interactive-communications.md), liste et fragment de disposition. Les conditions vous permettent de définir une ou plusieurs ressources contextuelles incluses dans une communication interactive en fonction des données et des règles fournies.

Exemples :

* Dans un relevé de carte de crédit, affichez les frais annuels et l’image de la carte de crédit en fonction du type de carte de crédit du client ou de la cliente.
* Dans un rappel relatif à une prime d’assurance, affichez les calculs de la taxe en fonction des impôts du client ou de la cliente.

Les actifs des conditions rendues en fonction des règles appliquées et des valeurs transmises à la règle. Les règles des conditions peuvent vérifier les valeurs dans les types de données suivants :

* Propriété du modèle de données de formulaire associé
* Toutes les variables que vous créez dans la condition
* Chaînes
* Nombres
* Expressions mathématiques
* Dates

## Créer la condition {#createcondition}

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Condition]**.
1. Saisissez les informations suivantes :

   * **[!UICONTROL Titre]** (facultatif) : saisissez le titre de la condition. Les titres ne doivent pas nécessairement être uniques et peuvent contenir des caractères spéciaux et des caractères dans une autre langue que l’anglais. Les conditions sont référencées par leur titre (le cas échéant) comme dans les vignettes et les propriétés.
   * **[!UICONTROL Nom]** : nom unique de la condition dans un dossier. Aucun fragment de document (texte, condition ou liste), quel que soit son état, ne peut porter le même nom qu’un autre fragment de document dans un dossier. Dans le champ Nom, vous pouvez saisir uniquement des caractères, des chiffres et des tirets de langue anglaise. Le champ Nom est automatiquement renseigné en fonction du champ Titre. Les caractères spéciaux, les espaces, les chiffres et les caractères non anglais saisis dans le champ Titre sont remplacés par des tirets dans le champ Nom. Bien que la valeur du champ Titre soit automatiquement copiée dans Nom, vous pouvez la modifier.

   * **[!UICONTROL Description]** : saisissez une description du fragment de document.
   * **[!UICONTROL Modèle de données de formulaire]** : éventuellement, sélectionnez le bouton radio Modèle de données de formulaire pour créer la condition en fonction d’un modèle de données de formulaire. Lorsque vous sélectionnez le bouton Modèle de données de formulaire, le champ **[!UICONTROL Modèle de données de formulaire]** s’affiche. Recherchez et sélectionnez un modèle de données de formulaire. Lors de la création de la condition d’une communication interactive, veillez à utiliser le même modèle de données que celui que vous avez l’intention d’utiliser dans la communication interactive. Pour plus d’informations sur le modèle de données de formulaire, consultez la section [Intégration de données](../../forms/using/data-integration.md).

   * **[!UICONTROL Balises]** : éventuellement, pour créer une balise personnalisée, entrez la valeur dans le champ de texte et appuyez sur Entrée. Lorsque vous enregistrez cette condition, les balises nouvellement ajoutées sont créées.

1. Sélectionnez **[!UICONTROL Suivant]**.

   La page Créer une condition apparaît.

   ![createcondition](assets/createcondition.png)

1. Sélectionnez **[!UICONTROL Ajouter des ressources]**.

   La page Sélectionner les actifs apparaît et affiche les textes, listes, conditions et images disponibles pour l’ajout dans la condition.

   >[!NOTE]
   >
   >Seules les ressources basées sur le FDM et celles sans modèle qui viennent d’être créées (à l’aide du même FDM que la condition créée) apparaissent dans la page Sélectionner les ressources.

1. Sélectionnez les ressources appropriées pour les sélectionner et les inclure dans la condition, puis choisissez **[!UICONTROL Terminé]**.

   La page Créer une condition apparaît et répertorie les ressources ajoutées.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Vous pouvez utiliser les options suivantes pour gérer les actifs dans une condition :

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] Rejeter la modification.** Sélectionnez cette icône pour rejeter les modifications que vous avez apportées à la ressource et à la règle dans la condition.
   **[B] Accepter la modification.** Sélectionnez cette icône pour accepter les modifications que vous avez apportées à la ressource et à la règle dans la condition.
   **[C] Dupliquer la ressource.** Sélectionnez cette icône pour créer une copie de la ressource avec la règle appliquée, le cas échéant, dans la condition. Vous pouvez ensuite modifier la règle et la ressource pour la ressource dupliquée. La duplication d’une ressource est utile pour créer des règles similaires afin d’afficher des ressources alternatives basées sur un contexte particulier.
   **[D] Afficher l’aperçu.** Sélectionnez cette icône pour afficher un aperçu de la ressource dans la page Créer/Modifier la condition.
   **Réorganiser le « serveur ».** Appuyez et maintenez cette icône enfoncée pour glisser-déposer des ressources et les réorganiser dans une condition.

   Vous pouvez sélectionner les options suivantes pour spécifier le comportement de la condition au moment de l’exécution :

   * **Évaluation des résultats multiples désactivée/Évaluation des résultats multiples activée** : lorsque cette option est activée (s’affiche comme « Évaluation des résultats multiples activée »), toutes les règles sont évaluées et le résultat est la somme de toutes les règles réelles. Si cette option est désactivée (« Évaluation des résultats multiples désactivée »), alors seule la première règle qui s’avère vraie est évaluée et devient la sortie de la condition.

   * **Saut de page** : sélectionnez cette option (![saut](assets/break.png)) afin d’insérer un saut de page entre les ressources des conditions. Lorsque cette option n’est pas sélectionnée (![nobreak](assets/nobreak.png)), si une condition déborde sur la page suivante dans la version imprimée, la condition entière est décalée vers la page suivante au lieu de faire irruption dans la page entre les ressources de la condition.

1. Sélectionnez **[!UICONTROL Créer une règle]** pour ajouter des règles d’affichage ou de masquage des ressources, selon les besoins. Pour utiliser des variables dans les règles, consultez la section [Créer des variables](#variables). Pour plus d’informations, consultez la section [Ajouter des règles à la condition](#ruleeditor).

   Les règles créées apparaissent dans la colonne RULE de l’écran Créer une condition.

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Vous pouvez insérer dans votre condition des actifs dans lesquels des règles ou des répétitions ont déjà été appliquées.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   La condition est créée. Vous pouvez maintenant utiliser la condition comme bloc de création lors de la création d’une communication interactive.

   >[!NOTE]
   >
   >Pour enregistrer une condition nouvelle ou modifiée, vous devez disposer d’au moins une règle pour chacune des ressources ajoutées à la condition.

## Modifier une condition {#edit-a-condition}

Vous pouvez modifier une condition en suivant les étapes suivantes. Vous pouvez également choisir de modifier une condition à partir d’une communication interactive en sélectionnant Modifier le fragment dans le menu contextuel.

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Accédez à la condition et sélectionnez-la.
1. Sélectionnez **[!UICONTROL Modifier]**.
1. Effectuez les modifications nécessaires dans la condition. Pour plus de détails sur les informations que vous pouvez modifier dans une condition, consultez la section [Créer une condition](#createcondition).
1. Sélectionnez **[!UICONTROL Enregistrer]**, puis **[!UICONTROL Fermer]**.

## Créer des règles dans une condition {#ruleeditor}

À l’aide de l’éditeur de règles dans une condition, vous pouvez créer des règles pour l’affichage ou le masquage des ressources en fonction de **conditions prédéfinies**. Ces conditions peuvent être construites en fonction de :

* Chaînes
* Nombres
* Expressions mathématiques
* Dates
* Propriétés du modèle de données de formulaire associé
* Toute [variable](#variables) que vous avez créée

### Créer une règle dans une condition {#create-rule-in-condition}

1. Lors de la création ou de la modification d’une condition, sélectionnez l’icône ![ruleeditoricon](assets/ruleeditoricon.png) (Éditeur de règles) de la ressource correspondante.

   La boîte de dialogue Créer une règle s’affiche. En plus de la chaîne, du nombre, de l’expression mathématique et de la date, les éléments suivants sont également disponibles dans l’éditeur de règles pour la création d’instructions :

   * Propriétés du modèle de données de formulaire associé
   * Les [variables](#variables) que vous avez créées.

   ![createruledialog](assets/createruledialog.png)

   Sélectionnez l’option pertinente à évaluer.

   >[!NOTE]
   >
   >La propriété Collection n’est pas prise en charge pour la création de règles d’affichage des actifs.

1. Sélectionnez l’opérateur approprié pour évaluer la règle, tel que Est égal à, Contient et Démarre avec.
1. Insérez l’expression d’évaluation, la chaîne, la propriété de modèle de données, la variable ou la date.

   ![Règle pour l’affichage d’un actif lorsque le type de politique est standard](assets/ruleincondition.png)

   Règle pour l’affichage d’un actif lorsque le type de politique est standard

   * Lors de la création ou de la modification d’une règle, vous pouvez également sélectionner ![icon_resize](assets/icon_resize.png) (Redimensionner) pour développer la boîte de dialogue Créer une règle/Modifier la règle. La boîte de dialogue développée, pleine fenêtre, vous permet de créer des [variables](#variables) pour construire des règles. Sélectionnez à nouveau Redimensionner pour revenir à la boîte de dialogue Créer une règle.

   * Vous pouvez également créer plusieurs conditions dans une règle.

1. Sélectionnez **[!UICONTROL Terminé]**.

   La règle est appliquée à la ressource.

## Création et utilisation de variables dans une condition {#variables}

Lorsque vous créez ou modifiez une règle dans une condition, vous pouvez cliquer sur ![icon_resize](assets/icon_resize.png) (Redimensionner) afin de développer la boîte de dialogue Créer une règle/Modifier la règle. La boîte de dialogue développée, pleine fenêtre, vous permet de :

* Créer et utiliser des variables dans la règle
* Glisser-déposer les propriétés et les variables du modèle de données de formulaire dans la règle

Sélectionnez nouveau Redimensionner pour revenir à la boîte de dialogue Créer une règle\Modifier la règle.

### Créer des variables {#create-variables}

1. Lorsque vous créez ou modifiez une règle dans une condition, vous pouvez sélectionner ![icon_resize](assets/icon_resize.png) (Redimensionner) pour développer la boîte de dialogue Créer une règle/Modifier la règle.

   La boîte de dialogue développée, pleine fenêtre, s’affiche.

   ![expandededitruledialog](assets/expandededitruledialog.png)

1. Dans le volet de gauche, sélectionnez **[!UICONTROL Variables]**.

   Le volet Variables apparaît.

   ![expandededitrulevariables](assets/expandededitrulevariables.png)

1. Sélectionnez **[!UICONTROL Créer]**.

   Le volet Créer des variables apparaît.

1. Saisissez les informations suivantes et sélectionnez **[!UICONTROL Créer]** :

   * **[!UICONTROL Nom]** : nom de la variable.
   * **[!UICONTROL Description]** : entrez éventuellement une description de la variable.
   * **[!UICONTROL Type]** : sélectionnez un type de variable : chaîne, nombre, valeur booléenne ou date.
   * **[!UICONTROL Autoriser les valeurs spécifiques uniquement]** : pour les variables de type Chaîne et Nombre, vous pouvez garantir que l’agent choisisse parmi un ensemble spécifique de valeurs pour un espace réservé dans l’interface utilisateur de l’agent. Pour spécifier l’ensemble de valeurs, sélectionnez cette option puis entrez des valeurs séparées par des virgules qui sont autorisées dans le champ **[!UICONTROL Valeurs]**.

1. Sélectionnez **[!UICONTROL Créer]**.

   La variable est créée et répertoriée dans le volet Variables.

1. Pour insérer une variable dans la règle, glissez-déposez-la dans un espace réservé à une option de la règle.
1. Après avoir construit une règle valide, sélectionnez **[!UICONTROL Terminé]**.

   Effectuez d’autres modifications dans la condition, si nécessaire, et enregistrez-la.
