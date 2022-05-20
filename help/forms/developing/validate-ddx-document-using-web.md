---
title: Valider un document DDX à l’aide de l’API de service web
seo-title: Validate a DDX document using theweb service API
description: Utilisez l’API Assembler Service pour valider un document DDX.
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '640'
ht-degree: 100%

---

# Valider un document DDX à l’aide de l’API de service web {#validate-a-ddx-document-using-theweb-service-api}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Pour valider un document DDX à l’aide de l’API Assembler Service (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez localhost par l’adresse IP du serveur Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM Forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur du mot de passe correspondant au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Remplissez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à sa propriété `MTOM`.

1. Définir les options d’exécution pour valider le document DDX

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez l’option d’exécution qui demande au service Assembler de valider le document DDX en attribuant la valeur « true » au membre de données `validateOnly` de l’objet `AssemblerOptionSpec`.
   * Définissez la quantité d’informations que le service Assembler écrit dans le fichier journal en attribuant une valeur de chaîne au membre de données `logLevel` de l’objet `AssemblerOptionSpec`. méthode Lors de la validation d’un document DDX, il convient dʼécrire plus dʼinformations dans le fichier journal pour faciliter le processus de validation. Pour ce faire, vous pouvez spécifier la valeur `FINE` ou `FINER`. Pour plus d’informations sur les options d’exécution que vous pouvez définir, consultez la référence de la classe `AssemblerOptionSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Effectuer la validation

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX.
   * La valeur `null` pour l’objet `Map` qui stocke généralement les documents PDF.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient des informations indiquant si le document DDX est valide.

1. Enregistrer les résultats de la validation dans un fichier journal

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en lui transmettant une valeur de chaîne qui représente l’emplacement du fichier journal et son mode d’ouverture. Assurez-vous que l’extension du nom du fichier est .xml.
   * Créez un objet `BLOB` qui stocke les informations du journal en obtenant la valeur du membre de données `jobLog` de l’objet `AssemblerResult`.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

   >[!NOTE]
   >
   >Si le document DDX n’est pas valide, une valeur `OperationException` est générée. Dans l’instruction catch, vous pouvez obtenir la valeur du membre `jobLog` de l’objet `OperationException`.

**Voir également**

[Valider les documents DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
