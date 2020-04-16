---
title: 'Création de flux de sortie '
seo-title: 'Création de flux de sortie '
description: 'null'
seo-description: 'null'
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Création de flux de sortie {#creating-document-output-streams}

**À propos du service Output**

Le service Output vous permet de générer des  au format PDF (y compris le  PDF/A), PostScript, PCL (Printer Control Language) et aux formats d’étiquette suivants :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Le service Output vous permet de fusionner des données de formulaire XML avec une conception de formulaire et de générer le  sur une imprimante ou un fichier réseau.

Il existe deux manières de transmettre une conception de formulaire (un fichier XDP) au service Output. Vous pouvez transmettre une `com.adobe.idp.Document` instance contenant une conception de formulaire au service Output. Vous pouvez également transmettre une valeur URI spécifiant l’emplacement de la conception de formulaire. Ces deux méthodes sont décrites dans *Programmation avec AEM Forms*.

>[!NOTE]
>
>Le service Output ne prend pas en charge les PDF Acrobat qui contiennent des scripts spécifiques aux objets d’application. Les  PDF Acroform qui contiennent des scripts spécifiques aux objets d’application ne sont pas rendus.

Les sections suivantes expliquent comment transmettre une conception de formulaire au service Output à l’aide d’une valeur URI :

* [Création de  PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Création d’une  de PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Les sections suivantes expliquent comment transmettre une conception de formulaire dans une `com.adobe.idp.Document` instance :

* [Transmission des  de situés dans Content Services (obsolète) vers Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Création de PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Lorsque vous décidez de la technique à utiliser, vous devez notamment savoir si vous obtenez la conception de formulaire à partir d’un autre service AEM Forms, puis la transmettre dans une `com.adobe.idp.Document` instance. Les sections *Transmission du au service* Output et *Création de PDF à l’aide de fragments* montrent comment obtenir une conception de formulaire à partir d’un autre service AEM Forms. La première section récupère la conception de formulaire de Content Services (obsolète). La deuxième section récupère la conception de formulaire à partir du service Assembler.

Si vous obtenez la conception de formulaire à un emplacement fixe, tel que le système de fichiers, vous pouvez utiliser l’une ou l’autre technique. En d’autres termes, vous pouvez spécifier la valeur URI d’un fichier XDP ou utiliser une `com.adobe.idp.Document` instance.

Pour transmettre une valeur URI spécifiant l’emplacement de la conception de formulaire lors de la création d’un PDF, utilisez la `generatePDFOutput` méthode. De même, pour transmettre une `com.adobe.idp.Document` instance au service Output lors de la création d’un PDF, utilisez la `generatePDFOutput2` méthode.

Lors de l’envoi d’un flux de sortie vers une imprimante réseau, vous pouvez également utiliser l’une ou l’autre technique. Pour envoyer un flux de sortie vers une imprimante en transmettant une `com.adobe.idp.Document` instance contenant une conception de formulaire, utilisez la `sendToPrinter2`méthode. Pour envoyer un flux de sortie vers une imprimante en transmettant une valeur URI, utilisez la `sendToPrinter`méthode. La section *Envoi des flux d’impression aux imprimantes* utilise la `sendToPrinter` méthode.

Vous pouvez accomplir ces  en utilisant le service Output :

* [Création de  PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Création d’une  de PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Transmission des  de situés dans Content Services (obsolète) vers Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Création de PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Impression dans des fichiers](creating-document-output-streams.md#printing-to-files)
* [Envoi de flux d&#39;impression aux imprimantes](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Création de plusieurs fichiers de sortie](creating-document-output-streams.md#creating-multiple-output-files)
* [Création de règles de recherche](creating-document-output-streams.md#creating-search-rules)
* [Aplatissement du PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Création de  PDF {#creating-pdf-documents}

Vous pouvez utiliser le service Output pour créer un PDF basé sur une conception de formulaire et des données de formulaire XML fournies. Le PDF créé par le service Output n’est pas un PDF interactif  ; un utilisateur ne peut pas saisir ni modifier les données d’un formulaire.

Si vous souhaitez créer un PDF destiné à un  à long terme, il est recommandé de créer un PDF/A. (Voir [Création d’un](creating-document-output-streams.md#creating-pdf-a-documents)PDF/A.)

Pour créer un formulaire PDF interactif permettant à un utilisateur de saisir des données, utilisez le service Forms. (Voir [Rendu de formulaires](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)PDF interactifs.)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour créer un  PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définissez les options d’exécution PDF.
1. Définissez les options d’exécution du rendu.
1. Générer un PDF.
1. Récupérez les résultats de l’opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceService` objet.

**Référence à une source de données XML**

Pour fusionner des données avec la conception de formulaire, vous devez référencer une source de données XML qui contient des données. Un élément XML doit exister pour chaque champ de formulaire que vous prévoyez de renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

Examinez l’exemple de formulaire de demande de prêt suivant.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Pour fusionner des données dans cette conception de formulaire, vous devez créer une source de données XML qui correspond au formulaire. Le code XML suivant représente une source de données XML XDP qui correspond à l’exemple de formulaire de demande de prêt immobilier.

```as3
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**Définition des options d’exécution PDF**

Définissez l’option URI du fichier lors de la création d’un  PDF. Cette option spécifie le nom et l’emplacement du fichier PDF généré par le service Output.

>[!NOTE]
>
>Au lieu de définir l’option d’exécution de l’URI du fichier, vous pouvez programmer la récupération du PDF à partir du type de données complexe renvoyé par le service Output. Toutefois, en définissant l’option d’exécution de l’URI du fichier, vous n’avez pas besoin de créer une logique d’application qui récupère par programmation le  PDF.

**Définition des options d’exécution du rendu**

Vous pouvez définir les options d’exécution du rendu lors de la création d’un PDF. Bien que ces options ne soient pas requises (contrairement aux options d’exécution PDF requises), vous pouvez effectuer des  telles que l’amélioration des performances du service Output. Vous pouvez, par exemple, mettre en cache la conception de formulaire utilisée par le service Output afin d’améliorer ses performances.

Si vous utilisez un formulaire Acrobat balisé comme entrée, vous ne pouvez pas utiliser le service Output Java ou l’API du service Web pour désactiver le paramètre balisé. Si vous tentez de définir cette option par programmation sur `false`, le PDF obtenu est toujours balisé.

>[!NOTE]
>
>Si vous ne spécifiez pas d’options d’exécution de rendu, les valeurs par défaut sont utilisées. Pour plus d’informations sur le rendu des options d’exécution, voir la référence de `RenderOptionsSpec` classe. (Voir Référence [sur l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

**Générer un PDF**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini des options d’exécution, vous pouvez appeler le service Output, ce qui génère un  PDF.

Lors de la génération d’un  PDF, vous spécifiez les valeurs URI requises par le service Output pour créer un  de PDF. Une conception de formulaire peut être stockée dans des emplacements tels que le système de fichiers du serveur ou dans le cadre d’une application AEM Forms. Une conception de formulaire (ou d’autres ressources telles qu’un fichier image) qui existe dans le cadre d’une application Forms peuvent être référencées à l’aide de la valeur URI racine du contenu `repository:///`. Prenons l’exemple de la conception de formulaire suivante nommée *Loan.xdp* située dans une application Forms nommée *Applications/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Pour accéder au fichier Loan.xdp illustré dans l’illustration précédente, spécifiez `repository:///Applications/FormsApplication/1.0/FormsFolder/` comme troisième paramètre transmis à la `OutputClient` `generatePDFOutput` méthode de l’objet. Spécifiez le nom du formulaire (*Loan.xdp*) comme second paramètre transmis à la `OutputClient` méthode de l’ `generatePDFOutput` objet.

Si le fichier XDP contient des images (ou d’autres ressources telles que des fragments), placez les ressources dans le même dossier d’application que le fichier XDP. AEM Forms utilise l’URI racine du contenu comme chemin de base pour résoudre les références aux images. Par exemple, si le fichier Loan.xdp contient une image, veillez à placer l’image dans `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Vous pouvez référencer un URI d’application Forms lors de l’appel des méthodes `OutputClient` ou `generatePDFOutput` `generatePrintedOutput` de l’objet.

>[!NOTE]
>
>Pour voir un  rapide complet qui crée un PDF  en référençant un fichier XDP situé dans une application Forms, reportez-vous à la section [Quick (mode EJB) : Création d’un  PDF basé sur un fichier XDP d’application à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)Java.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que des données XML d’état qui indiquent si l’opération a réussi.

**Voir également**

[Création d’un PDF à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Création d’un PDF à l’aide de l’API du service Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Création d’un PDF à l’aide de l’API Java {#create-a-pdf-document-using-the-java-api}

Créez un PDF à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client de sortie.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez une source de données XML.

   * Créez un `java.io.FileInputStream` objet représentant la source de données XML utilisée pour remplir le PDF à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur. Pass the `java.io.FileInputStream` object.

1. Définissez les options d’exécution PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option URI du fichier en appelant la `PDFOutputOptionsSpec` `setFileURI` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier PDF généré par le service Output. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire afin d’améliorer les performances du service Output en appelant le formulaire `RenderOptionsSpec` et en transmettant `setCacheEnabled` `true`.
   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du PDF à l’aide de la `RenderOptionsSpec` méthode de l’objet si le d’entrée est un formulaire Acrobat (un formulaire créé dans Acrobat) ou un `setPdfVersion` formulaire XFA  signé ou certifié. Le PDF de sortie conserve la version PDF d’origine. De même, vous ne pouvez pas définir l’option Adobe PDF balisé en appelant la `RenderOptionsSpec` `setTaggedPDF` méthode de l’objet si le  d’entrée est un formulaire Acrobat ou un  XFA signé ou certifié.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option PDF linéarisé à l’aide de la `RenderOptionsSpec` `setLinearizedPDF` méthode de l’objet si le PDF d’entrée est certifié ou signé numériquement. (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Générer un PDF.

   Create a PDF document by invoking the `OutputClient` object’s `generatePDFOutput` method and passing the following values:

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >Lorsque vous générez un PDF en appelant la `generatePDFOutput` méthode, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé ou certifié. (Voir [Signature numérique et certification des](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >La `OutputResult` méthode de l’ `getRecordLevelMetaDataList` objet renvoie `null`*.*

   >[!NOTE]
   >
   >Vous pouvez également créer un PDF en appelant la méthode `OutputClient` `generatePDFOutput2` de l’objet. (voir [Transmission des  de situés dans Content Services (obsolète) au service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*Output).)*

1. Récupérez les résultats de l’opération.

   * Récupérez un `com.adobe.idp.Document` objet qui représente l’état de l’ `generatePDFOutput` opération en appelant la `OutputResult` méthode de l’ `getStatusDoc` objet. Cette méthode renvoie des données XML d’état qui indiquent si l’opération a réussi.
   * Créez un `java.io.File` objet contenant les résultats de l’opération. Vérifiez que l’extension du nom de fichier est .xml.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getStatusDoc` méthode).
   Bien que le service Output écrive le PDF à l’emplacement spécifié par l’argument transmis à la `PDFOutputOptionsSpec` méthode de l’ `setFileURI` objet, vous pouvez par programmation récupérer le PDF/A  en appelant la `OutputResult` méthode de l’ `getGeneratedDoc` objet.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Création d’un PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[rapide (mode SOAP) : Création d’un PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création d’un PDF à l’aide de l’API du service Web {#create-a-pdf-document-using-the-web-service-api}

Créez un PDF à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker des données XML qui seront fusionnées avec le PDF.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier XML contenant les données du formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définition des options d’exécution PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option URI du fichier en attribuant une valeur de chaîne qui spécifie l’emplacement du fichier PDF généré par le service Output au membre `PDFOutputOptionsSpec` `fileURI` de données de l’objet. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en attribuant la valeur `true` au membre `RenderOptionsSpec` `cacheEnabled` de données de l’objet.
   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du PDF à l’aide de la `RenderOptionsSpec` méthode de l’objet si le d’entrée est un formulaire Acrobat (un formulaire créé dans Acrobat) ou un `setPdfVersion` formulaire XFA  signé ou certifié. Le PDF de sortie conserve la version PDF d’origine. De même, vous ne pouvez pas définir l’option Adobe PDF balisé en appelant la méthode `RenderOptionsSpec` * de l’ `setTaggedPDF`objet si le  d’entrée est un formulaire Acrobat ou un XFA signé ou certifié.*

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option PDF linéarisé en utilisant le `RenderOptionsSpec` `linearizedPDF` membre de l’objet si le PDF d’entrée est certifié ou signé numériquement. (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Générer un PDF.

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec les données de résultat. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   >[!NOTE]
   >
   >Lorsque vous générez un PDF en appelant la `generatePDFOutput` méthode, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé ou certifié. (Voir [Signature numérique et certification des](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Vous pouvez également créer un PDF en appelant la méthode `OutputClient` `generatePDFOutput2` de l’objet. (voir [Transmission des  de situés dans Content Services (obsolète) au service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*Output).)*

1. Récupérez les résultats de l’opération.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant des données de résultat. Vérifiez que l’extension du nom de fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet qui a été renseigné par la méthode `OutputServiceService` `generatePDFOutput` de l’objet (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de l’ `BLOB` objet `MTOM` `field`.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.
   Voir également

   [Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

   [Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >La méthode `OutputServiceService` de l’objet `generateOutput` est obsolète.

## Création d’une  de PDF/A {#creating-pdf-a-documents}

Vous pouvez utiliser le service Output pour créer un  de PDF/A. Le format PDF/A étant un format d’archivage pour la conservation à long terme du contenu du, toutes les polices sont incorporées et le fichier n’est pas compressé. Par conséquent, un document PDF/A est généralement plus volumineux qu’un document PDF standard. En outre, un PDF/A ne contient pas de contenu audio et vidéo. Comme les autres  du service Output, vous fournissez une conception de formulaire et des données à fusionner avec une conception de formulaire pour créer un  PDF/A.

La spécification PDF/A-1 se compose de deux niveaux de conformité, à savoir a et b. La principale différence entre les deux concerne la prise en charge de la structure logique (accessibilité), qui n&#39;est pas requise pour le niveau de conformité b. Quel que soit le niveau de conformité, PDF/A-1 exige que toutes les polices soient incorporées dans le  PDF/A généré.

Bien que PDF/A soit la norme pour l’archivage des  de PDF, il n’est pas obligatoire d’utiliser PDF/A pour l’archivage si un PDF standard  répondre aux besoins de votre . La norme PDF/A a pour objectif d’établir un fichier PDF pouvant être stocké pendant une longue période et répondant aux exigences de conservation des . Par exemple, une URL ne peut pas être incorporée dans un fichier PDF/A, car au fil du temps l’URL peut devenir non valide.

Votre organisation doit évaluer ses propres besoins, la durée de conservation du, la taille des fichiers et déterminer votre propre stratégie d&#39;archivage. Vous pouvez déterminer par programmation si un PDF est compatible PDF/A à l’aide du service DocConverter. (Voir Détermination [par programmation de la conformité](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)à la norme PDF/A.)

Un PDF/A doit utiliser la police spécifiée dans la conception de formulaire et les polices ne peuvent pas être remplacées. Par conséquent, si une police située dans un PDF n’est pas disponible sur le système d’exploitation hôte, une exception se produit.

Lorsqu’un PDF/A est ouvert dans Acrobat, un message s’affiche, confirmant que le est un  PDF/A, comme illustré ci-dessous.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>Le site Web AIIM comporte une section FAQ PDF/A accessible à l’adresse [https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf).

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour créer un  PDF/A, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définissez les options d’exécution PDF/A.
1. Définissez les options d’exécution du rendu.
1. Générez un  PDF/A.
1. Récupérez les résultats de l’opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application personnalisée à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceService` objet.

**Référence à une source de données XML**

Pour fusionner des données avec la conception de formulaire, vous devez référencer une source de données XML qui contient des données. Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définition des options d’exécution PDF/A**

Vous pouvez définir l’option URI du fichier lors de la création d’un  PDF/A. L’URI est relatif au serveur d’applications J2EE hébergeant AEM Forms. En d’autres termes, si vous définissez C:\Adobe, le fichier est écrit dans le dossier du serveur et non sur l’ordinateur client. L’URI spécifie le nom et l’emplacement du fichier PDF/A généré par le service Output.

**Définition des options d’exécution du rendu**

Vous pouvez définir les options d’exécution du rendu lors de la création d’un  PDF/A. Les deux options liées à PDF/A que vous pouvez définir sont les `PDFAConformance` valeurs et `PDFARevisionNumber` les valeurs. The `PDFAConformance` value refers to how a PDF document adheres to requirements that specify how long-term electronic documents are preserved. Les valeurs valides pour cette option sont `A` et `B`. Pour plus d’informations sur la conformité aux niveaux a et b, voir la spécification ISO PDF/A-1 intitulée *ISO 19005-1 management*.

La `PDFARevisionNumber` valeur fait référence au numéro de révision d’un  PDF/A. Pour plus d’informations sur le numéro de révision d’un  de PDF/A, voir la spécification ISO PDF/A-1 intitulée *ISO 19005-1* management.

>[!NOTE]
>
>Vous ne pouvez pas définir l’option Adobe PDF balisé sur `false` lors de la création d’un  PDF/A 1A. PDF/A 1A sera toujours un PDF balisé. En outre, vous ne pouvez pas définir l’option Adobe PDF balisé sur `true` lors de la création d’un  de PDF/A 1B. PDF/A 1B sera toujours un PDF non balisé.

**Générer un PDF/A**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini des options d’exécution, vous pouvez appeler le service Output, ce qui génère un  PDF/A.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que des données XML, qui indiquent si l’opération a réussi.

**Voir également**

[Création d’un  PDF/A à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Création d’un  PDF/A à l’aide de l’API du service Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Création d’un  PDF/A à l’aide de l’API Java {#create-a-pdf-a-document-using-the-java-api}

Créez un  PDF/A à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client de sortie.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez une source de données XML.

   * Créez un `java.io.FileInputStream` objet représentant la source de données XML utilisée pour remplir le PDF/A à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution PDF/A.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option URI du fichier en appelant la `PDFOutputOptionsSpec` `setFileURI` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier PDF généré par le service Output. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Définissez la `PDFAConformance` valeur en appelant la `RenderOptionsSpec` méthode de l’objet et en transmettant une `setPDFAConformance` `PDFAConformance` valeur d’énumération qui spécifie le niveau de conformité. Par exemple, pour spécifier le niveau de conformité A, transmettez `PDFAConformance.A`.
   * Définissez la `PDFARevisionNumber` valeur en appelant la `RenderOptionsSpec` méthode de l’objet et en transmettant `setPDFARevisionNumber` `PDFARevisionNumber.Revision_1`.
   >[!NOTE]
   >
   >La version PDF d’un PDF/A est de 1.4, quelle que soit la valeur spécifiée pour la `RenderOptionsSpec` méthode de l’ `setPdfVersion`*objet.*

1. Générez un  PDF/A.

   Créez un  PDF/A en appelant la `OutputClient` méthode de l’ `generatePDFOutput` objet et en transmettant les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF/A, spécifiez `TransformationFormat.PDFA`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >La `OutputResult` méthode de l’ `getRecordLevelMetaDataList` objet renvoie `null`.

   >[!NOTE]
   >
   >Vous pouvez également créer un PDF /A en appelant la méthode `OutputClient` 2 de l’objet `generatePDFOutput`2. (voir [Transmission des  de situés dans Content Services (obsolète) au service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)Output).)

1. Récupérez les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` objet qui représente l’état de la `generatePDFOutput` méthode en appelant la `OutputResult` méthode de l’ `getStatusDoc` objet.
   * Créez un `java.io.File` objet qui contiendra les résultats de l’opération. Vérifiez que l’extension du nom de fichier est .xml.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getStatusDoc` méthode).
   >[!NOTE]
   >
   >Bien que le service Output écrive le  PDF/A à l’emplacement spécifié par l’argument transmis à la `PDFOutputOptionsSpec` méthode de l’ `setFileURI` objet, vous pouvez, par programmation, récupérer le PDF/A  en appelant la `OutputResult` méthode de l’ `getGeneratedDoc` objet.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode SOAP) : Création d’un  PDF/A à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Création d’un  PDF/A à l’aide de l’API du service Web {#create-a-pdf-a-document-using-the-web-service-api}

Créez un  PDF/A à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker les données qui seront fusionnées avec le PDF/A.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution PDF/A.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option URI du fichier en attribuant une valeur de chaîne qui spécifie l’emplacement du fichier PDF généré par le service Output au membre `PDFOutputOptionsSpec` `fileURI` de données de l’objet. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Définissez la `PDFAConformance` valeur en attribuant une valeur `PDFAConformance` enum au membre `RenderOptionsSpec` `PDFAConformance` de données de l’objet. Par exemple, pour spécifier le niveau de conformité A, affectez-le `PDFAConformance.A` à ce membre de données.
   * Définissez la `PDFARevisionNumber` valeur en attribuant une valeur `PDFARevisionNumber` enum au membre `RenderOptionsSpec` `PDFARevisionNumber` de données de l’objet. Attribuez-vous `PDFARevisionNumber.Revision_1` à ce membre de données.
   >[!NOTE]
   >
   >La version PDF d’un  PDF/A est 1.4, quelle que soit la valeur spécifiée.

1. Générez un  PDF/A.

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * Valeur de  TransformationFormat. Pour générer un  PDF, spécifiez `TransformationFormat.PDFA`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   >[!NOTE]
   >
   >Vous pouvez également créer un PDF /A en appelant la méthode `OutputClient` 2 de l’objet `generatePDFOutput`2. (voir [Transmission des  de situés dans Content Services (obsolète) au service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)Output).)

1. Récupérez les résultats de l’opération.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant des données de résultat. Vérifiez que l’extension du nom de fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet qui a été renseigné par la méthode `OutputServiceService` `generatePDFOutput` de l’objet (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur du champ de l’ `BLOB` objet `MTOM` .
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Transmission des  de situés dans Content Services (obsolète) vers Output Service {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Le service Output effectue le rendu d’un formulaire PDF non interactif basé sur une conception de formulaire généralement enregistrée sous la forme d’un fichier XDP et créée dans Designer. Vous pouvez transmettre un `com.adobe.idp.Document` objet contenant la conception de formulaire au service Output. Le service Output effectue ensuite le rendu de la conception de formulaire située dans l’ `com.adobe.idp.Document` objet.

L’avantage de transmettre un `com.adobe.idp.Document` objet au service Output est que d’autres opérations du service AEM Forms renvoient une `com.adobe.idp.Document` instance. Autrement dit, vous pouvez obtenir une `com.adobe.idp.Document` instance à partir d’une autre opération de service et la rendre. Supposons, par exemple, qu’un fichier XDP soit stocké dans un noeud Content Services (obsolète) nommé `/Company Home/Form Designs`, comme illustré ci-dessous.

Vous pouvez par programmation récupérer le fichier Loan.xdp de Content Services (obsolète) et transmettre le fichier XDP au service Output dans un `com.adobe.idp.Document` objet.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour transmettre un  obtenu de Content Services (obsolète) au service Output, effectuez l’ suivante :

1. Incluez des fichiers de projet.
1. Créez un objet Output et un objet API Client de gestion des .
1. Récupérez la conception de formulaire à partir de Content Services (obsolète).
1. Générer le formulaire PDF non interactif.
1. Exécutez une action avec le flux de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires à votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’une sortie et d’un objet API Client Management**

Avant de pouvoir exécuter par programmation une opération d’API de service Output, créez un objet API Client de sortie. En outre, dans la mesure où ce processus récupère un fichier XDP de Content Services (obsolète), créez un objet API de gestion des.

**Récupération de la conception de formulaire à partir de Content Services (obsolète)**

Récupérez le fichier XDP à partir de Content Services (obsolète) à l’aide de l’API Java ou de service Web. Le fichier XDP est renvoyé dans une `com.adobe.idp.Document` instance (ou une `BLOB` instance si vous utilisez des services Web). Vous pouvez ensuite transmettre l’ `com.adobe.idp.Document` instance au service Output.

**Rendu du formulaire PDF non interactif**

Pour effectuer le rendu d’un formulaire non interactif, transmettez l’ `com.adobe.idp.Document` instance renvoyée par Content Services (obsolète) au service Output.

>[!NOTE]
>
>Deux nouvelles méthodes nommées `generatePDFOutput2`et g `eneratePrintedOutput2`acceptent un `com.adobe.idp.Document` objet contenant une conception de formulaire. Vous pouvez également transmettre une `com.adobe.idp.Document`qui contient la conception de formulaire au service Output lors de l’envoi d’un flux d’impression vers une imprimante réseau.

**Exécution d’une action avec le flux de données du formulaire**

Vous pouvez enregistrer le formulaire non interactif au format PDF. Le formulaire peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Transmettez  au service Output Service à l’aide de l’API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Transmettre  au service Output Service à l’aide de l’API du service Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Création de PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Transmettez  au service Output Service à l’aide de l’API Java {#pass-documents-to-the-output-service-using-the-java-api}

Transmettez un  récupéré de Content Services (obsolète) à l’aide du service Output et de l’API Content Services (obsolète) (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar et adobe-contentservices-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Output et un objet API Client de gestion des .

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez la conception de formulaire à partir de Content Services (obsolète).

   Appelez la méthode `DocumentManagementServiceClientImpl` `retrieveContent` de l’objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie le magasin où le contenu est ajouté. The default store is `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   La `retrieveContent` méthode renvoie un `CRCResult` objet contenant le fichier XDP. Récupérez une `com.adobe.idp.Document` instance en appelant la `CRCResult` `getDocument` méthode de l’objet.

1. Générer le formulaire PDF non interactif.

   Appelez la méthode `OutputClient` `generatePDFOutput2` de l’objet et transmettez les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur de chaîne qui spécifie la racine du contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `com.adobe.idp.Document` représentant la conception de formulaire (utilisez l’instance renvoyée par la `CRCResult` `getDocument` méthode de l’objet).
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. Exécutez une action avec le flux de données du formulaire.

   * Récupérez un `com.adobe.idp.Document` objet qui représente le formulaire non interactif en appelant la `OutputResult` `getGeneratedDoc` méthode de l’objet.
   * Créez un `java.io.File` objet contenant les résultats de l’opération. Vérifiez que l’extension du nom de fichier est .pdf.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getGeneratedDoc` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Transmission du au service Output à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[rapide (mode SOAP) : Transmission du au service Output à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Transmettre  au service Output Service à l’aide de l’API du service Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Transmettez un  récupéré de Content Services (obsolète) à l’aide du service Output et de l’API Content Services (obsolète) (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Comme cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Output : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Gestion des  : `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Le type de `BLOB` données étant commun aux deux références de service, qualifiez pleinement le type de `BLOB` données lors de son utilisation. Dans le  rapide du service Web correspondant, toutes les `BLOB` instances sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Output et un objet API Client de gestion des .

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Répétez ces étapes pour le client de `DocumentManagementServiceClient`service.

1. Récupérez la conception de formulaire à partir de Content Services (obsolète).

   Récupérez le contenu en appelant la `DocumentManagementServiceClient` `retrieveContent` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie le magasin où le contenu est ajouté. The default store is `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   * Paramètre de sortie de chaîne qui stocke la valeur du lien de navigation.
   * Paramètre `BLOB` de sortie qui stocke le contenu. Vous pouvez utiliser ce paramètre de sortie pour récupérer le contenu.
   * Paramètre `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` de sortie qui stocke les attributs de contenu.
   * Paramètre `CRCResult` de sortie. Au lieu d’utiliser cet objet, vous pouvez utiliser le paramètre `BLOB` output pour récupérer le contenu.

1. Générer le formulaire PDF non interactif.

   Appelez la méthode `OutputServiceClient` `generatePDFOutput2` de l’objet et transmettez les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur de chaîne qui spécifie la racine du contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `BLOB` représentant la conception de formulaire (utilisez l’ `BLOB` instance renvoyée par Content Services (obsolète)).
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet de sortie `BLOB` renseigné par la `generatePDFOutput2` méthode. La `generatePDFOutput2` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet output `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   La `generatePDFOutput2` méthode renvoie un `BLOB` objet contenant le formulaire PDF non interactif.

1. Exécutez une action avec le flux de données du formulaire.

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet récupéré à partir de la `generatePDFOutput2` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Transmission du  situé dans le référentiel vers le service Output {#passing-documents-located-in-the-repository-to-the-output-service}

Le service Output effectue le rendu d’un formulaire PDF non interactif basé sur une conception de formulaire généralement enregistrée sous la forme d’un fichier XDP et créée dans Designer. Vous pouvez transmettre un `com.adobe.idp.Document` objet contenant la conception de formulaire au service Output. Le service Output effectue ensuite le rendu de la conception de formulaire située dans l’ `com.adobe.idp.Document` objet.

L’avantage de transmettre un `com.adobe.idp.Document` objet au service Output est que d’autres opérations du service AEM Forms renvoient une `com.adobe.idp.Document` instance. Autrement dit, vous pouvez obtenir une `com.adobe.idp.Document` instance à partir d’une autre opération de service et la rendre. Supposons, par exemple, qu’un fichier XDP soit stocké dans le référentiel AEM Forms, comme illustré ci-dessous.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

Le dossier *FormsFolder* est un emplacement défini par l’utilisateur dans le référentiel AEM Forms (cet emplacement est un exemple et n’existe pas par défaut). Dans cet exemple, une conception de formulaire nommée Loan.xdp se trouve dans ce dossier. Outre la conception de formulaire, d’autres éléments collatéraux de formulaire, tels que des images, peuvent être stockés à cet emplacement. Le chemin d’accès à une ressource située dans le référentiel AEM Forms est :

`Applications/Application-name/Application-version/Folder.../Filename`

Vous pouvez récupérer par programmation le fichier Loan.xdp du référentiel AEM Forms et le transmettre au service Output dans un `com.adobe.idp.Document` objet.

Vous pouvez créer un fichier PDF à partir d’un fichier XDP situé dans le référentiel de l’une des deux manières suivantes. Vous pouvez transmettre l’emplacement XDP par référence ou, par programmation, récupérer le fichier XDP du référentiel et le transmettre au service Output dans un fichier XDP.

[rapide (mode EJB) : Création d’un  PDF basé sur un fichier XDP d’application à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) Java (indique comment transmettre l’emplacement du fichier XDP par référence).

[rapide (mode EJB) : La transmission d’un  situé dans le référentiel AEM Forms au service Output à l’aide de l’API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) Java (indique comment récupérer par programmation le fichier XDP du référentiel AEM Forms et le transmettre au service Output au sein d’une `com.adobe.idp.Document` instance). (Cette section explique comment effectuer cette  de)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour transmettre un  obtenu du référentiel AEM Forms au service Output, effectuez l’ de suivante :

1. Incluez des fichiers de projet.
1. Créez un objet Output et un objet API Client de gestion des .
1. Récupérez la conception de formulaire à partir du référentiel AEM Forms.
1. Générer le formulaire PDF non interactif.
1. Exécutez une action avec le flux de données.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires à votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’une sortie et d’un objet API Client Management**

Avant de pouvoir exécuter par programmation une opération d’API de service Output, créez un objet API Client de sortie. En outre, dans la mesure où ce processus récupère un fichier XDP de Content Services (obsolète), créez un objet API de gestion des.

**Récupération de la conception de formulaire à partir du référentiel AEM Forms**

Récupérez le fichier XDP depuis le référentiel AEM Forms à l’aide de l’API Repository. (Voir Ressources [](/help/forms/developing/aem-forms-repository.md#reading-resources)de lecture.)

Le fichier XDP est renvoyé dans une `com.adobe.idp.Document` instance (ou une `BLOB` instance si vous utilisez des services Web). Vous pouvez ensuite transmettre l’ `com.adobe.idp.Document` instance au service Output.

**Rendu du formulaire PDF non interactif**

Pour effectuer le rendu d’un formulaire non interactif, transmettez l’ `com.adobe.idp.Document` instance qui a été renvoyée à l’aide de l’API Repository d’AEM Forms.

>[!NOTE]
>
>Deux nouvelles méthodes nommées `generatePDFOutput2`et `generatePrintedOutput2`acceptant un `com.adobe.idp.Document`objet contenant une conception de formulaire. Vous pouvez également transmettre une `com.adobe.idp.Document` qui contient la conception de formulaire au service Output lors de l’envoi d’un flux d’impression vers une imprimante réseau.

**Exécution d’une action avec le flux de données du formulaire**

Vous pouvez enregistrer le formulaire non interactif au format PDF. Le formulaire peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Transmettez  situé dans le référentiel au service Output à l’aide de l’API Java.](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Transmettez  situé dans le référentiel au service Output à l’aide de l’API Java. {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Transmettez un  récupéré du référentiel à l’aide du service Output et de l’API Repository (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar et adobe-repository-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Output et un objet API Client de gestion des .

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez la conception de formulaire à partir du référentiel AEM Forms.

   Appelez la méthode `ResourceRepositoryClient` `readResourceContent` de l’objet et transmettez une valeur de chaîne qui spécifie l’emplacement URI au fichier XDP. Par exemple, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Cette valeur est obligatoire. Cette méthode renvoie une `com.adobe.idp.Document` instance représentant le fichier XDP.

1. Générer le formulaire PDF non interactif.

   Appelez la méthode `OutputClient` `generatePDFOutput2` de l’objet et transmettez les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur de chaîne qui spécifie la racine du contenu où se trouvent les ressources supplémentaires, telles que les images. Par exemple, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * Objet `com.adobe.idp.Document` représentant la conception de formulaire (utilisez l’instance renvoyée par la `ResourceRepositoryClient` `readResourceContent` méthode de l’objet).
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. Exécutez une action avec le flux de données du formulaire.

   * Récupérez un `com.adobe.idp.Document` objet qui représente le formulaire non interactif en appelant la `OutputResult` `getGeneratedDoc` méthode de l’objet.
   * Créez un `java.io.File` objet contenant les résultats de l’opération. Vérifiez que l’extension du nom de fichier est .pdf.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getGeneratedDoc` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Transmission d’un  situé dans le référentiel AEM Forms au service Output à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création de PDF à l’aide de fragments {#creating-pdf-documents-using-fragments}

Vous pouvez utiliser les services Output et Assembler pour créer un flux de sortie, tel qu’un PDF, basé sur des fragments. Le service Assembler assemble un XDP basé sur des fragments situés dans plusieurs fichiers XDP. Le  XDP assemblé est transmis au service Output, qui crée un PDF . Bien que ce flux de travail montre un PDF en cours de génération, le service Output peut générer d’autres types de sortie, tels que ZPL, pour ce flux de travail. Un PDF est utilisé à des fins de discussion uniquement.

L’illustration suivante illustre ce processus.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Avant de lire *Création d’un PDF à l’aide de fragments*, il est recommandé de se familiariser avec l’utilisation du service Assembler pour assembler plusieurs  de XDP. (Voir [Assemblage de plusieurs fragments](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)XDP.)

>[!NOTE]
>
>Vous pouvez également transmettre une conception de formulaire assemblée par le service Assembler au service Forms au lieu du service Output. La principale différence entre le service Output et le service Forms réside dans le fait que le service Forms génère des  PDF interactifs et le service Output génère des  PDF non interactifs. De même, le service Forms ne peut pas générer de flux de sortie basés sur l’imprimante comme ZPL.

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour créer un PDF basé sur des fragments, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client Output et Assembler.
1. Utilisez le service Assembler pour générer la conception de formulaire.
1. Utilisez le service Output pour générer le  PDF.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un objet Client Output et Assembler**

Avant de pouvoir exécuter par programmation une opération d’API de service Output, créez un objet API Client de sortie. En outre, comme ce processus appelle le service Assembler pour créer la conception de formulaire, créez un objet API Client Assembler.

**Utilisez le service Assembler pour générer la conception de formulaire.**

Utilisez le service Assembler pour générer la conception de formulaire à l’aide de fragments. Le service Assembler renvoie une `com.adobe.idp.Document` instance contenant la conception de formulaire.

**Utilisez le service Output pour générer le PDF**

Vous pouvez utiliser le service Output pour générer un PDF à l’aide de la conception de formulaire créée par le service Assembler. Transmettez l’ `com.adobe.idp.Document` instance renvoyée par le service Assembler au service Output.

**Enregistrer le  PDF en tant que fichier PDF**

Une fois que le service Output a généré un  PDF, vous pouvez l’enregistrer au format PDF.

**Voir également**

[Création d’un PDF basé sur des fragments à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Création d’un PDF basé sur des fragments à l’aide de l’API du service Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Assemblage de plusieurs fragments XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Création de  PDF](creating-document-output-streams.md#creating-pdf-documents)

### Création d’un PDF basé sur des fragments à l’aide de l’API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Créez un  PDF basé sur des fragments à l’aide de l’API Output Service et de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client Output et Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Utilisez le service Assembler pour générer la conception de formulaire.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le DDX à utiliser.
   * Objet `java.util.Map` contenant les fichiers XDP d’entrée.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau du journal des tâches.
   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant le  XDP assemblé. Pour récupérer le  XDP assemblé, effectuez les actions suivantes :

   * Appelez la méthode `AssemblerResult` `getDocuments` de l’objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet résultant.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le  XDP assemblé.


1. Utilisez le service Output pour générer le  PDF.

   Appelez la méthode `OutputClient` `generatePDFOutput2` de l’objet et transmettez les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`
   * Valeur de chaîne qui spécifie la racine du contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `com.adobe.idp.Document` représentant la conception de formulaire (utilisez l’instance renvoyée par le service Assembler)
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation

1. Enregistrez le  PDF au format PDF.

   * Récupérez un `com.adobe.idp.Document` objet représentant le PDF en appelant la `OutputResult` méthode de l’ `getGeneratedDoc` objet.
   * Créez un `java.io.File` objet contenant les résultats de l’opération. Assurez-vous que l’extension de nom de fichier est .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. (Veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getGeneratedDoc` méthode.)

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Création d’un PDF basé sur des fragments à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[rapide (mode SOAP) : Création d’un PDF basé sur des fragments à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Création d’un PDF basé sur des fragments à l’aide de l’API du service Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Créez un  PDF basé sur des fragments à l’aide de l’API Output Service et de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Utilisez la définition WSDL suivante pour la référence de service associée au service Output :

   ```as3
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilisez la définition WSDL suivante pour la référence de service associée au service Assembler :

   ```as3
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Le type de `BLOB` données étant commun aux deux références de service, qualifiez pleinement le type de `BLOB` données lors de son utilisation. Dans le  rapide du service Web correspondant, toutes les `BLOB` instances sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client Output et Assembler.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au `OutputServiceClient.ClientCredentials.UserName.UserName`champ.
      * Attribuez la valeur de mot de passe correspondante au `OutputServiceClient.ClientCredentials.UserName.Password`champ.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au `BasicHttpBindingSecurity.Transport.ClientCredentialType`champ.
   * Attribuez la valeur `BasicHttpSecurityMode.TransportCredentialOnly` constante au `BasicHttpBindingSecurity.Security.Mode`champ.
   >[!NOTE]
   >
   >Répétez ces étapes pour l’ `AssemblerServiceClient`objet.

1. Utilisez le service Assembler pour générer la conception de formulaire.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le DDX 
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution
   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues. Pour obtenir le nouveau  XDP, effectuez les actions suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant le  PDF résultant.
   * Parcourez l’ `Map` objet pour récupérer la conception de formulaire assemblée. Transformez les éléments `value` de ce membre de la baie en un `BLOB`. Transmettez cette `BLOB` instance au service Output.


1. Utilisez le service Output pour générer le  PDF.

   Appelez la méthode `OutputServiceClient` `generatePDFOutput2` de l’objet et transmettez les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur de chaîne qui spécifie la racine du contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `BLOB` représentant la conception de formulaire (utilisez l’ `BLOB` instance renvoyée par le service Assembler).
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet de sortie `BLOB` que la `generatePDFOutput2` méthode renseigne. La `generatePDFOutput2` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet output `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   La `generatePDFOutput2` méthode renvoie un `BLOB` objet contenant le formulaire PDF non interactif.

1. Enregistrez le  PDF au format PDF.

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet récupéré à partir de la `generatePDFOutput2` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Impression dans des fichiers {#printing-to-files}

Vous pouvez utiliser le service Output pour imprimer des flux tels que PostScript, PCL (Printer Control Language) ou les formats d’étiquette suivants dans un fichier :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Le service Output vous permet de fusionner des données XML avec une conception de formulaire et d’imprimer le formulaire dans un fichier. L’illustration suivante montre le service Output qui crée des fichiers laser et d’étiquettes.

>[!NOTE]
>
>Pour plus d’informations sur l’envoi de flux d’impression vers des imprimantes, voir [Envoi de flux d’impression vers des imprimantes](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour imprimer dans un fichier, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définissez les options d’exécution d’impression requises pour imprimer dans un fichier.
1. Imprimez le flux d’impression dans un fichier.
1. Récupérez les résultats de l’opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. (Voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceService` objet.

**Référence à une source de données XML**

Pour imprimer un qui contient des données, vous devez référencer une source de données XML qui contient des éléments XML pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définition des options d’exécution d’impression requises pour l’impression dans un fichier**

Pour imprimer dans un fichier, vous devez définir l’option d’exécution de l’URI du fichier en spécifiant l’emplacement et le nom du fichier dans lequel le service Output imprime. Par exemple, pour demander au service Output d’imprimer un fichier PostScript nommé *MortgageForm.ps* sur C:\Adobe, spécifiez C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Vous pouvez définir des options d’exécution facultatives. Pour plus d’informations sur toutes les options que vous pouvez définir, voir la référence de `PrintedOutputOptionsSpec` classe dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Imprimer le flux d’impression dans un fichier**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini les options d’exécution d’impression, vous pouvez appeler le service Output, ce qui entraîne l’impression d’un fichier.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que des données XML, qui indiquent si l’opération a réussi.

**Voir également**

[Imprimer dans des fichiers à l’aide de l’API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimer dans des fichiers à l’aide de l’API du service Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimer dans des fichiers à l’aide de l’API Java {#print-to-files-using-the-java-api}

Imprimer dans un fichier à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client de sortie.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez une source de données XML.

   * Créez un `java.io.FileInputStream` objet représentant la source de données XML utilisée pour remplir le à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution d’impression requises pour imprimer dans un fichier.

   * Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur.
   * Spécifiez le fichier en appelant la `setFileURI` méthode de l’objet PrintedOutputOptionsSpec et en transmettant une valeur de chaîne qui représente le nom et l’emplacement du fichier. Par exemple, si vous souhaitez que le service Output s’imprime dans un fichier PostScript appelé MortgageForm.ps situé dans C:\Adobe, spécifiez C:\\Adobe\MortgageForm.ps.
   * Spécifiez le nombre de copies à imprimer en appelant la `PrintedOutputOptionsSpec` `setCopies` méthode de l’objet et en transmettant un entier représentant le nombre de copies.

1. Imprimez le flux d’impression dans un fichier.

   Imprimez dans un fichier en appelant la `OutputClient` `generatePrintedOutput` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur  `PrintFormat` spécifiant le format de flux d’impression à créer. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie l’emplacement des fichiers de protection connexes, tels que les fichiers image.
   * Valeur de chaîne spécifiant l’emplacement du fichier XDC à utiliser (vous pouvez transmettre `null` si vous avez spécifié le fichier XDC à utiliser à l’aide de l’ `PrintedOutputOptionsSpec` objet).
   * Objet `PrintedOutputOptionsSpec` contenant les options d’exécution requises pour l’impression dans un fichier.
   * Objet `com.adobe.idp.Document` contenant la source de données XML qui contient des données de formulaire.
   The `generatePrintedOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >La `OutputResult` méthode de l’ `getRecordLevelMetaDataList` objet renvoie `null`.

1. Récupérez les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` objet qui représente l’état de la `generatePrintedOutput` méthode en appelant la `OutputResult` méthode de l’ `getStatusDoc` objet (l’objet a été renvoyé par la `OutputResult` `generatePrintedOutput` méthode).
   * Créez un `java.io.File` objet qui contiendra les résultats de l’opération. Vérifiez que l’extension de fichier est XML.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getStatusDoc` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode SOAP) : Impression dans un fichier à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Imprimer dans des fichiers à l’aide de l’API du service Web {#print-to-files-using-the-web-service-api}

Imprimer dans un fichier à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker les données de formulaire.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier XML contenant les données du formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `binaryData` propriété au contenu du tableau d’octets.

1. Définissez les options d’exécution d’impression requises pour imprimer dans un fichier.

   * Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur.
   * Spécifiez le fichier en attribuant une valeur de chaîne représentant l’emplacement et le nom du fichier au membre de `PrintedOutputOptionsSpec` données de l’ `fileURI` objet. Par exemple, si vous souhaitez que le service Output s’imprime dans un fichier PostScript nommé *MortgageForm.ps* situé dans C:\Adobe, spécifiez C:\\Adobe\MortgageForm.ps.
   * Spécifiez le nombre de copies à imprimer en attribuant un nombre entier représentant le nombre de copies aux membres de `PrintedOutputOptionsSpec` données de l’ `copies` objet.

1. Imprimez le flux d’impression dans un fichier.

   Imprimez dans un fichier en appelant la `OutputServiceService` `generatePrintedOutput` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur  `PrintFormat` spécifiant le format de flux d’impression à créer. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie l’emplacement des fichiers de protection connexes, tels que les fichiers image.
   * Valeur de chaîne spécifiant l’emplacement du fichier XDC à utiliser (vous pouvez transmettre `null` si vous avez spécifié le fichier XDC à utiliser à l’aide de l’ `PrintedOutputOptionsSpec` objet).
   * Objet `PrintedOutputOptionsSpec` contenant les options d’exécution d’impression requises pour l’impression dans un fichier.
   * Objet `BLOB` contenant la source de données XML qui contient des données de formulaire.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)

1. Récupérez les résultats de l’opération.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant des données de résultat. Vérifiez que l’extension de fichier est XML.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet qui a été renseigné par la méthode `OutputServiceService` `generatePDFOutput` de l’objet (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Envoi de flux d&#39;impression aux imprimantes {#sending-print-streams-to-printers}

Vous pouvez utiliser le service Output pour envoyer des flux d’impression tels que PostScript, PCL (Printer Control Language) ou les formats d’étiquette suivants aux imprimantes réseau :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Le service Output vous permet de fusionner des données XML avec une conception de formulaire et de générer le formulaire sous forme de flux d’impression. Par exemple, vous pouvez créer un flux d’impression PostScript et l’envoyer à une imprimante réseau. L’illustration suivante montre le service Output envoyant des flux d’impression vers des imprimantes réseau.

>[!NOTE]
>
>Pour démontrer comment envoyer un flux d’impression vers une imprimante réseau, cette section envoie un flux d’impression PostScript vers une imprimante réseau à l’aide du protocole d’imprimante SharedPrinter.

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour envoyer un flux d’impression vers une imprimante réseau, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définition des options d’exécution d’impression
1. Récupérez un  à imprimer.
1. Envoyez le  à une imprimante réseau.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, créez un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceClient` objet.

**Référence à une source de données XML**

Pour imprimer un qui contient des données, vous devez référencer une source de données XML qui contient des éléments XML pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définition des options d’exécution d’impression**

Vous pouvez définir les options d’exécution lors de l’envoi d’un flux d’impression vers une imprimante, notamment les options suivantes :

* **Copies**: Indique le nombre de copies à envoyer à l’imprimante. La valeur par défaut est 1.   
* **Agrafer**: Une option XCI est définie lorsqu’un agrafeur est utilisé. Cette option peut être spécifiée dans le modèle de configuration par l’élément agrafeuse et est utilisée uniquement pour les imprimantes PS et PCL.
* **OutputJog**: Une option XCI est définie lorsque les pages de sortie doivent être tracées (déplacées physiquement dans le bac de réception). Cette option s’applique uniquement aux imprimantes PS et PCL.
* **OutputBin**: Valeur XCI utilisée pour permettre au pilote d’impression de sélectionner la corbeille de sortie appropriée.

>[!NOTE]
>
>Pour plus d’informations sur toutes les options d’exécution que vous pouvez définir, voir la référence de `PrintedOutputOptionsSpec` classe.

**Récupération d’un  à imprimer**

Récupérez un flux d’impression à envoyer à une imprimante. Par exemple, vous pouvez récupérer un fichier PostScript et l’envoyer à une imprimante.

Vous pouvez choisir d’envoyer un fichier PDF si votre imprimante prend en charge le format PDF. Cependant, l’envoi d’un PDF à une imprimante pose problème, car chaque fabricant d’imprimante a une implémentation différente de l’interpréteur PDF. En d’autres termes, certains fabricants d’impression utilisent l’interprétation Adobe PDF, mais cela dépend de l’imprimante. D’autres imprimantes ont leur propre interprète PDF. Par conséquent, les résultats de l’impression peuvent varier.

Une autre limitation de l’envoi d’un PDF  à une imprimante est qu’il s’agit simplement d’une impression ; il ne peut pas accéder au mode recto verso, à la sélection des bacs à papier et à l’agrafage, sauf par le biais des paramètres de l’imprimante.

Pour récupérer un  à imprimer, utilisez la `generatePrintedOutput` méthode. Le tableau suivant spécifie les types de contenu définis pour un flux d’impression donné lors de l’utilisation de la `generatePrintedOutput` méthode.

<table>
 <thead>
  <tr>
   <th><p>Format d’impression </p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>Crée un flux de sortie xdc dpl203.xdc par défaut ou personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 300 ppp.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 400 ppp.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 600 ppp.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crée un flux de sortie PCL (5c) couleur générique.</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crée un flux de sortie PostScript Niveau 3 générique.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crée un flux de sortie IPL personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie IPL 300 ppp.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>Crée un flux de sortie IPL 400 ppp.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crée un flux de sortie Generic Monochrome PCL (5e).</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crée un flux de sortie PostScript Niveau 2 générique.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crée un flux de sortie TPCL personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>Crée un flux de sortie TPCL 305 ppp.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>Crée un flux de sortie TPCL 600 ppp.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crée un flux de sortie ZPL 203 ppp.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie ZPL 300 ppp.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez également envoyer un flux d’impression vers une imprimante à l’aide de la `generatePrintedOutput2` méthode. Cependant, le  rapide associé à la section Envoi des flux d’impression aux imprimantes utilise la `generatePrintedOutput` méthode.

**Envoi du flux d’impression vers une imprimante réseau**

Une fois que vous avez récupéré un à imprimer, vous pouvez appeler le service Output, ce qui entraîne l’envoi d’un flux d’impression vers une imprimante réseau. Pour que le service Output localise correctement l’imprimante, vous devez spécifier le serveur d’impression et le nom de l’imprimante. En outre, vous devez également spécifier le protocole d’impression.

>[!NOTE]
>
>Si PDFG est installé sur le serveur Forms et que le serveur s’exécute sur Windows Server 2008, vous ne pouvez pas utiliser la propriété SharedPrinter. Dans ce cas, utilisez un protocole d’imprimante différent.

>[!NOTE]
>
>Si vous utilisez une imprimante réseau et que le mécanisme d&#39;accès est SharedPrinter, vous devez spécifier le chemin d&#39;accès réseau complet de l&#39;imprimante.Envoyez un flux d&#39;impression vers une imprimante réseau à l&#39;aide de l&#39;API Java.

Envoyez un flux d’impression vers une imprimante réseau à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet Client de sortie

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référence à une source de données XML

   * Créez un `java.io.FileInputStream` objet représentant la source de données XML utilisée pour remplir le à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution d’impression

   Créez un `PrintedOutputOptionsSpec` objet représentant les options d’exécution d’impression. Par exemple, vous pouvez spécifier le nombre de copies à imprimer en appelant la méthode `PrintedOutputOptionsSpec` `setCopies` de l’objet.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la valeur de pagination à l’aide de la `PrintedOutputOptionsSpec` `setPagination` méthode de l’objet si vous générez un flux d’impression ZPL. De même, vous ne pouvez pas définir les options suivantes pour un flux d’impression ZPL : OutputJog, PageOffset et Staple. La `setPagination` méthode n’est pas valide pour la génération PostScript. Elle n’est valide que pour la génération PCL.

1. Récupération d’un  à imprimer

   * Récupérez un à imprimer en appelant la `OutputClient` `generatePrintedOutput` méthode de l’objet et en transmettant les valeurs suivantes :

      * Valeur  `PrintFormat` qui spécifie le flux d’impression. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
      * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
      * Valeur de chaîne qui spécifie l’emplacement des fichiers de support connexes, tels que les fichiers image.
      * Valeur de chaîne spécifiant l’emplacement du fichier XDC à utiliser.
      * Objet `PrintedOutputOptionsSpec` contenant des options d’exécution requises pour l’impression dans un fichier.
      * Objet `com.adobe.idp.Document` représentant la source de données XML contenant les données de formulaire à fusionner avec la conception de formulaire.
      Cette méthode renvoie un `OutputResult` objet contenant les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` objet à envoyer à l’imprimante en appelant la `OutputResult` méthode de l’ `getGeneratedDoc` objet. Cette méthode renvoie un `com.adobe.idp.Document` objet.


1. Envoi du flux d’impression vers une imprimante réseau

   Envoyez le flux d’impression vers une imprimante réseau en appelant la `OutputClient` `sendToPrinter` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le flux d’impression à envoyer à l’imprimante.
   * Valeur  `PrinterProtocol` spécifiant le protocole d’imprimante à utiliser. Par exemple, pour spécifier le protocole SharedPrinter, transmettez `PrinterProtocol.SharedPrinter`.
   * Valeur de chaîne qui spécifie le nom du serveur d’impression. Par exemple, en supposant que le nom du serveur d’impression soit PrintServer1, transmettez `\\\PrintSever1`.
   * Valeur de chaîne qui spécifie le nom de l’imprimante. Par exemple, en supposant que le nom de l’imprimante soit Printer1, transmettez `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >La `sendToPrinter` méthode a été ajoutée à l’API AEM Forms dans la version 8.2.1.

### Envoi d’un flux d’impression vers une imprimante à l’aide de l’API du service Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envoyez un flux d’impression vers une imprimante réseau à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker les données de formulaire.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML contenant les données de formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Déterminez la longueur du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution d’impression.

   Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur. Par exemple, vous pouvez spécifier le nombre de copies à imprimer en attribuant un nombre entier qui représente le nombre de copies au membre `PrintedOutputOptionsSpec` `copies` de données de l’objet.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la valeur de pagination à l’aide du membre `PrintedOutputOptionsSpec` `pagination` de données de l’objet si vous générez un flux d’impression ZPL. De même, vous ne pouvez pas définir les options suivantes pour un flux d’impression ZPL : OutputJog, PageOffset et Staple. Le membre `pagination` de données n’est pas valide pour la génération PostScript. Elle n’est valide que pour la génération PCL.

1. Récupérez un  à imprimer.

   * Récupérez un à imprimer en appelant la `OutputServiceService` `generatePrintedOutput` méthode de l’objet et en transmettant les valeurs suivantes :

      * Valeur  `PrintFormat` qui spécifie le flux d’impression. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
      * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
      * Valeur de chaîne qui spécifie l’emplacement des fichiers de support connexes, tels que les fichiers image.
      * Valeur de chaîne spécifiant l’emplacement du fichier XDC à utiliser.
      * Objet `PrintedOutputOptionsSpec` contenant les options d’exécution d’impression utilisées lors de l’envoi d’un flux d’impression vers une imprimante réseau.
      * Objet `BLOB` contenant la source de données XML qui contient des données de formulaire.
      * Objet `BLOB` renseigné par la `generatePrintedOutput` méthode. La `generatePrintedOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
      * Objet `BLOB` renseigné par la `generatePrintedOutput` méthode. La `generatePrintedOutput` méthode renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
      * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Créez un `BLOB` objet à envoyer à l’imprimante en obtenant la valeur de la `OutputResult` `generatedDoc` méthode de l’objet. Cette méthode renvoie un `BLOB` objet contenant des données PostScript renvoyées par la `generatePrintedOutput` méthode.


1. Envoyez le flux d’impression vers une imprimante réseau.

   Envoyez le flux d’impression vers une imprimante réseau en appelant la `OutputClient` `sendToPrinter` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` représentant le flux d’impression à envoyer à l’imprimante.
   * Valeur  `PrinterProtocol` spécifiant le protocole d’imprimante à utiliser. Par exemple, pour spécifier le protocole SharedPrinter, transmettez `PrinterProtocol.SharedPrinter`.
   * Valeur `bool` indiquant si la valeur du paramètre précédent doit être utilisée. Transmettez la valeur `true`. (Cette valeur de paramètre est requise pour l’appel de service Web uniquement.)
   * Valeur de chaîne qui spécifie le nom du serveur d’impression. Par exemple, en supposant que le nom du serveur d’impression soit PrintServer1, transmettez `\\\PrintSever1`.
   * Valeur de chaîne qui spécifie le nom de l’imprimante. Par exemple, en supposant que le nom de l’imprimante soit Printer1, transmettez `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >La `sendToPrinter` méthode a été ajoutée à l’API AEM Forms dans la version 8.2.1.

## Création de plusieurs fichiers de sortie {#creating-multiple-output-files}

Le service Output peut créer des  de distinctes pour chaque enregistrement dans une source de données XML ou un seul fichier contenant tous les enregistrements (cette fonctionnalité est la valeur par défaut). Supposons, par exemple, que dix enregistrements se trouvent dans une source de données XML et que vous demandiez au service Output de créer des  PDF (ou d’autres types de sortie) distincts pour chaque enregistrement à l’aide de l’API Output Service. En conséquence, le service Output génère dix  PDF. (Au lieu de créer des  de, vous pouvez envoyer plusieurs flux d’impression vers une imprimante.)

L’illustration suivante montre également le service Output qui traite un fichier de données XML contenant plusieurs enregistrements. Supposons toutefois que vous entriez au service Output de créer un PDF unique contenant tous les enregistrements de données. Dans ce cas, le service Output génère un  qui contient tous les enregistrements.

L’illustration suivante montre le service Output qui traite un fichier de données XML contenant plusieurs enregistrements. Supposons que vous demandiez au service Output de créer un PDF distinct pour chaque enregistrement de données. Dans ce cas, le service Output génère un PDF distinct pour chaque enregistrement de données.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Les données XML suivantes illustrent un exemple de fichier de données contenant trois enregistrements de données.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

Notez que l’élément XML qui  et termine chaque enregistrement de données est `LoanRecord`. Cet élément XML est référencé par la logique de l’application qui génère plusieurs fichiers.

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour créer plusieurs fichiers PDF à partir d’une source de données XML, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définissez les options d’exécution PDF.
1. Définissez les options d’exécution du rendu.
1. Générez plusieurs fichiers PDF.
1. Récupérez les résultats de l’opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceService` objet.

**Référence à une source de données XML**

Référencez une source de données XML contenant plusieurs enregistrements. Un élément XML doit être utilisé pour séparer les enregistrements de données. Par exemple, dans l’exemple de source de données XML illustré plus haut dans cette section, l’élément XML qui sépare les enregistrements de données est nommé `LoanRecord`.

Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définition des options d’exécution PDF**

Vous devez définir les options d’exécution suivantes pour que le service Output crée plusieurs fichiers en fonction d’une source de données XML :

* **Plusieurs fichiers**: Indique si le service Output crée un  de unique ou plusieurs  de. Vous pouvez spécifier true ou false. Pour créer un distinct pour chaque enregistrement de données dans la source de données XML, spécifiez true.
* **URI** du fichier : Indique l’emplacement des fichiers générés par le service Output. Supposons, par exemple, que vous indiquiez C:\\Adobe\forms\Loan.pdf. Dans ce cas, le service Output crée un fichier nommé Loan.pdf et le place dans le dossier C:\\Adobe\forms folder. S’il y a plusieurs fichiers, les noms des fichiers sont Loan0001.pdf, Loan0002.pdf, Loan0003.pdf, etc. Si vous spécifiez un emplacement de fichier, les fichiers sont placés sur le serveur et non sur l’ordinateur client.
* **Nom** de l&#39;enregistrement : Spécifie le nom de l’élément XML dans la source de données qui sépare les enregistrements de données. Par exemple, dans l’exemple de source de données XML illustré précédemment dans cette section, l’élément XML qui sépare les enregistrements de données est appelé `LoanRecord`. (Au lieu de définir l’option d’exécution Nom d’enregistrement, vous pouvez définir le niveau d’enregistrement en lui affectant une valeur numérique qui indique le niveau d’élément qui contient les enregistrements de données. Vous pouvez toutefois définir uniquement le nom de l’enregistrement ou le niveau d’enregistrement. Vous ne pouvez pas définir les deux valeurs.)

**Définition des options d’exécution du rendu**

Vous pouvez définir des options d’exécution de rendu lors de la création de plusieurs fichiers. Bien que ces options ne soient pas requises (contrairement aux options d’exécution de sortie, qui sont requises), vous pouvez effectuer des  telles que l’amélioration des performances du service Output. Vous pouvez, par exemple, mettre en cache la conception de formulaire utilisée par le service Output afin d’améliorer les performances.

Lorsque le service Output traite les enregistrements par lot, il lit les données qui contiennent plusieurs enregistrements de manière incrémentielle. En d’autres termes, le service Output lit les données en mémoire et les libère au fur et à mesure du traitement du lot d’enregistrements. Le service Output charge les données de manière incrémentielle lorsque l’une des deux options d’exécution est définie. Si vous définissez l’option d’exécution Nom d’enregistrement, le service Output lit les données de manière incrémentielle. De même, si vous définissez l’option d’exécution Niveau enregistrement sur 2 ou plus, le service Output lit les données de manière incrémentielle.

Vous pouvez contrôler si le service Output effectue un chargement incrémentiel à l’aide de la `PDFOutputOptionsSpec` méthode ou de la `PrintedOutputOptionSpec` `setLazyLoading` méthode de l’objet. Vous pouvez transmettre la valeur `false` à cette méthode qui désactive le chargement incrémentiel.

**Générer plusieurs fichiers PDF**

Après avoir référencé une source de données XML valide contenant plusieurs enregistrements de données et défini des options d’exécution, vous pouvez appeler le service Output, ce qui entraîne la génération de plusieurs fichiers. Lors de la génération de plusieurs enregistrements, la `OutputResult` méthode de l’objet renvoie `getGeneratedDoc` `null`.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie des données XML qui indiquent si l’opération a réussi. Le code XML suivant est renvoyé par le service Output. Dans ce cas, le service Output a généré 42 .

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Création de plusieurs fichiers PDF à l’aide de l’API Java {#create-multiple-pdf-files-using-the-java-api}

Créez plusieurs fichiers PDF à l’aide de l’API Output (Java) :

1. Inclure les fichiers de projet&quot;

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java. .

1. Création d’un objet Client de sortie

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référence à une source de données XML

   * Créez un `java.io.FileInputStream` objet qui représente la source de données XML contenant plusieurs enregistrements à l’aide de son constructeur et transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option Plusieurs fichiers en appelant la méthode `PDFOutputOptionsSpec` `setGenerateManyFiles` de l’objet. Par exemple, transmettez la valeur `true` pour demander au service Output de créer un fichier PDF distinct pour chaque enregistrement de la source de données XML. (Si vous transmettez `false`, le service Output génère un seul PDF qui contient tous les enregistrements).
   * Définissez l’option URI du fichier en appelant la `PDFOutputOptionsSpec` `setFileUri` méthode de l’objet et en transmettant une valeur de chaîne indiquant l’emplacement des fichiers générés par le service Output. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.
   * Définissez l’option Nom d’enregistrement en appelant la `OutputOptionsSpec` `setRecordName` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le nom de l’élément XML dans la source de données qui sépare les enregistrements de données. (Prenons l’exemple de la source de données XML présentée plus haut dans cette section. Le nom de l’élément XML qui sépare les enregistrements de données est LoanRecord.

1. Définition des options d’exécution du rendu

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en appelant l’objet `RenderOptionsSpec` et en transmettant une `setCacheEnabled` valeur de `Boolean` `true`.

1. Générer plusieurs fichiers PDF

   Générez plusieurs fichiers PDF en appelant la `OutputClient` `generatePDFOutput` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur `TransformationFormat` enum. Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. Récupérer les résultats de l’opération

   * Créez un `java.io.File` objet représentant un fichier XML qui contiendra les résultats de la `generatePDFOutput` méthode. Vérifiez que l’extension du nom de fichier est .xml.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `applyUsageRights` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Création de plusieurs fichiers PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de plusieurs fichiers PDF à l’aide de l’API du service Web {#create-multiple-pdf-files-using-the-web-service-api}

Créez plusieurs fichiers PDF à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker des données de formulaire contenant plusieurs enregistrements.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier XML contenant plusieurs enregistrements.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option Plusieurs fichiers en attribuant une valeur booléenne au membre `OutputOptionsSpec` `generateManyFiles` de données de l’objet. Par exemple, attribuez la valeur `true` à ce membre de données pour demander au service Output de créer un fichier PDF distinct pour chaque enregistrement de la source de données XML. (Si vous affectez `false` à ce membre de données, le service Output génère un seul fichier PDF contenant tous les enregistrements).
   * Définissez l’option URI du fichier en attribuant une valeur de chaîne qui spécifie l’emplacement du ou des fichiers générés par le service Output au membre `OutputOptionsSpec` `fileURI` de données de l’objet. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.
   * Définissez l’option de nom d’enregistrement en attribuant une valeur de chaîne qui spécifie le nom de l’élément XML dans la source de données qui sépare les enregistrements de données du membre `OutputOptionsSpec` `recordName` de données de l’objet.
   * Définissez l’option Copies en attribuant un nombre entier spécifiant le nombre de copies généré par le service Output au membre de `OutputOptionsSpec` `copies` données de l’objet.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en attribuant la valeur `true` au membre `RenderOptionsSpec` `cacheEnabled` de données de l’objet.

1. Générez plusieurs fichiers PDF.

   Créez plusieurs fichiers PDF en appelant la `OutputServiceService` `generatePDFOutput`méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur d’énumération TransformationFormat. Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec les données de résultat.
   * Objet `OutputResult` contenant les résultats de l’opération.

1. Récupérer les résultats de l’opération

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant des données de résultat. Vérifiez que l’extension du nom de fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet qui a été renseigné par la méthode `OutputServiceService` `generatePDFOutput` de l’objet (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `binaryData` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Création de règles de recherche {#creating-search-rules}

Vous pouvez créer des règles de recherche qui conduisent le service Output à examiner les données d’entrée et à utiliser différentes conceptions de formulaire basées sur le contenu des données pour générer la sortie. Par exemple, si le *prêt immobilier* texte se trouve dans les données d’entrée, le service Output peut alors utiliser une conception de formulaire nommée Mortgage.xdp. De même, si le texte *automobile* se trouve dans les données d’entrée, le service Output peut alors utiliser une conception de formulaire enregistrée sous le nom AutomobileLoan.xdp. Bien que le service Output puisse générer différents types de sortie, cette section suppose que le service Output génère un fichier PDF. Le diagramme suivant montre le service Output qui génère un fichier PDF en traitant un fichier de données XML et en utilisant l’une des nombreuses conceptions de formulaire.

En outre, le service Output est en mesure de générer des packages de , où plusieurs enregistrements sont fournis dans l’ensemble de données et chaque enregistrement correspond à une conception de formulaire et où un seul  de est généré avec plusieurs conceptions de formulaire.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour demander au service Output d’utiliser des règles de recherche lors de la génération d’un  de, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Référencez une source de données XML.
1. Définissez des règles de recherche.
1. Définissez les options d’exécution PDF.
1. Définissez les options d’exécution du rendu.
1. Générer un PDF.
1. Récupérez les résultats de l’opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, assurez-vous d’inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output.

**Référence à une source de données XML**

Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de faire correspondre l’ordre dans lequel les éléments XML sont affichés, tant que tous les éléments XML sont spécifiés.

**Définir des règles de recherche**

Pour définir des règles de recherche, vous définissez un ou plusieurs modèles de texte que les services Output recherchent dans les données d’entrée. Pour chaque modèle de texte que vous définissez, vous spécifiez une conception de formulaire correspondante qui est utilisée si le modèle de texte est situé. Si un modèle de texte se trouve, le service Output utilise la conception de formulaire correspondante pour générer la sortie. Un exemple de modèle de texte est le *prêt immobilier*.

>[!NOTE]
>
>Si les modèles de texte ne sont pas localisés, le formulaire par défaut est utilisé. Assurez-vous que toutes les conceptions de formulaire que vous utilisez se trouvent à la racine du contenu.

**Définition des options d’exécution PDF**

Définissez les options d’exécution PDF suivantes pour que le service Output puisse créer un PDF basé sur plusieurs conceptions de formulaire :

* **URI** du fichier : Indique le nom et l’emplacement du fichier PDF généré par le service Output.
* **Règles**: Indique les règles que vous avez définies.
* **LookAHead**: Indique le nombre d’octets à utiliser depuis le début du fichier de données d’entrée pour rechercher les modèles de texte définis. La valeur par défaut est de 500 octets.

**Définition des options d’exécution du rendu**

Vous pouvez définir des options d’exécution de rendu lors de la création de fichiers PDF. Bien que ces options ne soient pas requises (contrairement aux options d’exécution PDF), vous pouvez effectuer des  telles que l’amélioration des performances du service Output. Vous pouvez, par exemple, mettre en cache la conception de formulaire utilisée par le service Output afin d’améliorer les performances.

**Générer un PDF**

Après avoir référencé une source de données XML valide et défini les options d’exécution, vous pouvez appeler le service Output, ce qui génère un  PDF. Si le service Output localise un modèle de texte spécifié dans les données d’entrée, il utilise la conception de formulaire correspondante. Si aucun modèle de texte n’est utilisé, le service Output utilise la conception de formulaire par défaut.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie des données XML qui indiquent si l’opération a réussi.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Création de règles de recherche à l’aide de l’API Java {#create-search-rules-using-the-java-api}

Créez des règles de recherche à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client de sortie.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez une source de données XML.

   * Créez un `java.io.FileInputStream` objet représentant la source de données XML utilisée pour remplir le PDF à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez des règles de recherche.

   * Créez un objet `Rule` en utilisant son constructeur.
   * Définissez un modèle de texte en appelant la `Rule` `setPattern` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie un modèle de texte.
   * Définissez la conception de formulaire correspondante en appelant la `Rule` `setForm` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie le nom de la conception de formulaire.
   >[!NOTE]
   >
   >Pour chaque modèle de texte à définir, répétez les trois étapes secondaires précédentes.

   * Create a `java.util.List` object by using an `java.util.ArrayList` constructor.
   * Pour chaque `Rule` objet que vous avez créé, appelez la `java.util.List` méthode de l’ `add` `Rule` objet et transmettez-le.


1. Définissez les options d’exécution PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Spécifiez le nom et l’emplacement du fichier PDF généré par le service Output en appelant la `PDFOutputOptionsSpec` `setFileURI` méthode de l’objet. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier PDF. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.
   * Définissez les règles que vous avez définies en appelant la `PDFOutputOptionsSpec` `setRules` méthode de l’objet. Transmettez l’ `java.util.List` objet qui contient les `Rule` objets.
   * Définissez le nombre d’octets à analyser pour les modèles de texte définis en appelant la `PDFOutputOptionsSpec` `setLookAhead` méthode de l’objet. Transmettez une valeur entière qui représente le nombre d’octets.

1. Définissez les options d’exécution du rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire afin d’améliorer les performances du service Output en appelant le formulaire `RenderOptionsSpec` et en transmettant `setCacheEnabled` `true`l’objet.

1. Générer un PDF.

   Générez un PDF basé sur plusieurs conceptions de formulaire en appelant la `OutputClient` `generatePDFOutput` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur de chaîne qui spécifie le nom de la conception de formulaire par défaut. Autrement dit, la conception de formulaire utilisée si aucun modèle de texte n’est localisé.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouvent les conceptions de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant les données de formulaire recherchées par le service Output pour les modèles de texte définis.
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. Récupérez les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` objet qui représente l’état de la `generatePDFOutput` méthode en appelant la `OutputResult` méthode de l’ `getStatusDoc` objet.
   * Créez un `java.io.File` objet qui contiendra les résultats de l’opération. Vérifiez que l’extension de fichier est .xml.
   * Appelez la `com.adobe.idp.Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier (veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `getStatusDoc` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Création de règles de recherche à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[rapide (mode SOAP) : Création de règles de recherche à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de règles de recherche à l’aide de l’API de service Web {#create-search-rules-using-the-web-service-api}

Créez des règles de recherche à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker les données qui seront fusionnées avec le PDF.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez des règles de recherche.

   * Créez un objet `Rule` en utilisant son constructeur.
   * Définissez un modèle de texte en attribuant une valeur de chaîne qui spécifie un modèle de texte au membre `Rule` `pattern` de données de l’objet.
   * Définissez la conception de formulaire correspondante en attribuant une valeur de chaîne qui spécifie la conception de formulaire au membre `Rule` `form` de données de l’objet.
   >[!NOTE]
   >
   >Pour chaque modèle de texte à définir, répétez les trois étapes secondaires précédentes.

   * Créez un `MyArrayOf_xsd_anyType` objet qui stocke les règles.
   * Affectez chaque `Rule` objet à un élément du `MyArrayOf_xsd_anyType` tableau. Appelez la `MyArrayOf_xsd_anyType` méthode de l’ `Add` objet pour chaque `Rule` objet.


1. Définition des options d’exécution PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option URI du fichier en attribuant une valeur de chaîne qui spécifie l’emplacement du fichier PDF généré par le service Output au membre `PDFOutputOptionsSpec` `fileURI` de données de l’objet. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.
   * Définissez l’option Copies en attribuant un nombre entier spécifiant le nombre de copies généré par le service Output au membre de `PDFOutputOptionsSpec` `copies` données de l’objet.
   * Définissez les règles que vous avez définies en affectant l’ `MyArrayOf_xsd_anyType` objet qui stocke les règles au membre `PDFOutputOptionsSpec` `rules` de données de l’objet.
   * Définissez le nombre d’octets à analyser pour les modèles de texte définis en attribuant une valeur entière représentant le nombre d’octets à analyser à la méthode `PDFOutputOptionsSpec` `lookAhead` de données de l’objet.

1. Définition des options d’exécution du rendu

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire afin d’améliorer les performances du service Output en attribuant la valeur `true` au membre `RenderOptionsSpec` `cacheEnabled` de données de l’objet.
   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du PDF à l’aide du membre `RenderOptionsSpec` `pdfVersion` de l’objet si le d’entrée est un formulaire Acrobat. Le PDF de sortie conserve la version PDF du formulaire Acrobat. De même, vous ne pouvez pas définir l’option PDF balisé à l’aide de la `RenderOptionsSpec` `taggedPDF` méthode de l’objet si le  d’entrée est un formulaire Acrobat.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option PDF linéarisé en utilisant le `RenderOptionsSpec` `linearizedPDF` membre de l’objet si le PDF d’entrée est certifié ou signé numériquement. Pour plus d’informations, reportez-vous à la page [Signature numérique d’un](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF.

1. Générer un PDF 

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * Valeur  `TransformationFormat` . Pour générer un  PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant des options d’exécution PDF.
   * Objet `RenderOptionsSpec` contenant des options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec des métadonnées générées qui décrivent le  du. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet `BLOB` renseigné par la `generatePDFOutput` méthode. La `generatePDFOutput` méthode renseigne cet objet avec les données de résultat. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre n’est requise que pour l’appel de service Web).
   >[!NOTE]
   >
   >Lorsque vous générez un PDF en appelant la `generatePDFOutput` méthode, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé, certifié ou contenant des droits d’utilisation. Pour plus d’informations sur les droits d’utilisation, voir [Application de droits d’utilisation à un](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.

1. Récupérer les résultats de l’opération

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant des données de résultat. Vérifiez que l’extension de fichier est XML.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet qui a été renseigné par la méthode `OutputServiceService` `generatePDFOutput` de l’objet (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplatissement du PDF {#flattening-pdf-documents}

Vous pouvez utiliser le service Output pour transformer un PDF interactif en PDF non interactif. Un PDF interactif permet aux utilisateurs de saisir ou de modifier des données contenues dans les champs de PDF. The process of transforming an interactive PDF document to a non-interactive PDF document is called *flattening*. Lorsqu’un PDF est aplati, l’utilisateur ne peut pas modifier les données dans les champs  du. S’assurer que les données ne peuvent être modifiées est l’une des raisons de l’aplatissement d’un document PDF.

Vous pouvez aplatir les types de PDF suivants :

*  PDF XFA interactif
* Formulaires Acrobat

Toute tentative d’aplatissement d’un PDF non interactif  une exception.

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-9}

Pour aplatir un PDF interactif en un PDF non interactif, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet Client de sortie.
1. Récupérez un PDF interactif.
1. Transformez le  PDF.
1. Enregistrez le  PDF non interactif au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet Client de sortie**

Avant de pouvoir exécuter une opération de service Output par programmation, vous devez créer un objet client de service Output. Si vous utilisez l’API Java, créez un `OutputClient` objet. Si vous utilisez l’API du service Web Output, créez un `OutputServiceService` objet.

**Récupération d’un PDF interactif**

Récupérez un PDF interactif que vous souhaitez transformer en PDF non interactif. Toute tentative de transformation d’un PDF non interactif entraîne une exception.

**Transformation du PDF**

Une fois que vous avez récupéré un  PDF interactif, vous pouvez le transformer en PDF non interactif. Le service Output renvoie un PDF non interactif.

**Enregistrer le PDF non interactif en tant que fichier PDF**

Vous pouvez enregistrer le  PDF non interactif au format PDF.

**Voir également**

[Aplatissement d’un PDF à l’aide de l’API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Aplatissement d’un PDF à l’aide de l’API du service Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Aplatissement d’un PDF à l’aide de l’API Java {#flatten-a-pdf-document-using-the-java-api}

Aplatissement d’un PDF interactif en un PDF non interactif  à l’aide de l’API Output (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet Client de sortie.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Récupérez un PDF interactif.

   * Créez un `java.io.FileInputStream` objet représentant le PDF interactif à transformer à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier PDF interactif.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Transformez le  PDF.

   Transformez le PDF interactif en PDF non interactif  en appelant la `OutputServiceService` `transformPDF` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le  PDF interactif.
   * Valeur `TransformationFormat` enum. Pour générer un PDF non interactif, spécifiez `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` enum value that specifies the revision number. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `null`.
   * Valeur de chaîne qui représente le numéro de modification et l’année, séparés par un deux-points. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `null`.
   * Valeur d’ `PDFAConformance` énumération représentant le niveau de conformité PDF/A. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `null`.
   La `transformPDF` méthode renvoie un `com.adobe.idp.Document` objet contenant un PDF non interactif.

1. Enregistrez le  PDF non interactif au format PDF.

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `transformPDF` méthode).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[rapide (mode EJB) : Transformation d’un PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[rapide (mode SOAP) : Transformation d’un PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplatissement d’un PDF à l’aide de l’API du service Web {#flatten-a-pdf-document-using-the-web-service-api}

Aplatissement d’un PDF interactif en un PDF non interactif  à l’aide de l’API Output (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet Client de sortie.

   * Créez un `OutputServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `OutputServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `OutputServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un PDF interactif.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le  PDF interactif.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du  PDF interactif.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Transformez le  PDF.

   Transformez le PDF interactif en PDF non interactif  en appelant la `OutputClient` `transformPDF` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le  PDF interactif.
   * Valeur  `TransformationFormat` . Pour générer un PDF non interactif, spécifiez `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` enum value that specifies the revision number.
   * Valeur booléenne qui spécifie si la valeur `PDFARevisionNumber` enum est utilisée. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `false`.
   * Valeur de chaîne qui représente le numéro de modification et l’année, séparés par un deux-points. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `null`.
   * Valeur d’ `PDFAConformance` énumération représentant le niveau de conformité PDF/A.
   * Valeur booléenne qui spécifie si la valeur `PDFAConformance` enum est utilisée. Ce paramètre étant destiné à un  PDF/A, vous pouvez spécifier `false`.
   La `transformPDF` méthode renvoie un `BLOB` objet contenant un PDF non interactif.

1. Enregistrez le  PDF non interactif au format PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du  PDF non interactif.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `transformPDF` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
