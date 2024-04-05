---
title: Valider les documents DDX
description: Validez un document DDX par programme à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 100%

---

# Valider les documents DDX {#validating-ddx-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez valider par programme un document DDX utilisé par le service Assembler. En d’autres termes, vous pouvez déterminer si un document DDX est valide ou non à l’aide de l’API du service Assembler. Par exemple, si vous avez effectué une mise à niveau à partir d’une version précédente d’AEM Forms et que vous souhaitez vous assurer que votre document DDX est valide, vous pouvez le valider à l’aide de l’API du service Assembler.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour valider un document DDX, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler.
1. Référencez un document DX existant.
1. Définir les options d’exécution pour valider le document DDX
1. Effectuer la validation
1. Enregistrer les résultats de la validation dans un fichier journal

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un client Assembler PDF**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Pour valider un document DDX, vous devez référencer un document DDX existant.

**Définir des options d’exécution pour valider le document DDX**

Lors de la validation d’un document DDX, vous devez définir des options d’exécution spécifiques qui demandent au service Assembler de valider le document DDX plutôt que de l’exécuter. Vous pouvez également augmenter la quantité d’informations que le service Assembler écrit dans le fichier journal.

**Effectuer la validation**

Après avoir créé le client de service Assembler, référencé le document DDX et défini les options d’exécution, vous pouvez appeler l’opération `invokeDDX` pour valider le document DDX. Lors de la validation du document DDX, vous pouvez transmettre `null` comme paramètre de mappage (ce paramètre stocke généralement les documents PDF dont Assembler a besoin pour effectuer la ou les opérations spécifiées dans le document DDX).

Si la validation échoue, une exception est renvoyée et le fichier journal qui contient les détails expliquant pourquoi le document DDX n’est pas valide peut être obtenu à partir de l’instance `OperationException`. Une fois l’analyse XML de base et la vérification de schéma terminées, la validation de la spécification DDX est effectuée. Toutes les erreurs qui se trouvent dans le document DDX sont spécifiées dans le journal.

**Enregistrer les résultats de la validation dans un fichier journal**

Le service Assembler renvoie les résultats de validation que vous pouvez écrire dans un fichier journal XML. La quantité de détails que le service Assembler entre dans le fichier journal dépend de l’option d’exécution que vous avez définie.

**Voir également**

[Valider un document DDX à l’aide de l’API Java](#validate-a-ddx-document-using-the-java-api)

[Valider un document DDX à l’aide de l’API de service web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Valider un document DDX à l’aide de l’API Java {#validate-a-ddx-document-using-the-java-api}

Validez un document DDX à l’aide de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir les options d’exécution pour valider le document DDX

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en appelant la méthode setValidateOnly de l’objet `AssemblerOptionSpec` et en transmettant `true`.
   * Définissez la quantité d’informations que le service Assembler entre dans le fichier journal en appelant la méthode `getLogLevel` de l’objet `AssemblerOptionSpec` et en transmettant une valeur de chaîne qui répond à vos besoins. Lors de la validation d’un document DDX, un plus grand nombre d’informations écrites dans le fichier journal facilite le processus de validation. Par conséquent, vous pouvez transmettre la valeur `FINE` ou `FINER`.

1. Effectuer la validation

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document DDX.
   * La valeur `null` de l’objet java.io.Map qui stocke généralement les documents PDF.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult`, lequel contient des informations indiquant si le document DDX est valide.

1. Enregistrer les résultats de la validation dans un fichier journal

   * Créez un objet `java.io.File` et assurez-vous que l’extension du nom de fichier est .xml.
   * Appelez la méthode `getJobLog` de l’objet `AssemblerResult`. Cette méthode renvoie une instance `com.adobe.idp.Document` qui contient des informations de validation.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier.

   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, une exception `OperationException` est renvoyée. Dans l’instruction catch, vous pouvez appeler la méthode `getJobLog` de l’objet `OperationException`.

**Voir également**

[Valider les documents DDX](#validating-ddx-documents)

[Démarrage rapide (mode SOAP) : validation des documents DDX à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (mode SOAP)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Valider un document DDX à l’aide de l’API de service web {#validate-a-ddx-document-using-the-web-service-api}

Pour valider un document DDX à l’aide de l’API Assembler Service (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez localhost par l’adresse IP du serveur Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Définir les options d’exécution pour valider le document DDX

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en attribuant la valeur true (vrai) au membre de données `validateOnly` de l’objet `AssemblerOptionSpec`.
   * Définissez la quantité d’informations que le service Assembler écrit dans le fichier journal en attribuant une valeur de chaîne au membre de données `logLevel` de l’objet `AssemblerOptionSpec`. méthode Lors de la validation d’un document DDX, il convient dʼécrire plus dʼinformations dans le fichier journal pour faciliter le processus de validation. Par conséquent, vous pouvez spécifier la valeur `FINE` ou `FINER`. Pour plus d’informations sur les options d’exécution que vous pouvez définir, consultez la référence de classe `AssemblerOptionSpec` dans la [référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Effectuer la validation

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` qui représente le document DDX.
   * Valeur `null` pour l’objet `Map` qui stocke généralement des documents PDF.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient des informations indiquant si le document DDX est valide.

1. Enregistrer les résultats de la validation dans un fichier journal

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier journal et le mode d’ouverture du fichier. Assurez-vous que l’extension du nom du fichier est .xml.
   * Créez un objet `BLOB` qui stocke les informations du journal en obtenant la valeur du membre de données `jobLog` de l’objet `AssemblerResult`.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, un élément `OperationException` est généré. Dans l’instruction catch, vous pouvez obtenir la valeur du membre `jobLog` de l’objet `OperationException`.

**Voir également**

[Valider les documents DDX](#validating-ddx-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
