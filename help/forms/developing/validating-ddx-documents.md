---
title: Validation des Documents DDX
seo-title: Validation des Documents DDX
description: Validez un document DDX par programmation à l’aide de l’API Java et de l’API de service Web.
seo-description: Validez un document DDX par programmation à l’aide de l’API Java et de l’API de service Web.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 3%

---


# Validation des Documents DDX {#validating-ddx-documents}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Vous pouvez valider par programmation un document DDX utilisé par le service Assembler. En d’autres termes, à l’aide de l’API du service Assembler, vous pouvez déterminer si un document DDX est valide ou non. Par exemple, si vous avez effectué une mise à niveau à partir d’une version AEM Forms précédente et souhaitez vous assurer que votre document DDX est valide, vous pouvez le valider à l’aide de l’API du service Assembler.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Référencer un document DDX existant**

Pour valider un document DDX, vous devez référencer un document DDX existant.

**Définition des options d’exécution pour valider le document DDX**

Lors de la validation d’un document DDX, vous devez définir des options d’exécution spécifiques qui demandent au service Assembler de valider le document DDX au lieu de l’exécuter. Vous pouvez également augmenter la quantité d’informations que le service Assembler écrit dans le fichier journal.

**Effectuer la validation**

Après avoir créé le client de service Assembler, référencé le document DDX et défini les options d’exécution, vous pouvez appeler l’opération `invokeDDX` pour valider le document DDX. Lors de la validation du document DDX, vous pouvez transmettre `null` comme paramètre de mappage (ce paramètre stocke généralement les documents PDF dont Assembler a besoin pour effectuer les opérations spécifiées dans le document DDX).

Si la validation échoue, une exception est générée et le fichier journal contient des détails qui expliquent pourquoi le document DDX n&#39;est pas valide peut être obtenu à partir de l&#39;instance `OperationException`. Une fois passé le test d’analyse XML de base et la vérification de schéma, la validation par rapport à la spécification DDX est effectuée. Toutes les erreurs qui se trouvent dans le document DDX sont spécifiées dans le journal.

**Enregistrer les résultats de la validation dans un fichier journal**

Le service Assembler renvoie les résultats de validation que vous pouvez écrire dans un fichier journal XML. La quantité de détails que le service Assembler écrit dans le fichier journal dépend de l’option d’exécution que vous définissez.

**Voir également**

[Validation d’un document DDX à l’aide de l’API Java](#validate-a-ddx-document-using-the-java-api)

[Validation d’un document DDX à l’aide de l’API du service Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validation d’un document DDX à l’aide de l’API Java {#validate-a-ddx-document-using-the-java-api}

Validez un document DDX à l’aide de l’API Service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référencez un document DDX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution pour valider le document DDX.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en appelant la méthode setValidateOnly de l’objet `AssemblerOptionSpec` et en transmettant `true`.
   * Définissez la quantité d&#39;informations que le service Assembler écrit dans le fichier journal en appelant la méthode `AssemblerOptionSpec` de l&#39;objet `getLogLevel` et en transmettant une valeur de chaîne qui répond à vos besoins. Lors de la validation d’un document DDX, vous souhaitez que davantage d’informations soient écrites dans le fichier journal, ce qui facilitera le processus de validation. Par conséquent, vous pouvez transmettre la valeur `FINE` ou `FINER`.

1. Effectuez la validation.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX.
   * Valeur `null` de l’objet java.io.Map qui stocke généralement des documents PDF.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant des informations indiquant si le document DDX est valide.

1. Enregistrez les résultats de la validation dans un fichier journal.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .xml.
   * Appelez la méthode `AssemblerResult` de l’objet `getJobLog`. Cette méthode renvoie une instance `com.adobe.idp.Document` contenant des informations de validation.
   * Appelez la méthode `com.adobe.idp.Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `com.adobe.idp.Document` dans le fichier.

   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, un `OperationException` est généré. Dans l&#39;instruction catch, vous pouvez appeler la méthode `OperationException` de l&#39;objet `getJobLog`.

**Voir également**

[Validation des Documents DDX](#validating-ddx-documents)

[Début rapide (mode SOAP) : Validation des documents DDX à l’aide de l’API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  Java (mode SOAP)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validation d’un document DDX à l’aide de l’API de service Web {#validate-a-ddx-document-using-the-web-service-api}

Validez un document DDX à l’aide de l’API Service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez localhost par l’adresse IP du serveur Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Définissez les options d’exécution pour valider le document DDX.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en attribuant la valeur true au membre de données `validateOnly` de l’objet `AssemblerOptionSpec`.
   * Définissez la quantité d&#39;informations que le service Assembler écrit dans le fichier journal en attribuant une valeur de chaîne au membre de données `logLevel` de l&#39;objet `AssemblerOptionSpec`. lors de la validation d’un document DDX, vous souhaitez que davantage d’informations soient écrites dans le fichier journal, ce qui facilitera le processus de validation. Par conséquent, vous pouvez spécifier la valeur `FINE` ou `FINER`. Pour plus d&#39;informations sur les options d&#39;exécution que vous pouvez définir, consultez la référence de classe `AssemblerOptionSpec` dans [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Effectuez la validation.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Valeur `null` de l’objet `Map` qui stocke généralement des documents PDF.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant des informations indiquant si le document DDX est valide.

1. Enregistrez les résultats de la validation dans un fichier journal.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier journal et le mode d&#39;ouverture du fichier. Assurez-vous que l’extension de nom de fichier est .xml.
   * Créez un objet `BLOB` qui stocke les informations du journal en obtenant la valeur du membre de données `AssemblerResult` de l&#39;objet `jobLog`.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB`. Renseignez le tableau d’octets en obtenant la valeur du champ `BLOB` de l’objet `MTOM`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, un `OperationException` est généré. Dans l&#39;instruction catch, vous pouvez obtenir la valeur du membre `OperationException` de l&#39;objet `jobLog`.

**Voir également**

[Validation des Documents DDX](#validating-ddx-documents)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
