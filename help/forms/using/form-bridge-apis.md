---
title: API Form Bridge pour les formulaires HTML5
seo-title: API Form Bridge pour les formulaires HTML5
description: Les applications externes utilisent l’API FormBridge pour se connecter au formulaire pour périphériques mobiles XFA. L’API distribue un événement FormBridgeInitialized sur la fenêtre parent.
seo-description: Les applications externes utilisent l’API FormBridge pour se connecter au formulaire pour périphériques mobiles XFA. L’API distribue un événement FormBridgeInitialized sur la fenêtre parent.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 42%

---

# API Form Bridge pour les formulaires HTML5 {#form-bridge-apis-for-html-forms}

Vous pouvez utiliser les API Form Bridge pour ouvrir un canal de communication entre des formulaires HTML5 XFA et vos applications. Les API Form Bridge fournissent une API **connect** pour créer la connexion.

L’API de **connexion** accepte un gestionnaire en tant qu’argument. Une fois la connexion créée entre le formulaire HTML5 XFA et Form Bridge, la poignée est appelée.

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
* **Sortie** : Numéro de version de la bibliothèque de script
* **Errors** : aucune

**isConnected()**  Vérifie si l’état du formulaire a été initialisé.

* **Input** : aucune
* **Sortie** :  **** Vérification si l’état du formulaire XFA a été initialisé

* **Errors** : aucune

**connect(handler, context)** Se connecte à FormBridge et exécute la fonction une fois la connexion établie et l’état du formulaire initialisé.

* **Entrée**:

   * **handler** : fonction à exécuter après la connexion de Form Bridge
   * **context** : Objet pour lequel le contexte (ceci) de la  ** fonction handler est défini.

* **Output** : aucune
* **Error** : aucune

**getDataXML(options)** Renvoie les données de formulaire actuelles au format XML

* **Entrée:**

   * **options :** objet JavaScript contenant les propriétés suivantes :

      * **Error**: Error Handler Function
      * **success** : fonction du gestionnaire de réussite. Cette fonction transmet un objet contenant du code XML à la propriété *data*.
      * **context** : objet pour lequel le contexte (valeur « this ») de la fonction *success* est défini.
      * **validationChecker** : Fonction à appeler pour vérifier les erreurs de validation reçues du serveur. La fonction de validation transmet un tableau de chaînes d’erreur.
      * **formState** : L’état JSON du formulaire XFA pour lequel les données XML doivent être renvoyées. Si cette fonction n’est pas spécifiée, elle renvoie les données XML du formulaire actuellement généré.

* **Output :** aucune
* **Error :** aucune

**registerConfig(configName, config)** Enregistre les configurations spécifiques à l’utilisateur/au portail avec FormBridge. Ces configurations remplacent les configurations par défaut. Les configurations prises en charge sont spécifiées dans la section config.

* **Entrée:**

   * **configName :** nom de la configuration à remplacer.

      * **widgetConfig :** permet à l’utilisateur de remplacer les widgets par défaut du formulaire par des widgets personnalisés. La configuration est remplacée comme suit :

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig :** permet à l’utilisateur de remplacer le comportement par défaut du rendu de la première page uniquement. La configuration est remplacée comme suit :

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig :** permet à l’utilisateur de remplacer le niveau de journalisation, de désactiver la journalisation d’une catégorie ou d’afficher ou non la console des journaux ou de l’envoyer au serveur. La configuration peut être remplacée comme suit :

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

      * **SubmitServiceProxyConfig :** permet aux utilisateurs d’enregistrer les envois et les services proxy de journalisation.

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

**hideFields(fieldArray)** Masque les champs dont les expressions Som sont fournies dans le champArray. Définit la propriété presence des champs spécifiés sur invisible

* **Entrée:**

   * **fieldArray :** tableau des expressions Som des champs à masquer

* **Output :** aucune
* **Error :** aucune

**showFields(fieldArray)** Affiche les champs dont les expressions Som sont fournies dans le champArray. Définit la propriété presence des champs fournis sur visible

* **Entrée:**

   * **fieldArray :** tableau des expressions Som des champs à afficher

* **Output :** aucune
* **Error :** aucune

**hideSubmitButtons()** Masque tous les boutons d’envoi dans le formulaire

* **Input** : aucune
* **Output** : aucune
* **Error** : renvoie l’exception si l’état du formulaire n’est pas initialisé

**getFormState()** Renvoie le JSON représentant l’état du formulaire

* **Input :** aucune
* **Sortie :** objet contenant JSON représentant l’état actuel du formulaire dans la  ** propriété de données.

* **Error :** aucune

**restoreFormState(options)** Restaure l’état du formulaire à partir de l’état JSON fourni dans l’objet options. L’état est appliqué et les gestionnaires de réussite ou d’erreur sont appelés après que l’opération soit terminée

* **Entrée:**

   * **Options :** objet JavaScript contenant les propriétés suivantes :

      * **Erreur** : Fonction de gestionnaire d’erreurs
      * **success** : fonction du gestionnaire de réussite
      * **context** : Objet auquel le contexte (ceci) de la fonction  ** réussie est défini
      * **formState** : état JSON du formulaire. Le formulaire est restauré à l’état JSON.

* **Output :** aucune
* **Error :** aucune

**setFocus (som)** Définit le focus sur le champ spécifié dans l’expression Som

* **Entrée :** expression Som du champ sur lequel la cible d’action est définie
* **Output :** aucune
* **Error :** renvoie une exception si l’expression Som est incorrecte

**setFieldValue (som, value)** Définit la valeur des champs pour les expressions Som données

* **Entrée:**

   * **som :** tableau contenant les expressions Som du champ. L’expression om pour définir la valeur des champs.
   * **value :**  tableau contenant des valeurs correspondant aux expressions Som fournies dans un  **** somarray. Si le type de données de la valeur n’est pas le même que fieldType, la valeur n’est pas modifiée.

* **Output :** aucune
* **Error :** renvoie une exception dans le cas d’une expression Som incorrecte

**getFieldValue (som)** Renvoie la valeur des champs pour les expressions Som données

* **Input :** tableau contenant les expressions Som des champs dont la valeur doit être récupérée
* **Sortie :** objet contenant le résultat sous forme de tableau dans la  **** propriété dataproperty.

* **Error :** aucune

### Exemple d’API getFieldValue(){#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** Récupérez la liste des valeurs pour la propriété donnée des champs spécifiés par les expressions Som

* **Entrée:**

   * **som :** tableau contenant les expressions Som des champs
   * **property** : nom de la propriété dont la valeur est requise

* **Sortie :** objet contenant le résultat sous forme de tableau dans  ** dataproperty

* **Error :** aucune

**setFieldProperties(som, property, values)** Définit la valeur de la propriété donnée pour tous les champs spécifiés par les expressions Som

* **Entrée:**

   * **som :** tableau contenant les expressions Som des champs dont la valeur doit être définie
   * **property **: propriété dont la valeur doit être définie
   * **value :** tableau contenant les valeurs de la propriété donnée pour les champs spécifiés par les expressions Som

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
