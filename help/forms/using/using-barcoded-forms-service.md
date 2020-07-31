---
title: Service Barcoded Forms
seo-title: Utilisation du service AEM Forms Barcoded Forms
description: 'Utilisez le service AEM Forms Barcoded Forms pour extraire des données depuis des images électroniques de codes à barres. '
seo-description: 'Utilisez le service AEM Forms Barcoded Forms pour extraire des données depuis des images électroniques de codes à barres. '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 95%

---


# Service Barcoded Forms{#barcoded-forms-service}

## Présentation {#overview}

Le service Barcoded Forms extrait des données depuis des images électroniques de code à barres. Il accepte en entrée des fichiers PDF et TIFF qui contiennent un ou plusieurs codes à barres et extrait les données de code à barres. Les données de code à barres peuvent être formatées d’une multitude de façons, telles que les formats XML, chaîne délimitée ou tout format personnalisé créé avec JavaScript.

Le service Barcoded Forms prend en charge les symbologies **bidimensionnelles (2D)** ci-après, fournies sous la forme de documents TIFF ou PDF numérisés :

* PDF417
* Data Matrix
* Code QR

Ce service prend également en charge les symbologies **unidimensionnelles** fournies sous la forme de documents TIFF ou PDF numérisés :

* Codabar
* Code128
* Code 3 sur 9
* EAN13
* EAN8

Vous pouvez utiliser le service Barcoded Forms pour effectuer les tâches suivantes :

* Extraire des données de code à barres depuis des images de code à barres (TIFF ou PDF). Les données sont stockées dans un format de texte délimité.
* Convertir des données dans un format de texte délimité en données XML (XDP ou XFDF). Les données XML sont plus faciles à analyser que le texte délimité. De plus, les données au format XDP ou XFDF peuvent être utilisées en entrée pour d’autres services dans AEM Forms.

Le service Barcoded Forms recherche les codes à barres d’une image, les décode et en extrait les données. Le service renvoie les données de code à barres (à l’aide d’un codage d’entité lorsqu’il y a lieu) dans un élément content d’un document XML. Par exemple, l’image TIFF numérisée suivante d’un formulaire contient deux codes à barres :

![example](assets/example.png)

Après le décodage des codes à barres, le service Barcoded Forms renvoie le document XML suivant :

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## Remarques sur le service {#considerations}

### Flux de production utilisant des formulaires à code à barres {#workflows-that-use-barcoded-forms}

