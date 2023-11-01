---
title: Créer des flux de sortie de document
description: Utilisez le service Output pour convertir des documents en PDF (y compris des documents PDF/A), PostScript, PCL (Printer Control Language) et Zebra - ZPL, Intermec - IPL, Datamax - DPL et TecToshiba - TPCL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '19006'
ht-degree: 83%

---

# Créer des flux de sortie de document  {#creating-document-output-streams}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Output**

Le service Output vous permet de générer des documents en PDF (y compris des documents PDF/A), PostScript, PCL (Printer Control Language), ainsi que les formats d’étiquettes suivants :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Le service Output vous permet de fusionner des données de formulaire XML avec une conception de formulaire et de générer le document sur une imprimante ou un fichier réseau.

Il existe deux façons de transmettre une conception de formulaire (un fichier XDP) au service Output. Vous pouvez transmettre une instance `com.adobe.idp.Document` qui contenant une conception de formulaire au service Output. Vous pouvez également transmettre une valeur URI qui spécifie l’emplacement de la conception de formulaire. Ces deux méthodes sont abordées dans *Programmation avec AEM forms*.

>[!NOTE]
>
>Le service Output ne prend pas en charge les documents PDF Acroform contenant des scripts spécifiques à un objet d’application. Les documents PDF Acroform contenant des scripts spécifiques à un objet d’application ne sont pas rendus.

Les sections suivantes expliquent comment transmettre une conception de formulaire au service Output à l’aide d’une valeur URI :

