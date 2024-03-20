---
title: Appeler AEM Forms à l’aide de demandes REST
description: Appelez les processus créés dans Workbench à l’aide de requêtes REST.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 82%

---

# Appeler AEM Forms à l’aide de demandes REST {#invoking-aem-forms-using-rest-requests}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Les processus créés dans Workbench peuvent être configurés de sorte que vous puissiez les appeler par le biais de demandes REST (Really State Transfer). Les demandes REST sont envoyées à partir de pages de HTML. C’est pourquoi, vous pouvez appeler un processus Forms directement à partir d’une page web à l’aide d’une requête REST. Vous pouvez par exemple ouvrir une nouvelle instance d’une page web. Vous pouvez ensuite appeler un processus Forms et charger un document PDF généré avec les données envoyées dans une requête HTTP POST.

Il existe deux types de clients HTML. Le premier client HTML est un client AJAX écrit en JavaScript. Le second type de client est un formulaire HTML contenant un bouton d’envoi. Outre lʼapplication client HTML, il existe dʼautres clients REST possibles. Toute application client prenant en charge les requêtes HTTP peut appeler un service à l’aide d’un appel REST. Par exemple, vous pouvez appeler un service à partir d’un formulaire PDF via un appel REST. (Consultez la section [Appeler le processus MyApplication/EncryptDocument depuis Acrobat](#rest-invocation-examples)).

Lorsque vous utilisez des requêtes REST, il est recommandé de ne pas appeler directement les services Forms. Au lieu de cela, appelez les processus qui ont été créés dans Workbench. Lors de la création d’un processus destiné à un appel REST, utilisez un point de départ programmatique. Le point d’entrée REST est alors ajouté automatiquement. Pour plus d’informations sur la création de processus dans Workbench, consultez la section [Utiliser Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).

Lorsque vous appelez un service à l’aide de REST, vous êtes invité à saisir le nom d’utilisateur et le mot de passe d’AEM forms. Toutefois, si vous ne souhaitez pas spécifier un nom d’utilisateur et un mot de passe, vous pouvez désactiver la sécurité du service.

Pour appeler un service Forms (un processus devient un service lorsque le processus est activé) à l’aide de REST, configurez un point d’entrée REST. (Consultez la section « Gérer les points dʼentrée » dans lʼ[Aide dʼadministration](https://www.adobe.com/go/learn_aemforms_admin_63_fr).)

Une fois la configuration dʼun point d’entrée REST terminée, vous pouvez appeler un service Forms à l’aide d’une méthode HTTP GET ou POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

La valeur obligatoire `ServiceName` est le nom du service Forms à appeler. Le paramètre facultatif `OperationName` value est le nom de l’opération du service. Si cette valeur nʼest pas spécifiée, ce nom prend par défaut la valeur `invoke`, qui est le nom de lʼopération qui lance le processus. La valeur facultative `ServiceVersion` est la version encodée dans le format X.Y. Si cette valeur n’est pas spécifiée, la version la plus récente est utilisée. La valeur `enctype` peut également être `application/x-www-form-urlencoded`.

## Types de données pris en charge {#supported-data-types}

Les types de données suivants sont pris en charge lors de l’appel des services AEM Forms à l’aide de requêtes REST :

* Types de données primitifs de Java, tels que les chaînes et les entiers
* Type de données `com.adobe.idp.Document`
* Types de données XML tels que `org.w3c.Document` et `org.w3c.Element`
* Objets de collection, tels que `java.util.List` et `java.util.Map`

  Ces types de données sont généralement acceptés comme valeurs d’entrée des processus créés dans Workbench.

  Si un service Forms est appelé à lʼaide de la méthode de HTTP POST, les arguments sont transmis dans le corps de la requête HTTP. Si la signature du service AEM Forms comporte un paramètre d’entrée de chaîne, le corps de la requête peut contenir la valeur de texte du paramètre d’entrée. Si la signature du service définit plusieurs paramètres de chaîne, la requête peut suivre le `application/x-www-form-urlencoded` avec les noms des paramètres utilisés comme noms de champ du formulaire.

  Si un service Forms renvoie un paramètre de chaîne, le résultat est une représentation textuelle du paramètre de sortie. Si un service renvoie plusieurs paramètres de chaîne, le résultat est un document XML encodant les paramètres de sortie au format suivant :
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >La valeur `output-paramater1` représente le nom du paramètre de sortie.

  Si un service Forms requiert un paramètre `com.adobe.idp.Document`, le service ne peut être appelé qu’à l’aide de la méthode HTTP POST. Si le service en nécessite un paramètre `com.adobe.idp.Document`, le corps de la requête HTTP devient le contenu de l’objet Document d’entrée.

  Si un service AEM Forms nécessite plusieurs paramètres d’entrée, le corps de la requête HTTP doit être un message MIME multipartie, tel que défini par la norme RFC 1867. (Les navigateurs web utilisent la norme RFC 1867 pour télécharger des fichiers sur des sites web). Chaque paramètre d’entrée doit être envoyé en tant que partie distincte du message multipartie et codé dans le format `multipart/form-data`. Le nom de chaque partie doit correspondre au nom du paramètre.

  Les listes et les mappages sont également utilisés comme valeurs d’entrée dans les processus AEM Forms créés dans Workbench. Par conséquent, vous pouvez utiliser ces types de données lors de la réalisation d’une requête REST. Les tableaux Java ne sont pas pris en charge, car ils ne sont pas utilisés comme valeur d’entrée dans un processus AEM Forms.

  Si un paramètre d’entrée est une liste, un client REST peut l’envoyer en spécifiant le paramètre plusieurs fois (une fois pour chaque élément de la liste). Par exemple, si A est une liste de documents, lʼentrée doit être un message multipartie composé de plusieurs parties nommées A. Dans ce cas, chaque partie nommée A devient un élément de la liste dʼentrée. Si B est une liste de chaînes, l’entrée peut être un message `application/x-www-form-urlencoded` composé de plusieurs champs nommés B. Dans ce cas, chaque champ de formulaire nommé B devient un élément de la liste dʼentrée.

  Si un paramètre d’entrée est un mappage et qu’il s’agit du seul paramètre d’entrée des services, alors chaque partie/champ du message d’entrée devient un enregistrement clé/valeur dans le mappage. Le nom de chaque partie/champ devient la clé de l’enregistrement. Le contenu de chaque partie/champ devient la valeur de l’enregistrement.

  Si une carte d’entrée n’est pas le seul paramètre d’entrée des services, chaque enregistrement clé/valeur appartenant à la carte peut être envoyé à l’aide d’un paramètre nommé en tant que concaténation du nom du paramètre et de la clé de l’enregistrement. Par exemple, un mappage d’entrée appelé `attributes` peut être envoyé avec une liste des paires clé/valeur suivantes :

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  Cela se traduit par un mappage de trois enregistrements : `Color=red`, `Shape=box` et `Width=5`.

  Les paramètres de sortie des types liste et mappage font partie du message XML résultant. La liste de sortie est représentée en XML comme une série dʼéléments XML, un élément pour chaque élément de la liste. Chaque élément reçoit le même nom que le paramètre de la liste de sortie. Deux valeurs sont possibles pour chaque élément XML :

* Représentation textuelle de l’élément de la liste (si la liste est composée de chaînes)
* URL pointant vers le contenu du document (si la liste est composée dʼobjets `com.adobe.idp.Document`)

  L’exemple suivant est un message XML renvoyé par un service qui a un seul paramètre de sortie nommé *list*, qui est une liste de nombres entiers.
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un paramètre de mappage de sortie est représenté dans le message XML résultant comme une série d’éléments XML avec un élément pour chaque enregistrement dans le mappage. Chaque élément reçoit le même nom que la clé de l’enregistrement de carte. La valeur de chaque élément est soit une représentation textuelle de la valeur de l’enregistrement de carte (si la carte est composée d’enregistrements avec une valeur de chaîne), soit une URL pointant vers le contenu du document (si la carte est constituée d’enregistrements avec la variable `com.adobe.idp.Document` ). Consultez ci-dessous un exemple de message XML renvoyé par un service qui a un seul paramètre de sortie nommé `map`. Cette valeur de paramètre est un mappage constitué d’enregistrements qui associent des lettres aux objets `com.adobe.idp.Document`.
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Appels asynchrones {#asynchronous-invocations}

Certains services AEM Forms, tels que les processus pour des intervenants humains de longue durée, prennent beaucoup de temps. Ces services peuvent être appelés de manière asynchrone et non bloquante. (Voir [Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Un service AEM Forms peut être appelé de manière asynchrone en remplaçant `services` par `async_invoke` dans l’URL d’appel, comme illustré dans l’exemple suivant.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Cette URL renvoie la valeur de l’identifiant (au format « text/plain ») de la tâche responsable de cet appel.

Le statut de l’appel asynchrone peut être récupéré à lʼaide dʼune URL d’appel où `services` est remplacé par `async_status`. L’URL doit contenir un paramètre `job_id` spécifiant la valeur d’identifiant de la tâche associée à cet appel. Par exemple :

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Cette URL renvoie une valeur entière (au format &quot;text/plain&quot;) encodant l’état de la tâche selon la spécification de Job Manager (par exemple, 2 signifie exécution, 3 signifie achèvement, 4 signifie échec, etc.).

Si la tâche est terminée, l’URL renvoie le même résultat que si le service avait été appelé de manière synchrone.

Une fois la tâche terminée et le résultat récupéré, il est possible de supprimer la tâche à l’aide d’une URL d’appel où `services` est remplacé par `async_dispose`. L’URL doit également contenir un paramètre `job_id` spécifiant la valeur d’identifiant de la tâche. Par exemple :

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Si la suppression de la tâche est réussie, cette URL renvoie un message vide.

## Rapport d’erreurs {#error-reporting}

Si une demande d’appel synchrone ou asynchrone ne peut pas être effectuée en raison d’une exception générée sur le serveur, lʼexception est signalée dans le message de réponse HTTP. Si l’URL d’appel (ou la variable `async_result` URL en cas d’appel asynchrone) ne comporte pas de suffixe .xml, le fournisseur REST renvoie le code HTTP `500 Internal Server Error` suivi d’un message d’exception.

Si l’URL d’appel (ou la variable `async_result` L’URL (en cas d’appel asynchrone) comporte un suffixe .xml, le fournisseur REST renvoie le code HTTP `200 OK`suivi d’un document XML décrivant l’exception au format suivant.

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

Lʼélément `DSCError` est facultatif et présent uniquement si l’exception est une instance de `com.adobe.idp.dsc.DSCException`.

## Sécurité et authentification {#security-and-authentication}

Pour assurer un transport sécurisé aux appels REST, un administrateur d’AEM forms peut activer le protocole HTTPS sur le serveur d’applications J2EE hébergeant AEM Forms. Cette configuration est spécifique au serveur d’applications J2EE ; elle ne fait pas partie de la configuration du serveur Forms.

>[!NOTE]
>
>En tant que développeur Workbench souhaitant exposer ses processus via un point d’entrée REST, gardez à l’esprit le problème de la vulnérabilité XSS. Les vulnérabilités XSS peuvent être exploitées pour voler ou manipuler des cookies, modifier la présentation du contenu et compromettre des informations confidentielles. Il est recommandé d’étendre la logique de processus avec les règles supplémentaires de validation des données d’entrée et de sortie pour éviter les problèmes de vulnérabilité XSS.

## Services AEM Forms qui prennent en charge les appels REST {#aem-forms-services-that-support-rest-invocation}

Bien qu’il soit recommandé d’appeler directement les processus créés à l’aide de Workbench plutôt que les services, certains services AEM Forms prennent en charge les appels REST. La raison pour laquelle il est recommandé d’appeler un processus plutôt qu’un service directement est qu’il est plus efficace d’appeler un processus. Considérez le scénario suivant. Supposons que vous souhaitiez créer une politique à partir d’un client REST. En d’autres termes, vous souhaitez que le client REST définisse des valeurs telles que le nom de la politique et la période d’ouverture hors ligne.

Pour créer une politique, vous devez définir des types de données complexes tels que l’objet `PolicyEntry`. Un objet `PolicyEntry` définit des attributs tels que les autorisations associées à la politique. (Voir [Créer des politiques](/help/forms/developing/protecting-documents-policies.md#creating-policies)).

Au lieu d’envoyer une requête REST pour créer une politique (ce qui impliquerait de définir des types de données complexes tels qu’un objet `PolicyEntry`), créez un processus qui crée une politique à l’aide de Workbench. Définissez le processus pour qu’il accepte des variables d’entrée primitives telles qu’une valeur de chaîne qui définit le nom du processus ou un entier qui définit la période d’ouverture hors ligne.

De cette façon, vous n’avez pas à créer de requête d’appel REST qui inclut les types de données complexes requis par l’opération. Le processus définit les types de données complexes et tout ce que vous faites à partir du client REST est d’appeler le processus et de transmettre les types de données primitifs. Pour plus d’informations sur l’appel d’un processus à l’aide de REST, voir [Appel du processus MyApplication/EncryptDocument à l’aide de REST](#rest-invocation-examples).

Les listes suivantes spécifient les services AEM Forms qui prennent en charge les appels REST directs.

* Service Distiller
* Service Rights Management
* Service GeneratePDF
* Service Generate3dPDF
* FormDataIntegration

## Exemples d’appel REST {#rest-invocation-examples}

Les exemples d’appel REST suivants sont fournis :

* Transmettre des valeurs booléennes à un processus AEM Forms.
* Transmettre des valeurs de date à un processus AEM Forms.
* Transmettre des documents à un processus AEM Forms.
* Transmettre des valeurs de document et de texte à un processus AEM Forms.
* Transmettre des valeurs d’énumération à un processus AEM Forms.
* Appeler le processus MyApplication/EncryptDocument à l’aide de REST
* Appeler le processus MyApplication/EncryptDocument depuis d’Acrobat.

  Chaque exemple montre comment transmettre différents types de données à un processus AEM Forms.

**Transmettre des valeurs booléennes à un processus**

L’exemple HTML suivant transmet deux valeurs `Boolean` à un processus AEM Forms appelé `RestTest2`. Le nom de la méthode d’appel est `invoke` et la version est 1.0. Remarquez que la méthode Post HTML est utilisée.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Transmettre des valeurs de date à un processus**

L’exemple HTML suivant transmet une valeur de date à un processus AEM Forms appelé `SOAPEchoService`. Le nom de la méthode d’appel est `echoCalendar`. Remarquez que la méthode HTML `Post` est utilisée.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Transmettre des documents à un processus**

L’exemple HTML suivant appelle un processus AEM Forms nommé `MyApplication/EncryptDocument` qui nécessite un document PDF. Pour plus d’informations sur ce processus, voir [Appeler AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Transmettre des valeurs de document et de texte à un processus**

L’exemple HTML suivant appelle un processus AEM Forms nommé `RestTest3` qui nécessite un document et deux valeurs de texte. Remarquez que la méthode Post HTML est utilisée.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Transmettre des valeurs d’énumération à un processus**

L’exemple HTML suivant appelle un processus AEM Forms nommé `SOAPEchoService` qui nécessite une valeur d’énumération. Remarquez que la méthode Post HTML est utilisée.

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Appeler le processus MyApplication/EncryptDocument à l’aide de REST**

Vous pouvez appeler un processus de courte durée AEM Forms nommé *MyApplication/EncryptDocument* en utilisant REST.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre l’exemple de code, créez un processus appelé `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

Lorsque ce processus est appelé, il effectue les actions suivantes :

1. Obtention du document PDF non sécurisé transmis au processus. Cette action est basée sur l’opération `SetValue`. Le paramètre d’entrée pour ce processus est une variable de processus `document` désignée par `inDoc`.
1. Chiffrement du document PDF avec un mot de passe. Cette action est basée sur l’opération `PasswordEncryptPDF`. Le document PDF chiffré avec un mot de passe est retourné dans une variable de processus nommée `outDoc`.

   Lorsque ce processus est appelé à l’aide d’une requête REST, le document de PDF chiffré s’affiche dans le navigateur web. Avant d’afficher le document PDF, vous devez spécifier le mot de passe (sauf si la protection est désactivée). Le code HTML suivant représente une demande d’appel REST au processus `MyApplication/EncryptDocument`.

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Appeler le processus MyApplication/EncryptDocument depuis Acrobat** {#invoke-process-acrobat}

Vous pouvez appeler un processus Forms depuis Acrobat en effectuant une requête REST. Par exemple, vous pouvez appeler le processus *MyApplication/EncryptDocument*. Pour appeler un processus Forms à partir d’Acrobat, placez un bouton d’envoi sur un fichier XDP dans Designer. (Voir l’[aide de Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr).)

Spécifiez l’URL d’appel du processus dans le *Envoyer à l’URL* , comme illustré ci-dessous.

L’URL complète pour appeler le processus est la suivante : https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Si le processus nécessite un document PDF comme valeur d’entrée, veillez à envoyer le formulaire au format PDF, comme illustré ci-dessus. En outre, pour appeler correctement un processus, il doit renvoyer un document PDF. Sinon, Acrobat ne peut pas traiter la valeur renvoyée et une erreur se produit. Il n’est pas nécessaire de spécifier le nom de la variable de processus d’entrée. Par exemple, le processus *MyApplication/EncryptDocument* comporte une variable d’entrée nommée `inDoc`. Si le formulaire est envoyé au format PDF, il n’est pas nécessaire de spécifier inDoc.

Vous pouvez également envoyer des données de formulaire au format XML à un processus Forms. Pour envoyer des données XML, assurez-vous que la variable `Submit As` La liste déroulante indique le code XML. Comme la valeur renvoyée par le processus doit être un document PDF, ce dernier est affiché dans Acrobat.
