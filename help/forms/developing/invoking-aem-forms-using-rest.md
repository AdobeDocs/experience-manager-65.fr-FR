---
title: Appeler AEM Forms à l’aide de requêtes REST
seo-title: Appeler AEM Forms à l’aide de requêtes REST
description: Appelez les processus créés dans Workbench à l’aide de requêtes REST.
seo-description: Appelez les processus créés dans Workbench à l’aide de requêtes REST.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2521'
ht-degree: 4%

---


# Appeler AEM Forms à l’aide de requêtes REST {#invoking-aem-forms-using-rest-requests}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

les processus créés dans Workbench peuvent être configurés pour être invoqués via des demandes REST (Representational State Transfer). Ces demandes sont envoyées à partir de pages HTML. En d’autres termes, vous pouvez appeler un processus Forms directement à partir d’une page Web à l’aide d’une requête REST. Par exemple, vous pouvez ouvrir une nouvelle instance d’une page Web. Ensuite, vous pouvez appeler un processus Forms et charger un document PDF rendu avec des données qui ont été envoyées dans une demande de POST HTTP.

Il existe deux types de clients HTML. Le premier client HTML est un client AJAX qui est écrit en JavaScript. Le deuxième client est un formulaire HTML contenant un bouton d’envoi. Une application cliente HTML n’est pas le seul client REST possible. Toute application cliente prenant en charge les requêtes HTTP peut appeler un service à l’aide d’un appel REST. Par exemple, vous pouvez appeler un service en utilisant un appel REST à partir d’un formulaire PDF. (Voir [Appel du processus MyApplication/EncryptDocument à partir d’Acrobat](#rest-invocation-examples).)

Lors de l’utilisation de requêtes REST, il est recommandé de ne pas appeler directement les services Forms. Appelez plutôt les processus créés dans Workbench. Lors de la création d’un processus destiné à un appel REST, utilisez un point de début programmatique. Dans ce cas, le point de terminaison REST est ajouté automatiquement. Pour plus d’informations sur la création de processus dans Workbench, voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Lorsque vous appelez un service à l’aide de REST, vous êtes invité à saisir un nom d’utilisateur et un mot de passe AEM forms. Cependant, si vous ne souhaitez pas spécifier de nom d’utilisateur et de mot de passe, vous pouvez désactiver la sécurité du service.

Pour appeler un service Forms (un processus devient un service lorsque le processus est activé) à l’aide de REST, configurez un point de terminaison REST. (voir Gestion des points de terminaison dans [Aide à l&#39;administration](https://www.adobe.com/go/learn_aemforms_admin_63).)

Une fois qu’un point de terminaison REST est configuré, vous pouvez appeler un service Forms à l’aide d’une méthode de GET HTTP ou d’une méthode de POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

La valeur obligatoire `ServiceName` est le nom du service Forms à appeler. La valeur facultative `OperationName` correspond au nom de l’opération du service. Si cette valeur n&#39;est pas spécifiée, ce nom est défini par défaut sur `invoke`, qui est le nom de l&#39;opération qui début le processus. La valeur facultative `ServiceVersion` correspond à la version codée au format X.Y. Si cette valeur n’est pas spécifiée, la version la plus récente est utilisée. La valeur `enctype` peut également être `application/x-www-form-urlencoded`.

## Types de données pris en charge {#supported-data-types}

Les types de données suivants sont pris en charge lors de l’appel de services AEM Forms à l’aide de requêtes REST :

* Types de données Java primitifs, tels que Chaînes et entiers
* `com.adobe.idp.Document` type de données
* Types de données XML tels que `org.w3c.Document` et `org.w3c.Element`
* Objets de collection tels que `java.util.List` et `java.util.Map`

   Ces types de données sont généralement acceptés en tant que valeurs d’entrée pour les processus créés dans Workbench.

   Si un service Forms est appelé avec la méthode de POST HTTP, les arguments sont transmis dans le corps de la requête HTTP. Si la signature du service AEM Forms comporte un paramètre d’entrée de chaîne, le corps de la requête peut contenir la valeur de texte du paramètre d’entrée. Si la signature du service définit plusieurs paramètres de chaîne, la requête peut suivre la notation `application/x-www-form-urlencoded` HTTP avec les noms de paramètre utilisés comme noms de champ du formulaire.

   Si un service Forms renvoie un paramètre de chaîne, le résultat est une représentation textuelle du paramètre de sortie. Si un service renvoie plusieurs paramètres de chaîne, le résultat est un document XML codant les paramètres de sortie au format suivant :
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >La valeur `output-paramater1` représente le nom du paramètre de sortie.

   Si un service Forms requiert un paramètre `com.adobe.idp.Document`, le service ne peut être appelé qu&#39;à l&#39;aide de la méthode du POST HTTP. Si le service requiert un paramètre `com.adobe.idp.Document`, le corps de la requête HTTP devient le contenu de l’objet de Document d’entrée.

   Si un service AEM Forms requiert plusieurs paramètres d’entrée, le corps de la requête HTTP doit être un message MIME en plusieurs parties, tel que défini par la RFC 1867. (RFC 1867 est une norme utilisée par les navigateurs Web pour télécharger des fichiers sur des sites Web.) Chaque paramètre d&#39;entrée doit être envoyé en tant que partie distincte du message multipartie et codé au format `multipart/form-data`. Le nom de chaque pièce doit correspondre au nom du paramètre.

   Les listes et les mappages sont également utilisés comme valeurs d’entrée pour les processus AEM Forms créés dans Workbench. Par conséquent, vous pouvez utiliser ces types de données lors de l’utilisation d’une requête REST. Les tableaux Java ne sont pas pris en charge car ils ne sont pas utilisés comme valeur d’entrée pour un processus AEM Forms.

   Si un paramètre d’entrée est une liste, un client REST peut l’envoyer en le spécifiant plusieurs fois (une fois pour chaque élément de la liste). Par exemple, si A est une liste de documents, l&#39;entrée doit être un message en plusieurs parties composé de plusieurs parties nommées A. Dans ce cas, chaque partie nommée A devient un élément dans la liste d&#39;entrée. Si B est une liste de chaînes, l’entrée peut être un message `application/x-www-form-urlencoded` composé de plusieurs champs nommés B. Dans ce cas, chaque champ de formulaire nommé B devient un élément dans la liste d’entrée.

   Si un paramètre d’entrée est un mappage et qu’il s’agit du seul paramètre d’entrée des services, alors chaque partie/champ du message d’entrée devient un enregistrement clé/valeur dans le mappage. Le nom de chaque pièce/champ devient la clé de l&#39;enregistrement. Le contenu de chaque pièce/champ devient la valeur de l’enregistrement.

   Si un mappage d’entrée n’est pas le seul paramètre d’entrée des services, chaque enregistrement de clé/valeur qui appartient au mappage peut être envoyé à l’aide d’un paramètre nommé en tant que concaténation du nom du paramètre et de la clé de l’enregistrement. Par exemple, une carte d’entrée appelée `attributes` peut être envoyée avec une liste des paires clé/valeurs suivantes :

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Cela se traduit par une carte de trois records : `Color=red`, `Shape=box` et `Width=5`.

   Les paramètres de sortie des types de liste et de mappage deviennent partie intégrante du message XML résultant. La liste de sortie est représentée en XML sous la forme d’une série d’éléments XML avec un élément pour chaque élément de la liste. Chaque élément reçoit le même nom que le paramètre de liste de sortie. La valeur de chaque élément XML est l’une des deux valeurs suivantes :

* Représentation textuelle de l’élément dans la liste (si la liste se compose de types de chaîne)
* URL pointant vers le contenu du Document (si la liste se compose d&#39;objets `com.adobe.idp.Document`)

   L’exemple suivant est un message XML renvoyé par un service dont le paramètre de sortie unique est *liste*, qui est une liste de nombres entiers.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un paramètre de mappage de sortie est représenté dans le message XML résultant sous la forme d’une série d’éléments XML avec un élément pour chaque enregistrement dans le mappage. Chaque élément reçoit le même nom que la clé de l’enregistrement de mappage. La valeur de chaque élément est soit une représentation textuelle de la valeur de l’enregistrement de mappage (si le mappage est constitué d’enregistrements avec une valeur de chaîne), soit une URL pointant vers le contenu du Document (si le mappage est constitué d’enregistrements avec la valeur `com.adobe.idp.Document`). Vous trouverez ci-dessous un exemple de message XML renvoyé par un service dont le paramètre de sortie unique est `map`. Cette valeur de paramètre est une carte composée d’enregistrements qui associent des lettres à des objets `com.adobe.idp.Document`.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Appels asynchrones {#asynchronous-invocations}

Certains services AEM Forms, tels que les processus de longue durée centrés sur l&#39;homme, nécessitent un certain temps. Ces services peuvent être appelés de manière asynchrone sans blocage. (Voir [Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Un service AEM Forms peut être appelé de manière asynchrone en remplaçant `services` par `async_invoke` dans l’URL d’appel, comme indiqué dans l’exemple suivant.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Cette URL renvoie la valeur d’identificateur (au format &quot;texte/brut&quot;) de la tâche responsable de cet appel.

L&#39;état de l&#39;appel asynchrone peut être récupéré en utilisant une URL d&#39;appel avec `services` remplacé par `async_status`. L’URL doit contenir un paramètre `job_id` spécifiant la valeur d’identificateur de la tâche associée à cet appel. Par exemple :

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Cette URL renvoie une valeur entière (au format &quot;texte/brut&quot;) codant l’état de la tâche conformément aux spécifications de Job Manager (par exemple, 2 signifie en cours d’exécution, 3 signifie terminé, 4 signifie échoué, etc.).

Si la tâche est terminée, l’URL renvoie le même résultat que si le service a été appelé de manière synchrone.

Une fois la tâche terminée et le résultat récupéré, la tâche peut être éliminée en utilisant une URL d&#39;appel avec `services` est remplacée par `async_dispose`. L’URL doit également contenir un paramètre `job_id` spécifiant la valeur d’identificateur de la tâche. Par exemple :

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Si la tâche est correctement éliminée, cette URL renvoie un message vide.

## Rapports d&#39;erreur {#error-reporting}

Si une demande d’appel synchrone ou asynchrone ne peut pas être effectuée en raison d’une exception émise sur le serveur, l’exception est signalée dans le message de réponse HTTP. Si l’URL d’appel (ou l’URL `async_result` en cas d’appel asynchrone) ne comporte pas de suffixe .xml, le fournisseur REST renvoie le code HTTP `500 Internal Server Error` suivi d’un message d’exception.

Si l’URL d’appel (ou l’URL `async_result` en cas d’appel asynchrone) comporte un suffixe .xml, le fournisseur REST renvoie le code HTTP `200 OK`suivi d’un document XML décrivant l’exception au format suivant.

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

L&#39;élément `DSCError` est facultatif et présent uniquement si l&#39;exception est une instance de `com.adobe.idp.dsc.DSCException`.

## Sécurité et authentification {#security-and-authentication}

Pour fournir des appels REST avec un transport sécurisé, un administrateur d’AEM forms peut activer le protocole HTTPS sur le serveur d’applications J2EE hébergeant AEM Forms. Cette configuration est spécifique au serveur d’applications J2EE ; il ne fait pas partie de la configuration du serveur de formulaires.

>[!NOTE]
>
>En tant que développeur Workbench qui souhaite exposer vos processus via un point de terminaison REST, gardez à l’esprit le problème de vulnérabilité XSS. Les vulnérabilités XSS peuvent être utilisées pour voler ou manipuler des cookies, modifier la présentation du contenu et compromettre des informations confidentielles. Il est recommandé d’étendre la logique de processus avec les règles supplémentaires de validation des données d’entrée et de sortie si la vulnérabilité XSS pose problème.

## Services AEM Forms prenant en charge l’appel REST {#aem-forms-services-that-support-rest-invocation}

Bien qu’il soit recommandé d’appeler directement des processus créés à l’aide de Workbench plutôt que des services, certains services AEM Forms prennent en charge l’appel REST. La raison pour laquelle il est recommandé d’appeler directement un processus par rapport à un service est qu’il est plus efficace d’appeler un processus. Examinons le scénario suivant. Supposons que vous souhaitiez créer une stratégie à partir d’un client REST. Autrement dit, vous souhaitez que le client REST définisse des valeurs telles que le nom de la stratégie, la période d’ouverture hors connexion.

Pour créer une stratégie, vous devez définir des types de données complexes tels qu&#39;un objet `PolicyEntry`. Un objet `PolicyEntry` définit des attributs tels que les autorisations associées à la stratégie. (Voir [Création de stratégies](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Au lieu d’envoyer une requête REST pour créer une stratégie (qui inclurait la définition de types de données complexes tels qu’un objet `PolicyEntry`), créez un processus qui crée une stratégie à l’aide de Workbench. Définissez le processus pour accepter des variables d’entrée primitives, telles qu’une valeur de chaîne qui définit le nom du processus ou un entier qui définit la période d’ouverture hors connexion.

Ainsi, vous n’avez pas à créer une demande d’appel REST qui inclut des types de données complexes requis par l’opération. Le processus définit les types de données complexes et tout ce que vous faites à partir du client REST est d’appeler le processus et de transmettre des types de données primitifs. Pour plus d’informations sur l’appel d’un processus à l’aide de REST, voir [Appel du processus MyApplication/EncryptDocument à l’aide de REST](#rest-invocation-examples).

Les listes suivantes spécifient les services AEM Forms qui prennent en charge l’appel direct REST.

* Service Distiller
* Service Rights Management
* Service GeneratePDF
* Service Generate3dPDF
* FormDataIntegration

## Exemples d&#39;appel REST {#rest-invocation-examples}

Les exemples d’appel REST suivants sont fournis :

* Transmission de valeurs booléennes à un processus AEM Forms
* Transfert de valeurs de date à un processus AEM Forms
* Transmission de documents à un processus AEM Forms
* Transmission de valeurs de document et de texte à un processus AEM Forms
* Transmission de valeurs de énumération à un processus AEM Forms
* Appel du processus MyApplication/EncryptDocument à l’aide de REST
* Appel du processus MyApplication/EncryptDocument depuis Acrobat

   Chaque exemple montre comment transférer différents types de données à un processus AEM Forms

**Transfert de valeurs booléennes à un processus**

L&#39;exemple HTML suivant transmet deux valeurs `Boolean` à un processus AEM Forms nommé `RestTest2`. Le nom de la méthode d’appel est `invoke` et la version est 1.0. Notez que la méthode de publication HTML est utilisée.

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

**Transfert de valeurs de date à un processus**

L&#39;exemple HTML suivant transmet une valeur de date à un processus AEM Forms nommé `SOAPEchoService`. Le nom de la méthode d’appel est `echoCalendar`. Notez que la méthode HTML `Post` est utilisée.

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

**Transmission de documents à un processus**

L’exemple HTML suivant appelle un processus AEM Forms nommé `MyApplication/EncryptDocument` qui requiert un document PDF. Pour plus d’informations sur ce processus, voir [Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

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

**Transmission de valeurs de document et de texte à un processus**

L&#39;exemple HTML suivant appelle un processus AEM Forms nommé `RestTest3` qui requiert un document et deux valeurs de texte. Notez que la méthode de publication HTML est utilisée.

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

**Transfert de valeurs de énumération à un processus**

L&#39;exemple HTML suivant appelle un processus AEM Forms nommé `SOAPEchoService` qui requiert une valeur de énumération. Notez que la méthode de publication HTML est utilisée.

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

**Appel du processus MyApplication/EncryptDocument à l’aide de REST**

Vous pouvez appeler un processus de courte durée AEM Forms nommé *MyApplication/EncryptDocument* à l’aide de REST.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre l’exemple de code, créez un processus nommé `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Lorsque ce processus est appelé, il effectue les actions suivantes :

1. Obtention du document PDF non sécurisé transmis au processus. Cette action est basée sur l’opération `SetValue`. Le paramètre d’entrée pour ce processus est une variable de processus `document` désignée par `inDoc`.
1. Chiffrement du document PDF avec un mot de passe. Cette action est basée sur l’opération `PasswordEncryptPDF`. Le document PDF chiffré avec un mot de passe est retourné dans une variable de processus nommée `outDoc`.

   Lorsque ce processus est appelé à l’aide d’une requête REST, le document PDF chiffré s’affiche dans le navigateur Web. Avant de vue le document PDF, vous devez indiquer le mot de passe (sauf si la sécurité est désactivée). Le code HTML suivant représente une demande d&#39;appel REST au processus `MyApplication/EncryptDocument`.

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

**Appel du processus MyApplication/EncryptDocument depuis Acrobat** {#invoke-process-acrobat}

Vous pouvez appeler un processus Forms à partir de Acrobat en utilisant une requête REST. Par exemple, vous pouvez appeler le processus *MyApplication/EncryptDocument*. Pour appeler un processus Forms à partir de Acrobat, placez un bouton d’envoi sur un fichier XDP dans Designer. (Voir l’[aide de Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Spécifiez l’URL permettant d’appeler le processus dans le champ *Envoyer à l’URL* du bouton, comme illustré ci-dessous.

L’URL complète permettant d’appeler le processus est https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Si le processus nécessite un document PDF en tant que valeur d’entrée, veillez à envoyer le formulaire au format PDF, comme illustré ci-dessus. En outre, pour appeler un processus avec succès, le processus doit renvoyer un document PDF. Dans le cas contraire, Acrobat ne peut pas gérer la valeur renvoyée et une erreur se produit. Il n’est pas nécessaire de spécifier le nom de la variable de processus d’entrée. Par exemple, le processus *MyApplication/EncryptDocument* comporte une variable d’entrée nommée `inDoc`. Il n’est pas nécessaire de spécifier inDoc tant que le formulaire est envoyé au format PDF.

Vous pouvez également envoyer des données de formulaire au format XML à un processus Forms. Pour envoyer des données XML, assurez-vous que la liste déroulante `Submit As` spécifie XML. Dans la mesure où la valeur renvoyée par le processus doit être un document PDF, le document PDF s’affiche dans Acrobat.
