---
title: API facturables pour les rapports de transaction pour AEM Forms on JEE.
description: Liste de toutes les API prises en compte comme transactions pour AEM Forms on JEE.
topic-tags: forms-manager
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 54%

---

# API facturables pour les rapports de transaction pour AEM Forms on JEE {#transaction-reports-billable-apis}

AEM Forms on JEE fournit plusieurs API pour envoyer, traiter et générer des documents. Certaines API sont comptabilisées comme des transactions et d’autres sont gratuites. Ce document fournit une liste de toutes les API comptabilisées comme des transactions. Voici quelques scénarios courants dans lesquels une API facturable est utilisée :

* Conversion d’un document d’un format à un autre
* Aplatissement d’un document PDF dynamique
* Fusion d’un document PDF interactif avec un autre document PDF

Les API de facturation ne prennent pas en compte le nombre de pages, la longueur d’un document ou d’un formulaire, ni le format final du document rendu.
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

Vous trouverez ci-dessous la liste des API facturables JEE. Recherchez la liste de [API facturables pour AEM Forms sur OSGi](/help/forms/using/transaction-reports-billable-apis.md).

## API de Document Services facturables {#billable-document-services-apis}

### Service Generate PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
   <tr>
   <td><a>CreatePDF</a></td>
   <td>Crée Adobe PDF pour les types de fichiers pris en charge.</td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>Crée Adobe PDF pour les types de fichiers pris en charge. </td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>Convertit le fichier de HTML en Adobe PDF. </td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>Exporte PDF vers les types de fichiers pris en charge. </td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>Exporte PDF vers les types de fichiers pris en charge.</p> </td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF3</a></td>
   <td>Exporte PDF vers les types de fichiers pris en charge.</td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>Convertit le fichier de HTML en PDF.</td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>Convertit le fichier de HTML en PDF.</td>
   <td>Conversion<br /> </td>
  </tr>
  <tr>
   <td><a>OptimizePDF</a></td>
   <td>Optimise un fichier PDF pour réduire la taille du fichier en supprimant les métadonnées inutiles sans réduire la qualité.</td>
   <td>Conversion<br /> </td>
  </tr>
 </tbody>
</table>

### Service DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td><a>Sign/Certify</a><br /> </td>
   <td>Cette API vous permet de protéger votre document. Vous pouvez utiliser l’API pour signer et certifier un document de PDF.</td>
   <td>Conversion</td>
  </tr>
 </tbody>
</table>


### Service Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
  <tr>
   <td><a>CreatePDF</a></td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Conversion</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Conversion</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Service Output {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>Fusionne des données et des modèles pour créer un document PDF.</td>
   <td>Documents rendus</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>Fusionne des données et des modèles pour créer un document PDF.</td>
   <td>Documents rendus</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>Fusionne des données et des modèles pour créer un document PDF.</td>
   <td>Documents rendus</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>Convertit les documents XDP et PDF aux formats PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents rendus</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>Convertit les documents XDP et PDF aux formats PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents rendus</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>Convertit un ensemble de documents XDP et PDF en un ensemble de formats de fichiers PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Conversion de documents</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Service Convert PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>Convertit un document PDF en une liste de documents image. Les formats d’image pris en charge sont JPEG, JPEG2K, PNG et TIFF.</td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>Convertit un fichier PDF plat au format PostScript à l’aide des options spécifiées dans la spécification de l’option.</td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>Convertit un fichier de PDF plat au format SWF à l’aide des options spécifiées dans la spécification de l’option.</td>
   <td>Conversion de documents</td>
  </tr>
 </tbody>
</table>

### Service Barcoded Forms {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td><a>decode</a></td>
   <td>Décode tous les codes-barres d’un objet Document et renvoie un objet org.w3c.dom.Document contenant les données extraites du code-barre.</td>
   <td>Conversion de documents</td>
  </tr>
 </tbody>
</table>

### Incohérence affectant le service assembleur {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td><a>invoke</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet AssemblerResult contenant les documents créés. </td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet AssemblerResult contenant les documents créés. </td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>Convertissez un document spécifié en format PDF/A à l’aide d’options indiquées.</td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>Convertissez un document spécifié en format PDF/A à l’aide d’options indiquées.</td>
   <td>Conversion de documents</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>Convertissez un document spécifié en format PDF/A à l’aide d’options indiquées.</td>
   <td>Conversion de documents</td>
  </tr>
 </tbody>
</table>

L’utilisation de l’API d’appel est comptabilisée comme une transaction lorsque vous effectuez une ou plusieurs des opérations suivantes :
1. Conversion de formats non PDF en formats PDF. Par exemple, la conversion du format XDP au format PDF.<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversion du format PDF au format PDF/A.
1. Conversion du format PDF aux formats non PDF. Les exemples incluent la transformation du format PDF au format Image ou la conversion du format PDF au format Texte.

>[!NOTE]
>
>* L’API Invoke du service Assembler peut appeler en interne une API facturable d’un autre service selon l’entrée. Donc, la `invoke API` peuvent être comptabilisées comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend de l’entrée et des API internes appelées.
>* Un document PDF unique produit à l’aide du service d’assemblage, tel que `invoke` et `invokeDDX`, peut être comptabilisé comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend des <!--DDX--> code.

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## API de capture de données facturables {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Formulaires {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>Formulaire d’envoi.</td>
   <td>Formulaires envoyés</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>Formulaire d’envoi.</td>
   <td>Formulaires envoyés</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>Formulaire d’envoi.</td>
   <td>Forms rendu</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## Articles connexes

* [Activation et affichage du rapport de transaction pour AEM Forms on JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Enregistrement d’une transaction pour les API de composant personnalisées pour AEM Forms on JEE](/help/forms/using/record-transaction-custom-component-jee.md)