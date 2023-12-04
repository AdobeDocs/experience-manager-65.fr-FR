---
title: Documents PDF protégés par une politique Reader Extension à l’aide de la bibliothèque de protection portable
seo-title: Reader extending policy-protected PDF documents using Portable Protection Library
description: Les extensions de Reader activent des fonctions interactives dans les documents Adobe PDF via Acrobat Reader. Vous pouvez utiliser la bibliothèque portable de protection (PPL) pour étendre Reader aux documents de PDF protégés DRM.
seo-description: Reader extensions enable interactive features in Adobe PDF documents through Acrobat Reader. You can use the Portable Protection Library (PPL) to reader extend the DRM protected PDF documents.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 35%

---

# Documents PDF protégés par une politique Reader Extension à l’aide de la bibliothèque de protection portable {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Familiarisez-vous avec les concepts de sécurité des documents, d’extension de lecteur et de langage de programmation Java pour étendre Reader aux documents de PDF protégés par une stratégie de sécurité documentaire.

Vous pouvez utiliser Document Security pour restreindre l’accès de documents de PDF spécifiques à des utilisateurs autorisés uniquement. Vous pouvez également déterminer comment un destinataire peut utiliser un document protégé. Par exemple, vous pouvez spécifier si les destinataires peuvent imprimer, copier ou modifier le texte d’un document protégé par une stratégie Document Security. Pour en savoir plus sur Document Security, voir [à propos de Document Security](/help/forms/using/admin-help/document-security.md).

Vous pouvez utiliser des extensions Reader pour activer des fonctionnalités interactives dans le document Adobe PDF via Acrobat Reader. Ces fonctionnalités interactives, qui sont normalement disponibles uniquement via Adobe Acrobat Professional et Standard. Pour en savoir plus sur les fonctions interactives que l’extension Reader peut activer, voir [Service DocAssurance Adobe Experience Manager Forms ](/help/forms/using/overview-aem-document-services.md)**.**

Vous pouvez utiliser la bibliothèque portable de protection pour appliquer des politiques à des documents, sans avoir recours aux document transitant par le réseau. Seules les informations d’identification de sécurité et les politiques de protection transitent sur le réseau. Le document ne quitte jamais le client et les stratégies de protection sont appliquées localement sur le client.

## Reader de l’extension de documents de PDF protégés par une stratégie de sécurité documentaire {#reader-extending-document-security-policy-protected-pdf-documents}

Les documents protégés par une stratégie sont des documents chiffrés. Vous ne pouvez pas utiliser d’API Reader-extension standard pour appliquer, supprimer et récupérer des droits d’utilisation d’un document PDF protégé par une stratégie. Seul le service Reader Extensions de la bibliothèque portable de protection fournit des API nécessaires à l’exécution d’une telle tâche.

### Service Reader Extensions {#reader-extensions-service}

Le service d’extension Reader ajoute des droits d’utilisation à un document de PDF protégé par une stratégie, activant des fonctionnalités qui ne sont pas normalement disponibles lors de l’ouverture d’un document de PDF à l’aide de Adobe Acrobat Reader. Il dispose également d’API pour supprimer et récupérer les droits d’utilisation d’un document protégé par une stratégie.

Le service Reader Extensions prend entièrement en charge les documents de PDF basés sur la norme PDF 1.6 et versions ultérieures. En dehors d’Acrobat Reader, les utilisateurs tiers n’ont pas besoin de logiciels ou de modules externes supplémentaires pour utiliser les documents de PDF protégés par une stratégie.

Vous pouvez accomplir les tâches suivantes avec le service Reader Extensions :

* Appliquez des droits d’utilisation à un document de PDF protégé par une stratégie.
* Suppression des droits d’utilisation d’un document de PDF protégé par une stratégie.
* Rechercher les droits d’utilisation appliqués à un document PDF protégé par une politique.

### Appliquer les droits d’utilisation à un document PDF protégé par une politique de sécurité documentaire. {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Vous pouvez utiliser l’API Java `applyUsageRights` pour appliquer des droits d’utilisation aux documents PDF protégés par une politique. Les droits d’utilisation appartiennent à la fonctionnalité disponible par défaut dans Acrobat mais non dans Adobe Reader, telle que la capacité à ajouter des commentaires à un formulaire ou à remplir des champs de formulaire et enregistrer ce dernier. Les documents de PDF auxquels des droits d’utilisation sont appliqués sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document dont les droits sont activés dans Adobe Reader peut effectuer des opérations qui sont activées pour ce document spécifique.

**Syntaxe :** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Spécifiez InputStream représentant le document du PDF auquel des droits d’utilisation doivent être appliqués. Vous pouvez utiliser LiveCycle Rights Management ou des documents protégés par AEM Forms Document Security.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Spécifiez l’objet File représentant un fichier .jks. Le fichier .jks est un fichier de stockage de clés. Il pointe vers un certificat qui accorde des droits d’utilisation.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Indiquez le mot de passe du fichier de stockage des clés. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Spécifie un objet de type <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. L’objet usageRights représente les droits individuels pouvant être appliqués à un document de PDF protégé par une stratégie.</p> </td>
  </tr>
 </tbody>
</table>

### Rechercher les droits d’utilisation appliqués à un document PDF protégé par une politique.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Vous pouvez utiliser l’API Java `getDocumentUsageRights` pour récupérer les droits d’utilisation de l’extension Reader appliqués à un document PDF protégé par une politique. En récupérant des informations sur les droits d’utilisation, vous pourrez en savoir davantage sur les fonctionnalités Reader Extension activées pour le document PDF protégé par une politique.

**Syntaxe :** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Spécifiez InputStream représentant le document du PDF à partir duquel les droits d’utilisation doivent être récupérés. Vous pouvez utiliser LiveCycle Rights Management ou des documents protégés par AEM Forms Document Security.</p> </td>
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

System.out.println("UsageRights applied successfully to the document. ");
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

### Suppression des droits d’utilisation d’un document de PDF protégé par une stratégie {#remove-usage-rights-of-a-policy-protected-pdf-document}

Vous pouvez utiliser l’API Java `removeUsageRights` pour supprimer des droits d’utilisation d’un document protégé par une politique. La suppression des droits d’utilisation d’un document PDF protégé par une politique est nécessaire avant d’exécuter d’autres opérations AEM Forms sur le document. Vous devez par exemple signer numériquement (ou certifier) un document PDF avant de définir ses droits d’utilisation. Par conséquent, si vous souhaitez effectuer des opérations sur un document protégé par une stratégie, vous devez supprimer les droits d’utilisation du document du PDF, effectuer les autres opérations, telles que la signature numérique du document, puis réappliquer les droits d’utilisation au document.

**Syntaxe :** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Paramètre</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Spécifiez InputStream représentant le document du PDF à partir duquel l’utilisation<br /> Les droits doivent être supprimés. Vous pouvez utiliser LiveCycle Rights Management ou des documents protégés par AEM Forms Document Security.</td>
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
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
