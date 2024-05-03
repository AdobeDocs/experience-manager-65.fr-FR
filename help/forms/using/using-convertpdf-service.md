---
title: Service ConvertPDF
description: Utilisez le service Adobe Experience Manager Forms ConvertPDF pour convertir des documents PDF en fichiers PostScript ou en fichiers d’images.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
exl-id: 50c7a385-b56d-4573-932f-1f44eec948f8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 100%

---

# Service ConvertPDF {#convertpdf-service}

## Présentation {#overview}

Le service Convert PDF convertit des documents PDF en fichiers PostScript ou en images (aux formats JPEG, JPEG 2000, PNG et TIFF). La conversion d’un document PDF en PostScript est utile pour les impressions sans assistance reposant sur un serveur exécutées sur n’importe quelle imprimante PostScript. La conversion d’un document PDF en fichier TIFF comportant plusieurs pages est pratique lors de l’archivage de documents dans des systèmes de gestion de contenu qui ne prennent pas en charge les documents PDF.

Vous pouvez exécuter les tâches ci-dessous à l’aide du service ConvertPDF :

* Convertir des documents PDF en PostScript. Lors de la conversion au format PostScript, vous pouvez utiliser l’opération de conversion pour spécifier le document source et indiquer si vous souhaitez effectuer une conversion en PostScript de niveau 2 ou 3. Le document PDF que vous convertissez en fichier PostScript doit être non interactif.
* Convertir des documents PDF aux formats d’image JPEG, JPEG 2000, PNG et TIFF. Lors de cette conversion, vous pouvez préciser le document source et fournir une spécification portant sur les options d’image. La spécification contient diverses préférences, telles que le format de conversion d&#39;image, la résolution de l’image et la conversion des couleurs.

## Configurer les propriétés du service {#properties}

Vous pouvez utiliser le **Service AEMFD ConvertPDF** dans la console AEM pour configurer les propriétés de ce service. LʼURL par défaut de la console AEM est `https://[host]:'port'/system/console/configMgr`.

## Utiliser le service {#using-the-service}

Le service ConvertPDF fournit les deux API suivantes :

* **[toPS](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)** : convertit un document PDF en fichier PostScript.

* **[toImage](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr)** : convertit un document PDF en fichier image. Les formats d’image pris en charge sont JPEG, JPEG2000, PNG et TIFF.

### Utilisation de l’API toPS avec JSP ou des servlets {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### Utilisation de l’API toImage avec JSP ou des servlets {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### Utilisation du service ConvertPDF avec des workflows AEM {#using-convertpdf-service-with-aem-workflows}

L’exécution du service ConvertPDF à partir d’un workflow est similaire à l’exécution à partir de JSP/d’un Servlet.

La seule différence est que lors de l’exécution du service à partir de JSP/Servlet, l’objet document récupère automatiquement une instance de l’objet ResourceResolver de l’objet ResourceResolverHelper. Ce mécanisme automatique ne fonctionne pas lorsque le code est appelé à partir d’un processus. Pour un workflow, transmettez explicitement une occurrence de l’objet ResourceResolver au constructeur de classe du document. Ensuite, l’objet de document utilise l’objet ResourceResolver fourni pour lire le contenu à partir du référentiel.

L’exemple de processus de workflow suivant convertit le document d’entrée en document PostScript. Le code est écrit en ECMAScript et le document est transmis en tant que payload de workflow :

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from
 * crx repository.
 */

/* get ResourceResolverFactory service reference , used
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path
var inputDocument = new Document(payload_path, resourceResolver);

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
