---
title: Éditeur de règles de formulaires adaptatifs
description: L’éditeur de règles de formulaire adaptatif permet d’ajouter un comportement dynamique et de créer une logique complexe dans des formulaires, sans code ni script.
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms, Foundation Components
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
exl-id: c611a1f8-9d94-47f3-bed3-59eef722bf98
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '6607'
ht-degree: 100%

---

# Éditeur de règles de formulaires adaptatifs{#adaptive-forms-rule-editor}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=fr) |
| AEM 6.5 | Cet article |

## Vue d’ensemble {#overview}

La fonctionnalité d&#39;éditeur de règles dans Adobe Experience Manager Forms permet aux utilisateurs, aux utilisatrices, aux développeurs et aux développeuses professionnels de formulaires de créer des règles sur des objets de formulaire adaptatif. Ces règles déterminent les actions à déclencher sur des objets de formulaire en fonction des conditions prédéfinies, des entrées de l’utilisateur et des actions de l’utilisateur sur le formulaire. Cela permet de rationaliser davantage l’expérience de remplissage du formulaire en assurant précision et vitesse.

L’éditeur de règles fournit une interface utilisateur intuitive et simplifiée pour la création de règles. L’éditeur de règles met un éditeur visuel à disposition de tous les utilisateurs. En outre, l’éditeur de règles fournit un éditeur de code permettant d’écrire des règles et des scripts, mais seulement aux utilisateurs et utilisatrices expérimentés des formulaires.
<!-- Some of the key actions that you can perform on adaptive form objects using rules are:

* Show or hide an object
* Enable or disable an object
* Set a value for an object
* Validate the value of an object
* Execute functions to compute the value of an object
* Invoke a form data model service and perform an operation
* Set property of an object -->

