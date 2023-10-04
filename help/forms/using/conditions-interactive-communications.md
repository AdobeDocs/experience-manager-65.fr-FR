---
title: Conditions dans les communications interactives
seo-title: Conditions in Interactive Communications
description: Création et modification de fragments de condition à utiliser dans les communications interactives - condition est l’un des quatre types de fragments de document utilisés pour créer des communications interactives. Les trois autres sont des fragments de texte, de liste et de mise en page.
seo-description: Creating and editing conditions to be used in Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 62%

---

# Conditions dans les communications interactives{#conditions-in-interactive-communications}

Création et modification de fragments de condition à utiliser dans les communications interactives - condition est l’un des quatre types de fragments de document utilisés pour créer des communications interactives. Les trois autres sont des fragments de texte, de liste et de mise en page.

## Présentation {#overview}

La condition est un fragment de document que vous pouvez inclure dans une communication interactive. Les autres fragments de document sont : [text](../../forms/using/texts-interactive-communications.md), liste et fragment de mise en page. Les conditions vous permettent de définir une ou plusieurs ressources contextuelles incluses dans une communication interactive en fonction des données et des règles fournies.

Exemples :

* Dans un relevé de carte de crédit, affichez les frais annuels et l’image de carte de crédit de la carte de crédit en fonction du type de carte de crédit du client.
* Dans un rappel de primes d’assurance, affichez les calculs de la taxe en fonction des taxes de l’état du client.

Les actifs des conditions rendues en fonction des règles appliquées et des valeurs transmises à la règle. Les règles des conditions peuvent vérifier les valeurs dans les types de données suivants :

* Propriété du modèle de données de formulaire associé
* Toutes les variables que vous créez dans la condition
* Chaînes
* Nombres
* Expressions mathématiques
* Dates

## Création d’une condition {#createcondition}

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Condition]**.
1. Saisissez les informations suivantes :

   * **[!UICONTROL Titre]** (facultatif) : saisissez le titre de la condition. Les titres n’ont pas besoin d’être uniques et peuvent contenir des caractères spéciaux et des caractères non anglais. Les conditions sont référencées par leur titre (le cas échéant) comme dans les vignettes et les propriétés.
   * **[!UICONTROL Nom]** : nom unique de la condition dans un dossier. Aucun fragment de document (texte, condition ou liste), quel que soit son état, ne peut porter le même nom qu’un autre fragment de document dans un dossier. Dans le champ Nom, vous pouvez saisir uniquement des caractères, des chiffres et des tirets de langue anglaise. Le champ Nom est automatiquement renseigné en fonction du champ Titre. Les caractères spéciaux, les espaces, les chiffres et les caractères non anglais saisis dans le champ Titre sont remplacés par des tirets dans le champ Nom. Bien que la valeur du champ Titre soit automatiquement copiée dans Nom, vous pouvez la modifier.

   * **[!UICONTROL Description]**: saisissez une description du fragment de document.
   * **[!UICONTROL Modèle de données de formulaire]** : éventuellement, sélectionnez le bouton radio Modèle de données de formulaire pour créer la condition en fonction d’un modèle de données de formulaire. Lorsque vous sélectionnez le bouton Modèle de données de formulaire, le champ **[!UICONTROL Modèle de données de formulaire]** s’affiche. Recherchez et sélectionnez un modèle de données de formulaire. Lors de la création de la condition d’une communication interactive, veillez à utiliser le même modèle de données que celui que vous avez l’intention d’utiliser dans la communication interactive. Pour plus d’informations sur le modèle de données de formulaire, consultez la section [Intégration de données](../../forms/using/data-integration.md).

   * **[!UICONTROL Balises]**: si vous le souhaitez, vous pouvez saisir une valeur dans le champ de texte de la balise personnalisée et appuyer sur Entrée. Lorsque vous enregistrez cette condition, les balises nouvellement ajoutées sont créées.

1. Appuyez sur **[!UICONTROL Suivant]**.

   La page Créer une condition apparaît.

   ![createcondition](assets/createcondition.png)

1. Appuyez sur **[!UICONTROL Ajouter des actifs]**.

   La page Sélectionner les actifs apparaît et affiche les textes, listes, conditions et images disponibles pour l’ajout dans la condition.

   >[!NOTE]
   >
   >Seules les ressources nouvellement créées, sans base, et les ressources basées sur FDM (créées à l’aide du même FDM que la condition en cours de création) apparaissent dans la page Sélectionner les ressources.

