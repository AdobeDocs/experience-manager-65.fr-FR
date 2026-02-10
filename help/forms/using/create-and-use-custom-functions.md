---
title: Création et ajout de fonctions personnalisées dans un formulaire adaptatif
description: AEM Forms prend en charge les fonctions personnalisées qui permettent aux utilisateurs et utilisatrices de créer et d’utiliser leurs propres fonctions dans l’éditeur de règles.
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
exl-id: 14a52bc1-c1b4-4a12-b8e1-54523e5f30bd
source-git-commit: a0ef9925d1bcb84ea5bf733221875d0322cc6df1
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 96%

---

# Fonctions personnalisées dans les formulaires adaptatifs

## Présentation

>[!NOTE]
>
> Les fonctions personnalisées doivent être compatibles avec ECMAScript 5 (ES5). Foundation Forms prend uniquement en charge ES5. L’utilisation de versions ECMAScript plus récentes (ES6 et ultérieures) n’est pas prise en charge et peut entraîner des erreurs ou un comportement inattendu.

AEM Forms 6.5 offre la possibilité de définir des fonctions JavaScript pouvant être utilisées pour définir des règles métier complexes à l’aide de l’éditeur de règles. AEM Forms fournit un certain nombre de fonctions personnalisées prêtes à l’emploi, mais vous devrez définir vos propres fonctions personnalisées et les utiliser dans plusieurs formulaires.

Les fonctions personnalisées étendent les capacités des formulaires en facilitant la manipulation et le traitement des données saisies pour répondre aux exigences spécifiées. Elles permettent également une modification dynamique du comportement du formulaire en fonction de critères prédéfinis.
Dans les formulaires adaptatifs, vous pouvez utiliser des fonctions personnalisées dans l’[éditeur de règles](/help/forms/using/rule-editor.md) pour créer des règles de validation spécifiques pour les champs de formulaire.
Analysons l’utilisation de la fonction personnalisée dans laquelle les utilisateurs et utilisatrices saisissent l’adresse e-mail. Vous souhaitez vous assurer que l’adresse e-mail saisie respecte un format spécifique (elle contient un symbole « @ » et un nom de domaine). Créez une fonction personnalisée « ValidateEmail » qui prend l’adresse e-mail en entrée et renvoie true si elle est valide et false dans le cas contraire.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

Dans l’exemple ci-dessus, lorsque la personne tente d’envoyer le formulaire, la fonction personnalisée « ValidateEmail » est appelée pour vérifier si l’adresse e-mail saisie est valide.

## Utilisations des fonctions personnalisées {#uses-of-custom-function}

Les avantages des fonctions personnalisées dans les formulaires adaptatifs sont les suivants :

* **Manipulation des données** : les fonctions personnalisées manipulent et traitent les données saisies dans les champs de formulaires.
* **Validation des données** : les fonctions personnalisées vous permettent d’effectuer des vérifications personnalisées sur les entrées de formulaire et de fournir des messages d’erreur spécifiés.
* **Comportement dynamique** : les fonctions personnalisées vous permettent de contrôler le comportement dynamique de vos formulaires en fonction de conditions spécifiques. Vous pouvez, par exemple, afficher/masquer des champs, modifier les valeurs de champ ou ajuster dynamiquement la logique du formulaire.
* **Intégration** : vous pouvez utiliser des fonctions personnalisées pour intégrer des API ou des services externes. Cela permet de récupérer des données provenant de sources externes, d’envoyer des données à des points d’entrée Rest externes ou d’effectuer des actions personnalisées basées sur des événements externes.

## Annotations JS prises en charge

Assurez-vous que la fonction personnalisée que vous écrivez est accompagnée de la fonction `jsdoc` ci-dessus, au cas où vous auriez besoin d’une configuration et d’une description personnalisées. Il existe plusieurs façons de déclarer une fonction dans `JavaScript,` et les commentaires permettent de conserver une trace des fonctions. Pour plus d’informations, voir [usejsdoc.org](https://jsdoc.app/).

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
   2. nombre
   3. booléen
   4. portée

  La portée est utilisée pour les champs référents d’un formulaire adaptatif. Lorsqu’un formulaire utilise le chargement différé, vous pouvez utiliser `scope` pour accéder à ses champs. Vous pouvez accéder aux champs lorsque les champs sont chargés ou si les champs sont marqués comme généraux.

  Tous les autres types de paramètre sont classés en dessous de l’un des précédents. Ils sont tous pris en charge. Assurez-vous que vous sélectionnez l’un des types ci-dessus. Les types ne respectent pas la casse. Les espaces ne sont pas autorisés dans le paramètre `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* Syntaxe
**Type de retour** : `@return {type}`
Autrement, vous pouvez utiliser `@returns {type}`.
Ajoute des informations sur la fonction, telles que son objectif.
  {type} représente le type de retour de la fonction. Les types de valeur renvoyée autorisés sont les suivants :

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

## Types pris en charge pour la déclaration de fonction {#function-declaration-supported-types}

**Instruction de fonction**

```javascript
function area(len) {
    return len*len;
}
```

Cette fonction est incluse sans commentaires `jsdoc`.

**Expression de fonction**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Expression et instruction de fonction**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Déclaration de fonction en tant que variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limite : la fonction personnalisée prend uniquement la première déclaration de fonction de la liste des variables, si elles sont ensemble. Vous pouvez utiliser l&#39;expression de fonction pour chaque fonction déclarée.

**Déclaration de fonction en tant qu’objet**

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

## Création d’une fonction personnalisée {#create-custom-function}

Pour créer une fonction personnalisée, procédez comme suit :

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

Vous pouvez vous référer au dossier [fonction personnalisée](/help/forms/using/assets/customfunction.zip) suivant. Téléchargez et installez ce dossier dans votre instance AEM.

Désormais, vous pouvez utiliser la fonction personnalisée dans votre formulaire adaptatif en ajoutant la bibliothèque cliente.

## Ajout d’une bibliothèque cliente dans un formulaire adaptatif{#use-custom-function}

Une fois que vous avez déployé votre bibliothèque cliente dans votre environnement Forms CS, utilisez ses fonctionnalités dans votre formulaire adaptatif. Pour ajouter la bibliothèque cliente dans votre formulaire adaptatif

1. Ouvrez votre formulaire en mode d’édition. Pour ouvrir un formulaire en mode d’édition, sélectionnez-le et cliquez sur **[!UICONTROL Ouvrir]**.
1. Ouvrez l’explorateur de contenu, puis sélectionnez le composant **[!UICONTROL Conteneur de guide]** de votre formulaire adaptatif.
1. Cliquez sur l’icône des propriétés du conteneur de guide. La boîte de dialogue du conteneur de formulaires adaptatifs s’ouvre.
1. Ouvrez l’onglet **[!UICONTROL De base]** et sélectionnez le nom de la **[!UICONTROL catégorie de bibliothèque cliente]** dans la liste déroulante (dans ce cas, sélectionnez `customfunctionscategory`).

   ![Ajout de la bibliothèque cliente de fonctions personnalisées](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Cliquez sur **[!UICONTROL Terminé]**.

Vous pouvez maintenant créer une règle pour utiliser des fonctions personnalisées dans l’éditeur de règles :

![Ajout de la bibliothèque cliente de fonctions personnalisées](/help/forms/using//assets/calculateage-customfunction.png)

Maintenant, apprenons comment configurer et utiliser une fonction personnalisée à l’aide du [service Invoke de l’éditeur de règles dans AEM Forms](/help//forms/using/rule-editor.md).