* [Créer des documents PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Créer des documents PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Les sections suivantes expliquent comment transmettre une conception de formulaire dans une instance `com.adobe.idp.Document` :

* [Transmettre des documents se trouvant dans Content Services (obsolète) au service Output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Créer des documents PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Lorsque vous décidez de la technique à utiliser, vous devez savoir si vous obtenez la conception de formulaire d’un autre service AEM Forms, puis vous la transmettez dans une instance `com.adobe.idp.Document`. Les sections *Transmettre des documents au service Output* et *Créer des documents PDF à l’aide de fragments* montrent comment obtenir une conception de formulaire à partir d’un autre service AEM Forms. La première section récupère la conception de formulaire à partir de Content Services (obsolète). La deuxième section récupère la conception de formulaire à partir du service Assembler.

Si vous obtenez la conception de formulaire à partir d’un emplacement fixe, tel que le système de fichiers, vous pouvez utiliser l’une ou l’autre des techniques. En d’autres termes, vous pouvez spécifier la valeur URI d’un fichier XDP ou utiliser une `com.adobe.idp.Document` instance.

Pour transmettre une valeur URI qui spécifie l’emplacement de la conception de formulaire lors de la création d’un document PDF, utilisez la méthode `generatePDFOutput`. De même, pour transmettre une instance `com.adobe.idp.Document` au service Output lors de la création d’un document PDF, utilisez la méthode `generatePDFOutput2`.

Pour envoyer un flux de sortie à une imprimante réseau, vous pouvez également utiliser l’une ou l’autre des techniques. Pour envoyer un flux de sortie à une imprimante en transmettant une instance `com.adobe.idp.Document` contenant une conception de formulaire, utilisez la méthode `sendToPrinter2`. Pour envoyer un flux de sortie à une imprimante en transmettant une valeur URI, utilisez la méthode `sendToPrinter`. La section *Envoyer des flux d’impression aux imprimantes* utilise la méthode `sendToPrinter`.

Vous pouvez accomplir ces tâches à l’aide du service Output :

* [Créer des documents PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Créer des documents PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Transmettre des documents se trouvant dans Content Services (obsolète) au service Output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Créer des documents PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Imprimer des fichiers](creating-document-output-streams.md#printing-to-files)
* [Envoyer des flux d’impression aux imprimantes](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Création de plusieurs fichiers Output](creating-document-output-streams.md#creating-multiple-output-files)
* [Créer des règles de recherche](creating-document-output-streams.md#creating-search-rules)
* [Aplatissement de documents PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Créer des documents PDF {#creating-pdf-documents}

Avec le service Output, vous pouvez créer un document PDF basé sur une conception de formulaire et des données de formulaire XML que vous fournissez. Le document PDF créé par le service Output n’est pas un document PDF interactif ; un utilisateur ne peut pas saisir ni modifier des données de formulaire.

Si vous souhaitez créer un document PDF destiné au stockage à long terme, il est recommandé de créer un document PDF/A. (Voir [Créer des documents PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Pour créer un formulaire PDF interactif qui permet à l’utilisateur de saisir des données, utilisez le service Forms. (Consultez la section [Restituer des PDF Forms interactifs](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)).

>[!NOTE]
>
>Pour plus d’informations sur le service Output, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour créer un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définissez les options d’exécution du PDF.
1. Définissez les options d’exécution de rendu.
1. Générez un document PDF.
1. Récupérer les résultats de l’opération.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un objet client Output**

Avant de pouvoir effectuer par programmation une opération du service Output, vous devez créer un objet client du service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API Output du service web, créez un objet `OutputServiceService`.

**Référencer une source de données XML**

Pour fusionner les données avec la conception de formulaire, vous devez référencer une source de données XML contenant des données. Un élément XML doit exister pour chaque champ de formulaire que vous prévoyez de renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il nʼest pas nécessaire de faire correspondre lʼordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

Examinez l’exemple de formulaire de demande de prêt suivant :

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Pour fusionner les données dans cette conception de formulaire, vous devez créer une source de données XML correspondant au formulaire. Le code XML suivant représente une source de données XML XDP correspondant à l’exemple de formulaire de demande de prêt immobilier.

```xml
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

**Définir les options d’exécution du PDF**

Définir l’option URI du fichier lors de la création d’un document PDF. Cette option spécifie le nom et l’emplacement du fichier PDF généré par le service Output.

>[!NOTE]
>
>Au lieu de définir l’option d’exécution URI du fichier, vous pouvez récupérer par programmation le document PDF à partir du type de données complexe renvoyé par le service Output. Toutefois, en définissant l’option d’exécution URI du fichier, vous n’avez pas besoin de créer une logique d’application qui récupère par programmation le document PDF.

**Définir les options d’exécution de rendu**

Vous pouvez définir des options d’exécution de rendu lors de la création d’un document PDF. Bien que ces options ne soient pas obligatoires (contrairement aux options d’exécution du PDF), vous pouvez effectuer des tâches telles que l’amélioration des performances du service Output. Par exemple, vous pouvez mettre en cache la conception de formulaire utilisée par le service Output pour améliorer ses performances.

Si vous utilisez un formulaire Acrobat balisé comme entrée, vous ne pouvez pas utiliser l’API Java Output Service ou lʼAPI de service web pour désactiver le paramètre balisé. Si vous tentez de définir cette option par programmation sur `false`, le document PDF généré est toujours balisé.

>[!NOTE]
>
>Si vous ne spécifiez pas d’options d’exécution de rendu, les valeurs par défaut sont utilisées. Pour plus d’informations sur le les options d’exécution de rendu, consultez la référence de classe `RenderOptionsSpec`. (Consultez la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Générer un document PDF**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini des options d’exécution, vous pouvez appeler le service Output et générer un document PDF.

Lors de la génération d’un document PDF, vous devez spécifier les valeurs URI requises par le service Output afin de créer un document PDF. Une conception de formulaire peut être stockée dans différents emplacements, tels que le système de fichiers du serveur ou au sein dʼune application AEM Forms. Une conception de formulaire (ou d’autres ressources telles qu’un fichier image) qui existe au sein dʼune application Forms peut être référencée à l’aide de la valeur URI de la racine du contenu `repository:///`. Prenons l’exemple suivant, consistant en une conception de formulaire nommée *Loan.xdp* située dans une application Forms nommée *Applications/FormsApplication* :

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Pour accéder au fichier Loan.xdp affiché dans l’illustration précédente, spécifiez `repository:///Applications/FormsApplication/1.0/FormsFolder/` comme troisième paramètre transmis à la variable `OutputClient` de `generatePDFOutput` . Indiquez le nom du formulaire (*Loan.xdp*) comme second paramètre transmis à la variable `OutputClient` de `generatePDFOutput` .

Si le fichier XDP contient des images (ou d’autres ressources telles que des fragments), placez les ressources dans le même dossier de l’application que le fichier XDP. AEM Forms utilise l’URI racine du contenu comme chemin d’accès de base pour résoudre les références aux images. Par exemple, si le fichier Loan.xdp contient une image, veillez à la placer dans le dossier `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Vous pouvez référencer un URI d’application Forms lors de l’appel de la fonction `OutputClient` de `generatePDFOutput` ou `generatePrintedOutput` méthodes.

>[!NOTE]
>
>Pour afficher un démarrage rapide complet qui crée un document de PDF en référençant un XDP situé dans une application Forms, reportez-vous à la section [Démarrage rapide (mode EJB) : création d’un document de PDF basé sur un fichier XDP d’application utilisant l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que les données XML de statut qui spécifient si l’opération a réussi.

**Voir également**

[Créer un document PDF à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Créer un document PDF à l’aide de l’API Web Service](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Créer un document PDF à l’aide de l’API Java {#create-a-pdf-document-using-the-java-api}

Créez un document PDF à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez une source de données XML.

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML utilisée pour remplir le document PDF en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur. Transmettez l’objet `java.io.FileInputStream`.

1. Définissez les options d’exécution du PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option File URI en appelant la méthode `PDFOutputOptionsSpec` de `setFileURI` . Transmettez une valeur string qui spécifie l’emplacement du fichier PDF généré par le service Output. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en appelant la fonction `RenderOptionsSpec` de `setCacheEnabled` et transmission `true`.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du document du PDF à l’aide du `RenderOptionsSpec` de `setPdfVersion` si le document d’entrée est un formulaire Acrobat (un formulaire créé dans Acrobat) ou un document XFA signé ou certifié. Le document PDF de sortie conserve la version originale du PDF. De même, vous ne pouvez pas définir l’option Adobe PDF balisée en appelant la variable `RenderOptionsSpec` de `setTaggedPDF` si le document d’entrée est un formulaire Acrobat ou un document XFA signé ou certifié.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option de PDF linéarisé à l’aide de la variable `RenderOptionsSpec` de `setLinearizedPDF` si le document input PDF est certifié ou signé numériquement. (Voir [Signature numérique de documents PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Générez un document PDF.

   Créez un document de PDF en appelant la méthode `OutputClient` de `generatePDFOutput` et transmission des valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput` renvoie un objet `OutputResult` contenant les résultats de l’authentification.

   >[!NOTE]
   >
   >Lors de la génération d’un document PDF en appelant la méthode `generatePDFOutput`, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé ou certifié. (Voir [Signature numérique et certification de documents ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >La variable `OutputResult` de `getRecordLevelMetaDataList` method renvoie `null`*.*

   >[!NOTE]
   >
   >Vous pouvez également créer un document de PDF en appelant la méthode `OutputClient` de `generatePDFOutput2` . (Voir [Transmettre des documents situés dans Content Services (obsolète) vers le service Output ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Récupérer les résultats de l’opération.

   * Récupération d’une `com.adobe.idp.Document` qui représente l’état de la propriété `generatePDFOutput` en appelant la fonction `OutputResult` de `getStatusDoc` . Cette méthode renvoie des données XML de statut qui spécifient si l’opération a réussi.
   * Créez un objet `java.io.File` contenant les résultats de l’opération. Assurez-vous que l’extension du nom du fichier est .xml.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getStatusDoc` ).

   Bien que le service Output écrive le document du PDF à l’emplacement spécifié par l’argument transmis à la variable `PDFOutputOptionsSpec` de `setFileURI` , vous pouvez récupérer le document PDF/A par programmation en appelant la méthode `OutputResult` de `getGeneratedDoc` .

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : créer un document PDF à l’aide de l’API Java.](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Didacticiel de mise en route (mode SOAP) : créer un document PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer un document PDF à l’aide de l’API Web Service {#create-a-pdf-document-using-the-web-service-api}

Créez un document PDF à l’aide de l’API Output (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker les données XML qui seront fusionnées avec le document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier XML contenant les données de formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Définir les options d’exécution du PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option File URI en attribuant une valeur string qui spécifie l’emplacement du fichier de PDF généré par le service Output à la variable `PDFOutputOptionsSpec` de `fileURI` membre de données. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettre en cache la conception de formulaire pour améliorer les performances du service Output en affectant la valeur `true` à la fonction `RenderOptionsSpec` de `cacheEnabled` membre de données.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du document du PDF à l’aide du `RenderOptionsSpec` de `setPdfVersion` si le document d’entrée est un formulaire Acrobat (un formulaire créé dans Acrobat) ou un document XFA signé ou certifié. Le document PDF de sortie conserve la version originale du PDF. De même, vous ne pouvez pas définir l’option Adobe PDF balisée en appelant la variable `RenderOptionsSpec` de `setTaggedPDF`* si le document d’entrée est un formulaire Acrobat ou un document XFA signé ou certifié.*

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option de PDF linéarisé à l’aide de la variable `RenderOptionsSpec` de `linearizedPDF` membre si le document input PDF est certifié ou signé numériquement. (Voir [Signature numérique de documents PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Générez un document PDF.

   Créez un document de PDF en appelant la méthode `OutputServiceService` de `generatePDFOutput`et transmission des valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` qui est renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

   >[!NOTE]
   >
   >Lorsque vous générez un document PDF en appelant la méthode `generatePDFOutput`, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé ou certifié. (Voir [Signature numérique et certification de documents ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Vous pouvez également créer un document de PDF en appelant la méthode `OutputClient` de `generatePDFOutput2` . (Voir [Transmettre des documents situés dans Content Services (obsolète) vers le service Output ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Récupérer les résultats de l’opération.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant un emplacement de fichier XML contenant les données de résultat. Assurez-vous que l’extension du nom du fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de la variable `BLOB` qui a été renseigné avec les données de résultat de l’objet `OutputServiceService` de `generatePDFOutput` (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` `field`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

   Voir également

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >La variable `OutputServiceService` de `generateOutput` est obsolète.

## Créer des documents PDF/A {#creating-pdf-a-documents}

Vous pouvez utiliser le service Output pour créer un document PDF/A. Comme PDF/A est un format d’archivage pour la conservation à long terme du contenu du document, toutes les polices sont incorporées et le fichier est décompressé. Par conséquent, un document PDF/A est généralement plus volumineux qu’un document PDF standard. En outre, un document PDF/A ne comporte pas de contenu vidéo ou audio. Comme pour les autres tâches du service Output, vous fournissez une conception de formulaire et des données à fusionner avec une conception de formulaire pour créer un document PDF/A.

La spécification PDF/A-1 comporte deux niveaux de conformité, à savoir a et b. La principale différence entre les deux se situe au niveau de la prise en charge de la structure logique (accessibilité), qui n’est pas requise pour le niveau de conformité b. Quel que soit le niveau de conformité, le PDF/A-1 exige que toutes les polices soient incorporées dans le document PDF/A généré.

Bien que PDF/A soit la norme d’archivage des documents de PDF, il n’est pas obligatoire que PDF/A soit utilisé pour l’archivage si un document de PDF standard répond aux besoins de votre entreprise. L’objectif du standard PDF/A est d’établir un fichier PDF qui peut être stocké pendant une longue période de temps et qui répond aux exigences de conservation des documents. Par exemple, une URL ne peut pas être incorporée dans un PDF/A car, avec le temps, l’URL peut devenir non valide.

Votre entreprise doit évaluer ses propres besoins, la durée pendant laquelle vous avez l’intention de conserver le document, les considérations relatives à la taille du fichier, et déterminer votre propre stratégie d’archivage. Vous pouvez déterminer par programmation si un document PDF est conforme au format PDF/A à l’aide du service DocConverter. (Voir [Déterminer par programmation la conformité au format PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Un document PDF/A doit utiliser la police qui est spécifiée dans la conception du formulaire et les polices ne peuvent pas être remplacées. Par conséquent, si une police située dans un document PDF n’est pas disponible sur le système d’exploitation hôte, une exception se produit.

Lorsqu’un document PDF/A est ouvert dans Acrobat, un message s’affiche pour confirmer que le document est un document PDF/A, comme illustré ci-dessous.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>Le site Web de l’AIIM comporte une section FAQ sur le PDF/A que vous pouvez consulter à l’adresse [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Références des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65_fr).

### Résumé des étapes {#summary_of_steps-1}

Pour créer un document PDF/A, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définissez les options d’exécution du PDF/A.
1. Définissez les options d’exécution de rendu.
1. Générez un document PDF/A.
1. Récupérer les résultats de l’opération.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application personnalisée à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un objet client Output**

Avant de pouvoir effectuer par programmation une opération du service Output, vous devez créer un objet client du service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API Output du service web, créez un objet `OutputServiceService`.

**Référencer une source de données XML**

Pour fusionner les données avec la conception de formulaire, vous devez référencer une source de données XML contenant des données. Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il nʼest pas nécessaire de faire correspondre lʼordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définir les options d’exécution du PDF/A**

Vous pouvez définir l’option URI du fichier lors de la création d’un document PDF/A. L’URI est relatif au serveur d’applications J2EE hébergeant AEM Forms. En d’autres termes, si vous définissez C:\Adobe, le fichier est écrit dans le dossier sur le serveur, et non sur l’ordinateur client. L’URI spécifie le nom et l’emplacement du fichier PDF/A généré par le service Output.

**Définir les options d’exécution du rendu**

Vous pouvez définir des options d’exécution de rendu lors de la création de documents PDF/A. Vous pouvez définir deux options associées à PDF/A : valeurs `PDFAConformance` et `PDFARevisionNumber`. La valeur `PDFAConformance` fait référence à la manière dont un document PDF respecte les exigences spécifiant la manière dont les documents électroniques à long terme sont conservés. Les valeurs valides de cette option sont `A` et `B`. Pour plus d’informations sur la conformité de niveaux a et b, voir la spécification ISO PDF/A-1 intitulée *ISO 19005-1 Gestion des documents*.

La valeur `PDFARevisionNumber` fait référence au numéro de révision d’un document PDF/A. Pour plus d’informations sur le numéro de révision d’un document PDF/A, voir la spécification ISO PDF/A-1 intitulée *ISO 19005-1 Gestion des documents*.

>[!NOTE]
>
>Vous ne pouvez pas définir l’option Adobe PDF balisée sur `false` lors de la création d’un document PDF/A 1A. PDF/A 1A sera toujours un document PDF balisé. En outre, vous ne pouvez pas définir l’option Adobe PDF balisée sur `true` lors de la création d’un document PDF/A 1B. PDF/A 1B sera toujours un document PDF non balisé.

**Générer un document de PDF/A**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini des options d’exécution, vous pouvez appeler le service Output, ce qui génère un document PDF/A.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que des données XML qui spécifient si l’opération a réussi.

**Voir également**

[Créer un document PDF/A à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Créer un document PDF/A à l’aide de l’API Web Service](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Créer un document PDF/A à l’aide de l’API Java {#create-a-pdf-a-document-using-the-java-api}

Créez un document PDF/A à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez une source de données XML.

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML utilisée pour remplir le document PDF/A en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution PDF/A.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option File URI en appelant la méthode `PDFOutputOptionsSpec` de `setFileURI` . Transmettez une valeur string qui spécifie l’emplacement du fichier PDF généré par le service Output. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Définissez la variable `PDFAConformance` en appelant la variable `RenderOptionsSpec` de `setPDFAConformance` et transmission d’une `PDFAConformance` valeur enum qui spécifie le niveau de conformité. Par exemple, pour spécifier le niveau de conformité A, transmettez `PDFAConformance.A`.
   * Définissez la variable `PDFARevisionNumber` en appelant la variable `RenderOptionsSpec` de `setPDFARevisionNumber` méthode et transmission `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >La version PDF d’un document PDF/A est 1.4, quelle que soit la valeur que vous spécifiez pour la variable `RenderOptionsSpec` de `setPdfVersion`*.*

1. Générez un document PDF/A.

   Créez un document de PDF/A en appelant la fonction `OutputClient` de `generatePDFOutput` et transmission des valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF/A, spécifiez `TransformationFormat.PDFA`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML où se trouvent les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput` renvoie un objet `OutputResult` contenant les résultats de l’authentification.

   >[!NOTE]
   >
   >La variable `OutputResult` de `getRecordLevelMetaDataList` method renvoie `null`.

   >[!NOTE]
   >
   >Vous pouvez également créer un document /A de PDF en appelant le `OutputClient` de `generatePDFOutput`méthode 2. (Voir [Transmettre des documents situés dans Content Services (obsolète) vers Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Récupérer les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` qui représente l’état de la propriété `generatePDFOutput` en appelant la méthode `OutputResult` de `getStatusDoc` .
   * Créez un objet `java.io.File` qui contient les résultats de l’opération. Assurez-vous que l’extension du nom du fichier est .xml.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getStatusDoc` ).

   >[!NOTE]
   >
   >Bien que le service Output écrive le document PDF/A à l’emplacement spécifié par l’argument transmis à la variable `PDFOutputOptionsSpec` de `setFileURI` , vous pouvez récupérer le document PDF/A par programmation en appelant la méthode `OutputResult` de `getGeneratedDoc` .

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : créer un document PDF/A à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Créer un document PDF/A à l’aide de l’API Web Service {#create-a-pdf-a-document-using-the-web-service-api}

Créez un document PDF/A à l’aide de l’API Output (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker les données qui seront fusionnées avec le document PDF/A.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution du PDF/A.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option File URI en attribuant une valeur string qui spécifie l’emplacement du fichier de PDF généré par le service Output à la variable `PDFOutputOptionsSpec` de `fileURI` membre de données. L’option URI du fichier est relative au serveur d’applications J2EE hébergeant AEM Forms, et non à l’ordinateur client.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Définissez la variable `PDFAConformance` en affectant une `PDFAConformance` Enum value to the `RenderOptionsSpec` de `PDFAConformance` membre de données. Par exemple, pour spécifier le niveau de conformité A, affectez `PDFAConformance.A` à ce membre de données.
   * Définissez la variable `PDFARevisionNumber` en affectant une `PDFARevisionNumber` Enum value to the `RenderOptionsSpec` de `PDFARevisionNumber` membre de données. Affectez `PDFARevisionNumber.Revision_1` à ce membre de données.

   >[!NOTE]
   >
   >La version PDF d’un document PDF/A est 1.4, quelle que soit la valeur que vous indiquez.

1. Générez un document PDF/A.

   Créez un document de PDF en appelant la méthode `OutputServiceService` de `generatePDFOutput`et transmission des valeurs suivantes :

   * Valeur d’énumération TransformationFormat. Pour générer un document PDF, spécifiez `TransformationFormat.PDFA`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` qui est renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)

   >[!NOTE]
   >
   >Vous pouvez également créer un document /A de PDF en appelant le `OutputClient` de `generatePDFOutput`méthode 2. (Voir [Transmettre des documents situés dans Content Services (obsolète) vers Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Récupérer les résultats de l’opération.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant un emplacement de fichier XML contenant les données de résultat. Assurez-vous que l’extension du nom du fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de la variable `BLOB` qui a été renseigné avec les données de résultat de l’objet `OutputServiceService` de `generatePDFOutput` (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` champ .
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Transmettre des documents se trouvant dans Content Services (obsolète) au service Output {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Le service Output génère un formulaire PDF non interactif basé sur une conception de formulaire généralement enregistrée en tant que fichier XDP et créée dans Designer. Vous pouvez transmettre un objet `com.adobe.idp.Document` contenant la conception de formulaire au service Output. Le service Output effectue ensuite le rendu de la conception de formulaire se trouvant dans l’objet `com.adobe.idp.Document`.

L’un des avantages de transmettre un objet `com.adobe.idp.Document` au service Output est que d’autres opérations du service AEM Forms renvoient une instance `com.adobe.idp.Document`. En d’autres termes, vous pouvez obtenir une instance `com.adobe.idp.Document` à partir d’une autre opération de service et en effectuer le rendu. Supposons, par exemple, qu’un fichier XDP soit stocké dans un nœud Content Services (obsolète) nommé `/Company Home/Form Designs`, comme illustré ci-dessous.

Vous pouvez récupérer Loan.xdp par programmation à partir de Content Services (obsolète) et transmettre le fichier XDP au service Output dans un objet `com.adobe.idp.Document`.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour transmettre un document obtenu à partir de Content Services (obsolète) au service Output, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet d’API Output et Document Management Client.
1. Récupérez la conception de formulaire auprès de Content Services (obsolète).
1. Générez le formulaire PDF non interactif.
1. Exécutez une action avec le flux de données.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires au projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer une sortie et un objet API client Document Management**

Avant d’effectuer par programmation une opération d’API Output Service, créez un objet API Output Client. En outre, comme ce workflow récupère un fichier XDP de Content Services (obsolète), créez un objet API Document Management.

**Récupérer la conception de formulaire à partir de Content Services (obsolète)**

Récupérez le fichier XDP à partir de Content Services (obsolète) à l’aide de l’API Java ou de service web. Le fichier XDP est renvoyé dans une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services web). Vous pouvez ensuite transmettre l’instance `com.adobe.idp.Document` au service Output.

**Rendu du formulaire PDF non interactif**

Pour effectuer le rendu d’un formulaire non interactif, transmettez l’instance `com.adobe.idp.Document` renvoyée de Content Services (obsolète) au service Output.

>[!NOTE]
>
>Deux nouvelles méthodes nommées `generatePDFOutput2` et `eneratePrintedOutput2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire. Vous pouvez également transmettre un `com.adobe.idp.Document` qui contient la conception de formulaire au service Output lors de l’envoi d’un flux d’impression vers une imprimante réseau.

**Exécuter une action avec le flux de données de formulaire**

Vous pouvez enregistrer le formulaire non interactif en tant que fichier PDF. Le formulaire peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Transmettre des documents au service Output à l’aide de l’API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Transmettre des documents au service Output à l’aide de l’API Web Service](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Créer des documents PDF à l’aide de fragments](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Transmettre des documents au service Output à l’aide de l’API Java {#pass-documents-to-the-output-service-using-the-java-api}

Transmettez un document récupéré de Content Services (obsolète) à l’aide du service Output et de l’API Content Services (obsolète) (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar et adobe-contentservices-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet d’API Output et Document Management Client.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez la conception de formulaire auprès de Content Services (obsolète).

   Appeler la variable `DocumentManagementServiceClientImpl` de `retrieveContent` et transmettez les valeurs suivantes :

   * Valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.

   La méthode `retrieveContent` renvoie un objet `CRCResult` contenant le fichier XDP. Récupération d’une `com.adobe.idp.Document` en appelant la méthode `CRCResult` de `getDocument` .

1. Générez le formulaire PDF non interactif.

   Appeler la variable `OutputClient` de `generatePDFOutput2` et transmettez les valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez le `TransformationFormat.PDF`.
   * Valeur string qui spécifie la racine de contenu où se trouvent les ressources supplémentaires telles que les images.
   * A `com.adobe.idp.Document` qui représente la conception de formulaire (utilisez l’instance renvoyée par le `CRCResult` de `getDocument` ).
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput2` renvoie un objet `OutputResult` contenant les résultats de l’authentification.

1. Exécutez une action avec le flux de données de formulaire.

   * Récupération d’une `com.adobe.idp.Document` qui représente le formulaire non interactif en appelant la fonction `OutputResult` de `getGeneratedDoc` .
   * Créez un objet `java.io.File` contenant les résultats de l’opération. Assurez-vous que l’extension de nom de fichier est .pdf.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getGeneratedDoc` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : transmettre des documents au service Output à l’aide de l’API Java.](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Démarrage rapide (mode SOAP) : transmission de documents vers le service Output à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Transmettre des documents au service Output à l’aide de l’API Web Service {#pass-documents-to-the-output-service-using-the-web-service-api}

Transmettez un document récupéré de Content Services (obsolète) à l’aide du service Output et de l’API (service web) Content Services (obsolète) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Étant donné que cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Output : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Document Management : `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Étant donné que le type de données `BLOB` est commun aux deux références de service, il qualifie entièrement le type de données `BLOB` lors de son utilisation. Dans le démarrage rapide du service web correspondant, toutes les instances `BLOB` sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet d’API Output et Document Management Client.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour le client de service `DocumentManagementServiceClient`.

1. Récupérez la conception de formulaire auprès de Content Services (obsolète).

   Récupération du contenu en appelant la méthode `DocumentManagementServiceClient` de `retrieveContent` et transmission des valeurs suivantes :

   * Valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   * Paramètre de sortie string qui stocke la valeur du lien de navigation.
   * Paramètre de sortie `BLOB` stockant le contenu. Vous pouvez utiliser ce paramètre de sortie pour récupérer le contenu.
   * Paramètre de sortie `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` stockant les attributs de contenu.
   * Paramètre de sortie `CRCResult`. Au lieu d’utiliser cet objet, vous pouvez utiliser le paramètre de sortie `BLOB` pour récupérer le contenu.

1. Générez le formulaire PDF non interactif.

   Appeler la variable `OutputServiceClient` de `generatePDFOutput2` et transmettez les valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez le `TransformationFormat.PDF`.
   * Valeur string qui spécifie la racine de contenu où se trouvent les ressources supplémentaires telles que les images.
   * Objet `BLOB` représentant la conception de formulaire (utilisez l’instance `BLOB` renvoyée par Content Services (obsolète)).
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` de sortie qui est renseigné par la méthode `generatePDFOutput2`. La méthode `generatePDFOutput2` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Un objet `OutputResult` de sortie contenant les résultats de l’opération. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

   La méthode `generatePDFOutput2` renvoie un objet `BLOB` contenant le formulaire PDF non interactif.

1. Exécutez une action avec le flux de données de formulaire.

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` récupéré à partir de la méthode `generatePDFOutput2`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Transmettre des documents situés dans le référentiel vers le service Output {#passing-documents-located-in-the-repository-to-the-output-service}

Le service Output génère un formulaire PDF non interactif basé sur une conception de formulaire généralement enregistrée en tant que fichier XDP et créée dans Designer. Vous pouvez transmettre un objet `com.adobe.idp.Document` contenant la conception de formulaire au service Output. Le service Output effectue ensuite le rendu de la conception de formulaire se trouvant dans l’objet `com.adobe.idp.Document`.

L’un des avantages de transmettre un objet `com.adobe.idp.Document` au service Output est que d’autres opérations du service AEM Forms renvoient une instance `com.adobe.idp.Document`. C’est-à-dire que vous pouvez obtenir une instance `com.adobe.idp.Document` à partir d’une autre opération de service et en effectuer le rendu. Supposons, par exemple, qu’un fichier XDP soit stocké dans le référentiel AEM Forms, comme illustré ci-dessous.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

Le dossier *FormsFolder* est un emplacement défini par l’utilisateur dans le référentiel AEM Forms (cet emplacement est un exemple et n’existe pas par défaut). Dans cet exemple, une conception de formulaire nommée Loan.xdp se trouve dans ce dossier. Outre la conception de formulaire, d’autres documents de formulaire, tels que des images, peuvent être stockés à cet emplacement. Le chemin d’accès à une ressource située dans le référentiel AEM Forms est le suivant :

`Applications/Application-name/Application-version/Folder.../Filename`

Vous pouvez récupérer Loan.xdp par programmation à partir du référentiel AEM Forms et le transmettre au service Output dans un objet `com.adobe.idp.Document`.

Vous pouvez créer un PDF à partir d’un fichier XDP situé dans le référentiel de l’une des deux façons suivantes. Vous pouvez transmettre l’emplacement XDP par référence ou récupérer par programmation le XDP à partir du référentiel et le transmettre au service Output dans un fichier XDP.

[Démarrage rapide (mode EJB) : créer un document PDF basé sur un fichier XDP d’application à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (indique comment transmettre l’emplacement du fichier XDP par référence).

[Démarrage rapide (mode EJB) : transmettre un document situé dans le référentiel AEM Forms au service Output à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (indique comment récupérer le fichier XDP par programmation à partir du référentiel AEM Forms et le transmettre au service Output dans une instance `com.adobe.idp.Document`). (Cette section explique comment effectuer cette tâche.)

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-3}

Pour transmettre un document obtenu du référentiel AEM Forms au service Output, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet d’API Output et Document Management Client.
1. Récupérez la conception de formulaire à partir du référentiel AEM Forms.
1. Générez le formulaire PDF non interactif.
1. Exécutez une action avec le flux de données.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires au projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer une sortie et un objet API client Document Management**

Avant d’effectuer par programmation une opération d’API Output Service, créez un objet API Output Client. En outre, comme ce workflow récupère un fichier XDP de Content Services (obsolète), créez un objet API Document Management.

**Récupérer la conception de formulaire à partir du référentiel AEM Forms**

Récupérez le fichier XDP à partir du référentiel AEM Forms à l’aide de l’API Repository. (Voir [Lire les ressources](/help/forms/developing/aem-forms-repository.md#reading-resources).)

Le fichier XDP est renvoyé dans une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services web). Vous pouvez ensuite transmettre l’instance `com.adobe.idp.Document` au service Output.

**Rendu du formulaire PDF non interactif**

Pour effectuer le rendu d’un formulaire non interactif, transmettez l’instance `com.adobe.idp.Document` renvoyée à l’aide de l’API Repository AEM Forms.

>[!NOTE]
>
>Deux nouvelles méthodes nommées `generatePDFOutput2` et `generatePrintedOutput2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire. Vous pouvez également transmettre un `com.adobe.idp.Document` qui contient la conception de formulaire au service Output lors de l’envoi d’un flux d’impression vers une imprimante réseau.

**Exécuter une action avec le flux de données de formulaire**

Vous pouvez enregistrer le formulaire non interactif en tant que fichier PDF. Le formulaire peut être affiché dans Adobe Reader ou Acrobat.

**Voir également**

[Transmettre des documents situés dans le référentiel au service Output à l’aide de l’API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Transmettre des documents situés dans le référentiel au service Output à l’aide de l’API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Transmettez un document récupéré du référentiel à l’aide de l’API Repository et de l’API Output Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar et adobe-repository-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet d’API Output et Document Management Client.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez la conception de formulaire à partir du référentiel AEM Forms.

   Appeler la variable `ResourceRepositoryClient` de `readResourceContent` et transmettez une valeur string qui spécifie l’emplacement URI au fichier XDP. Par exemple, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Cette valeur n’est pas obligatoire. Cette méthode renvoie une instance `com.adobe.idp.Document` qui représente le fichier XDP.

1. Générez le formulaire PDF non interactif.

   Appeler la variable `OutputClient` de `generatePDFOutput2` et transmettez les valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string qui spécifie la racine de contenu où se trouvent les ressources supplémentaires telles que les images. Par exemple, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * A `com.adobe.idp.Document` qui représente la conception de formulaire (utilisez l’instance renvoyée par le `ResourceRepositoryClient` de `readResourceContent` ).
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput2` renvoie un objet `OutputResult` contenant les résultats de l’authentification.

1. Exécutez une action avec le flux de données de formulaire.

   * Récupération d’une `com.adobe.idp.Document` qui représente le formulaire non interactif en appelant la fonction `OutputResult` de `getGeneratedDoc` .
   * Créez un objet `java.io.File` contenant les résultats de l’opération. Assurez-vous que l’extension de nom de fichier est .pdf.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getGeneratedDoc` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : transmettre un document situé dans le référentiel AEM Forms au service Output à l’aide de l’API Java.](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Créer des documents PDF à l’aide de fragments {#creating-pdf-documents-using-fragments}

Vous pouvez utiliser les services Output et Assembler pour créer un flux de sortie, tel qu’un document PDF, basé sur des fragments. Le service Assembler assemble un document XDP basé sur des fragments situés dans plusieurs fichiers XDP. Le document XDP assemblé est transmis au service Output, ce qui crée un document PDF. Bien que ce workflow affiche un document PDF en cours de génération, le service Output peut générer d’autres types de sortie, tels que ZPL, pour ce workflow. Un document PDF est utilisé à des fins de discussion uniquement.

L’illustration suivante présente ce workflow.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Avant de lire *Créer des documents PDF à l’aide de fragments*, il est recommandé de vous familiariser avec l’utilisation du service Assembler pour assembler plusieurs documents XDP. (Voir [Assembler plusieurs fragments XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>Vous pouvez également transmettre une conception de formulaire assemblée par le service Assembler au service Forms au lieu du service Output. La principale différence entre le service Output et le service Forms réside dans le fait que le service Forms génère des documents PDF interactifs et le service Output génère des documents PDF non interactifs. De plus, le service Forms ne peut pas générer de flux de sortie basés sur des imprimantes comme ZPL.

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-4}

Pour créer un document PDF basé sur des fragments, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output et Assembler.
1. Utilisez le service Assembler pour générer la conception de formulaire.
1. Utilisez le service Output pour générer le document PDF.
1. Enregistrez le document PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un objet client Output et Assembler**

Avant d’effectuer par programmation une opération d’API Output Service, créez un objet API Output Client. En outre, comme ce workflow appelle le service Assembler pour créer la conception de formulaire, créez un objet API Assembler Client.

**Utiliser le service Assembler pour générer la conception de formulaire**

Utilisez le service Assembler pour générer la conception de formulaire à l’aide de fragments. Le service Assembler renvoie une instance `com.adobe.idp.Document` qui contient la conception de formulaire.

**Utiliser le service Output pour générer le document PDF**

Vous pouvez utiliser le service Output pour générer un document PDF à l’aide de la conception de formulaire créée par le service Assembler. Transmettez l’instance `com.adobe.idp.Document` que le service Assembler a renvoyée au service Output.

**Enregistrer le document PDF en tant que fichier PDF**

Une fois que le service Output a généré un document PDF, vous pouvez l’enregistrer en tant que fichier PDF.

**Voir également**

[Créer un document PDF basé sur des fragments à l’aide de l’API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Créer un document PDF basé sur des fragments à l’aide de l’API Web Service](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Assembler plusieurs fragments XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Créer des documents PDF](creating-document-output-streams.md#creating-pdf-documents)

### Créer un document PDF basé sur des fragments à l’aide de l’API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Créez un document PDF basé sur des fragments à l’aide de l’API Output Service et de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output et Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Utilisez le service Assembler pour générer la conception de formulaire.

   Appeler la variable `AssemblerServiceClient` de `invokeDDX` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser.
   * Objet `java.util.Map` contenant les fichiers XDP d’entrée.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le document XDP assemblé. Pour récupérer le document XDP assemblé, effectuez les actions suivantes :

   * Appeler la variable `AssemblerResult` de `getDocuments` . Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération à l’aide de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour extraire le document XDP assemblé.

1. Utilisez le service Output pour générer le document PDF.

   Appeler la variable `OutputClient` de `generatePDFOutput2` et transmettez les valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string qui spécifie la racine de contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `com.adobe.idp.Document` représentant la conception de formulaire (utilisez l’instance renvoyée par le service Assembler).
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput2` renvoie un objet `OutputResult` contenant les résultats de l’authentification.

1. Enregistrez le document PDF au format PDF.

   * Récupération d’une `com.adobe.idp.Document` qui représente le document du PDF en appelant la fonction `OutputResult` de `getGeneratedDoc` .
   * Créez un objet `java.io.File` contenant les résultats de l’opération. Assurez-vous que l’extension de nom de fichier est .pdf.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` vers le fichier . (Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` renvoyé par la méthode `getGeneratedDoc`).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : créer un document PDF basé sur des fragments à l’aide de l’API Java.](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Démarrage rapide (mode SOAP) : créer un document PDF basé sur des fragments à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Créer un document PDF basé sur des fragments à l’aide de l’API Web Service {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Créez un document PDF basé sur des fragments à l’aide de l’API Output Service et de l’API Assembler Service (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Utilisez la définition WSDL suivante pour la référence de service associée au service Output :

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilisez la définition WSDL suivante pour la référence de service associée au service Assembler :

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Parce que le type de données `BLOB` est commun aux deux références de service, qualifiez entièrement le type de données `BLOB` lors de son utilisation. Dans le démarrage rapide du service web correspondant, toutes les instances `BLOB` sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output et Assembler.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Affectez le nom d’utilisateur AEM Forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Affectez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour l’objet `AssemblerServiceClient`.

1. Utilisez le service Assembler pour générer la conception de formulaire.

   Appeler la variable `AssemblerServiceClient` de `invokeDDX` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions survenues. Pour obtenir le document XDP nouvellement créé, effectuez les actions suivantes :

   * Accédez au `AssemblerResult` de `documents` , qui est un `Map` contenant les documents de PDF générés.
   * Effectuez une itération à l’aide de l’objet `Map` pour récupérer la conception de formulaire assemblée. Construire le de ce membre du tableau `value` à `BLOB`. Transmettez l’instance `BLOB` au service Output.

1. Utilisez le service Output pour générer le document PDF.

   Appeler la variable `OutputServiceClient` de `generatePDFOutput2` et transmettez les valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string qui spécifie la racine de contenu où se trouvent les ressources supplémentaires, telles que les images.
   * Objet `BLOB` représentant la conception de formulaire (utilisez l’instance `BLOB` renvoyée par le service Assembler).
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` de sortie renseigné par la méthode `generatePDFOutput2`. La méthode `generatePDFOutput2` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Un objet `OutputResult` de sortie contenant les résultats de l’opération. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

   La méthode `generatePDFOutput2` renvoie un objet `BLOB` contenant le formulaire PDF non interactif.

1. Enregistrez le document PDF au format PDF.

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` récupéré à partir de la méthode `generatePDFOutput2`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Imprimer des fichiers {#printing-to-files}

Vous pouvez utiliser le service Output pour imprimer des flux tels que PostScript, PCL (Printer Control Language) ou les formats de libellé suivants dans un fichier :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Le service Output vous permet de fusionner des données XML avec une conception de formulaire et d’imprimer le formulaire dans un fichier. L’illustration suivante présente le service Output créant des fichiers laser et de libellés.

>[!NOTE]
>
>Pour plus d’informations sur l’envoi de diffusions d’impression vers des imprimantes, voir [Envoyer des flux d’impression aux imprimantes](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-5}

Pour imprimer sur un fichier, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définissez les options d’exécution d’impression requises pour l’impression dans un fichier.
1. Imprimer le flux d’impression dans un fichier.
1. Récupérer les résultats de l’opération.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. (Voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Créer un objet client de sortie**

Avant de pouvoir effectuer par programmation une opération du service Output, vous devez créer un objet client du service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API Output du service web, créez un objet `OutputServiceService`.

**Référencer une source de données XML**

Pour imprimer un document contenant des données, vous devez référencer une source de données XML contenant des éléments XML pour chaque champ de formulaire à remplir avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il nʼest pas nécessaire de faire correspondre lʼordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définir les options d’exécution d’impression requises pour l’impression dans un fichier**

Pour imprimer dans un fichier, vous devez définir l’option d’exécution URI du fichier en spécifiant l’emplacement et le nom du fichier dans lequel le service Output imprime. Par exemple, pour demander au service Output d’imprimer un fichier PostScript nommé *MortgageForm.ps* dans C:\Adobe, indiquez C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Vous avez la possibilité de définir des options d’exécution facultatives. Pour plus d’informations sur toutes les options que vous pouvez définir, consultez la référence de classe `PrintedOutputOptionsSpec` dans la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Imprimer le flux d’impression dans un fichier**

Après avoir référencé une source de données XML valide contenant des données de formulaire et défini les options d’exécution de l’impression, vous pouvez appeler le service Output, ce qui entraîne l’impression d’un fichier.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie divers éléments de données, tels que des données XML, qui indiquent si l’opération a réussi ou non.

**Voir également**

[Imprimer dans des fichiers à l’aide de l’API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimer dans des fichiers à l’aide de l’API de service web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimer dans des fichiers à l’aide de l’API Java {#print-to-files-using-the-java-api}

Imprimer dans un fichier à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez une source de données XML.

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML utilisée pour renseigner le document en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution d’impression requises pour l’impression dans un fichier.

   * Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur.
   * Spécifiez le fichier en appelant l’objet PrintedOutputOptionsSpec `setFileURI` et transmettre une valeur string qui représente le nom et l’emplacement du fichier. Par exemple, si vous souhaitez que le service Output imprime dans un fichier PostScript nommé MortgageForm.ps, situé dans C:\Adobe, indiquez le chemin C:\\Adobe\MortgageForm.ps.
   * Indiquez le nombre de copies à imprimer en appelant la fonction `PrintedOutputOptionsSpec` de `setCopies` et transmettre une valeur entière représentant le nombre de copies.

1. Imprimer le flux d’impression dans un fichier.

   Imprimer dans un fichier en appelant le `OutputClient` de `generatePrintedOutput` et transmission des valeurs suivantes :

   * Une valeur d’énumération `PrintFormat` qui spécifie le format du flux d’impression à créer. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie l’emplacement des fichiers associés, tels que les fichiers image.
   * Une valeur de chaîne qui spécifie l’emplacement du fichier XDC à utiliser (vous pouvez transmettre `null` si vous avez spécifié le fichier XDC à utiliser à l’aide de lʼobjet `PrintedOutputOptionsSpec`).
   * Lʼobjet `PrintedOutputOptionsSpec` contenant les options d’exécution requises pour l’impression dans un fichier.
   * Lʼobjet `com.adobe.idp.Document` contenant la source de données XML qui contient les données de formulaire.

   La méthode `generatePrintedOutput` renvoie un objet `OutputResult` contenant les résultats de l’opération.

   >[!NOTE]
   >
   >La variable `OutputResult` de `getRecordLevelMetaDataList` method renvoie `null`.

1. Récupérer les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` qui représente l’état de la propriété `generatePrintedOutput` en appelant la méthode `OutputResult` de `getStatusDoc` (la méthode `OutputResult` a été renvoyé par la fonction `generatePrintedOutput` ).
   * Créez un objet `java.io.File` qui contiendra les résultats de l’opération. Assurez-vous que l’extension de fichier est XML.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getStatusDoc` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : imprimer dans un fichier à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Imprimer dans des fichiers à l’aide de l’API de service web {#print-to-files-using-the-web-service-api}

Imprimez dans un fichier à l’aide de l’API Output (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker des données de formulaire.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier XML contenant les données de formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `binaryData` le contenu du tableau d’octets.

1. Définissez les options d’exécution d’impression requises pour l’impression dans un fichier.

   * Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur.
   * Spécifiez le fichier en attribuant une valeur string qui représente l’emplacement et le nom du fichier au `PrintedOutputOptionsSpec` de `fileURI` membre de données. Par exemple, si vous souhaitez que le service Output imprime un fichier PostScript appelé *MortgageForm.ps* situé dans C:\Adobe, indiquez C:\\Adobe\MortgageForm.ps.
   * Indiquez le nombre de copies à imprimer en attribuant une valeur entière qui représente le nombre de copies au `PrintedOutputOptionsSpec` de `copies` membres des données.

1. Imprimer le flux d’impression dans un fichier.

   Imprimer dans un fichier en appelant le `OutputServiceService` de `generatePrintedOutput` et transmission des valeurs suivantes :

   * Une valeur d’énumération `PrintFormat` qui spécifie le format du flux d’impression à créer. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie l’emplacement des fichiers associés, tels que les fichiers image.
   * Une valeur de chaîne qui spécifie l’emplacement du fichier XDC à utiliser (vous pouvez transmettre `null` si vous avez spécifié le fichier XDC à utiliser à l’aide de l’objet `PrintedOutputOptionsSpec`).
   * Objet `PrintedOutputOptionsSpec` qui contient les options d’exécution de l’impression requises pour imprimer un fichier.
   * Objet `BLOB` qui contient la source de données XML contenant les données du formulaire.
   * Un objet `BLOB` est renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)

1. Récupérer les résultats de l’opération.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant les données de résultat. Assurez-vous que l’extension de fichier est XML.
   * Créez un tableau d’octets qui stocke le contenu des données de la variable `BLOB` qui a été renseigné avec les données de résultat de l’objet `OutputServiceService` de `generatePDFOutput` (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Envoyer des flux d’impression aux imprimantes {#sending-print-streams-to-printers}

Vous pouvez utiliser le service Output pour envoyer des flux d’impression tels que PostScript, PCL (Printer Control Language) ou les formats d’étiquettes suivants à des imprimantes réseau :

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

À l’aide du service Output, vous pouvez fusionner des données XML avec une conception de formulaire et générer le formulaire sous forme de flux d’impression. Par exemple, vous pouvez créer un flux d’impression PostScript et l’envoyer à une imprimante réseau. L’illustration suivante montre le service Output envoyant des flux d’impression à des imprimantes réseau.

>[!NOTE]
>
>Pour démontrer comment envoyer un flux d’impression à une imprimante réseau, cette section envoie un flux d’impression PostScript à une imprimante réseau en utilisant le protocole d’imprimante SharedPrinter.

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-6}

Pour envoyer un flux d’impression à une imprimante réseau, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définir les options d’exécution de l’impression
1. Récupérez un document à imprimer.
1. Envoyez le document à une imprimante réseau.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un objet client Output**

Avant de pouvoir effectuer une opération du service Output par programmation, créez un objet client de service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API Output du service web, créez un objet `OutputServiceClient`.

**Référencer une source de données XML**

Pour imprimer un document contenant des données, vous devez référencer une source de données XML contenant des éléments XML pour chaque champ de formulaire à remplir avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il nʼest pas nécessaire de faire correspondre lʼordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définir les options d’exécution de l’impression**

Vous pouvez définir les options d’exécution lors de l’envoi d’un flux d’impression à une imprimante, notamment les options suivantes :

* **Copies :** indique le nombre de copies à envoyer à l’imprimante. La valeur par défaut est 1.
* **Agrafage :** une option XCI est définie lorsqu’une agrafeuse est utilisée. Cette option peut être spécifiée dans le modèle de configuration par l’élément staple (agrafage) et est utilisée uniquement pour les imprimantes PS et PCL.
* **OutputJog :** une option XCI est définie lorsque les pages de sortie doivent être déplacées (physiquement décalées dans le bac de sortie). Cette option est utilisée uniquement pour les imprimantes PS et PCL.
* **OutputBin :** valeur XCI qui permet au pilote d’impression de sélectionner le bac de sortie approprié.

>[!NOTE]
>
>Pour plus d’informations sur toutes les options d’exécution que vous pouvez définir, consultez la référence de la classe `PrintedOutputOptionsSpec`.

**Récupérer un document à imprimer**

Récupérez un flux d’impression à envoyer à une imprimante. Par exemple, vous pouvez récupérer un fichier PostScript et l’envoyer à une imprimante.

Vous pouvez choisir d’envoyer un fichier PDF si votre imprimante prend en charge le format PDF. Cependant, l’envoi d’un document PDF à une imprimante pose un problème : chaque fabricant d’imprimante dispose d’une implémentation différente de l’interpréteur PDF. Autrement dit, certains fabricants d’imprimantes utilisent l’interprétation Adobe PDF, mais cela dépend de l’imprimante. D’autres imprimantes ont leur propre interpréteur PDF. Par conséquent, les résultats d’impression peuvent varier.

Une autre limitation de l’envoi d’un document PDF à une imprimante est qu’il ne fait qu’imprimer. Il ne peut pas accéder aux options recto verso, à la sélection du bac à papier et à l’agrafage, sauf par le biais des paramètres de l’imprimante.

Pour récupérer un document à imprimer, vous utilisez la méthode `generatePrintedOutput`. Le tableau suivant indique les types de contenu qui sont définis pour un flux d’impression donné lorsque vous utilisez la méthode `generatePrintedOutput`.

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
   <td><p>Crée un flux de sortie dpl203.xdc par défaut ou un flux de sortie xdc personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>Crée un flux de sortie DPL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crée un flux de sortie Generic Color PCL (5c).</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crée un flux de sortie Generic PostScript niveau 3.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crée un flux de sortie IPL personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie IPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>Crée un flux de sortie IPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crée un flux de sortie Generic Monochrome PCL (5e).</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crée un flux de sortie Generic PostScript niveau 2.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crée un flux de sortie TPCL personnalisé.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>Crée un flux de sortie TPCL 305 DPI.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>Crée un flux de sortie TPCL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crée un flux de sortie ZPL 203 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>Crée un flux de sortie ZPL 300 DPI.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez également envoyer un flux d’impression à une imprimante à l’aide de la méthode `generatePrintedOutput2`. Toutefois, les démarrages rapides associés à la section Envoi de flux d’impression à des imprimantes utilisent la méthode `generatePrintedOutput`.

**Envoyer le flux d’impression vers une imprimante réseau**

Après avoir récupéré un document à imprimer, vous pouvez appeler le service Output, ce qui entraîne l’envoi d’un flux d’impression vers une imprimante réseau. Pour que le service Output localise correctement l’imprimante, vous devez spécifier le serveur d’impression et le nom de l’imprimante. En outre, vous devez également spécifier le protocole d’impression.

>[!NOTE]
>
>Si PDFG est installé sur le serveur Forms et que le serveur s’exécute sur Windows Server 2008, vous ne pouvez pas utiliser la propriété SharedPrinter. Dans ce cas, utilisez un protocole d’imprimante différent.

>[!NOTE]
>
>Si vous utilisez une imprimante réseau et que le mécanisme d’accès est SharedPrinter, vous devez spécifier le chemin réseau complet de l’imprimante. Envoyez un flux d’impression vers une imprimante réseau à l’aide de l’API Java.

Envoyez un flux d’impression à une imprimante réseau à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créer un objet client de sortie

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencer une source de données XML

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML utilisée pour remplir le document en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir les options d’exécution de l’impression

   Créez un objet `PrintedOutputOptionsSpec` qui représente les options d’exécution d’impression. Par exemple, vous pouvez spécifier le nombre de copies à imprimer en appelant la variable `PrintedOutputOptionsSpec` de `setCopies` .

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la valeur de pagination en utilisant la variable `PrintedOutputOptionsSpec` de `setPagination` si vous générez un flux d’impression ZPL. De même, vous ne pouvez pas définir les options suivantes pour un flux d’impression ZPL : OutputJog, PageOffset et Staple. La méthode `setPagination` n’est pas valide pour la génération PostScript. Il est valide uniquement pour la génération PCL.

1. Récupérer un document à imprimer

   * Récupération d’un document à imprimer en appelant la fonction `OutputClient` de `generatePrintedOutput` et transmission des valeurs suivantes :

      * Valeur d’énumération `PrintFormat` spécifiant le flux d’impression. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
      * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
      * Valeur de chaîne qui spécifie l’emplacement des fichiers collatéraux associés, tels que les fichiers image.
      * Valeur de chaîne qui spécifie l’emplacement du fichier XDC à utiliser.
      * Objet `PrintedOutputOptionsSpec` contenant les options d’exécution requises pour être imprimé dans un fichier.
      * Objet `com.adobe.idp.Document` représentant la source de données XML qui contient les données de formulaire à fusionner avec la conception de formulaire.

     Cette méthode renvoie un objet `OutputResult` contenant les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` à envoyer à l’imprimante en appelant la méthode `OutputResult` object’s `getGeneratedDoc` . Cette méthode renvoie un objet `com.adobe.idp.Document`.

1. Envoyer le flux d’impression vers une imprimante réseau

   Envoyez le flux d’impression à une imprimante réseau en appelant la méthode `OutputClient` de `sendToPrinter` et transmission des valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le flux d’impression à envoyer à l’imprimante.
   * Une valeur d’énumération `PrinterProtocol` spécifiant le protocole d’imprimante à utiliser. Par exemple, pour spécifier le protocole SharedPrinter, transmettez `PrinterProtocol.SharedPrinter`.
   * Valeur de chaîne spécifiant le nom du serveur d’impression. En supposant, par exemple, que le nom du serveur d’impression soit PrintServer1, transmettez `\\\PrintSever1`.
   * Valeur de chaîne qui spécifie le nom de l’imprimante. Par exemple, en supposant que le nom de l’imprimante soit Printer1, transmettez `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La méthode `sendToPrinter` a été ajoutée à l’API AEM Forms dans la version 8.2.1.

### Envoyer un flux d’impression vers une imprimante à l’aide de l’API du service web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envoyez un flux d’impression à une imprimante réseau à l’aide de l’API Output (service Web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker des données de formulaire.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML contenant les données de formulaire.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la longueur du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Définissez les options d’exécution de l’impression.

   Créez un objet `PrintedOutputOptionsSpec` en utilisant son constructeur. Par exemple, vous pouvez spécifier le nombre de copies à imprimer en attribuant une valeur entière qui représente le nombre de copies au `PrintedOutputOptionsSpec` de `copies` membre de données.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la valeur de pagination en utilisant la variable `PrintedOutputOptionsSpec` de `pagination` membre de données si vous générez un flux d’impression ZPL. De même, vous ne pouvez pas définir les options suivantes pour un flux d’impression ZPL : OutputJog, PageOffset et Staple. Le membre de données `pagination` n’est pas valide pour la génération PostScript. Il est valide uniquement pour la génération PCL.

1. Récupérez un document à imprimer.

   * Récupération d’un document à imprimer en appelant la fonction `OutputServiceService` de `generatePrintedOutput` et transmission des valeurs suivantes :

      * Valeur d’énumération `PrintFormat` spécifiant le flux d’impression. Par exemple, pour créer un flux d’impression PostScript, transmettez `PrintFormat.PostScript`.
      * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
      * Valeur de chaîne qui spécifie l’emplacement des fichiers collatéraux associés, tels que les fichiers image.
      * Valeur de chaîne qui spécifie l’emplacement du fichier XDC à utiliser.
      * L’objet `PrintedOutputOptionsSpec` contenant les options d’exécution de l’impression utilisées lors de l’envoi d’un flux d’impression vers une imprimante réseau.
      * L’objet `BLOB` contenant la source de données XML contenant les données de formulaire.
      * Un objet `BLOB` est renseigné par la méthode `generatePrintedOutput`. La méthode `generatePrintedOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
      * Objet `BLOB` renseigné par la méthode `generatePrintedOutput`. La méthode `generatePrintedOutput` renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
      * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)

   * Créez un `BLOB` à envoyer à l’imprimante en obtenant la valeur de la propriété `OutputResult` object’s `generatedDoc` . Cette méthode renvoie un objet `BLOB` qui contient des données PostScript renvoyées par la méthode `generatePrintedOutput`.

1. Envoyez le flux d’impression à une imprimante réseau.

   Envoyez le flux d’impression à une imprimante réseau en appelant la méthode `OutputClient` de `sendToPrinter` et transmission des valeurs suivantes :

   * Objet `BLOB` représentant le flux d’impression à envoyer à l’imprimante.
   * Une valeur d’énumération `PrinterProtocol` spécifiant le protocole d’imprimante à utiliser. Par exemple, pour spécifier le protocole SharedPrinter, transmettez `PrinterProtocol.SharedPrinter`.
   * Valeur `bool` spécifiant s’il faut utiliser la valeur du paramètre précédent. Transmettez la valeur `true`. (Cette valeur de paramètre est requise pour l’appel de service web uniquement.)
   * Valeur de chaîne spécifiant le nom du serveur d’impression. Par exemple, en supposant que le nom du serveur d’impression soit PrintServer1, transmettez `\\\PrintSever1`.
   * Valeur de chaîne qui spécifie le nom de l’imprimante. Par exemple, en supposant que le nom de l’imprimante soit Printer1, transmettez `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La méthode `sendToPrinter` a été ajoutée à l’API AEM Forms dans la version 8.2.1.

## Création de plusieurs fichiers Output {#creating-multiple-output-files}

Le service Output peut créer des documents distincts pour chaque enregistrement d’une source de données XML ou d’un seul fichier contenant tous les enregistrements (cette fonctionnalité est la valeur par défaut). Supposons, par exemple, que dix enregistrements se trouvent dans une source de données XML et que vous demandiez au service Output de créer des documents PDF distincts (ou d’autres types de sortie) pour chaque enregistrement à l’aide de l’API Output Service. Par conséquent, le service Output génère dix documents PDF. (Au lieu de créer des documents, vous pouvez envoyer plusieurs flux d’impression à une imprimante.)

L’illustration suivante présente comment le service Output traite un fichier de données XML contenant plusieurs enregistrements. Cependant, supposons que vous ordonniez au service Output de créer un document PDF unique contenant tous les enregistrements de données. Dans ce cas, le service Output génère un document contenant tous les enregistrements.

L’illustration suivante présente comment le service Output traite un fichier de données XML contenant plusieurs enregistrements. Supposons que vous demandiez au service Output de créer un document PDF distinct pour chaque enregistrement de données. Dans ce cas, le service Output génère un document PDF distinct pour chaque enregistrement de données.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Les données XML suivantes présentent un exemple de fichier de données contenant trois enregistrements de données.

```xml
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

Notez que l’élément XML qui démarre et termine chaque enregistrement de données est `LoanRecord`. Cet élément XML est référencé par la logique d’application qui génère plusieurs fichiers.

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-7}

Pour créer plusieurs fichiers PDF basés sur une source de données XML, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définissez les options d’exécution du PDF.
1. Définissez les options d’exécution de rendu.
1. Générez plusieurs fichiers PDF.
1. Récupérer les résultats de l’opération.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un objet client Output**

Avant de pouvoir effectuer par programmation une opération du service Output, vous devez créer un objet client du service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API Output du service web, créez un objet `OutputServiceService`.

**Référencer une source de données XML**

Référencez une source de données XML qui contient plusieurs enregistrements. Un élément XML doit être utilisé pour séparer les enregistrements de données. À titre d’illustration, dans l’exemple de source de données XML illustré précédemment dans cette section, l’élément XML qui sépare les enregistrements de données est nommé `LoanRecord`.

Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il nʼest pas nécessaire de faire correspondre lʼordre dans lequel les éléments XML sont affichés si tous les éléments XML sont spécifiés.

**Définir des options d’exécution du PDF**

Vous devez définir les options d’exécution suivantes pour que le service Output puisse créer plusieurs fichiers basés sur une source de données XML :

* **Plusieurs fichiers** : cette option indique si le service Output crée un ou plusieurs documents. Vous pouvez spécifier true ou false. Pour créer un document distinct pour chaque enregistrement de données dans la source de données XML, indiquez true.
* **URI du fichier** : il indique l’emplacement des fichiers générés par le service Output. Supposons, par exemple, que vous souhaitiez spécifier C:\\Adobe\forms\Loan.pdf. Dans ce cas, le service Output crée un fichier nommé Loan.pdf et le place dans le dossier C:\\Adobe\forms. S’il existe plusieurs fichiers, les noms seront Loan0001.pdf, Loan0002.pdf, Loan0003.pdf, etc. Si vous indiquez un emplacement de fichier, les fichiers sont placés sur le serveur, et non sur l’ordinateur client.
* **Nom d’enregistrement** : il s’agit du nom de l’élément XML de la source de données qui sépare les enregistrements de données. Par exemple, dans l’exemple de source de données XML illustré plus haut dans cette section, l’élément XML qui sépare les enregistrements de données est appelé `LoanRecord`. (Au lieu de définir l’option d’exécution Nom d’enregistrement, vous pouvez définir le niveau d’enregistrement en lui affectant une valeur numérique qui indique le niveau d’élément contenant les enregistrements de données. Cependant, vous ne pouvez définir que le nom d’enregistrement ou le niveau d’enregistrement. Vous ne pouvez pas définir les deux valeurs.)

**Définir des options d’exécution du rendu**

Vous pouvez définir des options d’exécution de rendu lors de la création de plusieurs fichiers. Bien que ces options ne soient pas requises (contrairement aux options d’exécution de sortie, qui sont requises), vous pouvez effectuer des tâches telles que l’amélioration des performances du service Output. Par exemple, vous pouvez mettre en cache la conception de formulaire utilisée par le service Output pour améliorer les performances.

Lorsque le service Output traite les enregistrements par lots, il lit les données qui contiennent plusieurs enregistrements de manière incrémentielle. En d’autres termes, le service Output lit les données en mémoire et les restitue au fur et à mesure que les lots d’enregistrements sont traités. Le service Output charge les données de manière incrémentielle lorsque l’une des deux options d’exécution est définie. Si vous définissez l’option d’exécution Nom d’enregistrement, le service Output lit les données de manière incrémentielle. De même, si vous définissez l’option d’exécution Record Level sur 2 ou plus, le service Output lit les données de manière incrémentielle.

Vous pouvez contrôler si le service Output effectue un chargement incrémentiel à l’aide de la variable `PDFOutputOptionsSpec` ou le `PrintedOutputOptionSpec` de `setLazyLoading` . Vous pouvez transmettre la valeur `false` à cette méthode, ce qui désactive le chargement incrémentiel.

**Générer plusieurs fichiers PDF**

Après avoir référencé une source de données XML valide contenant plusieurs enregistrements de données et défini des options d’exécution, vous pouvez appeler le service Output, ce qui entraîne la génération de plusieurs fichiers. Lors de la génération de plusieurs enregistrements, la variable `OutputResult` de `getGeneratedDoc` method renvoie `null`.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie des données XML qui indiquent si l’opération a réussi. Le code XML suivant est renvoyé par le service Output. Dans ce cas, le service Output a généré 42 documents.

```xml
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

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Créer plusieurs fichiers PDF à l’aide de l’API Java {#create-multiple-pdf-files-using-the-java-api}

Pour créer plusieurs fichiers PDF à l’aide de l’API Output (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java. .

1. Créer un objet client de sortie

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencer une source de données XML

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML contenant plusieurs enregistrements en utilisant son constructeur et en transmettant une valeur de chaîne qui indique l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir les options d’exécution du PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option Plusieurs fichiers en appelant la méthode `PDFOutputOptionsSpec` de `setGenerateManyFiles` . Par exemple, transmettez la valeur `true` pour demander au service Output de créer un fichier PDF distinct pour chaque enregistrement de la source de données XML. (Si vous transmettez `false`, le service Output génère un document PDF unique contenant tous les enregistrements).
   * Définissez l’option File URI en appelant la méthode `PDFOutputOptionsSpec` de `setFileUri` et transmission d’une valeur string qui spécifie l’emplacement des fichiers générés par le service Output. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.
   * Définissez l’option Record Name (Nom d’enregistrement) en appelant la méthode `OutputOptionsSpec` de `setRecordName` et transmettre une valeur string qui spécifie le nom de l’élément XML dans la source de données qui sépare les enregistrements de données. (Consultez l’exemple de source de données XML présenté plus haut dans cette section. Le nom de l’élément XML qui sépare les enregistrements de données est LoanRecord).

1. Définir des options d’exécution de rendu

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en appelant la fonction `RenderOptionsSpec` de `setCacheEnabled` et transmission d’une `Boolean` valeur de `true`.

1. Générer plusieurs fichiers PDF

   Générez plusieurs fichiers PDF en appelant la fonction `OutputClient` de `generatePDFOutput` et transmission des valeurs suivantes :

   * Une valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `com.adobe.idp.Document` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.

   La méthode `generatePDFOutput` renvoie un objet `OutputResult` contenant les résultats de l’opération.

1. Récupérer les résultats de l’opération

   * Créez un objet `java.io.File` qui représente un fichier XML qui contiendra les résultats de la méthode `generatePDFOutput`. Assurez-vous que l’extension du nom du fichier est .xml.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `applyUsageRights` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Didacticiel de mise en route (mode EJB) : créer plusieurs fichiers PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer plusieurs fichiers PDF à l’aide de l’API de service web {#create-multiple-pdf-files-using-the-web-service-api}

Pour créer plusieurs fichiers PDF à l’aide de l’API Output (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker des données de formulaire contenant plusieurs enregistrements.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier XML qui contient plusieurs enregistrements.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution du PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option Multiple Files en attribuant une valeur booléenne à la variable `OutputOptionsSpec` de `generateManyFiles` membre de données. Par exemple, affectez la valeur `true` à ce membre de données pour demander au service Output de créer un fichier PDF distinct pour chaque enregistrement de la source de données XML. (Si vous affectez `false` à ce membre de données, le service Output génère un seul PDF contenant tous les enregistrements.)
   * Définissez l’option d’URI de fichier en attribuant une valeur string qui spécifie l’emplacement du ou des fichiers générés par le service Output à la variable `OutputOptionsSpec` de `fileURI` membre de données. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.
   * Définissez l’option de nom d’enregistrement en attribuant une valeur string qui spécifie le nom de l’élément XML dans la source de données qui sépare les enregistrements de données à la valeur `OutputOptionsSpec` de `recordName` membre de données.
   * Définissez l’option Copies en attribuant une valeur entière qui spécifie le nombre de copies générées par le service Output à la variable `OutputOptionsSpec` de `copies` membre de données.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettre en cache la conception de formulaire pour améliorer les performances du service Output en affectant la valeur `true` à la fonction `RenderOptionsSpec` de `cacheEnabled` membre de données.

1. Générez plusieurs fichiers PDF.

   Créez plusieurs fichiers de PDF en appelant la méthode `OutputServiceService` de `generatePDFOutput`et transmission des valeurs suivantes :

   * Valeur d’énumération TransformationFormat. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document.
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec les données de résultat.
   * Objet `OutputResult` contenant les résultats de l’opération.

1. Récupérer les résultats de l’opération

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente un emplacement de fichier XML contenant les données de résultat. Assurez-vous que l’extension du nom du fichier est .xml.
   * Créez un tableau d’octets qui stocke le contenu des données de la variable `BLOB` qui a été renseigné avec les données de résultat de l’objet `OutputServiceService` de `generatePDFOutput` (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `binaryData` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Créer des règles de recherche {#creating-search-rules}

Vous pouvez créer des règles de recherche pour que le service Output examine les données d’entrée et utilise différentes conceptions de formulaire basées sur le contenu des données pour générer la sortie. Par exemple, si le texte *mortgage* se trouve dans les données d’entrée, le service Output peut ensuite utiliser une conception de formulaire nommée Mortgage.xdp. De même, si le texte *automobile* se trouve dans les données d’entrée, le service Output peut ensuite utiliser une conception de formulaire enregistrée sous le nom AutomobileLoan.xdp. Bien que le service Output puisse générer différents types de sortie, cette section suppose que le service Output génère un fichier PDF. Le diagramme suivant illustre le service Output qui génère un fichier PDF en traitant un fichier de données XML et en utilisant l’une des nombreuses conceptions de formulaire.

En outre, le service Output peut générer des packages de documents, où plusieurs enregistrements sont fournis dans le jeu de données et où chaque enregistrement est associé à une conception de formulaire et où un seul document est généré avec plusieurs conceptions de formulaire.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-8}

Pour demander au service Output d’utiliser des règles de recherche lors de la génération d’un document, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Référencez une source de données XML.
1. Définissez des règles de recherche.
1. Définissez les options d’exécution du PDF.
1. Définissez les options d’exécution de rendu.
1. Générez un document PDF.
1. Récupérer les résultats de l’opération.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un objet client Output**

Avant d’effectuer une opération de service Output par programmation, vous devez créer un objet client de service Output.

**Référencer une source de données XML**

Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez renseigner avec des données. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de correspondre à l’ordre dans lequel les éléments XML sont affichés, tant que tous les éléments XML sont spécifiés.

**Définir des règles de recherche**

Pour définir des règles de recherche, vous définissez un ou plusieurs modèles de texte que les services Output recherchent dans les données d’entrée. Pour chaque modèle de texte que vous définissez, vous spécifiez une conception de formulaire correspondante utilisée si le modèle de texte est localisé. Si un modèle de texte est localisé, le service Output utilise la conception de formulaire correspondante pour générer la sortie. Un exemple de modèle de texte est *mortgage*.

>[!NOTE]
>
>Si les modèles de texte ne sont pas localisés, le formulaire par défaut est utilisé. Assurez-vous que toutes les conceptions de formulaire que vous utilisez se trouvent à la racine de contenu.

**Définir des options d’exécution du PDF**

Définissez les options d’exécution de PDF suivantes afin que le service Output puisse créer un document de PDF basé sur plusieurs conceptions de formulaire :

* **URI du fichier** : indique le nom et l’emplacement du fichier PDF généré par le service Output.
* **Règles** : indique les règles que vous avez définies.
* **LookAHead** : définit le nombre d’octets à utiliser depuis le début du fichier de données d’entrée pour rechercher les modèles de texte. La valeur par défaut est de 500 octets.

**Définir les options d’exécution de rendu**

Vous pouvez définir les options d’exécution de rendu lors de la création de fichiers PDF. Bien que ces options ne soient pas requises (contrairement aux options d’exécution PDF), vous pouvez effectuer des tâches telles que l’amélioration des performances du service Output. Par exemple, vous pouvez mettre en cache la conception de formulaire utilisée par le service Output pour améliorer les performances.

**Générer un document PDF**

Après avoir référencé une source de données XML valide et défini les options d’exécution, vous pouvez utiliser le service Output, ce qui génère un document PDF. Si le service Output localise un modèle de texte spécifié dans les données d’entrée, il utilise la conception de formulaire correspondante. Si aucun modèle de texte n’est utilisé, le service Output utilise la conception de formulaire par défaut.

**Récupérer les résultats de l’opération**

Une fois que le service Output a effectué une opération, il renvoie des données XML spécifiant si l’opération a réussi.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Créer des règles de recherche à l’aide de l’API Java {#create-search-rules-using-the-java-api}

Créez des règles de recherche à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez une source de données XML.

   * Créez un objet `java.io.FileInputStream` qui représente la source de données XML utilisée pour remplir le document PDF en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez des règles de recherche.

   * Créez un objet `Rule` en utilisant son constructeur.
   * Définissez un modèle de texte en appelant la méthode `Rule` de `setPattern` et transmettre une valeur string qui spécifie un modèle de texte.
   * Définissez la conception de formulaire correspondante en appelant la méthode `Rule` de `setForm` de . Transmettez une valeur de chaîne spécifiant le nom de la nouvelle conception de formulaire.

   >[!NOTE]
   >
   >Pour chaque modèle de texte à définir, répétez les trois sous-étapes précédentes.

   * Créez un objet `java.util.List` en utilisant un constructeur `java.util.ArrayList`.
   * Pour chaque `Rule` que vous avez créé, appelez l’objet `java.util.List` de `add` et transmettez la méthode `Rule` .

1. Définissez les options d’exécution du PDF.

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Indiquez le nom et l’emplacement du fichier de PDF généré par le service Output en appelant la fonction `PDFOutputOptionsSpec` de `setFileURI` . Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier PDF. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.
   * Définissez les règles que vous avez définies en appelant la variable `PDFOutputOptionsSpec` de `setRules` . Transmettez l’objet `java.util.List` contenant les objets `Rule`.
   * Définissez le nombre d’octets à analyser pour les modèles de texte définis en appelant la variable `PDFOutputOptionsSpec` de `setLookAhead` . Transmettez une valeur entière qui représente le nombre d’octets.

1. Définissez les options d’exécution de rendu.

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettez en cache la conception de formulaire pour améliorer les performances du service Output en appelant la fonction `RenderOptionsSpec` de `setCacheEnabled` et transmission `true`.

1. Générez un document PDF.

   Générer un document de PDF basé sur plusieurs conceptions de formulaire en appelant la fonction `OutputClient` de `generatePDFOutput` et transmission des valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Une valeur de chaîne spécifiant le nom de la conception de formulaire par défaut. En d’autres termes, la conception de formulaire utilisée si aucun modèle de texte n’est localisé.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouvent les conceptions de formulaire.
   * Un objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Un objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * L’objet `com.adobe.idp.Document` contenant les données de formulaire recherchées par le service Output pour les modèles de texte définis.

   La méthode `generatePDFOutput` renvoie un objet `OutputResult` contenant les résultats de l’opération.

1. Récupérer les résultats de l’opération.

   * Créez un `com.adobe.idp.Document` qui représente l’état de la propriété `generatePDFOutput` en appelant la méthode `OutputResult` de `getStatusDoc` .
   * Créez un objet `java.io.File` qui contiendra les résultats de l’opération. Assurez-vous que l’extension de fichier est .xml.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` dans le fichier (assurez-vous d’utiliser la variable `com.adobe.idp.Document` qui a été renvoyé par l’objet `getStatusDoc` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : créer des règles de recherche à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Démarrage rapide (mode SOAP) : création de règles de recherche à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Créer des règles de recherche à l’aide de l’API de service web {#create-search-rules-using-the-web-service-api}

Créez des règles de recherche à l’aide de l’API Output (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker les données qui seront fusionnées avec le document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à chiffrer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez des règles de recherche.

   * Créez un objet `Rule` en utilisant son constructeur.
   * Définissez un modèle de texte en attribuant une valeur string qui spécifie un modèle de texte au `Rule` de `pattern` membre de données.
   * Définissez la conception de formulaire correspondante en attribuant une valeur string qui spécifie la conception de formulaire au `Rule` de `form` membre de données.

   >[!NOTE]
   >
   >Pour chaque modèle de texte à définir, répétez les trois sous-étapes précédentes.

   * Créez un objet `MyArrayOf_xsd_anyType` qui stocke les règles.
   * Affectez chaque objet `Rule` à un élément du tableau `MyArrayOf_xsd_anyType`. Appeler la variable `MyArrayOf_xsd_anyType` de `Add` pour chaque `Rule` .

1. Définir les options d’exécution du PDF

   * Créez un objet `PDFOutputOptionsSpec` en utilisant son constructeur.
   * Définissez l’option d’URI de fichier en attribuant une valeur string qui spécifie l’emplacement du fichier de PDF généré par le service Output à la variable `PDFOutputOptionsSpec` de `fileURI` membre de données. L’option URI du fichier concerne le serveur d’applications J2EE hébergeant AEM Forms, et non l’ordinateur client.
   * Définissez l’option Copies en attribuant une valeur entière qui spécifie le nombre de copies générées par le service Output à la variable `PDFOutputOptionsSpec` de `copies` membre de données.
   * Définissez les règles que vous avez définies en attribuant la variable `MyArrayOf_xsd_anyType` qui stocke les règles dans la variable `PDFOutputOptionsSpec` de `rules` membre de données.
   * Définissez le nombre d’octets à analyser pour les modèles de texte définis en attribuant une valeur entière qui représente le nombre d’octets à analyser au `PDFOutputOptionsSpec` de `lookAhead` data .

1. Définir des options d’exécution de rendu

   * Créez un objet `RenderOptionsSpec` en utilisant son constructeur.
   * Mettre en cache la conception de formulaire pour améliorer les performances du service Output en affectant la valeur `true` à la fonction `RenderOptionsSpec` de `cacheEnabled` membre de données.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir la version du document du PDF à l’aide du `RenderOptionsSpec` de `pdfVersion` membre si le document d’entrée est un formulaire Acrobat. Le document PDF de sortie conserve la version PDF du formulaire Acrobat. De même, vous ne pouvez pas définir l’option de PDF balisé à l’aide de la variable `RenderOptionsSpec` de `taggedPDF` si le document d’entrée est un formulaire Acrobat.

   >[!NOTE]
   >
   >Vous ne pouvez pas définir l’option de PDF linéarisé à l’aide de la variable `RenderOptionsSpec` de `linearizedPDF` membre si le document input PDF est certifié ou signé numériquement. Pour plus d’informations, voir [Signature numérique de documents PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Générer un document PDF

   Créez un document de PDF en appelant la méthode `OutputServiceService` de `generatePDFOutput`et transmission des valeurs suivantes :

   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF, spécifiez `TransformationFormat.PDF`.
   * Valeur string spécifiant le nom de la nouvelle conception de formulaire.
   * Une valeur de chaîne qui spécifie la racine de contenu où se trouve la conception de formulaire.
   * Objet `PDFOutputOptionsSpec` contenant les options d’exécution du PDF.
   * Objet `RenderOptionsSpec` contenant les options d’exécution de rendu.
   * Objet `BLOB` contenant la source de données XML contenant les données à fusionner avec la conception de formulaire.
   * Objet `BLOB` qui est renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec des métadonnées générées qui décrivent le document. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Objet `BLOB` renseigné par la méthode `generatePDFOutput`. La méthode `generatePDFOutput` renseigne cet objet avec les données de résultat. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Objet `OutputResult` contenant les résultats de l’opération. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

   >[!NOTE]
   >
   >Lors de la génération d’un document PDF en appelant la méthode `generatePDFOutput`, sachez que vous ne pouvez pas fusionner des données avec un formulaire PDF XFA signé, certifié ou contenant des droits d’utilisation. Pour plus d’informations sur les droits d’utilisation, voir [Appliquer des droits d’utilisation aux documents PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Récupérer les résultats de l’opération

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente un emplacement de fichier XML contenant les données de résultat. Assurez-vous que l’extension de fichier est XML.
   * Créez un tableau d’octets qui stocke le contenu des données de la variable `BLOB` qui a été renseigné avec les données de résultat de l’objet `OutputServiceService` de `generatePDFOutput` (le huitième paramètre). Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier XML en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aplatissement de documents PDF {#flattening-pdf-documents}

Vous pouvez utiliser le service Output pour convertir un document PDF interactif en PDF non interactif. Un document PDF interactif permet aux utilisateurs de saisir ou de modifier des données contenues dans les champs de ce document. Le processus de conversion d’un document PDF interactif en document PDF non interactif est appelé *aplatissement*. Lorsqu’un document PDF est aplati, un utilisateur ne peut pas modifier les données contenues dans les champs du document. S’assurer que les données ne peuvent être modifiées est l’une des raisons de l’aplatissement d’un document PDF.

Vous pouvez aplatir les types de documents PDF suivants :

* Documents PDF XFA interactifs
* Acrobat Forms

Toute tentative d’aplatissement d’un document PDF non interactif entraîne une exception.

>[!NOTE]
>
>Pour plus d’informations sur le service Output, voir [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-9}

Pour aplatir un document PDF interactif en document PDF non interactif, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet client Output.
1. Récupérez un document PDF interactif.
1. Transformez le document PDF.
1. Enregistrez le document PDF non interactif en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement des fichiers JAR AEM Forms, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet client Output**

Avant de pouvoir effectuer par programmation une opération du service Output, vous devez créer un objet client du service Output. Si vous utilisez l’API Java, créez un objet `OutputClient`. Si vous utilisez l’API du service Web Output, créez un objet `OutputServiceService`.

**Récupérer un document PDF interactif**

Récupérez un document PDF interactif que vous souhaitez convertir en document PDF non interactif. Toute tentative de conversion d’un document PDF non interactif entraîne une exception.

**Convertir le document PDF**

Après avoir récupéré un document PDF interactif, vous pouvez le convertir en document PDF non interactif. Le service Output renvoie un document PDF non interactif.

**Enregistrer le document PDF non interactif en tant que fichier PDF**

Vous pouvez enregistrer le document PDF non interactif en tant que fichier PDF.

**Voir également**

[Aplatir un document PDF à l’aide de l’API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Aplatir un document PDF à l’aide de l’API Web Service](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Aplatir un document PDF à l’aide de l’API Java {#flatten-a-pdf-document-using-the-java-api}

Aplatissez un document PDF interactif en document PDF non interactif à l’aide de l’API Output (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-output-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un objet client Output.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `OutputClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez un document PDF interactif.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF interactif à transformer à l’aide de son constructeur et en transmettant une valeur string spécifiant l’emplacement du fichier PDF interactif.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Transformez le document PDF.

   Transforme le document du PDF interactif en document du PDF non interactif en appelant la méthode `OutputServiceService` de `transformPDF` et transmission des valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF interactif.
   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF non interactif, spécifiez `TransformationFormat.PDF`.
   * Valeur d’énumération `PDFARevisionNumber` qui spécifie le numéro de révision. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `null`.
   * Valeur string qui représente le numéro de modification et l’année séparés par deux points. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `null`.
   * Valeur d’énumération `PDFAConformance` qui représente le niveau de conformité du PDF/A. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `null`.

   La méthode `transformPDF` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif en tant que fichier PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appeler la variable `Document` de `copyToFile` pour copier le contenu de la méthode `Document` dans le fichier (assurez-vous d’utiliser la variable `Document` qui a été renvoyé par l’objet `transformPDF` ).

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Démarrage rapide (mode EJB) : transformer un document PDF à l’aide de l’API Java.](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Démarrage rapide (mode SOAP) : transformation d’un document de PDF à l’aide de l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Aplatir un document PDF à l’aide de l’API Web Service {#flatten-a-pdf-document-using-the-web-service-api}

Aplatissez un document PDF interactif vers un document PDF non interactif à l’aide de l’API Output (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un objet client Output.

   * Créez un objet `OutputServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `OutputServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `OutputServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez un document PDF interactif.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF interactif.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF interactif.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Transformez le document PDF.

   Transforme le document du PDF interactif en document du PDF non interactif en appelant la méthode `OutputClient` de `transformPDF` et transmission des valeurs suivantes :

   * Objet `BLOB` contenant le document PDF interactif.
   * Valeur d’énumération `TransformationFormat`. Pour générer un document PDF non interactif, spécifiez `TransformationFormat.PDF`.
   * Valeur d’énumération `PDFARevisionNumber` qui spécifie le numéro de révision.
   * Valeur booléenne qui spécifie si la valeur d’énumération `PDFARevisionNumber` est utilisée. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `false`.
   * Valeur string qui représente le numéro de modification et l’année séparés par deux points. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `null`.
   * Valeur d’énumération `PDFAConformance` qui représente le niveau de conformité du PDF/A.
   * Valeur booléenne qui spécifie si la valeur d’énumération `PDFAConformance` est utilisée. Comme ce paramètre est destiné à un document PDF/A, vous pouvez indiquer `false`.

   La méthode `transformPDF` renvoie un objet `BLOB` contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif en tant que fichier PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF non interactif.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `transformPDF`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Résumé des étapes](creating-document-output-streams.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