1. Appuyez sur les ressources appropriées pour les sélectionner à inclure dans la condition, puis appuyez sur **[!UICONTROL Terminé]**.

   La page Créer une condition s’affiche et répertorie les ressources ajoutées.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Vous pouvez utiliser les options suivantes pour gérer les actifs dans une condition :

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] Rejeter la modification.** Appuyez sur cette icône pour rejeter les modifications que vous avez apportées à l’actif et à la règle dans la condition.
   **[B] Accepter la modification.** Appuyez sur cette icône pour accepter les modifications que vous avez apportées à l’actif et à la règle dans la condition.
   **[C] Dupliquer la ressource.** Appuyez sur cette icône pour créer une copie de la ressource avec la règle appliquée, le cas échéant, dans la condition. Vous pouvez ensuite modifier la règle et la ressource pour la ressource dupliquée. La duplication d’une ressource s’avère utile pour créer des règles similaires afin d’afficher d’autres ressources en fonction d’un contexte particulier.
   **[D] Afficher l’aperçu.** Appuyez sur cette icône pour afficher un aperçu de l’actif dans la page Créer/Modifier la condition.
   **Réorganiser le « serveur ».** Appuyez et maintenez cette icône enfoncée pour glisser-déposer des actifs et les réorganiser dans une condition.

   Vous pouvez sélectionner les options suivantes pour spécifier le comportement de la condition au moment de l’exécution :

   * **Évaluation de résultats multiples désactivée\Évaluation de résultats multiples activée**: lorsque cette option est activée (s’affiche comme &quot;Évaluation de résultats multiples activée&quot;), toutes les règles sont évaluées et le résultat est la somme de toutes les règles vraies. Si cette option est désactivée (« Évaluation des résultats multiples désactivée »), alors seule la première règle qui s’avère vraie est évaluée et devient la sortie de la condition.

   * **Saut de page** : sélectionnez cette option (![saut](assets/break.png)) afin d’insérer un saut de page entre les ressources des conditions. Lorsque cette option n’est pas sélectionnée (![nobreak](assets/nobreak.png)), si une condition déborde sur la page suivante dans la version imprimée, la condition entière est décalée vers la page suivante au lieu de faire irruption dans la page entre les ressources de la condition.

