---
title: Appel d’AEM Forms à l’aide de Remoting
seo-title: Appel d’AEM Forms à l’aide de Remoting
description: 'null'
seo-description: 'null'
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Appel d’AEM Forms à l’aide de Remoting {#invoking-aem-forms-using-remoting}

Les processus créés dans Workbench peuvent être appelés à l’aide de Remoting. En d’autres termes, vous pouvez appeler un processus AEM Forms à partir d’une application cliente créée avec Flex. Cette fonctionnalité est basée sur Data Services.

>[!NOTE]
>
>Lors de l’utilisation de Remoting, il est recommandé d’appeler les processus créés dans Workbench par opposition aux services AEM Forms. Il est toutefois possible d’appeler directement les services AEM Forms. (voir Chiffrement des PDF à l’aide de l’outil Remoting situé dans le Centre de développement AEM Forms).

>[!NOTE]
>
>Si un service AEM Forms n’est pas configuré pour autoriser l’accès anonyme, les requêtes d’un client Flex génèrent un problème de navigateur Web. L’utilisateur doit saisir son nom d’utilisateur et son mot de passe.

Le processus de courte durée AEM Forms suivant, nommé `MyApplication/EncryptDocument`, peut être appelé à l’aide de Remoting. (Pour plus d’informations sur ce processus, comme ses valeurs d’entrée et de sortie, voir l’exemple [de processus de](/help/forms/developing/aem-forms-processes.md)courte durée.)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Pour appeler un processus AEM Forms à l’aide d’une application Flex, assurez-vous qu’un point de fin distant est activé. Par défaut, un point de fin distant est activé lorsque vous déployez un processus.

Lorsque ce processus est appelé, il effectue les actions suivantes :

1. Obtient le  PDF non sécurisé transmis en tant que valeur d’entrée. Cette action est basée sur l’opération `SetValue`. Le nom du paramètre d’entrée est `inDoc` et son type de données est `document`. (Le type `document` de données est un type de données disponible dans Workbench.)
1. Chiffrement du document PDF avec un mot de passe. Cette action est basée sur l’opération `PasswordEncryptPDF`. Le nom de la valeur de sortie pour ce processus est `outDoc` et représente le PDF chiffré par mot de passe. Le type de données de outDoc est `document`.
1. Enregistre le PDF chiffré par mot de passe sous la forme d’un fichier PDF dans le système de fichiers local. Cette action est basée sur l’opération `WriteDocument`. 

>[!NOTE]
>
>The `MyApplication/EncryptDocument` process is not based on an existing AEM Forms process. To following along with the code examples, create a process named `MyApplication/EncryptDocument` using Workbench.

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation de Remoting pour appeler un processus de longue durée, voir [Appel de processus](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)longue durée centrés sur l’humain.

**Voir également**

[Inclusion du fichier de bibliothèque Flex d’AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Gestion des  avec AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Authentification des applications clientes créées avec Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Appel de services de composants personnalisés à l’aide de Remoting](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Création d’une application cliente créée avec Flex qui appelle un processus de longue durée axé sur l’humain](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Création d’applications Flash Builder qui effectuent une authentification SSO à l’aide de jetons HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Pour plus d’informations sur l’affichage des données de processus dans un contrôle graphique Flex, voir [Affichage des données de processus AEM Forms dans les graphiques](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)Flex.

>[!NOTE]
>
>*Veillez à placer le fichier crossdomain.xml au bon endroit. Par exemple, si vous avez déployé AEM Forms sur JBoss, placez ce fichier à l’emplacement suivant : &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Inclusion du fichier de bibliothèque Flex d’AEM Forms {#including-the-aem-forms-flex-library-file}

Pour appeler par programmation les processus AEM Forms à l’aide de Remoting, ajoutez le fichier adobe-remoting-provider.swc au chemin de classe de votre projet Flex. Ce fichier SWC se trouve à l’emplacement suivant :

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   où &lt;*install_directory*> correspond au répertoire dans lequel AEM Forms est installé.

**Voir également**

[Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestion des  avec AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Authentification des applications clientes créées avec Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Gestion des  avec Remoting {#handling-documents-with-remoting}

L’un des types Java non primitifs les plus importants utilisés dans AEM Forms est la `com.adobe.idp.Document` classe. Un  est généralement requis pour appeler une opération AEM Forms. Il s’agit principalement d’un  PDF, mais il peut contenir d’autres types de  de tels que SWF, HTML, XML ou un fichier DOC. (See [Passing data to AEM Forms services using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Une application cliente créée avec Flex ne peut pas demander directement un  de. Par exemple, vous ne pouvez pas lancer Adobe Reader pour demander une URL qui génère un fichier PDF. Les demandes de types de  de, tels que PDF et Microsoft Word, renvoient un résultat qui correspond à une URL. Il incombe au client d’afficher le contenu de l’URL. Le service Gestion des  de permet de générer l’URL et les informations sur le type de contenu. Les requêtes de XML  retournent le XML complet  dans le résultat.

### Transmission d’un  en tant que paramètre d’entrée {#passing-a-document-as-an-input-parameter}

Une application cliente créée avec Flex ne peut pas transmettre un  directement à un processus AEM Forms. L’application cliente utilise plutôt une instance de la classe `mx.rpc.livecycle.DocumentReference` ActionScript pour transmettre des paramètres d’entrée à une opération qui attend une `com.adobe.idp.Document` instance. Une application cliente Flex propose plusieurs options pour configurer un `DocumentReference` objet :

* Lorsque le se trouve sur le serveur et que l’emplacement de son fichier est connu, définissez la propriété referenceType de l’objet DocumentReference sur REF_TYPE_FILE. Définissez la propriété fileRef sur l’emplacement du fichier, comme l’illustre l’exemple suivant :

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Lorsque le se trouve sur le serveur et que vous connaissez son URL, définissez la propriété referenceType de l’objet DocumentReference sur REF_TYPE_URL. Définissez la propriété url sur URL, comme l’illustre l’exemple suivant :

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Pour créer un objet DocumentReference à partir d’une chaîne de texte dans l’application cliente, définissez la propriété referenceType de l’objet DocumentReference sur REF_TYPE_INLINE. Définissez la propriété text sur le texte à inclure dans l’objet, comme le montre l’exemple suivant :

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Lorsque le n’est pas sur le serveur, utilisez la servlet de téléchargement Remoting pour télécharger un  vers AEM Forms. La nouvelle fonctionnalité d’AEM Forms permet de télécharger des  sécurisées. Lorsque vous téléchargez un  sécurisé, vous devez utiliser un utilisateur doté du rôle Utilisateur *d’application de téléchargement de* . Sans ce rôle, l’utilisateur ne peut pas télécharger un  sécurisé. Il est recommandé d’utiliser la connexion unique pour télécharger un  sécurisé. (Voir [Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
si AEM Forms est configuré pour autoriser le téléchargement de  non sécurisés, vous pouvez utiliser un utilisateur qui n’a pas le rôle Utilisateur de l’application de téléchargement de  pour télécharger un . Un utilisateur peut également disposer de l’autorisation de téléchargement . Toutefois, si AEM Forms est configuré pour autoriser uniquement les  de sécurisés, assurez-vous que l’utilisateur dispose du rôle Utilisateur de l’application de téléchargement de ou de l’autorisation de téléchargement de l’application . (Voir [Configuration d’AEM Forms pour accepter les](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)sécurisées et non sécurisées.

Vous utilisez des fonctionnalités de téléchargement Flash standard pour l’URL de téléchargement désignée : `https://SERVER:PORT/remoting/lcfileupload`. Vous pouvez ensuite utiliser l’ `DocumentReference` objet lorsqu’un paramètre d’entrée de type `Document` est attendu` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`. Le rapide Remoting utilise la servlet de téléchargement Remoting pour transmettre un fichier PDF au `MyApplication/EncryptDocument`processus. (Voir [Appel d’un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)(obsolète pour AEM Forms).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

Le rapide Remoting  utilise la servlet de téléchargement Remoting pour transmettre un fichier PDF au `MyApplication/EncryptDocument`processus. (Voir [Appel d’un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)(obsolète pour AEM Forms).)

### Transfert d’un  à une application cliente {#passing-a-document-back-to-a-client-application}

Une application cliente reçoit un objet de type `mx.rpc.livecycle.DocumentReference` pour une opération de service qui renvoie une `com.adobe.idp.Document` instance en tant que paramètre de sortie. Comme une application cliente traite des objets ActionScript et non de Java, vous ne pouvez pas transmettre un objet de basé sur Java à un client Flex. Au lieu de cela, le serveur génère une URL pour le  et la transmet au client. La `DocumentReference` propriété de l’ `referenceType` objet spécifie si le contenu se trouve dans l’ `DocumentReference` objet ou doit être récupéré à partir d’une URL dans la propriété `DocumentReference.url` . The `DocumentReference.contentType` property specifies the type of document.

**Voir également**

[Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Inclusion du fichier de bibliothèque Flex d’AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Authentification des applications clientes créées avec Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide de Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Pour appeler un processus AEM Forms à partir d’une application créée avec Flex, effectuez le  de suivant :

1. Create a `mx:RemoteObject` instance.
1. Create a `ChannelSet` instance.
1. Transmettez les valeurs d’entrée requises.
1. Gérez les valeurs renvoyées.

>[!NOTE]
Cette section explique comment appeler un processus AEM Forms et télécharger un lorsqu’AEM Forms est configuré pour télécharger des  non sécurisés. Pour plus d’informations sur la manière d’appeler les processus AEM Forms et de télécharger des  sécurisées et de configurer AEM Forms pour accepter des  sécurisées et non sécurisées, reportez-vous à la page [Transmission d’un](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)de laversion sécurisée pour appeler des processus à l’aide de Remoting.

**Création d’une instance mx:RemoteObject**

Vous créez une `mx:RemoteObject` instance pour appeler un processus AEM Forms créé dans Workbench. Pour créer une `mx:RemoteObject` instance, spécifiez les valeurs suivantes :

* **id :** Nom de l’ `mx:RemoteObject` instance qui représente le processus à appeler.
* **destination :** Nom du processus AEM Forms à appeler. Par exemple, pour appeler le `MyApplication/EncryptDocument` processus, spécifiez `MyApplication/EncryptDocument`.
* **result :** Nom de la méthode Flex qui gère le résultat.

Dans la `mx:RemoteObject` balise, spécifiez une `<mx:method>` balise qui spécifie le nom de la méthode d’appel du processus. En règle générale, le nom d’une méthode d’appel Forms est `invoke`.

L’exemple de code suivant crée une `mx:RemoteObject` instance qui appelle le `MyApplication/EncryptDocument` processus.

```as3
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Création d’un à AEM Forms**

Une application cliente peut appeler AEM Forms en spécifiant un  de dans MXML ou ActionScript, comme l’illustre l’exemple ActionScript suivant. Le  doit être un `AMFChannel`, `SecureAMFChannel`, `HTTPChannel`ou `SecureHTTPChannel`.

```as3
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

Affectez l’ `ChannelSet` instance au champ `mx:RemoteObject` de l’ `channelSet` instance (comme illustré dans l’exemple de code précédent). En règle générale, vous importez la classe  dans une instruction d’importation au lieu de spécifier le nom complet lorsque vous appelez la `ChannelSet.addChannel` méthode.

**Transmission des valeurs d’entrée**

Un processus créé dans Workbench peut prendre zéro ou plusieurs paramètres d’entrée et renvoyer une valeur de sortie. Une application cliente transmet des paramètres d’entrée dans un `ActionScript` objet avec des champs qui correspondent à des paramètres appartenant au processus AEM Forms. Le processus de courte durée, nommé `MyApplication/EncryptDocument`, requiert un paramètre d’entrée nommé `inDoc`. Le nom de l’opération exposée par le processus est `invoke` (nom par défaut d’un processus de courte durée). (Voir [Appel d’AEM Forms à l’aide d’AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)(obsolète pour AEM Forms).)

L’exemple de code suivant transmet un  PDF au `MyApplication/EncryptDocument` processus :

```as3
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

Dans cet exemple de code, `pdfDocument` il s’agit d’une `DocumentReference` instance contenant un PDF non sécurisé. Pour plus d’informations sur une `DocumentReference`solution, voir [Gestion des  de avec AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)(obsolète pour AEM Forms).

**Appel d’une version spécifique d’un service**

Vous pouvez appeler une version spécifique d’un service Forms à l’aide d’un `_version` paramètre dans le mappage de paramètres de l’appel. Par exemple, pour appeler la version 1.2 du `MyApplication/EncryptDocument` service :

```as3
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

Le `version` paramètre doit être une chaîne contenant un point unique. Les valeurs de gauche, de version majeure et de droite, de version mineure de la période doivent être des entiers. Si ce paramètre n’est pas spécifié, la version active de l’en-tête est appelée.

**Gestion des valeurs de retour**

Les paramètres de sortie de processus AEM Forms sont désérialisés en objets ActionScript à partir desquels l’application cliente extrait des paramètres spécifiques par leur nom, comme le montre l’exemple suivant. (La valeur de sortie du `MyApplication/EncryptDocument` processus est nommée `outDoc`.)

```as3
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Appel du processus MyApplication/EncryptDocument**

Vous pouvez appeler le `MyApplication/EncryptDocument` processus en procédant comme suit :

1. Créez une `mx:RemoteObject` instance à l’aide d’ActionScript ou de MXML. Voir Création d’une instance mx:RemoteObject.
1. Configurez une `ChannelSet` instance pour communiquer avec AEM Forms et associez-la à l’ `mx:RemoteObject` instance. Voir Création d’un  à AEM Forms.
1. Appelez la `login` méthode de ChannelSet ou la `setCredentials` méthode du service pour spécifier la valeur d’identifiant utilisateur et le mot de passe. (Voir [Utilisation de la connexion](invoking-aem-forms-using-remoting.md#using-single-sign-on)unique.)
1. Renseignez une `mx.rpc.livecycle.DocumentReference` instance avec un PDF non sécurisé pour le transmettre au `MyApplication/EncryptDocument` processus. (Voir [Transmission d’un  en tant que paramètre](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)d’entrée.)
1. Chiffrez le PDF  en appelant la `mx:RemoteObject` méthode de l’ `invoke` instance. Transmettez le `Object` paramètre d’entrée qui contient le paramètre d’entrée (c’est-à-dire le  PDF non sécurisé). Voir Transfert de valeurs d’entrée.
1. Récupérez le PDF chiffré par mot de passe renvoyé par le processus. Voir Gestion des valeurs renvoyées.

[rapide : Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Authentification des applications clientes créées avec Flex {#authenticating-client-applications-built-with-flex}

Il existe plusieurs manières d’authentifier une requête Remoting à partir d’une application Flex par le gestionnaire utilisateur d’AEM Forms, notamment l’authentification unique d’AEM Forms via le service de connexion central, l’authentification de base et l’authentification personnalisée. Lorsque ni l’authentification unique ni l’accès anonyme ne sont activés, une requête Remoting entraîne une authentification de base (par défaut) ou une authentification personnalisée.

L’authentification de base repose sur l’authentification de base J2EE standard du d’applications Web. Pour l’authentification de base, une erreur HTTP 401 entraîne un problème de navigateur. Cela signifie que lorsque vous tentez de vous connecter à une application Forms à l’aide de RemoteObject et que vous n’êtes pas encore connecté à partir de l’application Flex, le navigateur vous invite à saisir un nom d’utilisateur et un mot de passe.

Pour l’authentification personnalisée, le serveur envoie une erreur au client pour indiquer que l’authentification est requise.

>[!NOTE]
Pour plus d’informations sur l’authentification à l’aide de jetons HTTP, voir [Création d’applications Flash Builder qui effectuent une authentification SSO à l’aide de jetons](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)HTTP.

### Utilisation de l’authentification personnalisée {#using-custom-authentication}

Vous activez l’authentification personnalisée dans Administration Console en passant de la méthode d’authentification de base à la méthode personnalisée sur le point de terminaison distant. Si vous utilisez l’authentification personnalisée, votre application cliente appelle la `ChannelSet.login` méthode de connexion et la `ChannelSet.logout` méthode de déconnexion.

>[!NOTE]
Dans la version précédente d’AEM Forms, vous avez envoyé des informations d’identification à une destination en appelant la `RemoteObject.setCredentials` méthode. La `setCredentials` méthode ne transmettait pas les informations d’identification au serveur avant la première tentative du composant de connexion au serveur. Par conséquent, si le composant a émis un  d’erreur, vous ne pourriez pas être certain que l’erreur est survenue en raison d’une erreur d’authentification ou pour une autre raison. La `ChannelSet.login` méthode se connecte au serveur lorsque vous l’appelez afin que vous puissiez traiter immédiatement un problème d’authentification. Bien que vous puissiez continuer à utiliser la `setCredentials` méthode, il est recommandé d’utiliser la `ChannelSet.login` méthode.

Dans la mesure où plusieurs destinations peuvent utiliser le même  de et l’objet ChannelSet correspondant, la connexion à une destination entraîne la connexion de l’utilisateur à une autre destination qui utilise le même ou le même d’annuaire. Si deux composants appliquent des informations d’identification différentes au même objet ChannelSet, les dernières informations d’identification appliquées sont utilisées. Si plusieurs composants utilisent le même objet ChannelSet authentifié, l’appel de la `logout` méthode déconnecte tous les composants des destinations.

L’exemple suivant utilise les méthodes `ChannelSet.login` et `ChannelSet.logout` avec un contrôle RemoteObject. Cette application effectue les actions suivantes :

* Crée un `ChannelSet` objet dans le `creationComplete` gestionnaire qui représente le  de utilisé par le `RemoteObject` composant.
* Transmet les informations d’identification au serveur en appelant la `ROLogin` fonction en réponse à un de clics sur un bouton 
* Utilise le composant RemoteObject pour envoyer une chaîne au serveur en réponse à un  de clic sur un bouton. Le serveur renvoie la même chaîne au composant RemoteObject.
* Utilise le de résultats du composant RemoteObject pour afficher la chaîne dans un contrôle TextArea
* Déconnecte le serveur en appelant la `ROLogout` fonction en réponse à un de clics sur un bouton 

```as3
 <?xml version=”1.0”?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%”
     height=”100%” creationComplete=”creationCompleteHandler();”>
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login(“sampleuser”, “samplepassword”);
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case “success”:
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case “Client.Authentication”:
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show(“Login failure: “ + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case “success”:
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show(“Logout failure: “ + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += “Server responded: “+ event.result + “\n”;
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += “Received fault: “ + event.fault + “\n”;
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text=”Enter a text for the server to echo”/>
         <mx:TextInput id=”ti” text=”Hello World!”/>
         <mx:Button label=”Login”
             click=”ROLogin();”/>
         <mx:Button label=”Echo”
             enabled=”{authenticatedCB.selected}”
             click=”remoteObject.echo(ti.text);”/>
         <mx:Button label=”Logout”
             click=”ROLogout();”/>
         <mx:CheckBox id=”authenticatedCB”
             label=”Authenticated?”
             enabled=”false”/>
     </mx:HBox>
     <mx:TextArea id=”ta” width=”100%” height=”100%”/>
 
     <mx:RemoteObject id=”remoteObject”
         destination=”myDest”
         result=”resultHandler(event);”
         fault=”faultHandler(event);”/>
 </mx:Application>
```

Les méthodes `login` et `logout` renvoient un objet AsyncToken. Affectez des gestionnaires de  à l’objet AsyncToken pour que le de résultats  gérer un appel réussi et pour que le d’erreur  gérer un échec.

### Utilisation de la connexion unique {#using-single-sign-on}

Les utilisateurs d’AEM Forms peuvent se connecter à plusieurs applications Web AEM Forms pour effectuer un . Lorsque les utilisateurs passent d’une application Web à une autre, il n’est pas efficace de les obliger à se connecter séparément à chaque application Web. Le mécanisme de connexion unique d’AEM Forms permet aux utilisateurs de se connecter une seule fois, puis d’accéder à toute application Web d’AEM Forms. Les développeurs AEM Forms pouvant créer des applications clientes à utiliser avec AEM Forms, ils doivent également pouvoir tirer parti du mécanisme de connexion unique.

Chaque application Web AEM Forms est mise en package dans son propre fichier d’archive Web (WAR), qui est ensuite inclus dans un fichier d’archive d’entreprise (EAR). Etant donné qu’un serveur d’applications n’autorise pas le partage des données de session entre différentes applications Web, AEM Forms utilise des cookies HTTP pour stocker les informations d’authentification. Les cookies d’authentification permettent à un utilisateur de se connecter à une application Forms, puis de se connecter à d’autres applications Web AEM Forms. Cette technique est connue sous le nom de connexion unique.

Les développeurs AEM Forms écrivent des applications clientes pour étendre les fonctionnalités des guides de formulaire (obsolète) et personnaliser Workspace. Par exemple, une application Workspace peut  un processus. L’application cliente utilise ensuite un point de fin distant pour récupérer les données du service Forms.

Lorsqu’un service AEM Forms est appelé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms), l’application cliente transmet le cookie d’authentification dans le cadre de la requête. L’utilisateur ayant déjà été authentifié, aucune connexion supplémentaire n’est requise pour établir une connexion à partir de l’application cliente vers le service AEM Forms.

>[!NOTE]
Si un cookie n’est pas valide ou est absent, il n’existe aucune redirection implicite vers une page de connexion. Par conséquent, vous pouvez toujours appeler un service anonyme.

Vous pouvez contourner le mécanisme de connexion unique d’AEM Forms en écrivant une application cliente qui se connecte et se déconnecte toute seule. Si vous contournez le mécanisme de connexion unique, vous pouvez utiliser l’authentification de base ou personnalisée avec votre application.

Ce mécanisme n’utilisant pas le mécanisme de connexion unique d’AEM Forms, aucun cookie d’authentification n’est écrit au client. Les informations d’identification de connexion sont stockées dans l’ `ChannelSet` objet pour le  de connexion à distance. Par conséquent, tous les `RemoteObject` appels que vous faites sur la même `ChannelSet` sont effectués dans le contexte de ces informations d’identification.

### Configuration de l’authentification unique dans AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Pour utiliser l’authentification unique dans AEM Forms, installez le composant de processus des formulaires, qui inclut le service de connexion centralisé. Une fois qu’un utilisateur se connecte correctement, le service de connexion centralisé renvoie un cookie d’authentification à l’utilisateur. Chaque requête suivante à une application Web Forms contient le cookie. Si le cookie est valide, l’utilisateur est considéré comme authentifié et n’a pas à se reconnecter.

### Ecriture d’une application cliente utilisant l’authentification unique {#writing-a-client-application-that-uses-single-sign-on}

Lorsque vous profitez du mécanisme de connexion unique, vous vous attendez à ce que les utilisateurs se connectent en utilisant le service de connexion centralisé avant de démarrer une application cliente. En d’autres termes, une application cliente ne se connecte pas par le biais du navigateur ou en appelant la `ChannelSet.login` méthode.

Si vous utilisez le mécanisme de connexion unique d’AEM Forms, configurez le point de fin Remoting pour qu’il utilise l’authentification personnalisée, et non l’authentification de base. Sinon, lors de l’utilisation de l’authentification de base, une erreur d’authentification entraîne un problème pour le navigateur, que vous ne souhaitez pas voir. Au lieu de cela, votre application détecte l’erreur d’authentification, puis affiche un message demandant à l’utilisateur de se connecter à l’aide du service de connexion centralisé.

Une application cliente accède à AEM Forms par le biais d’un point de fin distant à l’aide du `RemoteObject` composant, comme l’illustre l’exemple suivant.

```as3
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Connexion en tant que nouvel utilisateur pendant l’exécution de l’application Flex**

Une application créée avec Flex inclut le cookie d’authentification avec chaque requête à un service AEM Forms. Pour des raisons de performances, AEM Forms ne valide pas le cookie pour chaque requête. Toutefois, AEM Forms détecte lorsqu’un cookie d’authentification est remplacé par un autre cookie d’authentification.

Par exemple, vous  une application cliente et, lorsque l’application est active, vous utilisez le service de connexion centralisé pour vous déconnecter. Vous pouvez ensuite vous connecter en tant qu’utilisateur différent. La connexion en tant qu’autre utilisateur remplace le cookie d’authentification existant par un cookie d’authentification pour le nouvel utilisateur.

Dans la requête suivante de l’application cliente, AEM Forms détecte que le cookie a changé et déconnecte l’utilisateur. Par conséquent, la première requête après un changement de cookie échoue. Toutes les requêtes suivantes sont effectuées dans le contexte du nouveau cookie et sont réussies.

**Déconnexion**

Pour vous déconnecter d’AEM Forms et invalider une session, le cookie d’authentification doit être supprimé de l’ordinateur du client. L’authentification unique ayant pour but de permettre à un utilisateur de se connecter une seule fois, vous ne souhaitez pas qu’une application cliente supprime le cookie. Cette action déconnecte l’utilisateur.

Par conséquent, l’appel de la `RemoteObject.logout` méthode dans une application cliente génère un message d’erreur sur le client, indiquant que la session n’est pas déconnectée. L’utilisateur peut plutôt utiliser le service de connexion centralisé pour se déconnecter et supprimer le cookie d’authentification.

**Déconnexion pendant l’exécution de l’application Flex**

Vous pouvez  une application cliente créée avec Flex et utiliser le service de connexion centralisé pour vous déconnecter. Dans le cadre du processus de déconnexion, le cookie d’authentification est supprimé. Si une demande de suppression est effectuée sans cookie ou avec un cookie non valide, la session utilisateur est invalidée. Cette action est en effet une déconnexion. La prochaine fois que l’application cliente tente de se connecter à un service AEM Forms, l’utilisateur est invité à se connecter.

**Voir également**

[Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestion des  avec AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusion du fichier de bibliothèque Flex d’AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}

Vous pouvez transmettre des  sécurisées à AEM Forms lors de l’appel d’un processus qui nécessite un ou plusieurs  de. En transmettant un sécurisé, vous protégez les informations commerciales et les  de confidentielles. Dans ce cas, un peut faire référence à un  PDF, un XML, un Word, etc. La transmission d’un sécurisé à AEM Forms à partir d’une application cliente écrite dans Flex est requise lorsque AEM Forms est configuré pour autoriser des  sécurisées. (Voir [Configuration d’AEM Forms pour accepter les](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)sécurisées et non sécurisées.)

Lorsque vous transmettez un sécurisé, utilisez l’authentification unique et spécifiez un utilisateur AEM forms doté du rôle Utilisateur *d’application de téléchargement de l’* . Sans ce rôle, l’utilisateur ne peut pas télécharger un  sécurisé. Vous pouvez attribuer un rôle par programmation à un utilisateur. (voir [Gestion des rôles et des autorisations](/help/forms/developing/users.md#managing-roles-and-permissions)).

>[!NOTE]
Lorsque vous créez un nouveau rôle et souhaitez que les membres de ce rôle téléchargent des  de sécurisées, assurez-vous de spécifier l’autorisation de téléchargement .

AEM Forms prend en charge une opération nommée `getFileUploadToken` qui renvoie un jeton transmis à la servlet de téléchargement. La `DocumentReference.constructRequestForUpload` méthode requiert une URL vers AEM Forms avec le jeton renvoyé par la `LC.FileUploadAuthenticator.getFileUploadToken` méthode. Cette méthode renvoie un `URLRequest` objet utilisé dans l’appel à la servlet de téléchargement. Le code suivant illustre cette logique d’application.

```as3
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### Configuration d’AEM Forms pour accepter les  de sécurisées et non sécurisées {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

Vous pouvez utiliser Administration Console pour indiquer si les  sont sécurisés lors de la transmission d’un  d’une application cliente Flex à un processus AEM Forms. Par défaut, AEM Forms est configuré pour accepter les  de sécurisés. Vous pouvez configurer AEM Forms pour accepter des  sécurisées en procédant comme suit :

1. Connectez-vous à Administration Console.
1. Cliquez sur **Paramètres**.
1. Cliquez sur Paramètres **de Core System.**
1. Cliquez sur Configurations.
1. Assurez-vous que l’option Autoriser le téléchargement de  non sécurisés à partir des applications Flex est désélectionnée.

>[!NOTE]
Pour configurer AEM Forms de manière à accepter les  non sécurisées, sélectionnez l’option Autoriser le transfert de non sécurisés à partir des applications Flex. Redémarrez ensuite une application ou un service pour vous assurer que le paramètre prend effet.

###  rapide : Appel d’un processus de courte durée en transmettant un sécurisé à l’aide de l’option Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

L’exemple de code suivant appelle l’utilisateur `MyApplication/EncryptDocument.`A doit se connecter pour cliquer sur le bouton Sélectionner un fichier utilisé pour télécharger un fichier PDF et appeler le processus. En d’autres termes, une fois l’utilisateur authentifié, le bouton Sélectionner un fichier est activé. L’illustration suivante présente l’application cliente Flex après l’authentification d’un utilisateur. Notez que la case à cocher authentifiée est activée.

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

si AEM Forms est configuré pour autoriser uniquement le téléchargement d’un sécurisé et que l’utilisateur n’a pas le rôle Utilisateur *de l’application de téléchargement de* , une exception est générée. Si l’utilisateur dispose de ce rôle, le fichier est téléchargé et le processus est appelé.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef’s url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**Voir également**

[Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestion des  avec AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusion du fichier de bibliothèque Flex d’AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Authentification des applications clientes créées avec Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Appel de services de composants personnalisés à l’aide de Remoting {#invoking-custom-component-services-using-remoting}

Vous pouvez appeler des services situés dans un composant personnalisé à l’aide de Remoting. Prenons l’exemple du composant Banque qui contient le service à la clientèle. Vous pouvez appeler des opérations qui appartiennent au service Client à l’aide d’une application cliente écrite dans Flex. Avant d’exécuter le  rapide associé à cette section, vous devez créer le composant personnalisé Banque.

Le service clientèle expose une opération nommée `createCustomer`. Cette discussion explique comment créer une application cliente Flex qui appelle le service client et crée un client. Cette opération nécessite un objet complexe de type `com.adobe.livecycle.sample.customer.Customer` qui représente le nouveau client. L’illustration suivante présente l’application cliente qui appelle le service client et crée un nouveau client. L’ `createCustomer` opération renvoie une valeur d’identifiant client. La valeur de l’identifiant s’affiche dans la zone de texte Identifiant du client.

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

Le tableau suivant  les contrôles qui font partie de cette application cliente.

<table>
 <thead>
  <tr>
   <th><p>Nom du contrôle</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>Indique le prénom du client. </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>Indique le nom de famille du client. </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>Indique le numéro de téléphone du client.</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>Indique le nom de rue du client.</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>Indique l’état du client. </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>Indique le code postal du client. </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>Indique la ville du client.</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>Indique la valeur d’identifiant du client à laquelle appartient le nouveau compte. Cette zone de texte est renseignée par la valeur de retour de l’ <code>createCustomer</code> opération du service à la clientèle. </p></td>
  </tr>
 </tbody>
</table>

### Mappage des types de données complexes d’AEM Forms {#mapping-aem-forms-complex-data-types}

Certaines opérations AEM Forms nécessitent des types de données complexes comme valeurs d’entrée. Ces types de données complexes définissent les valeurs d’exécution utilisées par l’opération. Par exemple, l’ `createCustomer` opération du service clientèle nécessite une `Customer` instance qui contient les valeurs d’exécution requises par le service. Sans le type complexe, le service à la clientèle renvoie une exception et n’effectue pas l’opération.

Lors de l’appel d’un service AEM Forms, créez des objets ActionScript qui correspondent aux types complexes AEM Forms requis. Pour chaque type de données complexe requis par une opération, créez un objet ActionScript distinct.

Dans la classe ActionScript, utilisez la balise `RemoteClass` de métadonnées pour mapper au type complexe AEM Forms. Par exemple, lors de l’appel de l’ `createCustomer` opération du service client, créez une classe ActionScript qui mappe au type de `com.adobe.livecycle.sample.customer.Customer` données.

La classe ActionScript suivante nommée Customer indique comment mapper au type de données AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

```as3
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

Le type de données complet du type complexe AEM Forms est affecté à la balise d’alias.

Les champs de la classe ActionScript correspondent aux champs appartenant au type complexe AEM Forms. Les six champs situés dans la classe ActionScript du client correspondent aux champs qui appartiennent à `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Une bonne méthode pour déterminer les noms de champ appartenant à un type complexe Forms consiste à le fichier WSDL d’un service dans un navigateur Web. Un WSDL spécifie les types complexes d’un service et les membres de données correspondants. Le fichier WSDL suivant est utilisé pour le service clientèle : `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

La classe ActionScript du client appartient à un package nommé customer. Il est recommandé de placer toutes les classes ActionScript qui correspondent à des types de données AEM Forms complexes dans leur propre package. Créez un dossier dans le dossier src du projet Flex et importez le fichier ActionScript dans le dossier, comme illustré ci-dessous.

![iu_iu_customeras](assets/iu_iu_customeras.png)

###  rapide : Appel du service personnalisé Client à l’aide de Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}

L’exemple de code suivant appelle le service client et crée un nouveau client. Lorsque vous exécutez cet exemple de code, veillez à remplir toutes les zones de texte. Assurez-vous également de créer le fichier Customer.as vers `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Avant d’exécuter cette  rapide, vous devez créer et déployer le composant personnalisé Banque.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**Feuille de style**

Ce  rapide contient une feuille de style nommée *bank.css*. Le code suivant représente la feuille de style utilisée.

```as3
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**Voir également**

[Appel d’AEM Forms à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestion des  avec AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusion du fichier de bibliothèque Flex d’AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Appeler un processus de courte durée en transmettant un  non sécurisé à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Authentification des applications clientes créées avec Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmission d’un sécurisé pour appeler des processus à l’aide de Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
