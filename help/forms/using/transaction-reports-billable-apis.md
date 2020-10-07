---
title: API facturables des rapports de transaction
seo-title: API facturables des rapports de transaction
description: Liste de toutes les API comptabilisées en tant que transactions
seo-description: Liste de toutes les API comptabilisées en tant que transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 13016df927448d93af86899f746199e1815fdfe7
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 9%

---


# API facturables des rapports de transaction{#transaction-reports-billable-apis}

AEM Forms fournit plusieurs API pour envoyer des formulaires, traiter des documents et générer des documents. Certaines API sont comptabilisées comme des transactions et d&#39;autres sont libres d&#39;utiliser. Ce document fournit une liste de toutes les API qui sont comptabilisées comme des transactions dans un état de transaction. Voici quelques scénarios courants dans lesquels une API facturable est utilisée :

* Envoi d’un formulaire adaptatif, d’un formulaire HTML5 et d’un jeu de formulaires
* Rendu d’une version imprimée ou Web d’une communication interactive
* Conversion d’un document d’un format à un autre
* Aplatissement d’un document PDF dynamique
* Génération d&#39;un Document d&#39;enregistrement
* Fusion d’un document PDF interactif avec un autre document PDF
* Utilisation de l’étape d’affectation des tâches et des étapes des services de document des Workflows AEM
* Utilisation d’un formulaire adaptatif dans un formulaire adaptatif

Les API de facturation ne tiennent pas compte du nombre de pages, de la longueur d’un document ou d’un formulaire, ni du format final du document rendu. Un rapport de transactions divise les transactions en deux catégories : Documents rendus et Forms envoyés.

* **Forms Soumis :** Lorsque des données sont envoyées à partir de n’importe quel type de formulaire créé avec AEM Forms et que les données sont envoyées à n’importe quel référentiel d’enregistrement de données ou base de données est considérée comme un envoi de formulaire. Par exemple, l’envoi d’un formulaire adaptatif, d’un formulaire HTML5, de PDF forms et d’un jeu de formulaires est comptabilisé comme des formulaires envoyés. Chaque formulaire d’un jeu de formulaires est considéré comme un envoi. Par exemple, si un jeu de formulaires comporte 5 formulaires, lorsque le jeu de formulaires est envoyé, le service de rapports de transactions le compte comme 5 envois.

* **Documents rendus :** La génération d’un document en combinant un modèle et des données, en signant ou certifiant numériquement un document, en utilisant une API de services de document facturables pour les services de document ou en convertissant un document d’un format à un autre est comptabilisée comme des documents rendus.

>[!NOTE]
>
>L’interface utilisateur des rapports sur les transactions affiche trois catégories : Forms envoyée, Documents rendus et Documents traités. Les Documents générés et les Documents traités sont comptabilisés comme Documents générés.

## API de services de Document facturables {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Crée Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crée Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Convertit Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Convertit Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Convertit Adobe PDF en types de fichiers pris en charge. </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Crée un fichier PDF à partir de pages HTML.</p> </td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Crée un fichier PDF à partir d’URL pointant vers une page HTML.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Crée un fichier PDF à partir d’URL pointant vers une page HTML.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimise le format PDF pour réduire la taille du fichier en supprimant les métadonnées superflues sans affecter la qualité.</td>
   <td>Documents traités<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Crée Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Crée Adobe PDF à partir des types de fichiers pris en charge.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Service document d&#39;enregistrement (service de DE) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
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
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Fusionne les données et les modèles pour créer un document PDF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Fusionne les données et les modèles pour créer un document PDF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Fusionne les données et les modèles pour créer un ensemble de documents PDF.</td>
   <td>Documents traités</td>
   <td> L’API generatePDFOutputBatch combine un modèle de formulaire avec un enregistrement et génère un PDF. Lorsque vous traitez un lot d’enregistrements, le service de rapports de transactions comptabilise chaque enregistrement comme un rendu PDF distinct. <br> Vous pouvez utiliser l’indicateur <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> pour combiner plusieurs rendus dans un seul fichier PDF. Quel que soit l’état de l’indicateur, le service comptabilise chaque enregistrement en tant que rendu PDF distinct. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convertit les documents XDP et PDF aux formats de fichier PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Convertit les documents XDP et PDF aux formats de fichier PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Convertit un ensemble de documents XDP et PDF en un ensemble de formats de fichier PostScript (PS), PCL (Printer Command Language) et ZPL. </td>
   <td>Documents traités</td>
   <td> L’API generatePDFOutputBatch combine un modèle de formulaire avec un enregistrement et génère un PDF. Lorsque vous traitez un lot d’enregistrements, le service de rapports de transactions comptabilise chaque enregistrement comme un rendu PDF distinct. <br> Vous pouvez utiliser l’indicateur <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> pour combiner plusieurs rendus dans un seul fichier PDF. Quel que soit l’état de l’indicateur, le service comptabilise chaque enregistrement en tant que rendu PDF distinct. </td>
  </tr>
 </tbody>
</table>