1. Appuyer **[!UICONTROL Créer une règle]** pour ajouter des règles afin d’afficher ou de masquer les ressources, selon les besoins. Pour utiliser des variables dans les règles, voir [création de variables](#variables). Pour plus d’informations, consultez la section [Ajouter des règles à la condition](#ruleeditor).

   Les règles créées apparaissent dans la colonne RULE de l’écran Créer une condition.

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Vous pouvez insérer dans votre condition des actifs dans lesquels des règles ou des répétitions ont déjà été appliquées.

1. Appuyez sur **[!UICONTROL Enregistrer]**.

   La condition est créée. Vous pouvez maintenant utiliser la condition comme bloc de création lors de la création d’une communication interactive.

   >[!NOTE]
   >
   >Pour enregistrer une condition nouvelle ou modifiée, vous devez disposer d’au moins une règle pour chacun des actifs ajoutés à la condition.

## Modifier une condition {#edit-a-condition}

Vous pouvez modifier une condition en procédant comme suit. Vous pouvez également choisir de modifier une condition à partir d’une communication interactive en sélectionnant Modifier le fragment dans le menu contextuel.

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Accédez à la condition et sélectionnez-la.
1. Appuyez sur **[!UICONTROL Modifier]**.
1. Effectuez les modifications nécessaires dans la condition. Pour plus de détails sur les informations que vous pouvez modifier dans une condition, consultez la section [Créer une condition](#createcondition).
1. Appuyez sur **[!UICONTROL Enregistrer]** puis sur **[!UICONTROL Fermer]**.

## Création de règles dans une condition {#ruleeditor}

À l’aide de l’éditeur de règles dans une condition, vous pouvez créer des règles pour afficher ou masquer des ressources en fonction de **conditions prédéfinies**. Ces conditions peuvent être construites sur la base des éléments suivants :

* Chaînes
* Nombres
* Expressions mathématiques
* Dates
* Propriétés du modèle de données de formulaire associé
* Quelconque [variables](#variables) que vous avez créé

### Créer une règle dans une condition {#create-rule-in-condition}

1. Lors de la création ou de la modification d’une condition, cliquez sur l’icône ![ruleeditoricon](assets/ruleeditoricon.png) (Éditeur de règles) de la ressource correspondante.

   La boîte de dialogue Créer une règle s’affiche. Outre la chaîne, le nombre, l’expression mathématique et la date, les éléments suivants sont également disponibles dans l’éditeur de règles pour la création d’instructions des règles :

   * Propriétés du modèle de données de formulaire associé
   * Quelconque [variables](#variables) que vous avez peut-être créé.

   ![createruledialog](assets/createruledialog.png)

   Sélectionnez l’option pertinente à évaluer.

   >[!NOTE]
   >
   >La propriété Collection n’est pas prise en charge pour la création de règles d’affichage des actifs.

1. Sélectionnez l’opérateur approprié pour évaluer la règle, tel que Est égal à, Contient et Démarre avec.
1. Insérez l’expression d’évaluation, la chaîne, la propriété de modèle de données, la variable ou la date.

   ![Règle pour l’affichage d’un actif lorsque le type de politique est standard](assets/ruleincondition.png)

   Règle pour l’affichage d’un actif lorsque le type de politique est standard

   * Lors de la création ou de la modification d’une règle, vous pouvez également cliquer sur ![icon_resize](assets/icon_resize.png) (Redimensionner) pour développer la boîte de dialogue Créer une règle/Modifier la règle. La boîte de dialogue développée, pleine fenêtre, vous permet de créer des [variables](#variables) pour créer des règles. Appuyez à nouveau sur Redimensionner pour revenir à la boîte de dialogue Créer une règle.

   * Vous pouvez également créer plusieurs conditions dans une règle.

1. Appuyez sur **[!UICONTROL Terminé]**.

   La règle est appliquée à la ressource.

## Création et utilisation de variables dans une condition {#variables}

Lorsque vous créez ou modifiez une règle dans une condition, vous pouvez cliquer sur ![icon_resize](assets/icon_resize.png) (Redimensionner) afin de développer la boîte de dialogue Créer une règle/Modifier la règle. La boîte de dialogue développée, pleine fenêtre, vous permet d’effectuer les opérations suivantes :

* Créer et utiliser des variables dans la règle
* Glisser-déposer les propriétés et les variables du modèle de données de formulaire dans la règle

Appuyez à nouveau sur Redimensionner pour revenir à la boîte de dialogue Créer une règle\Modifier la règle .

### Créer des variables {#create-variables}

1. Lorsque vous créez ou modifiez une règle dans une condition, vous pouvez cliquer sur ![icon_resize](assets/icon_resize.png) (Redimensionner) pour développer la boîte de dialogue Créer une règle/Modifier la règle.

   La boîte de dialogue développée, pleine fenêtre, s’affiche.

   ![expandededitruledialog](assets/expandededitruledialog.png)

1. Dans le volet de gauche, appuyez sur **[!UICONTROL Variables]**.

   Le volet Variables apparaît.

   ![expandededitrulevariables](assets/expandededitrulevariables.png)

1. Appuyez sur **[!UICONTROL Créer]**.

   Le volet Créer des variables s’affiche.

1. Saisissez les informations suivantes et cliquez sur **[!UICONTROL Créer]** :

   * **[!UICONTROL Nom]** : nom de la variable.
   * **[!UICONTROL Description]** : entrez éventuellement une description de la variable.
   * **[!UICONTROL Type]** : sélectionnez un type de variable : chaîne, nombre, valeur booléenne ou date.
   * **[!UICONTROL Autoriser les valeurs spécifiques uniquement]** : pour les variables de type Chaîne et Nombre, vous pouvez garantir que l’agent choisisse parmi un ensemble spécifique de valeurs pour un espace réservé dans l’interface utilisateur de l’agent. Pour spécifier l’ensemble de valeurs, sélectionnez cette option puis entrez des valeurs séparées par des virgules qui sont autorisées dans le champ **[!UICONTROL Valeurs]**.

1. Appuyez sur **[!UICONTROL Créer]**.

   La variable est créée et répertoriée dans le volet Variables.

1. Pour insérer une variable dans la règle, glissez-déposez-la dans un espace réservé à une option de la règle.
1. Après avoir construit une règle valide, appuyez sur **[!UICONTROL Terminé]**.

   Effectuez d’autres modifications dans la condition, si nécessaire, et enregistrez-la.
