---
title: Documents PDF protégés par une stratégie Reader Extension à l’aide de la bibliothèque de protection portable
seo-title: Documents PDF protégés par une stratégie Reader Extension à l’aide de la bibliothèque de protection portable
description: Les extensions Reader permettent d’activer des fonctions interactives dans les documents Adobe PDF via Acrobat Reader. Vous pouvez utiliser la bibliothèque portable de protection (PPL) et étendre Reader aux document PDF protégés DRM.
seo-description: Les extensions Reader permettent d’activer des fonctions interactives dans les documents Adobe PDF via Acrobat Reader. Vous pouvez utiliser la bibliothèque portable de protection (PPL) et étendre Reader aux document PDF protégés DRM.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 98%

---


# Documents PDF protégés par une stratégie Reader Extension à l’aide de la bibliothèque de protection portable {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Vous devez vous familiariser avec les concepts de sécurité documentaire, d’extensions Reader et de langage de programmation Java afin d’étendre Reader aux documents PDF protégés par une stratégie de sécurité documentaire.

Vous pouvez utiliser la sécurité documentaire pour restreindre l’accès à des documents PDF spécifiques uniquement à des utilisateurs autorisés. Vous pouvez également déterminer la manière dont un destinataire peut utiliser un document protégé. Par exemple, vous pouvez indiquer si les destinataires peuvent imprimer, copier ou modifier le texte d’un document protégé par une stratégie de protection documentaire. Pour en savoir plus sur la protection documentaire, voir [À propos de la sécurité documentaire](/help/forms/using/admin-help/document-security.md).

Vous pouvez utiliser des extensions Reader pour activer des fonctions interactives dans les documents Adobe PDF via Acrobat Reader. Ces fonctions interactives sont normalement disponibles uniquement via Adobe Acrobat Professional et standard. Pour en savoir plus sur les fonctions interactives que l’extension Reader peut activer, voir [Service DocAssurance Adobe Experience Manager Forms ](/help/forms/using/overview-aem-document-services.md)**.**

Vous pouvez utiliser la bibliothèque portable de protection pour appliquer des stratégies à des documents, sans avoir recours aux document transitant par le réseau. Seules les informations d’identification de sécurité et les stratégies de protection transitent sur le réseau. Le document ne quitte jamais le client et les stratégies de protection s’appliquent localement sur le client.

## Extension Reader des documents PDF protégés par une stratégie de sécurité documentaire {#reader-extending-document-security-policy-protected-pdf-documents}

Les documents protégés par une stratégie sont chiffrés. Il n’est pas possible d’utiliser les API Reader Extension standard pour appliquer, supprimer et rechercher des droits d’utilisation dans des documents PDF protégés par une stratégie. Seul le service Reader Extensions de la bibliothèque portable de protection fournit des API nécessaires à l’exécution d’une telle tâche.

### Service Reader Extensions {#reader-extensions-service}

Le service d’extension Reader dote un document PDF de droits d’utilisation qui activent des fonctions généralement non indisponibles à l’ouverture d’un document PDF dans Adobe Acrobat Reader. Il est également doté d’API qui suppriment et recherchent des droits d’utilisation dans les documents PDF protégés par une stratégie.

Le service Reader Extensions prend totalement en charge les documents PDF basés sur la norme PDF 1.6 et versions ultérieures. Indépendamment d’Acrobat Reader, les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents PDF protégés par une stratégie.

Vous pouvez exécuter les tâches ci-dessous à l’aide du service Reader Extensions :

* Appliquer les droits d’utilisation à un document PDF protégé par une stratégie.
* Supprimer les droits d’utilisation d’un document PDF protégé par une stratégie.
* Rechercher les droits d’utilisation appliqués à un document PDF protégé par une stratégie.

### Appliquer les droits d’utilisation à un document PDF protégé par une stratégie de sécurité documentaire.{#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Vous pouvez utiliser l’API Java `applyUsageRights` pour appliquer des droits d’utilisation aux documents PDF protégés par une stratégie. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document dont les droits sont activés dans Adobe Reader peut effectuer les opérations autorisées pour ce document spécifique.

**Syntaxe :** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Spécifiez InputStream correspondant au document PDF auquel des droits d’utilisation doivent être appliqués. Vous pouvez utiliser les documents protégés par la sécurité documentaire LiveCycle Rights Management ou AEM Forms.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Spécifiez l’objet File représentant un fichier .jks. Le fichier .jks est un fichier de stockage de clés. Il indique un certificat qui accorde des droits d’utilisation.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Spécifiez le mot de passe du stockage de clés. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Spécifie un objet de type <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L’objet usageRights représente les droits individuels qui peuvent être appliqués à un document PDF protégé par une stratégie.</p> </td>
  </tr>
 </tbody>
</table>

### Rechercher les droits d’utilisation appliqués à un document PDF protégé par une stratégie.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Vous pouvez utiliser l’API Java `getDocumentUsageRights` pour récupérer les droits d’utilisation de l’extension Reader appliqués à un document PDF protégé par une stratégie. En récupérant des informations sur les droits d’utilisation, vous pourrez en savoir davantage sur les fonctionnalités Reader Extension activées pour le document PDF protégé par une stratégie.

**Syntaxe :** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Spécifiez InputStream correspondant au document PDF duquel des droits d’utilisation doivent être supprimés. Vous pouvez utiliser les documents protégés par la sécurité documentaire LiveCycle Rights Management ou AEM Forms.</p> </td>
  </tr>
 </tbody>
</table>

#### Exemple de code {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ”);
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Supprimer les droits d’utilisation d’un document PDF protégé par une stratégie {#remove-usage-rights-of-a-policy-protected-pdf-document}

Vous pouvez utiliser l’API Java `removeUsageRights` pour supprimer des droits d’utilisation d’un document protégé par une stratégie. La suppression des droits d’utilisation d’un document PDF protégé par une stratégie est nécessaire avant d’exécuter d’autres opérations AEM Forms sur le document. Vous devez par exemple signer numériquement (ou certifier) un document PDF avant de définir ses droits d’utilisation. Par conséquent, pour effectuer des opérations sur un document défini avec des droits d’utilisation, vous devez supprimer les droits du document PDF, effectuer les autres opérations, comme la signature numérique d’un document, puis réappliquer des droits d’utilisation à ce même document.

**Syntaxe :** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Spécifiez InputStream correspondant au document PDF duquel des droits d’utilisation <br /> doivent être supprimés. Vous pouvez utiliser les documents protégés par la sécurité documentaire LiveCycle Rights Management ou AEM Forms.</td>
  </tr>
 </tbody>
</table>

#### Exemple de code {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

