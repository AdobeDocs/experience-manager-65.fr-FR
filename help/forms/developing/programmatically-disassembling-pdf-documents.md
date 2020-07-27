---
title: Démontage programmatique des Documents PDF
seo-title: Démontage programmatique des Documents PDF
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 3%

---


# Démontage programmatique des Documents PDF {#programmatically-disassembling-pdf-documents}

Vous pouvez désassembler un document PDF en le transmettant au service Assembler. En règle générale, cette tâche est utile lorsque le document PDF a été créé à l’origine à partir de nombreux documents individuels, tels qu’un ensemble d’instructions. Dans l’illustration suivante, DocA est divisé en plusieurs documents résultants, où le signet de premier niveau 1 sur une page identifie le début d’un nouveau document résultant.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Pour désassembler un document PDF, assurez-vous que l’ `PDFsFromBookmarks` élément se trouve dans le document DDX. L’ `PDFsFromBookmarks` élément est un élément cible et ne peut être qu’un élément enfant de l’ `DDX` élément. Il n’a pas d’ `result` attribut, car il peut générer plusieurs documents.

L’ `PDFsFromBookmarks` élément génère un document unique pour chaque signet de niveau 1 dans le document source.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. (voir Assemblage [par programmation de Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

>[!NOTE]
>
>Lorsque vous transmettez un seul document PDF au service Assembler et que vous récupérez un seul document, vous pouvez appeler l’ `invokeOneDocument` opération. Cependant, pour désassembler un document PDF, utilisez l’ `invokeDDX` opération car, bien qu’un document PDF d’entrée soit transmis au service Assembler, le service Assembler renvoie un objet de collection contenant un ou plusieurs documents.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour désassembler un document PDF, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez un document PDF à désassembler.
1. Définissez les options d’exécution.
1. Désassemblez le document PDF.
1. Enregistrez les documents PDF déassemblés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel les AEM Forms sont déployés.

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour désassembler un document PDF. Ce document DDX doit contenir l’ `PDFsFromBookmarks` élément.

**Référence à un document PDF à désassembler**

Pour désassembler un document PDF, référencez un fichier PDF représentant le document PDF à désassembler. Lorsqu’il est transmis au service Assembler, un document PDF distinct est renvoyé pour chaque signet de niveau 1 du document.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Désassembler le document PDF**

Après avoir créé le client de service Assembler, fait référence au document DDX, fait référence à un document PDF pour le désassembler et défini les options d’exécution, vous pouvez désassembler un document PDF en invoquant la `invokeDDX` méthode. Si le document DDX contient des instructions pour désassembler le document PDF, le service Assembler renvoie les documents PDF désassemblés dans un objet de collection.

**Enregistrer les documents PDF déassemblés**

Tous les documents PDF déassemblés sont renvoyés dans un objet de collection. Effectuez une itération dans l’objet de collection et enregistrez chaque document PDF au format PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Démonter un document PDF à l’aide de l’API Java {#disassemble-a-pdf-document-using-the-java-api}

Désassembler un document PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF à désassembler.

   * Créez un `java.util.Map` objet utilisé pour stocker des documents PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du document PDF à désassembler.
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet contenant le document PDF à désassembler.
   * Ajoutez une entrée à l’ `java.util.Map` objet en invoquant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` contenant le document PDF à désassembler.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et passez `false`.

1. Désassemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant le document PDF à désassembler
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau du journal des tâches

   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant les documents PDF désassemblés et les exceptions survenues.

1. Enregistrez les documents PDF déassemblés.

   Pour obtenir les documents PDF déassemblés, effectuez les actions suivantes :

   * Appelle la méthode `AssemblerResult` de l’ `getDocuments` objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet obtenu.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document PDF.

**Voir également**

[Démontage programmatique des Documents PDF](#programmatically-disassembling-pdf-documents)

[Début rapide (mode SOAP) : Démontage d’un document PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Démonter un document PDF à l’aide de l’API du service Web {#disassemble-a-pdf-document-using-the-web-service-api}

Désassemblez un document PDF à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en attribuant sa `MTOM` propriété au contenu du tableau d’octets.

1. Référencez un document PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée. Cet `BLOB` objet est transmis à l’ `invokeOneDocument` objet en tant qu’argument.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker le PDF à désassembler.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’objet `BLOB` qui stocke le document PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet.
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet sur l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Appelez la `MyMapOf_xsd_string_To_xsd_anyType` méthode de l’ `Add` objet et transmettez l’ `MyMapOf_xsd_string_To_xsd_anyType` objet.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez-lui `false` au `AssemblerOptionSpec` `failOnError` champ de l’objet.

1. Désassemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs suivantes :

   * Un `BLOB` objet représentant le document DDX qui désassemble le document PDF
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant le document PDF à désassembler
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La `invokeDDX` méthode renvoie un `AssemblerResult` objet contenant les résultats de la tâche et les exceptions survenues.

1. Enregistrez les documents PDF déassemblés.

   Pour obtenir les documents PDF nouvellement créés, effectuez les opérations suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF déassemblés.
   * Effectuez une itération sur l’ `Map` objet pour obtenir chaque document résultant. Ensuite, déposez les éléments `value` de ce membre de la baie sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la `BLOB` propriété de l’objet `MTOM` en question. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Démontage programmatique des Documents PDF](#programmatically-disassembling-pdf-documents)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
