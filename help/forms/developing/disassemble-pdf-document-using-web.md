---
title: Désassembler un document PDF en utilisant l’API du service web
description: Désassemblez un document PDF en utilisant l’API du service Assembler.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 100%

---

# Désassembler un document PDF à l’aide de l’API de service web {#disassemble-a-pdf-document-usingthe-web-service-api}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Pour désassembler un document PDF à l’aide de l’API du service Assembler (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

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

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Référencez un document de PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à l’opération `invokeOneDocument` comme argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document PDF d’entrée et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker le PDF à désassembler.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
   * Attribuez l’objet `BLOB` qui stocke le document PDF au champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez `false` au champ `failOnError` de l’objet `AssemblerOptionSpec`.

1. Désassemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX qui désassemble le document PDF.
   * L’objet `MyMapOf_xsd_string_To_xsd_anyType` qui contient le document PDF à désassembler.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir les documents PDF nouvellement créés, procédez comme suit :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF désassemblés.
   * Effectuez une itération par le biais de l’objet `Map` pour obtenir chaque document généré. Convertissez ensuite l’élément `value` du membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Désassembler des documents PDF par programme](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
