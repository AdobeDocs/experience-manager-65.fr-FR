---
title: Validation d’un document DDX à l’aide de l’API de service Web
seo-title: Validation d’un document DDX à l’aide de l’API de service Web
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Validation d’un document DDX à l’aide de l’API de service Web {#validate-a-ddx-document-using-theweb-service-api}

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

[Validation de documents DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
