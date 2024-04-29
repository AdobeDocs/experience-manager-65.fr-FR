---
title: API FormBridge pour les formulaires HTML5
description: Les applications externes utilisent l’API FormBridge pour se connecter au formulaire mobile XFA. L’API distribue un événement FormBridgeInitialized sur la fenêtre parent.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '938'
ht-degree: 100%

---

# API FormBridge pour les formulaires HTML5 {#form-bridge-apis-for-html-forms}

Vous pouvez utiliser l’API Form Bridge pour ouvrir un canal de communication entre les formulaires HTML5 XFA et vos applications. L’API Form Bridge fournit une API de **connexion** pour créer la connexion.

L’API de **connexion** accepte un gestionnaire en tant qu’argument. Une fois la connexion créée entre le formulaire HTML5 XFA et Form Bridge, le descripteur est appelé.

Vous pouvez utiliser l’exemple de code suivant pour créer la connexion.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Assurez-vous d’avoir créé la connexion avant d’ajouter le fichier formruntime.jsp.

## API Form Bridge disponible  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Renvoie le numéro de version de la bibliothèque de script.

* **Input** : aucune
* **Output** : numéro de version de la bibliothèque de script.
* **Errors** : aucune

**isConnected()** : permet de vérifier que l’état du formulaire a été initialisé.

* **Input** : aucune
* **Output :** valeur **true** si l’état du formulaire XFA a été initialisé.

* **Errors** : aucune

**connect(handler, context)** : se connecte à FormBridge et exécute la fonction une fois la connexion établie et l’état du formulaire initialisé.

* **Entrée**:

   * **handler** : fonction à exécuter après la connexion de Form Bridge
   * **context** : objet pour lequel le contexte (valeur « this ») du *gestionnaire* est défini.

* **Output :** aucune
* **Error :** aucune

**getDataXML(options)** : renvoie les données actuelles du formulaire au format XML.

* **Entrée:**

   * **options :** objet JavaScript contenant les propriétés suivantes :

      * **Error**: Error Handler Function
      * **success** : fonction du gestionnaire de réussite. Cette fonction transmet un objet contenant du code XML à la propriété *data*.
      * **context** : objet pour lequel le contexte (valeur « this ») de la fonction *success* est défini.
      * **validationChecker** : fonction à appeler pour vérifier les erreurs de validation reçues du serveur. La fonction de validation transmet un tableau de chaînes d’erreur.
      * **formState** : état JSON du formulaire XFA pour lequel les données XML doivent être renvoyées. Si cette fonction n’est pas spécifiée, elle renvoie les données XML du formulaire actuellement généré.

* **Output :** aucune
* **Error :** aucune

**registerConfig(configName, config)** : enregistre les configurations propres à l’utilisateur/au portail avec FormBridge. Ces configurations remplacent les configurations par défaut. Les configurations prises en charge sont spécifiées dans la section config.

* **Entrée:**

   * **configName :** nom de la configuration à remplacer.

      * **widgetConfig :** permet à l’utilisateur de remplacer les widgets par défaut par des widgets personnalisés, dans le formulaire. La configuration est remplacée comme suit :

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig :** permet à l’utilisateur de remplacer le comportement par défaut du rendu de la première page uniquement. La configuration est remplacée comme suit :

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig :** permet à l’utilisateur de remplacer le niveau de journalisation, de désactiver la journalisation d’une catégorie ou d’afficher ou non la console de journaux ou l’envoi au serveur. La configuration peut être remplacée comme suit :

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig :** permet aux utilisateurs d’enregistrer les soumissions et les services proxy de journal.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **config :** valeur de la configuration

* **Output :** objet contenant la valeur d’origine de la configuration dans la propriété *data*.

* **Error :** aucune

**hideFields(fieldArray)** : masque les champs dont les expressions SOM sont fournies dans le tableau fieldArray. Définit la propriété presence des champs spécifiés sur invisible

* **Entrée:**

   * **fieldArray :** tableau des expressions SOM des domaines à masquer.

* **Output :** aucune
* **Error :** aucune

**showFields(fieldArray)** : affiche les champs dont les expressions Som sont fournies dans le tableau fieldArray. Définit la propriété presence des champs fournis sur visible

* **Entrée:**

   * **fieldArray :** tableau des expressions SOM des champs à afficher.

* **Output :** aucune
* **Error :** aucune

**hideSubmitButtons()** : masque tous les boutons d’envoi dans le formulaire.

* **Input** : aucune
* **Output** : aucune
* **Error** : renvoie l’exception si l’état du formulaire n’est pas initialisé.

**getFormState()** : renvoie le JSON représentant l’état du formulaire.

* **Input :** aucune
* **Output :** objet contenant le JSON représentant l’état actuel du formulaire dans la propriété *data*.

* **Error :** aucune

**restoreFormState(options)** : restaure l’état du formulaire à partir de l’état JSON fourni dans l’objet options. L’état est appliqué et les gestionnaires de réussite ou d’erreur sont appelés après que l’opération soit terminée.

* **Entrée:**

   * **Options :** objet JavaScript contenant les propriétés suivantes :

      * **Error**: Error Handler Function
      * **success** : fonction du gestionnaire de réussite
      * **context** : objet pour lequel le contexte (valeur « this ») de la fonction *success* est défini.
      * **formState** : état JSON du formulaire. Le formulaire est restauré à l’état JSON.

* **Output :** aucune
* **Error :** aucune

**setFocus (som)** : met le focus sur le champ spécifié dans l’expression Som.

* **Input :** expression SOM du champ sur lequel le ciblage est défini.
* **Output :** aucune
* **Error :** renvoie une exception si une expression SOM est incorrecte.

**setFieldValue (som, value)** : définit la valeur des champs pour les expressions SOM données.

* **Entrée:**

   * **som :** tableau contenant les expressions Som du champ. L’expression SOM pour définir la valeur des champs.
   * **value :** tableau contenant des valeurs correspondant aux expressions SOM fournies dans un tableau **SOM**. Si le type de données de la valeur n’est pas identique à fieldType, la valeur n’est pas modifiée.

* **Output :** aucune
* **Error :** renvoie une exception si une expression SOM est incorrecte.

**getFieldValue (som)** : renvoie la valeur des champs des expressions SOM données.

* **Input :** tableau contenant les expressions SOM des champs dont la valeur doit être récupérée.
* **Output :** objet contenant le résultat sous forme de tableau dans la propriété **data**.

* **Error :** aucune

### Exemple d’API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** : permet de récupérer la liste des valeurs de la propriété donnée des champs spécifiés par les expressions SOM.

* **Entrée:**

   * **som :** tableau contenant les expressions Som des champs
   * **property** : nom de la propriété dont la valeur est requise

* **Output :** objet contenant le résultat sous forme de tableau dans la propriété *data*.

* **Error :** aucune

**setFieldProperties(som, property, values)** : permet de définir la valeur de la propriété donnée pour tous les champs spécifiés par les expressions SOM.

* **Entrée:**

   * **SOM :** tableau contenant les expressions SOM des champs dont la valeur doit être définie.
   * **property** : propriété dont la valeur doit être définie
   * **value :** tableau contenant les valeurs de la propriété donnée pour les champs spécifiés par les expressions SOM.

* **Output :** aucune
* **Error :** aucune

## Exemple d’utilisation de l’API Form Bridge {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
