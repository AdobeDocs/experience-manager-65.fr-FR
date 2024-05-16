---
title: API de rapports de transactions facturables
description: Liste de toutes les API comptabilisées comme des transactions
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: e92f1b59-79ef-40fa-af9a-7380cd701a75
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: ht
source-wordcount: '1754'
ht-degree: 100%

---

# API facturables pour les rapports de transaction pour AEM Forms sur OSGi {#transaction-reports-billable-apis}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/transaction-reports-billable-apis) |
| AEM 6.5 | Cet article |

AEM Forms fournit plusieurs API permettant d’envoyer des formulaires, de traiter et de générer des documents. Certaines API sont comptabilisées comme des transactions et d’autres sont gratuites. Ce document fournit une liste de toutes les API comptabilisées comme des transactions dans un rapport de transaction. Voici quelques scénarios courants dans lesquels une API facturable est utilisée :

* Envoi d’un formulaire adaptatif, d’un formulaire HTML5 et d’un jeu de formulaires
* Rendu d’une version imprimée ou web d’une communication interactive
* Conversion d’un document d’un format à un autre
* Aplatissement d’un document PDF dynamique
* Génération d’un document d’enregistrement
* Fusion d’un document PDF interactif avec un autre document PDF
* Utilisation des étapes Affecter des tâches et des services de document des workflows AEM
* Utilisation d’un formulaire adaptatif dans un autre formulaire adaptatif

Les API de facturation ne prennent pas en compte le nombre de pages, la taille d’un document ou d’un formulaire, ni le format final du document rendu. Un rapport de transaction divise les transactions en deux catégories : les documents rendus et les formulaires envoyés.

* **Formulaires envoyés :** les données envoyées à partir de n’importe quel type de formulaire créé avec AEM Forms et les données envoyées à nʼimporte quel référentiel de stockage de données ou base de données sont considérées comme un envoi de formulaire. Par exemple, l’envoi d’un formulaire adaptatif, d’un HTML5, de formulaires PDF et d’un jeu de formulaires est comptabilisé comme un formulaire envoyé. Chaque formulaire d’un jeu de formulaires est considéré comme un envoi. Par exemple, si un jeu de formulaires comporte 5 formulaires, le service de rapport sur les transactions compte 5 envois lorsque le jeu de formulaires est envoyé.

* **Documents rendus :** la génération d’un document en combinant un modèle et des données, la signature ou la certification numérique d’un document, l’utilisation dʼune API Document Services facturable pour les services de documents ou la conversion d’un document d’un format à un autre sont comptabilisés comme des documents rendus.

>[!NOTE]
>
>L’interface utilisateur des rapports de transaction affiche trois catégories : formulaires envoyés, documents rendus et documents traités. Les documents rendus et les documents traités sont tous deux comptabilisés comme des documents rendus.

## API de Document Services facturables {#billable-document-services-apis}

