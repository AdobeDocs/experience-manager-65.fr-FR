---
title: Messages d’erreur de validation standard des formulaires adaptatifs
seo-title: Standard validation error messages for adaptive forms
description: Transformer les messages d’erreur de validation des formulaires adaptatifs au format standard à l’aide de gestionnaires d’erreurs personnalisés
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
source-git-commit: 34be3b4695679a9b5e8001d28f05ed804f929e61
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 95%

---


# Messages d’erreur de validation standard des formulaires adaptatifs {#standard-validation-error-messages}

Les formulaires adaptatifs valident les entrées que vous fournissez dans les champs en fonction de critères de validation prédéfinis. Les critères de validation font référence aux valeurs d’entrée acceptables pour les champs d’un formulaire adaptatif. Vous pouvez définir les critères de validation en fonction de la source de données que vous utilisez avec le formulaire adaptatif. Par exemple, si vous utilisez des services web RESTful comme source de données, vous pouvez définir les critères de validation dans un fichier de définition Swagger.

Si les valeurs d’entrée répondent aux critères de validation, elles sont envoyées à la source de données. Dans le cas contraire, le formulaire adaptatif affiche un message d’erreur.

De la même manière que cette approche, les formulaires adaptatifs peuvent désormais s’intégrer aux services personnalisés pour effectuer des validations de données. Si les valeurs d’entrée ne répondent pas aux critères de validation et que le message d’erreur de validation renvoyé par le serveur est au format standard du message, les messages d’erreur s’affichent au niveau du champ dans le formulaire.

Si les valeurs d’entrée ne répondent pas aux critères de validation et que le message d’erreur de validation du serveur n’est pas au format standard du message, les formulaires adaptatifs fournissent un mécanisme pour transformer les messages d’erreur de validation en un format standard afin qu’ils s’affichent au niveau du champ dans le formulaire. Vous pouvez transformer le message d’erreur au format standard à l’aide de l’une des deux méthodes suivantes :

* Ajouter un gestionnaire d’erreur personnalisé lors de l’envoi du formulaire adaptatif
* Ajouter un gestionnaire personnalisé à l’action Service d’appel à l’aide de l’éditeur de règles

Cet article décrit le format standard des messages d’erreur de validation et les instructions pour transformer les messages d’erreur d’un format personnalisé en un format standard.

## Format du message d’erreur de validation standard {#standard-validation-message-format}

Les formulaires adaptatifs affichent les erreurs au niveau du champ si les messages d’erreur de validation du serveur sont au format standard suivant :

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

Où :

* `errorCausedBy` décrit le motif de l’échec.
* `errors` mentionne l’expression SOM des champs qui ont échoué aux critères de validation avec le message d’erreur de validation.
* `originCode` contient le code d’erreur renvoyé par le service externe.
* `originMessage` contient les données d’erreur brutes renvoyées par le service externe.

## Configurer l’envoi de formulaire adaptatif pour ajouter des gestionnaires personnalisés {#configure-adaptive-form-submission}

Si le message d’erreur de validation du serveur ne s’affiche pas dans le format standard, vous pouvez activer l’envoi asynchrone et ajouter un gestionnaire d’erreur personnalisé lors de l’envoi du formulaire adaptatif pour convertir le message dans un format standard.

### Configurer l’envoi asynchrone du formulaire adaptatif {#configure-asynchronous-adaptive-form-submission}

Avant d’ajouter un gestionnaire personnalisé, vous devez configurer le formulaire adaptatif pour l’envoi asynchrone. Procédez comme suit :

<!-- 1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/af_properties.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Tap ![Save](assets/af_save.png) to save the properties.-->

### Ajouter un gestionnaire d’erreur personnalisé lors de l’envoi du formulaire adaptatif {#add-custom-error-handler-af-submission}

AEM Forms fournit des gestionnaires de succès et d’erreur prêts à l’emploi pour les envois de formulaires. Les gestionnaires sont des fonctions côté client qui s’exécutent en fonction de la réponse du serveur. Lorsqu’un formulaire est envoyé, les données sont transmises au serveur pour validation, ce qui renvoie une réponse au client avec des informations sur l’événement de succès ou d’erreur pour l’envoi. Les informations sont transmises comme paramètres au gestionnaire approprié pour exécuter la fonction.