Les auteurs de formulaires utilisent Designer pour créer des formulaires à code à barres interactifs (Voir [l’aide de Designer](https://www.adobe.com/go/learn_aemforms_designer_63).) Lorsqu’un utilisateur remplit un formulaire à code à barres en utilisant Adobe Reader ou Acrobat, le code à barres est automatiquement mis à jour afin de coder les données de formulaire.

Le service Barcoded Forms permet de convertir dans un format électronique des données qui existent sur papier. Par exemple, quand un formulaire à code à barres est rempli et imprimé, la copie imprimée peut être numérisée et utilisée comme fichier d’entrée pour le service Barcoded Forms.

Des points de fin Watched Folder sont généralement utilisés pour lancer des applications qui utilisent le service Barcoded Forms. Par exemple, les scanners de documents peuvent enregistrer les images TIFF ou PDF de formulaires à code à barres dans un dossier de contrôle. Le point de fin du dossier de contrôle transmet ces images au service, à des fins de décodage.

### Formats de codage et décodage recommandés {#recommended-encoding-and-decoding-formats}

Les auteurs de formulaires à code à barres sont encouragés à utiliser un format simple et délimité (des tabulations, par exemple) lors de l’encodage des données dans les codes à barres. Évitez également d’utiliser le retour chariot comme délimiteur de champ. Designer propose une sélection de codages délimités qui génèrent automatiquement du script JavaScript pour le codage de code à barres. Les données décodées présentent les noms de champ sur la première ligne et leurs valeurs sur la seconde ligne, avec des tabulations entre chacun des champs.

Lors du décodage de code à barres, vous devez indiquer le caractère utilisé pour délimiter les champs. Le caractère spécifié pour le décodage du code à barres doit être identique à celui utilisé pour son codage. Par exemple, lors de l’utilisation du format délimité par des tabulations recommandé, l’opération d’extraction vers XML doit utiliser la valeur par défaut de tabulation comme délimiteur de champ.

### Jeux de caractères définis par l’utilisateur {#user-specified-character-sets}

Lorsque les auteurs de formulaires ajoutent des objets codes à barres à leurs formulaires à l’aide de Designer, ils peuvent spécifier un codage de caractères. Les codages reconnus sont les suivants : UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16. Par défaut, toutes les données sont codées dans les codes à barres au format UTF-8.

Lors du décodage de code à barres, vous pouvez spécifier le jeu de caractères à utiliser. Pour garantir le décodage correct de toutes les données, spécifiez le jeu de caractères indiqué par l’auteur du formulaire lors de sa conception.

### Limitations de l’API {#api-limitations}

Lorsque vous utilisez les API BCF, tenez compte des restrictions suivantes :

* Les formulaires dynamiques ne sont pas pris en charge.
* Les formulaires interactifs ne sont pas décodés correctement, sauf s’ils sont aplatis.
* Les codes à barres 1-D doivent contenir uniquement des valeurs alphanumériques (s’ils sont pris en charge). Les codes à barres contenant des symboles spéciaux ne sont pas décodés.

### Autres restrictions {#other-limitations}

En outre, considérez les restrictions suivantes lorsque vous utilisez le service Barcoded Forms :

* Le service prend entièrement en charge AcroForms et les formulaires statiques contenant des codes à barres 2D qui sont enregistrés avec Adobe Reader ou Acrobat. Toutefois, pour les codes à barres 1D, aplatissez le formulaire ou fournissez-le sous forme de document PDF ou TIFF numérisé.
* Les formulaires XFA dynamiques ne sont pas entièrement pris en charge. Pour décoder correctement les codes à barres 1D et 2D dans un formulaire dynamique, aplatissez le formulaire ou fournissez-le sous forme de document PDF ou TIFF numérisé.

En outre, le service peut décoder tout code à barres qui utilise une symbologie prise en charge si les restrictions indiquées ci-dessus sont respectées. Pour plus d’informations sur la manière de créer des formulaires à code-barres interactifs, voir [l’Aide de Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Configurer les propriétés du service   {#configureproperties}

Vous pouvez utiliser le **service AEMFD Barcoded Forms** dans la console AEM pour configurer les propriétés de ce service. The default URL of AEM console is `https://[host]:'port'/system/console/configMgr`.

## Utilisation du service {#using}

Le service Barcoded Forms fournit les deux API suivantes :

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)** : Décode tous les codes à barres disponibles dans un document PDF ou une image tiff d’entrée. Elle renvoie un autre document XML contenant des données extraites à partir de tous les codes à barres disponibles dans le document ou l’image d’entrée.

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)** : convertissez des données décodées en données XML à l’aide de l’API de décodage. Ces données XML peuvent être fusionnées avec un formulaire XFA. Elle renvoie une liste des documents XML, un pour chaque code à barres.

### Utilisation du service BCF avec un JSP ou des servlets {#using-bcf-service-with-a-jsp-or-servlets}

L’exemple de code suivant décode un code à barres dans un document et enregistre le code XML de sortie sur le disque.

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // Please see Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // Please see javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### Utilisation du service BCF avec des processus AEM {#using-the-bcf-service-with-aem-workflows}

L’exécution du service Barcoded Forms à partir d’un processus est semblable à l’exécution du service à partir de JSP/Servlet. La seule différence réside dans le fait qu’avec une exécution du service à partir de JSP/Servlet, l’objet de document récupère automatiquement une instance d’objet ResourceResolver à partir de l’objet ResourceResolverHelper. Ce mécanisme automatique ne fonctionne pas lorsque le code est appelé à partir d’un processus.

Pour un flux de travail, transmettez explicitement une occurrence de l’objet ResourceResolver au constructeur de classe du document. Ensuite, l’objet Document utilise l’objet ResourceResolver fourni pour lire le contenu du référentiel.

L’exemple de processus suivant décode un code à barres dans un document et enregistre le résultat sur le disque. Le code est écrit dans ECMAScript et le document est transmis en tant que charge utile de flux de travail :

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

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

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```