L’éditeur de règles remplace les fonctionnalités de script dans AEM Forms 6.1 et les versions antérieures. Toutefois, les scripts existants sont conservés dans le nouvel éditeur de règles. Pour plus d’informations sur l’utilisation des scripts existants dans l’éditeur de règles, reportez-vous à la section[ Impact de l’éditeur de règles sur les scripts existants](#impact-of-rule-editor-on-existing-scripts).

Les utilisateurs et utilisatrices ajoutés au groupe des utilisateurs et utilisatrices expérimentés de formulaires peuvent créer de nouveaux scripts et modifier les scripts existants. Les utilisateurs et utilisatrices appartenant au groupe d’utilisateurs et d’utilisatrices de formulaires peuvent utiliser les scripts, mais ne peuvent ni en créer ni en modifier.

## Compréhension d’une règle {#understanding-a-rule}

Une règle est une combinaison d’actions et de conditions. Dans l’éditeur de règles, les actions incluent des activités telles que masquer, afficher, activer, désactiver ou calculer la valeur d’un objet dans un formulaire. Les conditions sont des expressions booléennes qui sont évaluées en effectuant des vérifications et des opérations sur l’état, la valeur ou la propriété d’un objet de formulaire. Les actions sont exécutées en fonction de la valeur (`True` ou `False`) renvoyée par l’évaluation d’une condition.

L’éditeur de règles fournit un ensemble de types de règle prédéfinis, tels que Lorsque, Afficher, Masquer, Activer, Désactiver, Définir la valeur de et Valider pour vous aider à créer des règles. Chaque type de règle vous permet de définir des conditions et des actions dans une règle. Le document décrit de façon plus détaillée chaque type de règle.

Une règle suit généralement l’un des concepts suivants :

**Condition-action** Dans ce concept, une règle définit d’abord une condition suivie d’une action à déclencher. Le concept est comparable à l’instruction if-then des langages de programmation.

Dans l’éditeur de règles, le type de règle **Lorsque** applique le concept de condition-action.

**Action-condition** Dans ce concept, une règle définit d’abord une action à déclencher suivie de conditions d’évaluation. Une autre variante de ce concept est une action alternative d’action-condition, qui définit également une action alternative à déclencher si la condition renvoie la valeur False.

Les types de règles Afficher, Masquer, Activer, Désactiver, Définir la valeur de et Valider de l’éditeur de règles appliquent le concept de règle d’action-condition. Par défaut, l’action alternative d’Afficher est Masquer et l’action alternative d’Activer est Désactiver, et inversement. Vous ne pouvez pas modifier l’action alternative par défaut.

>[!NOTE]
>
>Les types de règles disponibles, y compris les conditions et actions que vous définissez dans l’éditeur de règles, dépendent également du type d’objet de formulaire sur lequel vous créez une règle. L’éditeur de règles affiche uniquement les types de règle et les options valides lors de la création des instructions de condition et d’action pour un type particulier d’objet de formulaire. Par exemple, les types de règle Valider, Définir la valeur de, Activer et Désactiver ne s’affichent pas pour un objet de panneau.

Pour plus d’informations sur les types de règle disponibles dans l’éditeur de règles, reportez-vous à la section [Types de règle disponibles dans l’éditeur de règles](#available-rule-types-in-rule-editor).

### Recommandations pour la sélection d’un concept de règle {#guidelines-for-choosing-a-rule-construct}

Même si vous pouvez obtenir la plupart des cas d’utilisation avec n’importe quel concept de règle, voici quelques recommandations pour sélectionner un concept plutôt qu’un autre. Pour plus d’informations sur les règles disponibles dans l’éditeur de règles, reportez-vous à la section [Types de règles disponibles dans l’éditeur de règles](#available-rule-types-in-rule-editor).

* Lors de la création d’une règle, réfléchissez d’abord au contexte de l’objet pour lequel vous la créez. Supposons que vous souhaitiez masquer ou afficher le champ B en fonction de la valeur spécifiée par un utilisateur ou une utilisatrice dans le champ A. Dans ce cas, vous évaluez une condition sur le champ A, et selon la valeur qu’elle renvoie, vous déclenchez une action sur le champ B.

  Par conséquent, si vous créez une règle pour le champ B (l’objet pour lequel vous évaluez une condition), utilisez le concept de condition-action ou le type de règle Lorsque. De même, utilisez le concept de condition-action ou le type de règle Afficher ou Masquer sur le champ A.

* Parfois, vous devez effectuer plusieurs actions en fonction d’une condition. Dans ce cas, il est recommandé d’utiliser le concept de condition-action. Dans ce concept, vous pouvez évaluer une condition une fois et spécifier plusieurs instructions d’action.

  Par exemple, pour masquer les champs B, C et D en fonction de la condition qui vérifie la valeur spécifiée par un utilisateur ou une utilisatrice dans le champ A, écrivez une règle avec le concept de condition-action ou le type de règle Lorsque dans le champ A et spécifiez les actions pour contrôler la visibilité des champs B, C et D. Dans le cas contraire, vous avez besoin de trois règles distinctes sur les champs B, C et D, où chaque règle vérifie la condition et affiche ou masque le champ correspondant. Dans cet exemple, il est plus efficace de créer le type de règle Lorsque sur un objet plutôt que le type de règle Afficher ou Masquer sur trois objets.

* Pour déclencher une action selon plusieurs conditions, il est recommandé d’utiliser le concept d’action-condition. Par exemple, pour afficher et masquer le champ A en évaluant les conditions des champs B, C et D, utilisez le type de règle Afficher ou Masquer sur le champ A.
* Utilisez le concept de condition-action ou d’action-condition si la règle contient une action pour une condition.
* Si une règle vérifie une condition et exécute immédiatement une action en fournissant une valeur dans un champ ou en quittant un champ, il est recommandé de créer une règle avec le concept de condition-action ou le type de règle Lorsque sur le champ sur lequel la condition est évaluée.
* La condition dans la règle Lorsque est évaluée lorsqu’un utilisateur modifie la valeur de l’objet pour lequel la règle Lorsque est appliquée. Cependant, si vous souhaitez déclencher l’action lorsque la valeur change du côté serveur, comme lorsque vous préremplissez la valeur, il est recommandé de créer une règle Lorsque qui déclenche l’action lors de l’initialisation du champ.
* Lorsque vous créez des règles pour les menus déroulants, les boutons radio ou les cases à cocher, les options ou les valeurs de ces objets de formulaire sont préremplies dans l’éditeur de règles.

## Types d’opérateur et événements disponibles dans l’éditeur de règles {#available-operator-types-and-events-in-rule-editor}

L’éditeur de règles fournit les opérateurs logiques et les événements suivants à l’aide desquels vous pouvez créer des règles.

* **est égal à**
* **n&#39;est pas égal à**
* **Commence par**
* **Se termine par**
* **Contient**
* **Est vide**
* **N’est pas vide**
* **A sélectionné :** renvoie la valeur True lorsque l’utilisateur sélectionne une option donnée pour une case à cocher, une liste déroulante, un bouton radio.
* **Est initialisé (événement) :** renvoie la valeur True si un objet de formulaire est généré dans le navigateur.
* **Est modifié (événement) :** renvoie la valeur True si l’utilisateur modifie la valeur saisie ou l’option sélectionnée pour un objet de formulaire.

## Types de règle disponibles dans l’éditeur de règles {#available-rule-types-in-rule-editor}

L’éditeur de règles fournit un ensemble de types de règle prédéfinis que vous pouvez utiliser pour créer des règles. Examinons en détail chaque type de règle. Pour plus d’informations sur la création de règles dans l’éditeur de règles, reportez-vous à la section [Création de règles](#write-rules).

### Quand {#whenruletype}

Le type de règle **Lorsque** suit le concept de règle d’**action alternative de condition-action** ou parfois simplement le concept de **condition-action**. Dans ce type de règle, vous spécifiez d’abord une condition à évaluer, puis une action à déclencher si la condition est remplie (`True`). Lors de l’utilisation du type de règle Lorsque, vous pouvez utiliser plusieurs opérateurs ET et OU afin de créer des [expressions imbriquées](#nestedexpressions).

Avec le type de règle Lorsque, vous pouvez évaluer une condition sur un objet de formulaire et exécuter des actions sur un ou plusieurs objets.

En clair, un type de règle Lorsque standard est structuré comme suit :

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Action 2 sur Objet B ;
ET 
Action 3 sur Objet C ;

_

Lorsque vous avez un composant à valeurs multiples, comme des boutons radio ou une liste, les options sont récupérées automatiquement et mises à disposition du créateur de la règle lorsque vous créez une règle pour ce composant. Vous n’avez pas besoin de saisir à nouveau les valeurs de l’option.

Prenons l’exemple d’une liste comportant quatre options : rouge, bleu, vert et jaune. Lors de la création de la règle, les options (boutons radio) sont automatiquement récupérées et mises à la disposition de la personne chargée de la création de la règle comme suit :

![multivaluefcdisplaysoptions](assets/multivaluefcdisplaysoptions.png)

Lorsque vous créez une règle Lorsque, vous pouvez déclencher l’action Effacer la valeur de. L’action Effacer la valeur d’efface la valeur de l’objet spécifié. L’option Effacer la valeur de dans l’instruction Lorsque permet de créer des conditions complexes comportant plusieurs champs.

![clearvalueof](assets/clearvalueof.png)

**Masquer** Masque l’objet spécifié.

**Afficher** Affiche l’objet spécifié.

**Activer** Active l’objet spécifié.

**Désactiver** Désactive l’objet spécifié.

**Appel du service** Appel un service configuré dans un modèle de données de formulaire. Lorsque vous sélectionnez l’opération Appel du service, un champ s’affiche. Lorsque vous touchez le champ, il affiche tous les services configurés dans tous les modèles de données de formulaire de votre instance AEM. Lorsque vous choisissez un service de modèle de données de formulaire, des champs supplémentaires permettant de mapper les objets de formulaires avec des paramètres d’entrée et de sortie pour le service spécifié apparaissent. Voir l’exemple de règle pour appeler des services de modèle de données de formulaire.

Outre le service de modèle de données de formulaire, vous pouvez spécifier une URL WSDL directe pour appeler un service web. Cependant, un service de modèle de données de formulaire possède de nombreux avantages et l’approche recommandée permettant d’appeler un service.

Pour plus d’informations à propos de la configuration des services dans le modèle de données de formulaire, voir [Intégration des données AEM Forms](/help/forms/using/data-integration.md).

**Définir la valeur de** Calcule et définit la valeur de l’objet spécifié. Vous pouvez définir cette valeur par une chaîne, la valeur d’un autre objet, la valeur calculée avec une expression ou une fonction mathématique, la valeur d’une propriété d’un objet ou la valeur de sortie d’un service de modèle de données de formulaire configuré. Lorsque vous sélectionnez l’option Service web, elle affiche tous les services configurés dans tous les modèles de données de formulaire de votre instance AEM. Lorsque vous choisissez un service de modèle de données de formulaire, des champs supplémentaires permettant de mapper les objets de formulaires avec des paramètres d’entrée et de sortie pour le service spécifié apparaissent.

Pour plus d’informations à propos de la configuration des services dans le modèle de données de formulaire, voir [Intégration des données AEM Forms](/help/forms/using/data-integration.md).

Le type de règle **[!UICONTROL Définir la propriété]** permet de définir la valeur d’une propriété de l’objet spécifié en fonction d’une action de condition. Vous pouvez définir la propriété sur l’une des options suivantes :

* visible (booléen)
* dorExclusion (booléen)
* chartType (chaîne)
* title (chaîne)
* enabled (booléen)
* mandatory (booléen)
* validationsDisabled (booléen)
* validateExpMessage (chaîne)
* value (nombre, chaîne, date)
* items (liste)
* valid (booléen)
* errorMessage (chaîne)

Il permet de définir des règles pour ajouter de façon dynamique des cases à cocher au formulaire adaptatif. Pour définir une règle, vous pouvez utiliser une fonction personnalisée, un objet de formulaire ou une propriété d’objet.

![Définir la propriété](assets/set_property_rule_new.png)

Pour définir une règle basée sur une fonction personnalisée, sélectionnez **Sortie de fonction** dans la liste déroulante, puis faites glisser et déposez une fonction personnalisée à partir de l’onglet **Fonctions**. Si l’action de condition est remplie, le nombre de cases à cocher définies dans la fonction personnalisée est ajouté au formulaire adaptatif.

Pour définir une règle basée sur un objet de formulaire, sélectionnez **Objet de formulaire** dans la liste déroulante, puis faites glisser et déposez un objet de formulaire à partir de l’onglet **Objets de formulaire**. Si l’action de condition est remplie, le nombre de cases à cocher définies dans l’objet de formulaire est ajouté au formulaire adaptatif.

Une règle Définir la propriété basée sur une propriété d’objet permet d’ajouter le nombre de cases à cocher dans un formulaire adaptatif en fonction d’une autre propriété d’objet incluse dans le formulaire adaptatif.

La figure ci-dessous présente un exemple d’ajout dynamique de cases à cocher en fonction du nombre de listes déroulantes dans le formulaire adaptatif :

![Propriété de l’objet](assets/object_property_set_property_new.png)

**Effacer la valeur de** : efface la valeur de l’objet spécifié.

**Définir la cible d’action**: définit la cible d’action sur l’objet spécifié.

**Enregistrer le formulaire** : enregistre le formulaire.

**Envoyer les formulaires** : envoie le formulaire.

**Réinitialiser le formulaire** : réinitialise le formulaire.

**Valider le formulaire** : valide le formulaire.

**Ajouter une instance** : ajoute une instance de la ligne de panneau ou de tableau répétable spécifiée.

**Supprimer une instance** : supprime une instance de la ligne de panneau ou de tableau répétable spécifiée.

**Accéder à** : permet d’accéder à d’autres communications interactives, d’autres formulaires adaptatifs, d’autres ressources, comme des images ou des fragments de document ou une URL externe. Pour plus d’informations, voir [Ajouter un bouton à la communication interactive](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel).

### Définir la valeur de {#set-value-of}

Le type de règle **[!UICONTROL Définir la valeur de]** permet de définir la valeur d’un objet de formulaire selon que la condition spécifiée est remplie ou non. La valeur peut être définie sur la valeur d’un autre objet, d’une chaîne littérale, la valeur dérivée d’une expression ou d’une fonction mathématique, la valeur d’une propriété d’un autre objet ou la sortie d’un service de modèle de données de formulaire. De même, vous pouvez vérifier la condition d’un composant, d’une chaîne, d’une propriété ou les valeurs dérivées d’une fonction ou d’une expression mathématique.

Le type de règle Définir la valeur de n’est pas disponible pour tous les objets de formulaire, comme les boutons de panneaux et de barres d’outils. Une règle Définir la valeur de standard possède la structure suivante :



Définir la valeur d’Objet A sur :

(chaîne ABC) OU
(propriété d’objet X de l’objet C) OU
(valeur d’une fonction) OU
(valeur d’une expression mathématique) OU
(valeur de sortie d’un service de modèle de données ou d’un service Web) ;

Lorsque (facultatif) :

(Condition 1 ET Condition 2 ET Condition 3) est TRUE ;



L’exemple suivant prend la valeur du champ `dependentid` comme valeur d’entée et définit la valeur du champ `Relation` comme valeur de sortie de l’argument `Relation` du service de modèle de données de formulaire `getDependent`.

![set-value-web-service](assets/set-value-web-service.png)

Exemple de règle Définir la valeur de à l’aide du service de modèle de données de formulaire

>[!NOTE]
>
>De plus, vous pouvez utiliser la règle Définir la valeur de pour remplir toutes les valeurs d’un composant de type liste déroulante à partir de la sortie d’un service de modèle de données de formulaire ou d’un service web. Cependant, assurez-vous que l’argument de sortie que vous choisissez est de type tableau. Toutes les valeurs renvoyées dans un tableau sont disponibles dans la liste déroulante spécifiée.

### Afficher {#show}

Le type de règle **Afficher** permet de créer une règle pour afficher ou masquer un objet de formulaire selon qu’une condition est remplie ou non. Le type de règle Afficher déclenche également l’action Masquer au cas où la condition ne serait pas remplie ou renverrait `False`.

Une règle standard Afficher est structurée comme suit :



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### Masquer {#hide}

De la même manière que pour le type de règle Afficher, vous pouvez utiliser le type de règle **Masquer** pour afficher ou masquer un objet de formulaire selon qu’une condition est remplie ou non. Le type de règle Masquer déclenche également l’action Afficher au cas où la condition ne serait pas remplie ou renverrait `False`.

Une règle standard Masquer est structurée comme suit :



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### Activer {#enable}

Le type de règle **Activer** permet d’activer ou de désactiver un objet de formulaire selon qu’une condition est remplie ou non. Le type de règle Activer déclenche également l’action Désactiver au cas où la condition ne serait pas remplie ou renverrait `False`.

Une règle Activer standard est structurée comme suit :



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### Désactiver {#disable}

De la même manière que le type de règle Activer, le type de règle **Désactiver** permet d’activer ou de désactiver un objet de formulaire selon qu’une condition est remplie ou non. Le type de règle Désactiver déclenche également l’action Activer au cas où la condition ne serait pas remplie ou renverrait `False`.

Une règle Désactiver standard est structurée comme suit :



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### Valider {#validate}

Le type de règle **Valider** valide la valeur d’un champ à l’aide d’une expression. Par exemple, vous pouvez créer une expression pour vérifier que le champ de texte qui indique un nom ne contient pas de caractères spéciaux ni de nombres.

Une règle Valider standard est structurée comme suit :

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Si la valeur spécifiée n’est pas conforme à la règle Valider, vous pouvez afficher un message de validation à l’utilisateur ou utilisatrice. Vous pouvez spécifier le message dans le champ **[!UICONTROL Message de validation du script]** dans les propriétés de composant dans la barre latérale.

![script-validation](assets/script-validation.png)

### Définir les options de {#setoptionsof}

Le type de règle **Définir les options de** permet de définir des règles pour ajouter dynamiquement des cases à cocher au formulaire adaptatif. Vous pouvez utiliser un modèle de données de formulaire ou une fonction personnalisée pour définir la règle.

Pour définir une règle basée sur une fonction personnalisée, sélectionnez **Sortie de fonction** dans la liste déroulante, puis faites glisser et déposez une fonction personnalisée à partir de l’onglet **Fonctions**. Le nombre de cases à cocher définies dans la fonction personnalisée est ajouté au formulaire adaptatif.

![Fonctions personnalisées](assets/custom_functions_set_options_new.png)

Pour créer une fonction personnalisée, voir [Fonctions personnalisées dans l’éditeur de règles](#custom-functions).

Pour définir une règle basée sur un modèle de données de formulaire :

1. Sélectionnez **Sortie du service** dans la liste déroulante.
1. Sélectionnez l’objet de modèle de données.
1. Sélectionnez une propriété d’objet de modèle de données dans la liste déroulante **Valeur d’affichage**. Le nombre de cases à cocher dans le formulaire adaptatif est dérivé du nombre d’instances définies pour cette propriété dans la base de données.
1. Sélectionnez une propriété d’objet de modèle de données dans la liste déroulante **Enregistrer la valeur**.

![Options de jeu FDM](assets/fdm_set_options_new.png)

## Présentation de l’interface utilisateur de l’éditeur de règles {#understanding-the-rule-editor-user-interface}

L’éditeur de règles offre une interface utilisateur exhaustive et néanmoins simple, qui permet de créer et de gérer des règles. Vous pouvez lancer l’interface utilisateur de l’éditeur de règles depuis un formulaire adaptatif en mode Création.

Pour lancer l’interface utilisateur de l’éditeur de règles :

1. Ouvrez un formulaire adaptatif en mode Création.
1. Sélectionnez l’objet de formulaire pour lequel vous voulez créer une règle, puis ![edit-rules](assets/edit-rules.png) de la barre d’outils Composant. L’interface utilisateur de l’éditeur de règles s’affiche.

   ![create-rules](assets/create-rules.png)

   Toutes les règles existantes pour les objets de formulaire sélectionnés sont répertoriées dans cet écran. Pour plus d’informations sur la gestion des règles existantes, voir [Gestion des règles](#manage-rules).

1. Sélectionnez **[!UICONTROL Créer]** pour créer une règle. L’éditeur visuel de l’interface utilisateur de l’éditeur de règles s’affiche par défaut la première fois que vous lancez l’éditeur de règles.

   ![Interface utilisateur de l’éditeur de règles](assets/rule-editor-ui.png)

Examinons en détail chaque composant de l’interface utilisateur de l’éditeur de règles.

### A. Affichage composant-règle {#a-component-rule-display}

Affiche le titre de l’objet de formulaire adaptatif à partir duquel vous avez lancé l’éditeur de règles et le type de règle actuellement sélectionné. Dans l’exemple ci-dessus, l’éditeur de règles est lancé depuis l’objet d’un formulaire adaptatif intitulé Salary et le type de règle sélectionné est Lorsque. 

### B. Objets de formulaire et fonctions {#b-form-objects-and-functions-br}

Le volet situé à gauche de l’interface utilisateur de l’éditeur de règles comporte deux onglets: **[!UICONTROL Objets de formulaire]** et **[!UICONTROL Fonctions]**.

L’onglet Objets de formulaire affiche une arborescence de tous les objets contenus dans le formulaire adaptatif. Il affiche le titre et le type des objets. Lors de la création d’une règle, vous pouvez faire glisser-déposer les objets de formulaire dans l’éditeur de règles. Lorsque vous créez ou modifiez une règle en faisant glisser et en déposant un objet ou une fonction dans un espace réservé, cet espace prend automatiquement le type de valeur approprié.

Les objets de formulaire contenant une ou plusieurs règles valides appliquées sont désignés par un point vert. Si l’une des règles appliquées à un objet de formulaire n’est pas valide, l’objet de formulaire est identifié par un point jaune.

L’onglet Fonctions comporte un jeu de fonctions intégrées, comme Somme de, Minimum de, Maximum de, Moyenne de, Nombre de et Valider le formulaire. Vous pouvez utiliser ces fonctions pour calculer des valeurs dans les panneaux et les lignes de tableau répétables et pour les instructions d’action et de condition lors de la création de règles. Cependant, vous pouvez créer des [fonctions personnalisées](#custom-functions).

![L’onglet Fonctions](assets/functions.png)

>[!NOTE]
>
>Vous pouvez effectuer une recherche de texte dans les noms et titres des objets et des fonctions à partir des onglets Objets de formulaire et Fonctions.

Dans l’arborescence de gauche des objets de formulaire, vous pouvez sélectionner les objets de formulaire pour afficher les règles appliquées à chacun des objets. Vous pouvez non seulement parcourir les règles des différents objets de formulaire mais également copier-coller des règles entre les objets du formulaire. Pour plus d’informations, reportez-vous à la section [Règles de copier-coller](#copy-paste-rules).

### C. Basculement entre les objets de formulaire et les fonctions {#c-form-objects-and-functions-toggle-br}

Le bouton Basculer, lorsqu’il est sélectionné, permet de basculer entre le volet des objets de formulaire et celui des fonctions.

### D. Éditeur de règles visuel {#d-visual-rule-editor}

Lorsque l’interface utilisateur de l’éditeur de règles est en mode éditeur visuel, l’éditeur de règles visuel est la zone dans laquelle vous créez des règles. Il vous permet de sélectionner un type de règle et de définir en conséquence des conditions et des actions. Lors de la définition des conditions et des actions dans une règle, vous pouvez glisser-déposer des objets de formulaire et des fonctions depuis le volet Objets de formulaire et Fonctions.

Pour plus d’informations sur l’utilisation de l’éditeur de règles visuel, voir [Création de règles](#write-rules).

### E. Sélecteur des modes éditeur visuel-éditeur de code {#e-visual-code-editors-switcher}

Les utilisateurs et utilisatrices appartenant au groupe des utilisateurs et utilisatrices avancés de formulaires peuvent accéder à l’éditeur de code. L’éditeur de code n’est pas disponible pour les autres utilisateurs et utilisatrices. Si vous disposez des droits, vous pouvez passer du mode éditeur visuel en mode éditeur de code et inversement, à l’aide d’un sélecteur situé au-dessus de l’éditeur de règles. Lorsque vous lancez l’éditeur de règles pour la première fois, il s’ouvre en mode Éditeur visuel. Vous pouvez créer des règles en mode Éditeur visuel ou passer en mode Éditeur de code pour créer un script de règle. Notez toutefois que si vous modifiez une règle ou si vous créez une règle dans l’éditeur de code, vous ne pouvez pas revenir à l’éditeur visuel pour cette règle sauf si vous avez désélectionné l’éditeur de code.

AEM Forms suit le mode Éditeur de règles que vous avez utilisé en dernier pour créer une règle. Lorsque vous lancez l’éditeur de règles la fois suivante, il s’ouvre dans ce mode. Toutefois, vous pouvez également configurer un mode par défaut pour ouvrir l’éditeur de règles dans le mode spécifié. Pour ce faire :

1. Accédez à la console web AEM à l’adresse `https://[host]:[port]/system/console/configMgr`.
1. Cliquez pour modifier **[!UICONTROL Configuration du canal web du formulaire adaptatif et de la communication interactive]**.
1. Sélectionnez **[!UICONTROL Éditeur visuel]** ou **[!UICONTROL Éditeur de code]** dans la liste déroulante **[!UICONTROL Mode par défaut de l&#39;éditeur de règle]**.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

### F. Boutons Terminé et Annuler {#f-done-and-cancel-buttons}

Le bouton **[!UICONTROL Terminé]** permet d’enregistrer une règle. Vous pouvez enregistrer une règle incomplète. Toutefois, les règles incomplètes ne sont pas valides et ne s’exécutent pas. Les règles enregistrées sur un objet de formulaire sont répertoriées lorsque vous lancez l’éditeur de règles la prochaine fois à partir du même objet de formulaire. Vous pouvez gérer des règles existantes dans cette vue. Pour plus d’informations, consultez la section [Gérer les règles](#manage-rules).

Le bouton **[!UICONTROL Annuler]** annule tous les changements apportés à une règle et ferme l’éditeur de règles.

## Règles d’écriture {#write-rules}

Vous pouvez créer des règles à l’aide de l’éditeur de règles visuel ou l’éditeur de code. Lorsque vous lancez l’éditeur de règles pour la première fois, il s’ouvre en mode d’éditeur visuel. Vous pouvez passer au mode d’éditeur de code et créer des règles. Notez toutefois que si vous créez ou modifiez une règle dans l’éditeur de code, vous ne pouvez pas basculer vers l’éditeur visuel pour cette règle sauf si vous avez désélectionné l’éditeur de code. Lorsque vous lancez l’éditeur de règles la fois suivante, il s’ouvre dans le mode que vous avez utilisé en dernier pour créer une règle.

Tout d&#39;abord, examinons l’écriture de règles utilisant l’éditeur visuel.

### À l’aide de l’éditeur visuel {#using-visual-editor}

Examinons comment créer une règle dans l’éditeur visuel en utilisant l’exemple de formulaire suivant.

![create-rule-example](assets/create-rule-example.png)

La section Conditions de prêt dans l’exemple de formulaire de demande de prêt requiert des demandeurs et demandeuses de spécifier leur état civil, leur salaire, leur statut marital et le salaire de leur épouse ou épouse, le cas échéant. D’après les entrées de l’utilisateur ou utilisatrice, la règle permet de calculer le montant d’éligibilité du prêt et l’affiche dans le champ Éligibilité de prêt. Appliquez les règles suivantes pour mettre en œuvre le scénario :

* Le champ Salaire de l’époux ou de l’épouse s’affiche uniquement lorsque la valeur État civil est Marié ou Mariée.
* Le montant d’éligibilité de prêt est de 50 % du salaire total.

Effectuez les étapes suivantes pour créer les règles :

1. Tout d’abord, créez la règle pour contrôler la visibilité du champ Salaire du conjoint en fonction de l’option de l’utilisateur pour le bouton radio État civil.

   Ouvrez le formulaire de demande de prêt en mode Création. Sélectionnez le composant **État civil** et choisissez ![edit-rules](assets/edit-rules.png). Ensuite, sélectionnez **[!UICONTROL Créer]** pour lancer l’éditeur de règles.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Lorsque vous lancez l’éditeur de règles, la règle Lorsque est sélectionnée par défaut. En outre, l’objet de formulaire (dans ce cas, État civil) d’où vous avez lancé l’éditeur de règles est spécifié dans l’instruction Lorsque.

   Bien que vous ne puissiez pas changer ou modifier l’objet sélectionné, vous pouvez utiliser la liste déroulante de règles, comme indiqué ci-dessous, pour sélectionner un autre type de règle. Si vous souhaitez créer une règle sur un autre objet, sélectionnez Annuler pour quitter l’éditeur de règles et relancez-le depuis l’objet de formulaire de votre choix.

1. Sélectionnez le menu déroulant **[!UICONTROL Sélectionner l’état]** et choisissez **[!UICONTROL est égal à]**. Le champ **[!UICONTROL Saisissez une chaîne]** s’affiche.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   Pour le bouton radio État civil, les options **Marié(e)** et **Célibataire** sont définies respectivement sur les valeurs **0** et **1**. Vous pouvez vérifier les valeurs affectées sur l’onglet Titre de la boîte de dialogue Modifier le bouton radio, comme indiqué ci-dessous.

   ![Valeurs de bouton radio dans l’éditeur de règles](assets/radio-button-values.png)

1. Dans le champ **Saisissez une chaîne** dans la règle, indiquez **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Vous avez défini la condition comme `When Marital Status is equal to Married`. Définissez ensuite l’action à effectuer si cette condition est True.

1. Dans l’instruction Alors, sélectionnez **[!UICONTROL Afficher]** dans le menu déroulant **[!UICONTROL Sélectionner une action]**.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Faites glisser et déposez le champ **Salaire du conjoint** de l’onglet Objets de formulaire vers le champ **Déposez l’objet ou sélectionnez ici**. Vous pouvez également sélectionner le champ **Déposer l’objet ou sélectionner ici**, puis le champ **Salaire du conjoint ou de la conjointe** dans le menu contextuel, qui répertorie tous les objets de formulaire dans le formulaire.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   La règle s’affiche comme suit dans l’éditeur de règles.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   Cliquez sur **Terminé** pour enregistrer la règle.

1. Répétez les étapes 1 à 5 pour définir une autre règle pour masquer le champ de salaire du conjoint ou de la conjointe si la valeur de l’état civil est Célibataire. La règle s’affiche comme suit dans l’éditeur de règles.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >Vous pouvez également créer une règle Afficher dans le champ Salaire du conjoint, au lieu de deux règles Lorsque dans le champ État civil pour mettre en œuvre le même comportement.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Ensuite, créez une règle pour calculer le niveau d’éligibilité de prêt, à hauteur de 50 % du salaire total, puis affichez-la dans le champ Éligibilité de prêt. À cet effet, créez des règles **Définir la valeur de** sur le champ Éligibilité de prêt.

   En mode Création, sélectionnez le champ **[!UICONTROL Éligibilité de prêt]**, puis ![edit-rules](assets/edit-rules.png). Ensuite, sélectionnez **[!UICONTROL Créer]** pour lancer l’éditeur de règles.

1. Sélectionnez la règle **[!UICONTROL Définir la valeur de]** dans la liste déroulante des règles.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Choisissez **[!UICONTROL Sélectionner l’option]** et sélectionnez **[!UICONTROL Expression mathématique]**. Un champ permettant de saisir l’expression mathématique s’ouvre.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. Dans le champ d&#39;expression :

   * Sélectionnez ou faites glisser et déposez le champ **Salaire**, de l’onglet Objet de formulaire vers le premier champ **Déposez l’objet ou sélectionnez ici**.

   * Sélectionnez **Plus** dans le champ **Sélectionner un opérateur**.

   * Sélectionnez ou faites glisser et déposez depuis le champ **Salaire du conjoint** de l’onglet Objets de formulaire vers l’autre champ **Déposez l’objet ou sélectionnez ici**.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Ensuite, sélectionnez la zone en surbrillance autour du champ Expression et choisissez **Étendre l’expression**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   Dans le champ d’expression étendue, sélectionnez **divisé par** dans le champ **Sélectionner un opérateur** et **Nombre** dans le champ **Sélectionner une option**. Ensuite, spécifiez **2** dans le champ Nombre.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Vous pouvez créer des expressions complexes à l’aide de composants, fonctions, expressions mathématiques et valeurs de propriété dans le champ Sélectionner une option.

   Créez ensuite une condition qui, lorsqu’elle renvoie True, permet que l’expression s’exécute.

1. Sélectionnez **Ajouter une condition** pour ajouter une instruction Lorsque.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   Dans l’instruction Lorsque :

   * Sélectionnez ou glissez-déposez depuis l’onglet Objets de formulaire le champ **État civil** dans le premier champ **Déposez l’objet ou sélectionnez ici**.

   * Sélectionnez **est égal à** dans le champ **Sélectionner un opérateur**.

   * Sélectionnez Chaîne dans l’autre champ **Déposez l’objet ou sélectionnez ici** et spécifiez **Marié(e)** dans le champ **Saisissez la chaîne**.

   Enfin, la règle s’affiche comme suit dans l’éditeur de règles. ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   Sélectionnez **Terminé** pour enregistrer la règle.

1. Répétez les étapes 7 à 12 pour définir une autre règle pour calculer le montant d’éligibilité si la valeur d’état civil est Célibataire. La règle s’affiche comme suit dans l’éditeur de règles.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>Vous pouvez également utiliser la règle Définir la valeur de pour calculer l’éligibilité de prêt dans la règle Lorsque que vous avez créée pour afficher ou masquer le champ Salaire du conjoint. La règle combinée résultante, lorsque l’état civil est Célibataire, s’affiche comme suit dans l’éditeur de règles.
>
>De même, vous pouvez entrer une règle combinée pour contrôler la visibilité du champ Salaire de l’époux ou de l’épouse lorsque la valeur d&#39;état civil est Marié ou Mariée.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

### À l&#39;aide de l&#39;éditeur de code {#using-code-editor}

Les utilisateurs et utilisatrices ajoutés au groupe des utilisateurs et utilisatrices expérientés de formulaires peuvent utiliser l’éditeur de code. L’éditeur de règles génère automatiquement le code JavaScript pour toute règle que vous créez à l’aide de l’éditeur visuel. Vous pouvez basculer de l&#39;éditeur visuel à l&#39;éditeur de code pour afficher le code généré. Cependant, si vous modifiez le code de règle dans l&#39;éditeur de code, vous ne pouvez pas revenir à l&#39;éditeur visuel. Si vous préférez les règles d’écriture de l’éditeur de code plutôt que celles de l’éditeur visuel, vous avez la possibilité de définir de nouvelles règles dans l’éditeur de code. Le bouton bascule des éditeurs visuel-code vous permet de passer d’un mode à l’autre.

L’éditeur de code JavaScript est le langage d’expression des formulaires adaptatifs. Toutes les expressions sont des expressions JavaScript valides qui utilisent des API de modèle de script pour les formulaires adaptatifs. Ces expressions renvoient des valeurs de certains types. Pour obtenir la liste complète des classes de formulaires adaptatifs, des événements, des objets et des API publiques, consultez [Référence d’API de bibliothèque JavaScript pour les formulaires adaptatifs](https://helpx.adobe.com/fr/experience-manager/6-5/forms/javascript-api/index.html).

Pour plus d’informations sur la création de règles dans l’éditeur de code, reportez-vous à la section [Expressions de formulaire adaptatif](/help/forms/using/adaptive-form-expressions.md).

Lorsque vous écrivez du code en JavaScript dans l’éditeur de règles, les repères visuels suivants vous aident avec la structure et la syntaxe :

* Mise en valeur de la syntaxe
* Mise en retrait automatique
* Conseils et suggestions pour les objets Formulaire, leurs fonctions et leurs propriétés
* Remplissage automatique des noms de composants du formulaire et des fonctions JavaScript courantes

![javascriptruleeditor](assets/javascriptruleeditor.png)

#### Fonctions personnalisées dans l’éditeur de règles {#custom-functions}

Outre les fonctionnalités prêtes à l’emploi, comme *Somme de*, qui sont répertoriées sous Fonctions, vous pouvez créer des fonctions personnalisées dont vous avez besoin fréquemment. Assurez-vous de la présence de la balise `jsdoc` au-dessus de la fonction que vous créez.

La balise `jsdoc` associée est nécessaire :

* Si vous souhaitez personnaliser la configuration et la description.
* Parce qu’il y a plusieurs façons de déclarer une fonction dans`JavaScript,` et que les commentaires permettent de conserver une trace des fonctions.

Pour plus d’informations, voir [usejsdoc.org](https://jsdoc.app/).

Balises `jsdoc` prises en charge :

* Syntaxe
**Privé** : `@private`
Une fonction privée n’est pas incluse comme fonction personnalisée.

* Syntaxe
**Nom** : `@name funcName <Function Name>`
Autrement,`,` vous pouvez utiliser : `@function funcName <Function Name>` **ou** `@func` `funcName <Function Name>`.
  `funcName` est le nom de la fonction (les espaces ne sont pas autorisés).
  `<Function Name>` est le nom d’affichage de la fonction.

* Syntaxe
**Membre** : `@memberof namespace`
Associe un espace de noms à la fonction.

* Syntaxe
**Paramètre** : `@param {type} name <Parameter Description>`
Autrement, vous pouvez utiliser : `@argument` `{type} name <Parameter Description>` **ou** `@arg` `{type}` `name <Parameter Description>`.
Affiche les paramètres utilisés par la fonction. Une fonction peut comporter plusieurs balises de paramètre, une balise pour chaque paramètre dans l’ordre d’occurrence.
  `{type}` représente le type de paramètre. Les types de paramètre sont les suivants :

   1. chaîne
   1. nombre
   1. booléen
   1. portée

  La portée est utilisée pour les champs référents d’un formulaire adaptatif. Lorsqu’un formulaire utilise le chargement différé, vous pouvez utiliser `scope` pour accéder à ses champs. Vous pouvez accéder aux champs lorsque les champs sont chargés ou si les champs sont marqués comme généraux.

  Tous les autres types de paramètre sont classés en dessous de l’un des précédents. Ils sont tous pris en charge. Assurez-vous que vous sélectionnez l’un des types ci-dessus. Les types ne respectent pas la casse. Les espaces ne sont pas autorisés dans le paramètre `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* Syntaxe
**Type de retour** : `@return {type}`
Autrement, vous pouvez utiliser `@returns {type}`.
Ajoute des informations sur la fonction, comme son objectif.
{type} représente le type de valeur renvoyée de la fonction. Les types de valeur renvoyée autorisés sont les suivants :

   1. chaîne
   1. nombre
   1. booléen

  Tous les autres types de retour sont classés en dessous de l’un des précédents. Ils sont tous pris en charge. Assurez-vous que vous sélectionnez l’un des types ci-dessus. Les types de retour ne respectent pas la casse.

* **Cette**
syntaxe : `@this currentComponent`

  Utilisez @this pour faire référence au composant Formulaire adaptatif à partir duquel la règle a été créée.

  L’exemple ci-dessous repose sur la valeur du champ. Dans l’exemple ci-dessous, la règle masque un champ dans le formulaire. La partie `this` de `this.value` fait référence au composant Formulaire adaptatif sous-jacent, à partir duquel la règle a été créée.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

>[!NOTE]
>
>Les commentaires avant la fonction personnalisée sont utilisés pour le résumé. Le résumé peut s’étendre sur plusieurs lignes jusqu’à ce qu’une balise soit rencontrée. Limitez la taille à une seule pour une description concise dans le créateur de règles.

<!--
**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

Perform the following steps to create a client library and add it in the CRX repository.

1. Create a client library. For more information, see [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your adaptive form. It lets you use your custom function as a rule in your form. Perform the following steps to add the client library in your adaptive form.

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **Open**.
1. In the edit mode, select a component, then select ![field-level](assets/field-level.png) &gt; **Adaptive Form Container**, and then select ![cmppr](assets/cmppr.png).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules.png) to open the rule editor.
1. Select **Create Rule**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.
   [ ![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)Select **Done**. Your custom function is added.

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.
-->

Vous pouvez également utiliser des fonctions personnalisées dans votre éditeur de règles. Pour plus d’informations sur la création de fonctions personnalisées, consultez l’article [Fonctions personnalisées dans les formulaires adaptatifs](/help/forms/using/create-and-use-custom-functions.md).

## Gestion des règles {#manage-rules}

Les règles existantes sur un objet de formulaire sont répertoriées lorsque vous sélectionnez l’objet et ![edit-rules1](assets/edit-rules1.png). Vous pouvez afficher le titre et un aperçu du résumé de la règle. En outre, l’interface utilisateur vous permet de développer et d’afficher le résumé complet d’une règle, de changer l’ordre des règles, de les modifier et de les supprimer.

![list-rules](assets/list-rules.png)

Vous pouvez effectuer les actions suivantes sur les règles :

* **Développer/Réduire** : la colonne Contenu dans la liste des règles affiche le contenu des règles. Si le contenu entier des règles n’est pas visible dans l’affichage par défaut, sélectionnez ![expand-rule-content](assets/expand-rule-content.png) pour le développer.

* **Réorganiser** : toute nouvelle règle que vous créez est empilée au bas de la liste des règles. Les règles sont exécutées de haut en bas. La règle en haut s’exécute en premier, suivie des autres règles du même type. Par exemple, si vous avez les règles Lorsque, Afficher, Activer et Lorsque en première, deuxième, troisième et quatrième positions depuis le haut respectivement, la règle Lorsque du haut est exécutée en premier, suivie de la règle Lorsque à la quatrième position. Ensuite, les règles Afficher et Activer seront exécutées.
Vous pouvez modifier l’ordre d’une règle en appuyant sur ![sort-rules](assets/sort-rules.png) en regard ou la faire glisser et la déposer dans l’ordre souhaité dans la liste.

* **Modifier** : pour modifier une règle, cochez la case située en regard du titre de la règle. D’autres options de modification et de suppression de la règle s’affichent. Sélectionnez **Modifier** pour ouvrir la règle sélectionnée dans l’éditeur de règles en mode visuel ou dans l’éditeur de code, selon le mode utilisé pour créer la règle.

* **Supprimer** : pour supprimer une règle, sélectionnez-la puis choisissez **Supprimer**.

* **Activer/Désactiver** : vous devrez peut-être suspendre temporairement l’utilisation d’une règle. Vous pouvez sélectionner une ou plusieurs règles puis choisir Désactiver dans la barre d’outils Actions pour les désactiver. Si une règle est désactivée, elle ne s’exécute pas lors de l’exécution. Pour activer une règle désactivée, vous pouvez la sélectionner puis choisir Activer dans la barre d’outils Actions. La colonne Statut de la règle indique si la règle est activée ou désactivée.

![disablerule](assets/disablerule.png)

## Règles de copier-coller {#copy-paste-rules}

Vous pouvez copier-coller une règle d’un champ à d’autres champs similaires pour gagner du temps.

Pour copier-coller des règles, procédez comme suit :

1. Sélectionnez l’objet de formulaire à partir duquel vous souhaitez copier une règle puis, dans la barre d’outils des composants, sélectionnez ![editrule](assets/editrule.png). L’interface utilisateur de l’éditeur de règles s’affiche avec l’objet de formulaire sélectionné, et les règles existantes s’affichent.

   ![copyrule](assets/copyrule.png)

   Pour plus d’informations sur la gestion des règles existantes, voir [Gestion des règles](#manage-rules).

1. Cochez la case en regard du titre de la règle. D’autres options de gestion des règles s’affichent. Sélectionnez **Copie**.

   ![copyrule2](assets/copyrule2.png)

1. Sélectionnez un autre objet de formulaire dans lequel vous souhaitez coller la règle et choisissez **Coller**. De plus, vous pouvez modifier la règle pour y apporter des modifications.

   >[!NOTE]
   >
   >Vous pouvez coller une règle dans un autre objet de formulaire uniquement si cet objet de formulaire prend en charge les événement de la règle copiée. Par exemple, un bouton prend en charge l’événement Cliquer. Vous pouvez coller une règle avec un événement Cliquer sur un bouton mais pas dans une case à cocher.

1. Sélectionnez **Terminé** pour enregistrer la règle.

## Expressions imbriquées {#nestedexpressions}

L’éditeur de règles vous permet d’utiliser plusieurs opérateurs ET et OU afin de créer des règles imbriquées. Vous pouvez fusionner plusieurs opérateurs ET et OU dans les règles.

Voici un exemple de règle imbriquée qui affiche un message concernant l’éligibilité pour un droit de garde lorsque les conditions nécessaires sont remplies à l’intention de l’utilisateur.

![complexexpression](assets/complexexpression.png)

Vous pouvez également faire glisser et déposer des conditions dans une règle pour la modifier. Appuyez et passez le curseur sur la poignée (![handle](assets/handle.png)) avant une condition. Une fois le pointeur affiché sous forme de main comme illustré ci-dessous, faites glisser la condition et déposez-la n’importe où dans la règle. La structure de la règle change.

![glisser-déposer](assets/drag-and-drop.png)

## Conditions d’expression de date {#dateexpression}

L’éditeur de règles vous permet d’utiliser des comparaisons de dates afin de créer des conditions.

Voici un exemple de condition qui contient un objet de texte statique si le prêt hypothécaire sur la maison est déjà utilisé, ce que l’utilisateur ou l’utilisatrice indique en remplissant le champ de date.

Lorsque la date du prêt hypothécaire de la propriété indiquée par l’utilisateur ou l’utilisatrice est déjà dépassée, le formulaire adaptatif affiche une remarque concernant le calcul des revenus. La règle ci-dessous compare la date indiquée par l’utilisateur à la date actuelle et si la date indiquée par l’utilisateur est antérieure à la date actuelle, le formulaire affiche le message texte (appelé « Revenu »).

![dateexpressioncondition](assets/dateexpressioncondition.png)

Lorsque la date remplie est antérieure à la date actuelle, le formulaire affiche le message texte (Revenu), comme suit :

![dateexpression.condition](assets/dateexpressionconditionmet.png)

## Conditions de comparaison des nombres {#number-comparison-conditions}

L’éditeur de règles vous permet de créer des conditions qui comparent deux nombres.

Voici un exemple de condition qui contient un objet de texte statique si le demandeur habite à son adresse actuelle depuis moins de 36 mois.

![numbercomparisoncondition](assets/numbercomparisoncondition.png)

Lorsque l’utilisateur indique qu’il habite à son adresse résidentielle actuelle depuis moins de 36 mois, le formulaire affiche une notification indiquant qu’un justificatif de domicile supplémentaire peut être demandé.

![additionalproofrequested](assets/additionalproofrequested.png)

## Impact de l’éditeur de règles sur les scripts existants {#impact-of-rule-editor-on-existing-scripts}

Dans les versions AEM Forms antérieures à la version AEM Forms 6.1 Pack 1, les équipes de création et de développement de formulaires créaient des expressions dans l’onglet Script de la boîte de dialogue Modifier le composant pour ajouter un comportement dynamique aux formulaires adaptatifs. L’onglet Scripts est désormais remplacé par l’éditeur de règles.

Tous les scripts ou expressions que vous deviez saisir dans l’onglet Scripts sont disponibles dans l’éditeur de règles. Alors que vous ne pouvez pas les afficher ou les modifier dans l’éditeur visuel, vous pouvez modifier les scripts dans l’éditeur de code si vous appartenez au groupe des utilisateurs avancés de formulaires.

## Exemples de règles {#example}

### Appeler le service de modèle de données de formulaire {#invoke}

Imaginons un service Web `GetInterestRates` prenant le montant du prêt, la durée et la cote de solvabilité du demandeur comme valeurs d’entrée et renvoyant un plan de prêt incluant le montant des mensualités et le taux d’intérêt. Créez un modèle de données de formulaire en utilisant le service Web comme source de données. Ajoutez des objets de modèle de données et un service `get` au modèle de formulaire. Le service s’affiche sur l’onglet Services du modèle de données de formulaire. Ensuite, créez un formulaire adaptatif incluant des champs des objets de modèle de données pour capturer les données saisies par l’utilisateur ou l’utilisatrice pour le montant et la durée du prêt et la cote de solvabilité. Ajoutez un bouton qui demande au service web d’extraire les détails du plan. La sortie est renseignée dans les champs appropriés.

La règle suivante indique comment configurer l’action Appel du service pour accomplir l’exemple de scénario.

![example-invoke-services](assets/example-invoke-services.png)

Appeler le service de modèle de données de formulaire à l’aide d’une règle de formulaire adaptatif

>[!NOTE]
>
>Si l’entrée est de type tableau, les champs qui prennent en charge les tableaux sont visibles dans la section déroulante Sortie.

### Déclenchement de plusieurs actions à l’aide de la règle Lorsque {#triggering-multiple-actions-using-the-when-rule}

Dans un formulaire de demande de prêt, vous voulez savoir si la personne demandant le prêt est un client ou une cliente existante ou non. En fonction des informations fournies par l’utilisateur ou l’utilisatrice, le champ ID du client ou de la cliente doit s’afficher ou se masquer. En outre, vous souhaitez placer le focus sur le champ d’ID de client ou cliente si l’utilisateur ou l’utilisatrice est un client ou une cliente existant. Le formulaire de demande de prêt est composé des éléments suivants :

* Un bouton radio,**Êtes-vous déjà client(e) chez Geometrixx ?**, qui propose les options Oui et Non. La valeur Oui est **0** ; la valeur Non est **1**.

* Un champ de texte, **ID de client Geometrixx**, pour indiquer l’ID du client ou de la cliente.

Lorsque vous entrez une règle Lorsque sur le bouton radio pour implémenter ce comportement, la règle s’affiche comme suit dans l’éditeur de règles visuel. ![when-rule-example](assets/when-rule-example.png)

Règle dans l’éditeur visuel

Dans l’exemple de règle, l’instruction suivante dans la section Lorsque est la condition qui, si elle renvoie True, exécute les actions spécifiées dans la section Alors.

La règle s’affiche comme suit dans l’éditeur de code.

![when-rule-example-code](assets/when-rule-example-code.png)

Règle dans l’éditeur de code

### Utilisation d’une sortie de fonction dans une règle {#using-a-function-output-in-a-rule}

Dans un formulaire de bon de commande, vous avez le tableau suivant, dans lequel les utilisateurs et les utilisatrices rempliront leurs commandes. Dans ce tableau :

* La première ligne est répétable, de sorte que les utilisateurs et utilisatrices puissent commander plusieurs produits et spécifier différentes quantités. Son nom d’élément est `Row1`.
* Le titre de la cellule dans la colonne Quantité de produit de la ligne répétable est Quantité. Le nom de l’élément pour cette cellule est `productquantity`.
* La deuxième ligne du tableau est non répétable, et le titre de la cellule dans la colonne Quantité de produit sur cette ligne est Quantité totale.

![example-function-table](assets/example-function-table.png)

**A.** Ligne 1 **B.** Quantité **C.** Quantité totale

Maintenant, vous souhaitez ajouter des quantités spécifiées dans la colonne Quantité de produit pour tous les produits et afficher la somme dans la cellule Quantité totale. Vous pouvez obtenir ce résultat en saisissant une règle Définir la valeur de sur la cellule Quantité totale, comme illustré ci-dessous.

![example-function-output](assets/example-function-output.png)

Règle dans l’éditeur visuel

La règle s’affiche comme suit dans l’éditeur de code.

![example-function-output-code](assets/example-function-output-code.png)

Règle dans l’éditeur de code

### Validation d’une valeur de champ à l’aide d’une expression {#validating-a-field-value-using-expression}

Dans le formulaire de bon de commande décrit dans l’exemple précédent, vous souhaitez empêcher l’utilisateur de commander plus d’une quantité d’un produit dont le prix est supérieur à 10 000. Pour ce faire, vous pouvez rédiger pour une règle Valider comme illustré ci-dessous.

![example-validate](assets/example-validate.png)

Règle dans l’éditeur visuel

La règle s’affiche comme suit dans l’éditeur de code.

![example-validate-code](assets/example-validate-code.png)

Règle dans l’éditeur de code