### Service Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Génère un formulaire PDF à partir de modèles XDP. Les modèles XP sont créés dans Forms Designer.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extrait les données d’un formulaire PDF ou de modèles XDP.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Convertit un document PDF en liste de documents d’image. Les formats d’image pris en charge sont JPEG, JPEG2K, PNG et TIFF.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Convertit un fichier PDF aplati au format PostScript à l’aide des options spécifiées dans la spécification d’options.</td>
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
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">décoder</a></td>
   <td>Décode tous les codes à barres d’un objet Document et renvoie un objet org.w3c.dom.Document contenant des données récupérées à partir du code à barres.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Incohérence affectant le service {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invoke</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenant les documents résultants. </td>
   <td>Documents traités</td>
   <td>Les opérations suivantes ne sont pas comptabilisées comme des transactions :
    <ul>
     <li>Création de packs ou de portefeuilles</li>
     <li>Assemblage de plusieurs fichiers XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invoke</a></td>
   <td>Exécute le document DDX spécifié et renvoie un objet <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contenant les documents résultants. </td>
   <td>Documents traités</td>
   <td>Tous les formats de fichier d’entrée pris en charge par les services PDF Generator, Forms et Output, le service Assembler prend en charge tous ces formats en tant que formats de fichier de sortie. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Convertissez un document spécifié en PDF/A à l’aide des options spécifiées.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* L’API d’appel du service Assembler peut, en interne, appeler une API facturable d’un autre service en fonction de l’entrée. Ainsi, l’API d’appel peut être comptabilisée comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend de l&#39;entrée et des API internes invoquées.
>* Un document PDF unique créé à l’aide du service Assembler peut être comptabilisé comme aucune, une ou plusieurs transactions. Le nombre de transactions comptabilisées dépend du code DDX fourni.

>



### Service PDF Utility  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Convertit un document PDF en fichier XDP. Pour qu’un document PDF soit converti en fichier XDP, le document PDF doit contenir un flux XFA dans le dictionnaire AcroForm.</td>
   <td>Documents traités</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## API de capture de données facturables {#billable-data-capture-apis}

Tous les événements d’envoi des formulaires adaptatifs, du Forms HTML5 et du jeu de formulaires sont comptabilisés comme des transactions. Par défaut, l’envoi d’un formulaire PDF n’est pas comptabilisé comme une transaction. Utilisez l&#39;API [d&#39;enregistrement de](record-transaction-custom-implementation.md) transactions fournie pour enregistrer un envoi PDF forms en tant que transaction.

### Formulaires adaptatifs {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Exemple d’utilisation </p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoi d’un formulaire adaptatif</td>
   <td>Envoie un formulaire adaptatif à l’action d’envoi configurée. </td>
   <td>Formulaires envoyés</td>
   <td>
    <ul>
     <li>Les envois réussis sont comptabilisés pour une ou deux transactions. Le nombre de transactions comptabilisées dépend du type d’action d’envoi utilisée pour l’envoi. Par exemple, l’envoi d’un fichier PDF par le biais d’un compte d’action Envoyer par messagerie pour deux comptes de transactions. Une transaction pour l’envoi du formulaire et une autre pour le PDF généré à l’aide du service Document d’enregistrement (DOR). </li>
     <li>L’utilisation du formulaire adaptatif dans un formulaire adaptatif (jeu de formulaires adaptatifs) ne tient compte que d’une seule transaction. Vous pouvez avoir n’importe quel nombre de formulaires adaptatifs dans un formulaire adaptatif.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Formulaires HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Exemple d’utilisation </p> </td>
   <td>Description </td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoi d’un formulaire HTML5</td>
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
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoi d’un jeu de formulaires</td>
   <td>Envoie le jeu de formulaires à l’URL d’envoi configurée dans le jeu de formulaires.</td>
   <td>Formulaires envoyés</td>
   <td>
    <ul>
     <li>L’utilisation du formulaire adaptatif dans un formulaire adaptatif (jeu de formulaires adaptatifs) ne tient compte que d’une seule transaction. Vous pouvez avoir n’importe quel nombre de formulaires adaptatifs dans un formulaire adaptatif.</li>
     <li>Chaque formulaire d’un jeu de formulaires Forms HTML5 est comptabilisé comme une transaction distincte. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Workflows d&#39;AEM de communication interactive facturables et orientés formulaires sur les API OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Affectez des étapes de tâche et de services de document des Workflows d&#39;AEM orientés formulaire sur OSGi et tous les rendus de communication interactive et sont comptabilisés comme des transactions. La prévisualisation d’une communication interactive sur l’instance d’auteur et la prévisualisation sur l’instance de publication à l’aide de l’interface utilisateur de l’agent ne sont pas comptabilisées comme des transactions. Si une étape de workflow comptabilise une transaction et que celle-ci ne se termine pas, le décompte de transaction n&#39;est pas inversé.

### Communication interactive - canal Web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Rendu d’un canal Web</td>
   <td>Ouvre la version Web d’une communication interactive.</td>
   <td>Documents rendus</td>
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
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convertir en PDF)</td>
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
   <td>Catégorie de rapports de transactions</td>
   <td>Informations supplémentaires</td>
  </tr>
  <tr>
   <td>Envoi d’une étape d’affectation de Tâche</td>
   <td>Formulaires envoyés</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envoi d’un point de départ d’application de processus </td>
   <td>Formulaires envoyés</td>
   <td> </td>
  </tr>
  <tr>
   <td>Envoi d’une communication interactive (Canal d’impression) depuis l’interface utilisateur de l’agent vers un processus</td>
   <td>Documents rendus</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Enregistrement des API facturables en tant que transactions pour le code personnalisé {#recording-billable-apis-as-transactions-for-custom-code}

Les actions telles que l’envoi d’un formulaire PDF, l’utilisation de l’interface utilisateur de l’agent pour prévisualisation une communication interactive, l’envoi de formulaires non standard et les implémentations personnalisées ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API pour enregistrer des actions telles que des transactions. Vous pouvez appeler l’API à partir de vos implémentations personnalisées pour [enregistrer une transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Présentation des rapports sur les transactions](../../forms/using/transaction-reports-overview.md)
* [Affichage et compréhension des rapports sur les transactions](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Enregistrer une transaction pour les implémentations personnalisées](/help/forms/using/record-transaction-custom-implementation.md)