Exécutez les étapes suivantes pour ajouter un gestionnaire d’erreurs personnalisé lors de l’envoi du formulaire adaptatif :

1. Ouvrez le formulaire adaptatif en mode création, sélectionnez n’importe quel objet de formulaire et appuyez sur <!--![Rule Editor](assets/af_edit_rules.png)--> pour ouvrir l’éditeur de règles.
1. Sélectionnez **[!UICONTROL Formulaire]** dans l’arborescence des objets de formulaire et appuyez sur **[!UICONTROL Créer]**.
1. Sélectionnez **[!UICONTROL Erreur dans l’envoi]** dans la liste déroulante Événement.
1. Créez une règle pour convertir la structure d’erreur personnalisée en structure d’erreur standard, puis appuyez sur **[!UICONTROL Terminé]** pour enregistrer la règle.

Voici un exemple de code pour convertir une structure d’erreur personnalisée en structure d’erreur standard :

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

Le `var som_map` répertorie l’expression SOM des champs de formulaire adaptatif que vous souhaitez transformer au format standard. Vous pouvez afficher l’expression SOM de n’importe quel champ d’un formulaire adaptatif en appuyant sur le champ et en sélectionnant **[!UICONTROL Afficher l’expression SOM]**.

À l’aide de ce gestionnaire d’erreurs personnalisé, le formulaire adaptatif convertit les champs répertoriés dans `var som_map` au format standard du message d’erreur. Par conséquent, les messages d’erreur de validation s’affichent au niveau du champ dans le formulaire adaptatif.

## Ajouter un gestionnaire personnalisé à l’aide de l’action Invoke Service

Exécutez les opérations suivantes pour ajouter un gestionnaire d’erreurs afin de convertir une structure d’erreur personnalisée en structure d’erreur standard à l’aide de l’action Invoke Service de l’ [Éditeur de règles](rule-editor.md) :

<!-- 1. Open the adaptive form in authoring mode, select any form object, and tap ![Rule Editor](assets/af_edit_rules.png) to open the rule editor.
1. Tap **[!UICONTROL Create]**.
1. Create a condition in the **[!UICONTROL When]** section of the rule. For example, When[Name of field] is changed. Select **[!UICONTROL is changed]** from the **[!UICONTROL Select State]** drop-down list to achieve this condition.
1. In the **[!UICONTROL Then]** section, select **[!UICONTROL Invoke Service]** from the **[!UICONTROL Select Action]** drop-down list.
1. Select a Post service and its corresponding data bindings from the **[!UICONTROL Input]** section. For example, if you want to validate **Name**, **ID**, and **Status** fields in the adaptive form, select a Post service (pet) and select pet.name, pet.id, and pet.status in the **[!UICONTROL Input]** section.-->

    En raison de cette règle, les valeurs que vous saisissez pour les champs **Name**, **ID** et **Status** sont validées, dès que le champ défini à l’étape 2 est modifié et que vous vous déposez du champ du formulaire.

1. Sélectionnez l’**[!UICONTROL éditeur de code]** dans la liste déroulante de sélection de mode.
1. Appuyer sur **[!UICONTROL Modifier le code]**.
1. Supprimez la ligne suivante du code existant :

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Créez une règle pour convertir la structure d’erreur personnalisée en structure d’erreur standard, puis appuyez sur **[!UICONTROL Terminé]** pour enregistrer la règle.
Par exemple, ajoutez l’exemple de code suivant à la fin pour convertir une structure d’erreur personnalisée en structure d’erreur standard :

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   Le `var som_map` répertorie l’expression SOM des champs de formulaire adaptatif que vous souhaitez transformer au format standard. Vous pouvez afficher l’expression SOM de n’importe quel champ d’un formulaire adaptatif en appuyant sur le champ et en sélectionnant **[!UICONTROL Afficher l’expression SOM]** du menu **[!UICONTROL Autres options]** (...).

   Veillez à copier la ligne suivante de l’exemple de code dans le gestionnaire d’erreurs personnalisé :

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   L’API executeOperation comprend les paramètres `null` et `errorHandler` en fonction du nouveau gestionnaire d’erreurs personnalisé.

   À l’aide de ce gestionnaire d’erreurs personnalisé, le formulaire adaptatif convertit les champs répertoriés dans `var som_map` au format standard du message d’erreur. Par conséquent, les messages d’erreur de validation s’affichent au niveau du champ dans le formulaire adaptatif.