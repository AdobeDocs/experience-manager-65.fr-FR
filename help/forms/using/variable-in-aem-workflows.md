---
title: Variables dans les processus AEM Forms
seo-title: Variables dans les processus AEM Forms
description: Créez une variable, définissez une valeur pour la variable et utilisez-la dans les étapes du processus AEM Forms.
seo-description: Créez une variable, définissez une valeur pour la variable et utilisez-la dans les étapes du processus AEM Forms.
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
translation-type: tm+mt
source-git-commit: 56f7db792b340ed6774c54170e9b5d2a52153cd5

---


# Variables dans les processus AEM Forms{#variables-in-aem-forms-workflows}

Une variable d’un modèle de flux de travail permet de stocker une valeur en fonction de son type de données. Vous pouvez ensuite utiliser le nom de la variable dans n’importe quelle étape du processus pour récupérer la valeur stockée dans la variable. Vous pouvez également utiliser des noms de variable pour définir des expressions pour prendre des décisions de routage.

Dans les modèles de processus AEM, vous pouvez :

* [Créez une variable](../../forms/using/variable-in-aem-workflows.md#create-a-variable) d’un type de données en fonction du type d’informations que vous souhaitez y stocker.
* [Définissez une valeur pour la variable](../../forms/using/variable-in-aem-workflows.md#set-a-variable) à l’aide de l’étape de flux de travail Définir la variable.
* [Utilisez la variable](../../forms/using/variable-in-aem-workflows.md#use-a-variable) dans toutes les étapes du processus AEM Forms pour récupérer la valeur stockée et dans OU Fractionner et atteindre les étapes pour définir une expression de routage.

La vidéo suivante montre comment créer, définir et utiliser des variables dans les modèles de flux de travaux AEM :

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

Les variables sont une extension de l’interface [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) existante. Vous pouvez utiliser [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) dans ECMAScript pour accéder aux métadonnées enregistrées à l’aide de variables.

## Création d’une variable {#create-a-variable}

Vous créez des variables à l’aide de la section Variables disponible dans le panneau latéral du modèle de flux de travail. Les variables de processus AEM prennent en charge les types de données suivants :

* **Types** de données primitives : Long, Double, Boolean, Date et String
* **Types** de données complexes : [Document](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html), [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html), [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)et instance de modèle de données de formulaire.

>[!NOTE]
>
>Les flux de travaux prennent uniquement en charge le format ISO8601 pour les variables de type de date.

Vous avez besoin du package [de module complémentaire](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms pour les types de données Document et Modèle de données de formulaire.  Utilisez le type de données ArrayList pour créer des collections de variables. Vous pouvez créer une variable ArrayList pour tous les types de données primitifs et complexes. Par exemple, créez une variable ArrayList et sélectionnez String comme sous-type pour stocker plusieurs valeurs de chaîne à l’aide de la variable.

Pour créer une variable, procédez comme suit :

1. Sur une instance AEM, accédez à Outils ![](/help/forms/using/assets/hammer.png) > Processus > Modèles.
1. Appuyez sur **[!UICONTROL Créer]** et spécifiez le titre et un nom facultatif pour le modèle de processus. Sélectionnez le modèle et appuyez sur **[!UICONTROL Modifier]**.
1. Appuyez sur l’icône de variables disponible dans le panneau latéral du modèle de flux de travail et appuyez sur **[!UICONTROL Ajouter une variable]**.

   ![Ajouter une variable](assets/variables_add_variable_new.png)

1. Dans la boîte de dialogue Ajouter une variable, indiquez le nom et sélectionnez le type de la variable.
1. Sélectionnez le type de données dans la liste déroulante **[!UICONTROL Type]** et spécifiez les valeurs suivantes :

   * Type de données primitives : spécifiez une valeur par défaut facultative pour la variable.
   * JSON ou XML : spécifiez un chemin d’accès facultatif au schéma JSON ou XML. Le système valide le chemin du schéma lors du mappage et du stockage des propriétés disponibles dans ce schéma sur une autre variable.
   * Modèle de données de formulaire : spécifiez un chemin d’accès au modèle de données de formulaire.
   * ArrayList : spécifiez un sous-type pour la collection.

1. Spécifiez une description facultative pour la variable et appuyez sur ![](assets/done_icon.png) pour enregistrer les modifications. La variable s’affiche dans la liste disponible dans le volet de gauche.

Lorsque vous créez des variables, prenez en compte les bonnes pratiques suivantes :

* Créez autant de variables qu’un flux de travail le requiert. Toutefois, pour conserver les ressources de base de données, utilisez le nombre minimum de variables requises et réutilisez les variables dès que possible.
* Les variables sont sensibles à la casse. Veillez à référencer des variables en utilisant le même cas dans votre flux de travail.
* Evitez d’utiliser des caractères spéciaux dans le nom de la variable

## Définition d’une variable {#set-a-variable}

Vous pouvez utiliser l’étape Définir la variable pour définir la valeur d’une variable et définir l’ordre dans lequel les valeurs sont définies. La variable est définie dans l’ordre dans lequel les mappages de variables sont répertoriés à l’étape de définition de la variable.

Les modifications apportées aux valeurs de variable affectent uniquement l’instance du processus dans lequel la modification se produit. Par exemple, lorsqu’un processus est lancé et que des données variables sont modifiées, les modifications affectent uniquement cette instance du processus. Les modifications n’affectent pas les autres instances du flux de travaux qui ont été lancées précédemment ou qui sont lancées ultérieurement.

Selon le type de données de la variable, vous pouvez utiliser les options suivantes pour définir la valeur d’une variable :

* **Littéral :** utilisez cette option lorsque vous connaissez la valeur exacte à spécifier.

* **** Expression : Utilisez cette option lorsque la valeur à utiliser est calculée en fonction d’une expression. L’expression est créée dans l’éditeur d’expression fourni.

* **** Notation de point JSON : Utilisez l’option pour récupérer une valeur d’une variable de type JSON ou FDM.
* **** XPATH : Utilisez cette option pour récupérer une valeur d’une variable de type XML.

* **** Par rapport à la charge utile : Utilisez l’option lorsque la valeur à enregistrer dans la variable est disponible à un chemin d’accès relatif à la charge utile.

* **** Chemin absolu : Utilisez cette option lorsque la valeur à enregistrer dans la variable est disponible à un chemin absolu.

Vous pouvez également mettre à jour des éléments spécifiques d’une variable de type JSON ou XML à l’aide de la notation JSON DOT ou XPATH.

### Ajout d’un mappage entre variables {#add-mapping-between-variables}

Exécutez les étapes suivantes pour ajouter un mappage entre des variables :

1. Dans la page de modification du flux de travail, appuyez sur l’icône Etapes disponible dans le sidekick du modèle de flux de travail.
1. Faites glisser l’étape **Définir la variable** vers l’éditeur de flux de travaux, appuyez sur l’étape et sélectionnez ![](assets/configure_icon.png) (Configurer).
1. Dans la boîte de dialogue Définir la variable, sélectionnez **[!UICONTROL Mappage]** > **[!UICONTROL Ajouter un mappage]**.
1. Dans la section Variable **de** mappage, sélectionnez la variable à stocker, sélectionnez le mode de mappage et spécifiez une valeur à stocker dans la variable. Les modes de mappage varient en fonction du type de variable.
1. Faites correspondre davantage de variables pour créer une expression significative. Tap ![](assets/done_icon.png) to save the changes.

### Exemple 1 : Interroger une variable XML pour définir la valeur d’une variable de chaîne {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Sélectionnez une variable de type XML pour stocker un fichier XML. Recherchez la variable XML pour définir la valeur d’une variable de chaîne pour la propriété disponible dans le fichier XML. Utilisez **Spécifier XPATH pour le champ de variable** XML pour définir la propriété à stocker dans la variable de chaîne.

Dans cet exemple, sélectionnez une variable XML **formdata** pour stocker le fichier **cc-app.xml** . Recherchez la variable **formdata** pour définir la valeur de la variable de chaîne **emailaddress** afin de stocker la valeur de la propriété **emailAddress** disponible dans le fichier **cc-app.xml.**

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Définir la valeur d’une variable")

### Exemple 2 : Utiliser une expression pour stocker une valeur en fonction d’autres variables {#example2}

Utilisez une expression pour calculer la somme des variables et stocker le résultat dans une variable.

Dans cet exemple, utilisez l’éditeur d’expression pour définir une expression afin de calculer la somme des variables **de coût** et de **montant** d’équilibre et de stocker le résultat dans une variable **de valeur** totale.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Utiliser l’éditeur d’expression {#use-expression-editor}

Vous utilisez également des expressions pour calculer la valeur d’une variable au moment de l’exécution. Les variables fournissent un éditeur d’expression pour définir des expressions.

Utilisez l’éditeur d’expression pour :

* Définissez la valeur des variables à l’aide d’autres variables de processus, nombres ou expressions mathématiques.
* Utiliser des variables de flux de travail, une chaîne, un nombre ou une expression dans une expression mathématique
* Ajoutez des conditions pour définir des valeurs de variables.
* Ajoutez des opérateurs entre les conditions.

![Editeur d’expression](assets/variables_expression_editor_new.png)

Il est basé sur l’éditeur de règles de formulaires adaptatifs avec les modifications suivantes. Éditeur de règles dans les variables :

* Ne prend pas en charge les fonctions.
* Ne fournit pas d’interface utilisateur pour afficher le résumé des règles
* N’a pas d’éditeur de code.
* Ne prend pas en charge l’activation et la désactivation de la valeur d’un objet.
* Ne prend pas en charge la définition de la propriété d’un objet.
* Ne prend pas en charge l’appel d’un service Web.

For more information, see [adaptive forms rule editor](../../forms/using/rule-editor.md).

## Use a variable {#use-a-variable}

Vous pouvez utiliser des variables pour récupérer les entrées et les sorties ou enregistrer le résultat d’une étape. L’éditeur de flux de travail fournit deux types d’étapes de flux de travail :

* Procédure de flux de travail avec prise en charge des variables
* Procédure de flux de travail sans prise en charge des variables

### Procédure de flux de travail avec prise en charge des variables {#workflow-steps-with-support-for-variables}

L’étape Atteindre, OU Scinder, et toutes les étapes du processus AEM Forms prennent en charge les variables.

#### OU Etape de fractionnement {#or-split-step}

La Division OU divise le processus et une seule branche est active par la suite. Cette étape vous permet d’ajouter des chemins de traitement conditionnels dans le workflow. Vous ajoutez des étapes de workflow à chaque branche selon vos besoins.

Vous pouvez définir l&#39;expression de routage pour une branche à l&#39;aide d&#39;une définition de règle, d&#39;un script ECMA ou d&#39;un script externe.

Vous pouvez utiliser des variables pour définir l’expression de routage à l’aide de l’éditeur d’expression. Pour plus d’informations sur l’utilisation des expressions de routage pour l’étape de fractionnement OU, voir [OU l’étape](/help/sites-developing/workflows-step-ref.md#or-split)de fractionnement.

Dans cet exemple, avant de définir l&#39;expression de routage, utilisez l&#39; [exemple 2](../../forms/using/variable-in-aem-workflows.md#example2) pour définir la valeur de la variable **totalvalue** . La branche 1 est active si la valeur de la variable **totalvalue** est supérieure à 50 000. De même, vous pouvez définir une règle pour activer la branche 2 si la valeur de la variable **totalvalue** est inférieure à 50 000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

De même, sélectionnez un chemin de script externe ou spécifiez le script ECMA pour les expressions de routage afin d’évaluer la branche active. Appuyez sur **[!UICONTROL Renommer la branche]** pour spécifier un autre nom pour la branche.

Pour plus d’exemples, voir [Création d’un modèle](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)de processus.

#### Aller à l’étape {#go-to-step}

The **Goto Step** allows you to specify the next step in the workflow model to execute, dependent on the result of a routing expression.

Tout comme l’étape de fractionnement OU, vous pouvez définir l’expression de routage pour l’étape Goto à l’aide d’une définition de règle, d’un script ECMA ou d’un script externe.

Vous pouvez utiliser des variables pour définir l’expression de routage à l’aide de l’éditeur d’expression. Pour plus d’informations sur l’utilisation des expressions de routage pour l’étape de destination, voir [Atteindre l’étape](/help/sites-developing/workflows-step-ref.md#goto-step).

![Règle d’accès](assets/variables_goto_rule1_new.png)

Dans cet exemple, l’étape Atteindre indique l’étape suivante Réviser la demande de carte de crédit si la valeur de la variable **Action** est égale à **Besoin de plus d’informations**.

Pour plus d’exemples sur l’utilisation de la définition de règle dans l’étape Goto, voir [Simulation d’une boucle](/help/sites-developing/workflows-step-ref.md#simulateforloop)For.

#### Procédure de flux de travaux orientée processus des formulaires {#forms-workflow-centric-workflow-steps}

Toutes les étapes du processus AEM Forms prennent en charge les variables. For more information, see [Forms-centric workflow on OSGi](../../forms/using/aem-forms-workflow-step-reference.md).

### Procédure de flux de travail sans prise en charge des variables {#workflow-steps-without-support-for-variables}

Vous pouvez utiliser l’interface [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) pour accéder à des variables dans les étapes du flux de travail qui ne prennent pas en charge les variables.

#### Récupérer la valeur de la variable {#retrieve-the-variable-value}

Utilisez les API suivantes dans le script ECMA pour récupérer les valeurs des variables existantes en fonction du type de données :

| Type de données variable | API |
|---|---|
| Primitif (Long, Double, Boolean, Date et String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| Document | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| Modèle de données de formulaire | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Vous avez besoin du package [de module complémentaire](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms pour les types de données de variable Document et Modèle de données de formulaire.

**Exemple**

Récupérez la valeur du type de données de chaîne à l’aide de l’API suivante :

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Mettre à jour la valeur de la variable {#update-the-variable-value}

Utilisez l’API suivante dans le script ECMA pour mettre à jour la valeur d’une variable :

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Exemple**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

met à jour la valeur de la variable **de salaire** sur 50 000.

### Définition de variables pour appeler des processus {#apiinvokeworkflow}

Vous pouvez utiliser une API pour définir des variables et les transmettre pour appeler des instances de flux de travail.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utilise model, wfData et metaData comme arguments. Utilisez MetaDataMap pour définir la valeur de la variable.

Dans cette API, la variable **variableName** est définie sur **valeur** à l’aide de metaData.put(variableName, valeur);

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**Exemple**

Initialisez l’objet de document **doc** sur un chemin d’accès (&quot;a/b/c&quot;) et définissez la valeur de la variable **docVar** sur le chemin d’accès stocké dans l’objet de document.

```java
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Modification d’une variable {#edit-a-variable}

1. Dans la page Modifier le processus, appuyez sur l’icône Variables disponible dans le sidekick du modèle de processus. La section Variables du volet de gauche affiche toutes les variables existantes.
1. Appuyez sur l’icône ![](assets/edit.png) (Modifier) en regard du nom de la variable que vous souhaitez modifier.
1. Modifiez les informations de la variable et appuyez ![](assets/done_icon.png) sur pour enregistrer les modifications. Vous ne pouvez pas modifier les champs **[!UICONTROL Nom]** et **[!UICONTROL Type]** d’une variable.

## Suppression d’une variable {#delete-a-variable}

Avant de supprimer la variable, supprimez toutes les références de la variable du processus. Assurez-vous que la variable n’est pas utilisée dans le processus.

Pour supprimer une variable, procédez comme suit :

1. Dans la page Modifier le processus, appuyez sur l’icône Variables disponible dans le sidekick du modèle de processus. La section Variables du volet de gauche affiche toutes les variables existantes.
1. Appuyez sur l’icône Supprimer en regard du nom de la variable à supprimer.
1. Appuyez sur ![](assets/done_icon.png) pour confirmer et supprimer la variable.

## Références {#references}

Pour plus d’exemples sur l’utilisation des variables dans les étapes du processus AEM Forms, reportez-vous à la section [Variables dans les processus](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html)AEM.
