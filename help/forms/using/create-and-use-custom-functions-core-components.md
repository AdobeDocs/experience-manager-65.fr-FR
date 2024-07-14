---
title: Création et ajout de fonctions personnalisées dans un formulaire adaptatif
description: AEM Forms prend en charge les fonctions personnalisées qui permettent aux utilisateurs de créer et d’utiliser leurs propres fonctions dans l’éditeur de règles.
keywords: Ajoutez une fonction personnalisée, utilisez une fonction personnalisée, créez une fonction personnalisée, utilisez une fonction personnalisée dans l’éditeur de règles.
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 5%

---

# Fonctions personnalisées dans les composants principaux de Forms adaptatif

Cet article décrit la création de fonctions personnalisées avec le dernier composant principal de formulaire adaptatif, qui comporte les dernières fonctionnalités telles que :

* Fonction de mise en cache des fonctions personnalisées
* Prise en charge des objets de champ et d’objet de portée globale pour les fonctions personnalisées
* Prise en charge des fonctionnalités JavaScript modernes telles que les fonctions de gauche et de flèche (prise en charge ES10)

Veillez à définir la [dernière version de formulaire](https://github.com/adobe/aem-core-forms-components/tree/release/650) sur votre environnement de composant principal AEM Forms pour utiliser les dernières fonctionnalités des fonctions personnalisées. </span>


| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM 6.5 | Cet article |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## Présentation

AEM Forms 6.5 comprend des fonctions JavaScript qui vous permettent de définir des règles métier complexes à l’aide de l’éditeur de règles. Bien qu’AEM Forms offre une variété de fonctions personnalisées d’usine, de nombreux cas d’utilisation nécessitent la définition de vos propres fonctions personnalisées à utiliser dans plusieurs formulaires. Ces fonctions personnalisées améliorent les fonctionnalités des formulaires en permettant la manipulation et le traitement des données saisies pour répondre à des besoins spécifiques. En outre, elles permettent une modification dynamique du comportement du formulaire en fonction de critères prédéfinis.

### Utilisation de fonctions personnalisées {#uses-of-custom-function}

Les avantages des fonctions personnalisées dans les composants principaux de Forms adaptatif sont les suivants :


* **Gestion des données** : les fonctions personnalisées gèrent et traitent les données saisies dans les champs de formulaires.
* **Traitement des données** : les fonctions personnalisées aident à traiter les données saisies dans les champs de formulaires.
* **Validation des données** : les fonctions personnalisées vous permettent d’effectuer des vérifications personnalisées sur les entrées de formulaire et de fournir des messages d’erreur spécifiés.
* **Comportement dynamique** : les fonctions personnalisées vous permettent de contrôler le comportement dynamique de vos formulaires en fonction de conditions spécifiques. Vous pouvez, par exemple, afficher/masquer des champs, modifier les valeurs de champ ou ajuster dynamiquement la logique du formulaire.
* **Intégration** : vous pouvez utiliser des fonctions personnalisées pour intégrer des API ou des services externes. Il permet de récupérer des données provenant de sources externes, d’envoyer des données à des points de terminaison Rest externes ou d’effectuer des actions personnalisées basées sur des événements externes.

Les fonctions personnalisées sont essentiellement des bibliothèques clientes ajoutées dans le fichier JavaScript. Une fois que vous avez créé une fonction personnalisée, elle est disponible dans l’éditeur de règles et peut être sélectionnée par l’utilisateur dans un formulaire adaptatif. Les fonctions personnalisées sont identifiées par les annotations JavaScript dans l’éditeur de règles.

### Annotations JavaScript prises en charge pour la fonction personnalisée {#js-annotations}

**Les annotations JavaScript fournissent des métadonnées pour le code JavaScript**. Il comprend des commentaires commençant par des symboles spécifiques, par exemple `/**` et `@`. Les annotations fournissent des informations importantes sur les fonctions, variables et autres éléments du code. Le formulaire adaptatif prend en charge les annotations JavaScript suivantes pour les fonctions personnalisées :

#### Nom

**Name** est utilisé pour identifier la fonction personnalisée dans l’éditeur de règles d’un formulaire adaptatif. Les syntaxes suivantes sont utilisées pour nommer une fonction personnalisée :

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` est le nom de la fonction. Les espaces ne sont pas autorisés.
>`<Function Name>` est le nom d’affichage de la fonction dans l’éditeur de règles d’Adaptive Forms.
>Si le nom de la fonction est identique au nom de la fonction elle-même, vous pouvez omettre `[functionName]` dans la syntaxe .

#### Paramètre

**Paramètre** est une liste d’arguments utilisés par des fonctions personnalisées. Une fonction peut prendre en charge plusieurs paramètres. Les syntaxes suivantes sont utilisées pour définir un paramètre dans une fonction personnalisée :

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` représente le type de paramètre. Les types de paramètres autorisés sont les suivants :

   * string : représente une seule valeur de chaîne.
   * number : représente une seule valeur numérique.
   * boolean : représente une seule valeur booléenne (true ou false).
   * string[] : représente un tableau de valeurs de chaîne.
   * number[] : représente un tableau de valeurs numériques.
   * boolean[] : représente un tableau de valeurs booléennes.
   * date : représente une seule valeur de date.
   * date[] : représente un tableau de valeurs de date.
   * array : représente un tableau générique contenant des valeurs de différents types.
   * object : représente l’objet de formulaire transmis à une fonction personnalisée au lieu de transmettre directement sa valeur.
   * scope : représente l’objet global, qui contient des variables en lecture seule telles que des instances de formulaire, des instances de champ cible et des méthodes permettant d’effectuer des modifications dans les fonctions personnalisées. Il est déclaré comme dernier paramètre dans les annotations JavaScript et n’est pas visible par l’éditeur de règles d’un formulaire adaptatif. Le paramètre scope accède à l’objet du formulaire ou du composant pour déclencher la règle ou l’événement requis pour le traitement du formulaire. Pour plus d’informations sur l’objet Globals et comment l’utiliser, [cliquez ici](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

Le type de paramètre est **non sensible à la casse** et les espaces ne sont pas autorisés dans le nom du paramètre.

`<Parameter Description>` contient des détails sur l’objectif du paramètre. Il peut avoir plusieurs mots.

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### Type de retour

Le type de retour spécifie le type de valeur que la fonction personnalisée renvoie après l’exécution. Les syntaxes suivantes sont utilisées pour définir un type de retour dans une fonction personnalisée :

* `@return {type}`
* `@returns {type}`
  `{type}` représente le type de retour de la fonction. Les types de retour autorisés sont les suivants :
* string : représente une seule valeur de chaîne.
* number : représente une seule valeur numérique.
* boolean : représente une seule valeur booléenne (true ou false).
* string[] : représente un tableau de valeurs de chaîne.
* number[] : représente un tableau de valeurs numériques.
* boolean[] : représente un tableau de valeurs booléennes.
* date : représente une seule valeur de date.
* date[] : représente un tableau de valeurs de date.
* array : représente un tableau générique contenant des valeurs de différents types.
* object : représente l’objet de formulaire au lieu de sa valeur directement.

Le type de retour n’est pas sensible à la casse.

#### Privée

La fonction personnalisée, déclarée comme privée, n’apparaît pas dans la liste des fonctions personnalisées de l’éditeur de règles d’un formulaire adaptatif. Par défaut, les fonctions personnalisées sont publiques. La syntaxe pour déclarer une fonction personnalisée en tant que privée est `@private`.

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

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
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

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
-->

## Instructions relatives à la création de fonctions personnalisées {#considerations}

Pour répertorier les fonctions personnalisées dans l’éditeur de règles, vous pouvez utiliser l’un des formats suivants :

### Instruction de fonction avec ou sans commentaires jsdoc

Vous pouvez créer une fonction personnalisée avec ou sans commentaires jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

Si l’utilisateur n’ajoute aucune annotation JavaScript à la fonction personnalisée, elle est répertoriée dans l’éditeur de règles par son nom de fonction. Toutefois, il est recommandé d’inclure des annotations JavaScript pour améliorer la lisibilité des fonctions personnalisées.


### Fonction Flèche avec annotations ou commentaire JavaScript obligatoires

Vous pouvez créer une fonction personnalisée à l’aide d’une syntaxe de fonction de flèche :

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Si l’utilisateur n’ajoute aucune annotation JavaScript à la fonction personnalisée, celle-ci n’est pas répertoriée dans l’éditeur de règles d’un formulaire adaptatif.

### Expression de fonction avec annotations ou commentaire JavaScript obligatoires

Pour répertorier les fonctions personnalisées dans l’éditeur de règles d’un formulaire adaptatif, créez des fonctions personnalisées au format suivant :

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Si l’utilisateur n’ajoute aucune annotation JavaScript à la fonction personnalisée, celle-ci n’est pas répertoriée dans l’éditeur de règles d’un formulaire adaptatif.

### Conditions préalables à la création d’une fonction personnalisée

Avant de commencer à ajouter une fonction personnalisée à votre Forms adaptatif, assurez-vous que les logiciels suivants sont installés sur votre ordinateur :

* **Éditeur de texte brut (IDE)** : bien que tout éditeur de texte brut puisse fonctionner, un environnement de développement intégré (IDE) comme Microsoft Visual Studio Code offre des fonctionnalités avancées pour faciliter la modification.

* **Git :** Ce système de contrôle de version est nécessaire pour gérer les modifications de code. Si vous ne l’avez pas installé, téléchargez-le à partir de https://git-scm.com.


## Créer une fonction personnalisée {#create-custom-function}

Les étapes de création de fonctions personnalisées sont les suivantes :
1. [Créez une bibliothèque côté client à l’aide de l’archétype de projet AEM et ajoutez une fonction personnalisée](#create-client-library-archetype)
OU
   [Créer des fonctions personnalisées via CRXDE](#create-add-custom-function)
1. [Ajout d’une bibliothèque cliente à un formulaire adaptatif](#add-client-library)
1. [Utilisation d’une fonction personnalisée dans un formulaire adaptatif](#use-custom-functions)


### Création d’une bibliothèque cliente à l’aide de l’archétype de projet AEM{#create-client-library-archetype}

Vous pouvez ajouter des fonctions personnalisées en ajoutant une bibliothèque cliente au projet créé [à l’aide de l’ archétype de projet AEM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using#getting-started).
Si vous disposez d’un projet <!--and have already the project structure as shown in the image below,-->, vous pouvez directement ajouter des [fonctions personnalisées](#create-add-custom-function) à votre projet local.

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

Après avoir créé un projet Archetype ou utilisé un projet existant, créez une bibliothèque cliente. Pour créer une bibliothèque cliente, procédez comme suit :

**Ajouter un dossier de bibliothèque cliente**

Pour ajouter un nouveau dossier de bibliothèques clientes à votre [répertoire de projet AEM], procédez comme suit :

1. Ouvrez le [répertoire AEM projet] dans un éditeur.

   ![Structure de dossier de fonctions personnalisées](assets/custom-library-folder-structure.png)

1. Recherchez `ui.apps`.
1. Ajoutez un nouveau dossier. Par exemple, ajoutez un dossier nommé `experience-league`.
1. Accédez au dossier `/experience-league/` et ajoutez un dossier `ClientLibraryFolder`. Par exemple, créez un dossier de bibliothèques clientes nommé `customclientlibs`.

   L’emplacement est : `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Ajouter des fichiers et des dossiers au dossier de bibliothèque cliente**

Ajoutez ce qui suit au dossier de bibliothèque cliente ajouté :

* `.content.xml` approuvé
* `js.txt` approuvé
* dossier `js`

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Dans le `.content.xml`, ajoutez les lignes de code suivantes :

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Vous pouvez choisir n’importe quel nom pour les propriétés `client library folder` et `categories`.

1. Dans le `js.txt`, ajoutez les lignes de code suivantes :

   ```javascript
         #base=js
       function.js
   ```

1. Dans le dossier `js`, ajoutez le fichier javascript `function.js` qui comprend les fonctions personnalisées :

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. Enregistrez les fichiers.

![Structure de dossier de fonctions personnalisées](assets/custom-function-added-files.png)

**Inclure le nouveau dossier dans filter.xml** :

1. Accédez au fichier `/ui.apps/src/main/content/META-INF/vault/filter.xml` dans votre [ répertoire de projet AEMaaCS].

1. Ouvrez le fichier et ajoutez la ligne suivante à la fin :

   `<filter root="/apps/experience-league" />`
1. Enregistrez le fichier.

   ![filtre de fonction personnalisé xml](assets/custom-function-filterxml.png)

1. Créez le dossier de bibliothèques clientes nouvellement créé dans votre environnement AEM en suivant les étapes décrites dans la section [Comment créer une section](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build).

## Création et déploiement de fonctions personnalisées via CRXDE{#create-add-custom-function}

Si vous utilisez le dernier module complémentaire AEM Forms et Forms, vous pouvez créer une fonction personnalisée via CRXDE pour utiliser les dernières mises à jour des fonctions personnalisées. Pour ce faire, procédez comme suit :

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. Connectez-vous à `http://server:port/crx/de/index.jsp#`.
1. Créez un dossier sous le dossier `/apps`. Par exemple, créez un dossier nommé `experience-league`.
1. Enregistrez vos modifications.
1. Accédez au dossier créé et créez un noeud de type `cq:ClientLibraryFolder` sous `clientlibs`.
1. Accédez au dossier `clientlibs` nouvellement créé et ajoutez les propriétés `allowProxy` et `categories` :

   ![Propriétés du nœud de bibliothèque personnalisée](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > Vous pouvez utiliser le nom de votre choix à la place de `customfunctionsdemo`.

1. Enregistrez vos modifications.

1. Créez un dossier appelé `js` sous le dossier `clientlibs`.
1. Créez un fichier JavaScript appelé `functions.js` sous le dossier `js`.
1. Créez un fichier appelé `js.txt` sous le dossier `clientlibs`.
1. Enregistrez vos modifications.
La structure de dossiers créée ressemble à ce qui suit :

   ![Structure de dossier de bibliothèque cliente créée](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Double-cliquez sur le fichier `functions.js` pour ouvrir l’éditeur. Le fichier comprend le code de la fonction personnalisée.
Ajoutons le code suivant au fichier JavaScript pour calculer l’âge en fonction de la date de naissance (AAAA-MM-JJ).

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. Enregistrez `function.js`.
1. Accédez à `js.txt` et ajoutez le code suivant :

   ```javascript
       #base=js
       functions.js
   ```

1. Enregistrez le fichier `js.txt`.

Vous pouvez vous référer au dossier [custom function](/help/forms/using/assets/customfunction.zip) suivant. Téléchargez et installez ce dossier sur votre instance AEM.

Désormais, vous pouvez utiliser la fonction personnalisée dans votre formulaire adaptatif en ajoutant la bibliothèque cliente.

## Ajout d’une bibliothèque cliente dans un formulaire adaptatif{#add-client-library}

Une fois que vous avez déployé votre bibliothèque cliente dans votre environnement AEM Forms, utilisez ses fonctionnalités dans votre formulaire adaptatif. Pour ajouter la bibliothèque cliente dans votre formulaire adaptatif

1. Ouvrez votre formulaire en mode d’édition. Pour ouvrir un formulaire en mode d’édition, sélectionnez un formulaire et choisissez **[!UICONTROL Modifier]**.
1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** de votre formulaire adaptatif.
1. Cliquez sur l’icône Propriétés du conteneur de guide . La fenêtre du conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez l’onglet **[!UICONTROL Basic]** et sélectionnez le nom de la **[!UICONTROL catégorie de bibliothèque cliente]** dans la liste déroulante (dans ce cas, sélectionnez `customfunctionscategory`).

   ![Ajout de la bibliothèque cliente de fonction personnalisée](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Cliquez sur **[!UICONTROL Terminé]**.

Vous pouvez maintenant créer une règle pour utiliser des fonctions personnalisées dans l’éditeur de règles :

![Ajout de la bibliothèque cliente de fonction personnalisée](/help/forms/using//assets/calculateage-customfunction.png)

Maintenant, comprenons comment configurer et utiliser une fonction personnalisée à l’aide du [service d’appel de l’éditeur de règles dans AEM Forms 6.5](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)

## Utilisation d’une fonction personnalisée dans un formulaire adaptatif {#use-custom-functions}

Dans un formulaire adaptatif, vous pouvez utiliser des [fonctions personnalisées dans l’éditeur de règles](/help/forms/using/rule-editor-core-components.md).
Ajoutons le code suivant au fichier JavaScript (`Function.js`) pour calculer l’âge en fonction de la date de naissance (AAAA-MM-JJ). Créez une fonction personnalisée `calculateAge()` qui prend la date de naissance comme entrée et renvoie l’âge :

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

Dans l’exemple ci-dessus, lorsque l’utilisateur saisit la date de naissance au format (AAAA-MM-JJ), la fonction personnalisée `calculateAge` est appelée et renvoie l’âge.

![Fonction personnalisée Calculate Age dans l’éditeur de règles](/help/forms/using/assets/custom-function-calculate-age.png)

Prévisualisons le formulaire pour observer comment les fonctions personnalisées sont implémentées par le biais de l’éditeur de règles :

![Fonction personnalisée Calcul de l’âge dans l’aperçu de formulaire de l’éditeur de règles](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Vous pouvez vous référer au dossier [custom features](/help/forms/using/assets/customfunctions.zip) suivant. Téléchargez et installez ce dossier dans votre instance AEM à l’aide du [Gestionnaire de modules](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager).

### Prise en charge des fonctions asynchrones dans les fonctions personnalisées {#support-of-async-functions}

Les fonctions personnalisées asynchrones n’apparaissent pas dans la liste de l’éditeur de règles. Cependant, il est possible d’appeler des fonctions asynchrones dans des fonctions personnalisées créées à l’aide d’expressions de fonction synchrones.

![Fonction personnalisée de synchronisation et asynchrone](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> L’avantage de l’appel de fonctions asynchrones dans les fonctions personnalisées est que les fonctions asynchrones permettent l’exécution simultanée de plusieurs tâches, avec le résultat de chaque fonction utilisée dans les fonctions personnalisées.

Consultez le code ci-dessous pour découvrir comment nous pouvons appeler des fonctions asynchrones à l’aide de fonctions personnalisées :

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

Dans l’exemple ci-dessus, la fonction asyncFunction est `asynchronous function`. Il effectue une opération asynchrone en effectuant une requête `GET` vers `https://petstore.swagger.io/v2/store/inventory`. Il attend la réponse à l’aide de `await`, analyse le corps de la réponse en tant que JSON à l’aide de `response.json()`, puis renvoie les données. La fonction `callAsyncFunction` est une fonction personnalisée synchrone qui appelle la fonction `asyncFunction` et affiche les données de réponse dans la console. Bien que la fonction `callAsyncFunction` soit synchrone, elle appelle la fonction asynchrone asyncFunction et gère son résultat avec des instructions `then` et `catch`.

Pour en voir le fonctionnement, nous allons ajouter un bouton et créer une règle pour le bouton qui appelle la fonction asynchrone lors d’un clic sur un bouton.

![création d’une règle pour la fonction asynchrone](/help/forms/using/assets/rule-for-async-funct.png)

Reportez-vous à l’illustration de la fenêtre de console ci-dessous pour démontrer que lorsque l’utilisateur clique sur le bouton `Fetch`, la fonction personnalisée `callAsyncFunction` est appelée, ce qui à son tour appelle une fonction asynchrone `asyncFunction`. Inspect dans la fenêtre de la console pour afficher la réponse lorsque vous cliquez sur le bouton :

![Fenêtre de console](/help/forms/using/assets/async-custom-funct-console.png)

Explorons les fonctionnalités des fonctions personnalisées.

## Diverses fonctionnalités des fonctions personnalisées

Vous pouvez utiliser des fonctions personnalisées pour ajouter des fonctions personnalisées aux formulaires. Ces fonctions prennent en charge diverses fonctionnalités, telles que l’utilisation de champs spécifiques, l’utilisation de champs globaux ou la mise en cache. Cette flexibilité vous permet de personnaliser les formulaires en fonction des besoins de votre entreprise.

### Objets de champ et de portée globale dans les fonctions personnalisées {#support-field-and-global-objects}

Les objets de champ font référence aux composants ou éléments individuels d’un formulaire, tels que les champs de texte et les cases à cocher. L’objet Globals contient des variables en lecture seule, telles que l’instance de formulaire, l’instance de champ cible et des méthodes permettant de modifier le formulaire dans des fonctions personnalisées.

>[!NOTE]
>
> `param {scope} globals` doit être le dernier paramètre et il ne s’affiche pas dans l’éditeur de règles d’un formulaire adaptatif.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Découvrez comment les fonctions personnalisées utilisent des objets de champ et globaux à l’aide d’un formulaire `Contact Us` utilisant différents cas d’utilisation.

![Formulaire de contact](/help/forms/using/assets/contact-us-form.png)

#### **Cas d’utilisation** : afficher un panneau à l’aide de la règle `SetProperty`

Ajoutez le code suivant dans la fonction personnalisée, comme expliqué dans la section [create-custom-function](#create-custom-function), pour définir le champ de formulaire comme `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * Vous pouvez configurer les propriétés de champ à l’aide des propriétés disponibles situées dans `[form-path]/jcr:content/guideContainer.model.json`.
> * Les modifications apportées au formulaire à l’aide de la méthode `setProperty` de l’objet Globals sont de nature asynchrone et ne sont pas reflétées lors de l’exécution de la fonction personnalisée.

Dans cet exemple, la validation du panneau `personaldetails` se produit lorsque vous cliquez sur le bouton. Si aucune erreur n’est détectée dans le panneau, un autre panneau, le panneau `feedback`, devient visible lorsque l’utilisateur clique sur le bouton.

Créez une règle pour le bouton `Next` , qui valide le panneau `personaldetails` et rend le panneau `feedback` visible lorsque l’utilisateur clique sur le bouton `Next`.

![Définir la propriété](/help/forms/using/assets/custom-function-set-property.png)

Reportez-vous à l’illustration ci-dessous pour démontrer où le panneau `personaldetails` est validé en cliquant sur le bouton `Next`. Si tous les champs de `personaldetails` sont validés, le panneau `feedback` devient visible.

![Définir l’aperçu du formulaire de propriété](/help/forms/using/assets/set-property-form-preview.png)

Si des erreurs sont présentes dans les champs du panneau `personaldetails`, elles s’affichent au niveau du champ lorsque vous cliquez sur le bouton `Next` et le panneau `feedback` reste invisible.

![Définir l’aperçu du formulaire de propriété](/help/forms/using/assets/set-property-panel.png)

#### **Cas d’utilisation** : validez le champ.

Ajoutez le code suivant dans la fonction personnalisée, comme expliqué dans la section [create-custom-function](#create-custom-function) , pour valider le champ.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Si aucun argument n’est transmis dans la fonction `validate()`, le formulaire est validé.

Dans cet exemple, un modèle de validation personnalisé est appliqué au champ `contact`. Les utilisateurs doivent saisir un numéro de téléphone commençant par `10` suivi de `8` chiffres. Si l’utilisateur saisit un numéro de téléphone qui ne commence pas par `10` ou qui contient plus ou moins de `8` chiffres, un message d’erreur de validation s’affiche lorsque l’utilisateur clique sur le bouton :

![Modèle de validation d’adresse de courriel](/help/forms/using/assets/custom-function-validation-pattern.png)

L’étape suivante consiste à créer une règle pour le bouton `Next` qui valide le champ `contact` sur le bouton de clic.

![Modèle de validation](/help/forms/using/assets/custom-function-validate.png)

Reportez-vous à l’illustration ci-dessous pour démontrer que si l’utilisateur saisit un numéro de téléphone qui ne commence pas par `10`, un message d’erreur s’affiche au niveau du champ :

![Modèle de validation d’adresse de courriel](/help/forms/using/assets/custom-function-validate-error-message.png)

Si l’utilisateur saisit un numéro de téléphone valide et que tous les champs du panneau `personaldetails` sont validés, le panneau `feedback` s’affiche à l’écran :

![Modèle de validation d’adresse de courriel](/help/forms/using/assets/validate-form-preview-form.png)

#### **Cas d’utilisation** : réinitialisation d’un panneau

Ajoutez le code suivant dans la fonction personnalisée, comme expliqué dans la section [create-custom-function](#create-custom-function) , pour réinitialiser le panneau.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Si aucun argument n’est transmis dans la fonction `reset()`, le formulaire est validé.

Dans cet exemple, le panneau `personaldetails` se réinitialise lorsque vous cliquez sur le bouton `Clear` . L’étape suivante consiste à créer une règle pour le bouton `Clear` qui réinitialise le panneau sur le bouton de clic.

![Bouton Effacer](/help/forms/using/assets/custom-function-reset-field.png)

Consultez l’illustration ci-dessous pour afficher que si l’utilisateur clique sur le bouton `clear`, le panneau `personaldetails` réinitialise :

![Réinitialiser le formulaire](assets/custom-function-reset-form.png)

#### **Cas d’utilisation** : pour afficher un message personnalisé au niveau du champ et marquer le champ comme non valide

Vous pouvez utiliser la fonction `markFieldAsInvalid()` pour définir un champ comme non valide et définir un message d’erreur personnalisé au niveau du champ. La valeur `fieldIdentifier` peut être `fieldId`, `field qualifiedName` ou `field dataRef`. La valeur de l’objet nommé `option` peut être `{useId: true}`, `{useQualifiedName: true}` ou `{useDataRef: true}`.
Les syntaxes utilisées pour marquer le champ comme non valide et définir un message personnalisé sont les suivantes :

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Ajoutez le code suivant dans la fonction personnalisée, comme expliqué dans la section [create-custom-function](#create-custom-function), pour activer le message personnalisé au niveau du champ.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

Dans cet exemple, si l’utilisateur saisit moins de 15 caractères dans la zone de texte des commentaires, un message personnalisé s’affiche au niveau du champ.

L’étape suivante consiste à créer une règle pour le champ `comments` :

![Marquer le champ comme non valide](/help/forms/using/assets/custom-function-invalid-field.png)

Voir la démonstration ci-dessous pour afficher que la saisie de commentaires négatifs dans le champ `comments` déclenche l’affichage d’un message personnalisé au niveau du champ :

![Marquer le champ comme formulaire d’aperçu non valide](/help/forms/using/assets/custom-function-invalidfield-form.png)

Si l’utilisateur saisit plus de 15 caractères dans la zone de texte des commentaires, le champ est validé et le formulaire est envoyé :

![Marquer le champ comme formulaire d’aperçu valide](/help/forms/using/assets/custom-function-validfield-form.png)


#### **Cas d’utilisation** : envoi de données modifiées au serveur

La ligne de code suivante :
`globals.functions.submitForm(globals.functions.exportData(), false);` est utilisé pour envoyer les données de formulaire après la manipulation.
* Le premier argument est celui des données à soumettre.
* Le deuxième argument indique si le formulaire doit être validé avant envoi. Il est `optional` et est défini sur `true` par défaut.
* Le troisième argument est le `contentType` de l’envoi, qui est également facultatif avec la valeur par défaut `multipart/form-data`. Les autres valeurs peuvent être `application/json` et `application/x-www-form-urlencoded`.

Ajoutez le code suivant dans la fonction personnalisée, comme expliqué dans la section [create-custom-function](#create-custom-function) , pour envoyer les données manipulées sur le serveur :

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

Dans cet exemple, si l’utilisateur laisse la zone de texte `comments` vide, `NA` est envoyé au serveur lors de l’envoi du formulaire.

Créez maintenant une règle pour le bouton `Submit` qui envoie les données :

![Envoi de données](/help/forms/using/assets/custom-function-submit-data.png)

Reportez-vous à l’illustration de `console window` ci-dessous pour démontrer que si l’utilisateur laisse la zone de texte `comments` vide, la valeur `NA` est envoyée au serveur :

![Envoi de données dans la fenêtre de console](/help/forms/using/assets/custom-function-submit-data-form.png)

Vous pouvez également vérifier la fenêtre de la console pour visualiser les données envoyées au serveur :

![Données Inspect dans la fenêtre de console](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## Prise en charge de la mise en cache d’une fonction personnalisée

Les Forms adaptatives implémentent la mise en cache pour les fonctions personnalisées afin d’améliorer le temps de réponse lors de la récupération de la liste des fonctions personnalisées dans l’éditeur de règles. Un message tel que `Fetched following custom functions list from cache` apparaît dans le fichier `error.log`.

![fonction personnalisée avec prise en charge du cache](/help/forms/using/assets/custom-function-cache-error.png)

Si les fonctions personnalisées sont modifiées, la mise en cache est invalidée et elle est analysée.

## Résolution des problèmes {#troubleshooting}

* L’utilisateur doit s’assurer que la version [du composant principal et de la spécification est définie sur la dernière version](https://github.com/adobe/aem-core-forms-components/tree/release/650). Toutefois, pour les projets et formulaires AEM existants, d’autres étapes sont à suivre :

   * Pour le projet AEM, l’utilisateur doit remplacer toutes les instances de `submitForm('custom:submitSuccess', 'custom:submitError')` par `submitForm()` et déployer le projet.

   * Pour les formulaires existants, si les gestionnaires d’envoi personnalisés ne fonctionnent pas correctement, l’utilisateur doit ouvrir et enregistrer la règle `submitForm` sur le bouton **Envoyer** à l’aide de l’éditeur de règles. Cette action remplace la règle existante de `submitForm('custom:submitSuccess', 'custom:submitError')` par `submitForm()` dans le formulaire.


* Si le fichier JavaScript contenant du code pour les fonctions personnalisées comporte une erreur, les fonctions personnalisées ne sont pas répertoriées dans l’éditeur de règles d’un formulaire adaptatif. Pour vérifier la liste des fonctions personnalisées, vous pouvez accéder au fichier `error.log` correspondant à l’erreur. En cas d’erreur, la liste des fonctions personnalisées apparaît vide :

  ![fichier journal d’erreur](/help/forms/using/assets/custom-function-list-error-file.png)

  En l’absence d’erreur, la fonction personnalisée est récupérée et apparaît dans le fichier `error.log`. Un message sous la forme `Fetched following custom functions list` apparaît dans le fichier `error.log` :

  ![ fichier journal d&#39;erreur avec fonction personnalisée appropriée](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## Considérations

* `parameter type` et `return type` ne prennent pas en charge `None`.

* Les fonctions qui ne sont pas prises en charge dans la liste des fonctions personnalisées sont les suivantes :
   * Fonctions du générateur
   * Fonctions asynchrones/attendues
   * Définitions des méthodes
   * Méthodes de classe
   * Paramètres par défaut
   * Paramètres REST
