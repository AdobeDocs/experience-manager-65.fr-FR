---
title: Validation de documents DDX
seo-title: Validation de documents DDX
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Validation de documents DDX {#validating-ddx-documents}

Vous pouvez valider par programmation un document DDX utilisé par le service Assembler. En d’autres termes, à l’aide de l’API du service Assembler, vous pouvez déterminer si un document DDX est valide ou non. Par exemple, si vous avez effectué une mise à niveau à partir d’une version précédente d’AEM Forms et souhaitez vous assurer que votre document DDX est valide, vous pouvez le valider à l’aide de l’API du service Assembler.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Assembler Service et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour valider un document DDX, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client Assembler.
1. Référencez un document DDX existant.
1. Définissez les options d’exécution pour valider le document DDX.
1. Effectuez la validation.
1. Enregistrez les résultats de la validation dans un fichier journal.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référence à un document DDX existant**

Pour valider un document DDX, vous devez référencer un document DDX existant.

**Définition des options d’exécution pour valider le document DDX**

Lors de la validation d’un document DDX, vous devez définir des options d’exécution spécifiques qui demandent au service Assembler de valider le document DDX au lieu de l’exécuter. Vous pouvez également augmenter la quantité d’informations que le service Assembler écrit dans le fichier journal.

**Effectuer la validation**

Après avoir créé le client de service Assembler, fait référence au document DDX et défini les options d’exécution, vous pouvez appeler l’ `invokeDDX` opération pour valider le document DDX. Lors de la validation du document DDX, vous pouvez transmettre `null` le paramètre map (ce paramètre stocke généralement les documents PDF dont Assembler a besoin pour effectuer les opérations spécifiées dans le document DDX).

Si la validation échoue, une exception est générée et le fichier journal contient des détails qui expliquent pourquoi le document DDX n’est pas valide peut être obtenu à partir de l’ `OperationException` instance. Une fois passée l’analyse XML de base et la vérification de schéma, la validation par rapport à la spécification DDX est effectuée. Toutes les erreurs qui se trouvent dans le document DDX sont spécifiées dans le journal.

**Enregistrer les résultats de la validation dans un fichier journal**

Le service Assembler renvoie les résultats de validation que vous pouvez écrire dans un fichier journal XML. La quantité de détails que le service Assembler écrit dans le fichier journal dépend de l’option d’exécution que vous avez définie.

**Voir également**

[Validation d’un document DDX à l’aide de l’API Java](#validate-a-ddx-document-using-the-java-api)

[Validation d’un document DDX à l’aide de l’API de service Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validation d’un document DDX à l’aide de l’API Java {#validate-a-ddx-document-using-the-java-api}

Validez un document DDX à l’aide de l’API du service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution pour valider le document DDX.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en appelant la méthode setValidateOnly de l’ `AssemblerOptionSpec` objet et en transmettant `true`.
   * Définissez la quantité d’informations que le service Assembler écrit dans le fichier journal en appelant la `AssemblerOptionSpec` `getLogLevel` méthode de l’objet et en transmettant une valeur de chaîne qui répond à vos besoins. Lors de la validation d’un document DDX, vous souhaitez que davantage d’informations soient écrites dans le fichier journal afin de faciliter le processus de validation. Par conséquent, vous pouvez transmettre la valeur `FINE` ou `FINER`.

1. Effectuez la validation.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX.
   * Valeur `null` de l’objet java.io.Map qui stocke généralement des documents PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options.
   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient des informations indiquant si le document DDX est valide.

1. Enregistrez les résultats de la validation dans un fichier journal.

   * Create a `java.io.File` object and ensure that the file name extension is .xml.
   * Appelez la méthode `AssemblerResult` `getJobLog` de l’objet. Cette méthode renvoie une `com.adobe.idp.Document` instance contenant des informations de validation.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.
   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, un `OperationException` est généré. Dans l’instruction catch, vous pouvez appeler la `OperationException` `getJobLog` méthode de l’objet.

**Voir également**

[Validation de documents DDX](#validating-ddx-documents)

[Démarrage rapide (mode SOAP) : Validation de documents DDX à l’aide de l’API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) Java (mode SOAP)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validation d’un document DDX à l’aide de l’API de service Web {#validate-a-ddx-document-using-the-web-service-api}

Validez un document DDX à l’aide de l’API du service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez localhost par l’adresse IP du serveur Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Définissez les options d’exécution pour valider le document DDX.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en attribuant la valeur true au membre `AssemblerOptionSpec` `validateOnly` de données de l’objet.
   * Définissez la quantité d’informations que le service Assembler écrit dans le fichier journal en attribuant une valeur de chaîne au membre `AssemblerOptionSpec` `logLevel` de données de l’objet. lors de la validation d’un document DDX, vous souhaitez que davantage d’informations soient écrites dans le fichier journal afin de faciliter le processus de validation. Par conséquent, vous pouvez spécifier la valeur `FINE` ou `FINER`. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Effectuez la validation.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Valeur `null` de l’ `Map` objet qui stocke généralement des documents PDF.
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution.
   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient des informations indiquant si le document DDX est valide.

1. Enregistrez les résultats de la validation dans un fichier journal.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier journal et le mode d’ouverture du fichier. Vérifiez que l’extension du nom de fichier est .xml.
   * Créez un `BLOB` objet qui stocke les informations du journal en obtenant la valeur du membre `AssemblerResult` `jobLog` de données de l’objet.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet. Renseignez le tableau d’octets en obtenant la valeur du champ de l’ `BLOB` objet `MTOM` .
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.
   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, un `OperationException` est généré. Dans l’instruction catch, vous pouvez obtenir la valeur du membre de l’ `OperationException` objet `jobLog` .

**Voir également**

[Validation de documents DDX](#validating-ddx-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