### Service Generate PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Convertit des fichiers Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Convertit des fichiers Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Convertit des fichiers Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crée des fichiers PDF à partir de pages HTML.</p> </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crée un fichier PDF à partir d’URL pointant vers une page HTML.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crée un fichier PDF à partir d’URL pointant vers une page HTML.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimise un fichier PDF pour réduire la taille du fichier en supprimant les métadonnées inutiles sans réduire la qualité.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
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
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>Cette API vous permet de protéger votre document. Vous pouvez utiliser l’API pour signer, certifier, étendre Reader ou chiffrer un document PDF.</td>
   <td>Documents traités</td>
   <td>Seule l’opération de signature et de certification du secureDocument est facturée.</td>
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
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crée des fichiers Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Service Document of Record (service DoR) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Appelle la méthode de rendu spécifiée pour générer un document d’enregistrement à l’aide des paramètres fournis.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Service Output {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Fusionne des données et des modèles pour créer un document PDF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Fusionne des données et des modèles pour créer un document PDF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Fusionne des données et des modèles pour créer un ensemble de documents PDF.</td>
   <td>Documents traités</td>
   <td> L’API generatePDFOutputBatch combine un modèle de formulaire avec un enregistrement et génère un PDF. Lorsque vous traitez un lot d’enregistrements, le service de reporting des transactions comptabilise chaque enregistrement comme un rendu de PDF distinct. <br> Vous pouvez utiliser l’indicateur <a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> pour combiner plusieurs rendus en un seul fichier PDF. Quel que soit l’état de l’indicateur, le service comptabilise chaque enregistrement comme un rendu de PDF distinct. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convertit les documents XDP et PDF aux formats PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convertit les documents XDP et PDF aux formats PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Convertit un ensemble de documents XDP et PDF en un ensemble de formats de fichiers PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> L’API generatePDFOutputBatch combine un modèle de formulaire avec un enregistrement et génère un PDF. Lorsque vous traitez un lot d’enregistrements, le service de reporting des transactions comptabilise chaque enregistrement comme un rendu de PDF distinct. <br> Vous pouvez utiliser l’indicateur <a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> pour combiner plusieurs rendus en un seul fichier PDF. Quel que soit l’état de l’indicateur, le service comptabilise chaque enregistrement comme un rendu de PDF distinct. </td>
  </tr>
 </tbody>
</table>

### Service Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Rend le formulaire PDF à partir de modèles XDP. Les modèles XP sont créés dans Forms Designer.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extrait les données d’un formulaire PDF ou de modèles XDP.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Service Convert PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Convertit un document PDF en une liste de documents image. Les formats d’image pris en charge sont JPEG, JPEG2K, PNG et TIFF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Convertit un fichier PDF plat au format PostScript à l’aide des options spécifiées dans la spécification de l’option.</td>
   <td>Documents traités</td>
   <td> </td>
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
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Décode tous les codes-barres d’un objet Document et renvoie un objet org.w3c.dom.Document contenant les données extraites du code-barre.</td>
   <td>Documents traités</td>
   <td> </td>
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
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invoke</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet <a href="https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenant les documents créés. </td>
   <td>Documents traités</td>
   <td>Les opérations suivantes ne sont pas comptabilisées comme des transactions :
    <ul>
     <li>Créer des packages ou des portfolios</li>
     <li>Assembler plusieurs fichiers XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invoke</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet <a href="https://helpx.adobe.com/fr/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenant les documents créés. </td>
   <td>Documents traités</td>
   <td>Tous les formats de fichiers d’entrée pris en charge par PDF Generator, Forms et Output, le service Assembler prend en charge tous ces formats en tant que formats de fichiers de sortie. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convertissez un document spécifié en format PDF/A à l’aide d’options indiquées.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

L’utilisation de l’API d’appel est comptabilisée comme une transaction lorsque vous effectuez une ou plusieurs des opérations suivantes :
1. Conversion de formats non PDF en formats PDF. Par exemple, la conversion du format XDP au format PDF, qui prend en charge les formes de communication interactives et non interactives, et la conversion de Word au format PDF.
1. Conversion du format PDF au format PDF/A.
1. Conversion du format PDF aux formats non PDF. Les exemples incluent la transformation du format PDF au format Image ou la conversion du format PDF au format Texte.

>[!NOTE]
>
>* L’API Invoke du service Assembler peut appeler en interne une API facturable d’un autre service selon l’entrée. Ainsi, l’API Invoke peut être comptabilisée comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend de l’entrée et des API internes appelées.
>* Un seul document PDF produit à l’aide du service Assembler peut être comptabilisé comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend du code DDX fourni.

### Service PDF Utility  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Convertit un document PDF en fichier XDP. Pour réussir la conversion d’un document PDF en fichier XDP, le document PDF doit contenir un flux XFA dans le dictionnaire AcroForm.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API de capture de données facturables {#billable-data-capture-apis}

Tous les événements d’envoi des formulaires adaptatifs, de formulaires HTML5 et du jeu de formulaires sont comptabilisés comme des transactions. Par défaut, l’envoi d’un formulaire PDF n’est pas comptabilisé comme une transaction. Utilisez les [API d’enregistrement de transaction](record-transaction-custom-implementation.md) pour enregistrer un envoi de formulaires PDF en tant que transaction.

### Formulaires adaptatifs {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Cas d’utilisation</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoi d’un formulaire adaptatif</td>
   <td>Envoie un formulaire adaptatif à une action d’envoi configurée. </td>
   <td>Formulaires envoyés</td>
   <td>
    <ul>
     <li>Les envois réussis comptabilisent une ou deux transactions. Le nombre de transactions comptabilisées dépend du type d’action d’envoi utilisée pour l’envoi. Par exemple, l’envoi d’un PDF par le biais d’une action d’envoi par e-mail comptabilise deux transactions. Une transaction pour l’envoi de formulaire et une autre pour le PDF généré à l’aide du service Document of Record (DOR). </li>
     <li>L’utilisation du formulaire adaptatif dans un formulaire adaptatif (jeu de formulaires adaptatifs) comptabilise une seule transaction. Vous pouvez avoir un nombre illimité de formulaires adaptatifs dans un formulaire adaptatif.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Formulaires HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Cas d’utilisation</p> </td>
   <td>Description </td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoyer un formulaire HTML5</td>
   <td>Envoie un formulaire HTML5 pour envoyer l’URL configurée dans le formulaire.</td>
   <td>Formulaires envoyés</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Jeu de formulaires {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoyer un jeu de formulaires</td>
   <td>Envoie le jeu de formulaires à l’URL d’envoi configurée dans le jeu de formulaires.</td>
   <td>Formulaires envoyés</td>
   <td>
    <ul>
     <li>L’utilisation du formulaire adaptatif dans un formulaire adaptatif (jeu de formulaires adaptatifs) comptabilise une seule transaction. Vous pouvez avoir un nombre illimité de formulaires adaptatifs dans un formulaire adaptatif.</li>
     <li>Chaque formulaire d’un jeu de formulaires HTML5 est comptabilisé comme une transaction distincte. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Communication interactive facturable et workflows AEM basés sur des formulaires sur les API OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Les étapes Affecter des tâches et des services de document des workflows AEM basés sur des formulaires sur OSGi et tous les rendus de communication interactive sont comptabilisés comme des transactions. La prévisualisation d’une communication interactive sur l’instance de création et la prévisualisation sur l’instance de publication à l’aide de l’interface utilisateur de l’agent ne sont pas comptabilisées comme des transactions. Si une étape de workflow comptabilise une transaction et que le workflow ne se termine pas, le nombre de transactions n’est pas inversé.

### Communication interactive - canal Web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Rendu d’un canal web</td>
   <td>Ouvre la version web d’une communication interactive.</td>
   <td>Documents rendus</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Communication interactive - Canal d’impression {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> : (convertir en PDF).</td>
   <td>Génère la version PDF d’une communication interactive.</td>
   <td>Documents rendus</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Processus AEM de formulaire sur OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Cas d’utilisation</p> </td>
   <td>Catégorie de rapport de transaction</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoyer une opération Affecter une tâche</td>
   <td>Formulaires envoyés</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envoyer un point de départ d’application de workflow </td>
   <td>Formulaires envoyés</td>
   <td> </td>
  </tr>
  <tr>
   <td>Envoyer une communication interactive (canal d’impression) depuis l’interface utilisateur de l’agent vers un workflow</td>
   <td>Documents rendus</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Enregistrer les API de facturation en tant que transactions pour le code personnalisé {#recording-billable-apis-as-transactions-for-custom-code}

Les actions telles que l’envoi d’un formulaire PDF, l’utilisation de l’interface utilisateur de l’agent pour prévisualiser une communication interactive, l’utilisation d’un formulaire non standard et les implémentations personnalisées ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API pour enregistrer ces actions en tant que transactions. Vous pouvez appeler l’API à partir de vos implémentations personnalisées pour [enregistrer une transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Articles connexes {#related-articles}

* [Vue d’ensemble des rapports de transaction pour AEM Forms sur OSGi](../../forms/using/transaction-reports-overview.md)
* [Afficher et comprendre les rapports de transaction pour AEM Forms sur OSGi](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Enregistrer une transaction pour les implémentations personnalisées pour AEM Forms sur OSGi](/help/forms/using/record-transaction-custom-implementation.md)
