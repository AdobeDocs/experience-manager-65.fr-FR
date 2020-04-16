---
title: 'Signature numérique et certification des '
seo-title: 'Signature numérique et certification des '
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Signature numérique et certification des {#digitally-signing-and-certifying-documents}

**À propos du service Signature**

Le service Signature permet à votre entreprise de protéger la sécurité et la confidentialité des Adobe PDF qu’elle diffuse et reçoit. Ce service utilise les signatures numériques et la certification pour s’assurer que seuls les prévus peuvent modifier les . Comme les fonctions de sécurité sont appliquées au  lui-même, le  reste sécurisé et contrôlé pendant tout son cycle de vie. Un reste sécurisé au-delà du pare-feu, lorsqu’il est téléchargé hors ligne et lorsqu’il est renvoyé à votre entreprise.

>[!NOTE]
>
>Vous pouvez créer un gestionnaire de signatures personnalisé pour le service Signature qui est appelé lors de l’appel de certaines opérations, comme la signature d’un  PDF.

**Noms des champs de signature**

Certaines opérations du service Signature nécessitent de spécifier le nom du champ de signature sur lequel une opération est effectuée. Par exemple, lors de la signature d’un  PDF, vous indiquez le nom du champ de signature à signer. Supposons que le nom complet d’un champ de signature soit `form1[0].Form1[0].SignatureField1[0]`. Vous pouvez spécifier `SignatureField1[0]` plutôt que `form1[0].Form1[0].SignatureField1[0]`.

Il arrive qu’un conflit entraîne la signature du service Signature (ou l’exécution d’une autre opération nécessitant le nom du champ de signature) du mauvais champ. Ce conflit est le résultat du nom `SignatureField1[0]` apparaissant à plusieurs endroits dans le même  PDF. Prenons l’exemple d’un PDF qui contient deux champs de signature nommés `form1[0].Form1[0].SignatureField1[0]` et `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` et que vous spécifiez `SignatureField1[0]`. Dans ce cas, le service Signature signe le premier champ de signature qu’il trouve lors de l’itération sur tous les champs de signature du .

Si plusieurs champs de signature se trouvent dans un  PDF, il est recommandé de spécifier le nom complet des champs de signature. C&#39;est-à-dire, spécifiez `form1[0].Form1[0].SignatureField1[0]`au lieu de `SignatureField1[0]`.

Vous pouvez accomplir ces  à l’aide du service Signature :

* Ajouter et supprimez des champs de signature numérique dans un  PDF. (Voir [Ajout de champs](digitally-signing-certifying-documents.md#adding-signature-fields)de signature.)
* Récupérez les noms des champs de signature situés dans un  PDF. (Voir [Récupération des noms](digitally-signing-certifying-documents.md#retrieving-signature-field-names)des champs de signature.)
* Modifier les champs de signature. (Voir [Modification des champs](digitally-signing-certifying-documents.md#modifying-signature-fields)de signature.)
* Signez numériquement le  PDF. (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifier les  PDF. (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Validez les signatures numériques situées dans un  PDF. (Voir [Vérification des signatures](digitally-signing-certifying-documents.md#verifying-digital-signatures)numériques.)
* Validez toutes les signatures numériques situées dans un  PDF. (See [Verifying Multiple Digital Signatures](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Supprimez une signature numérique d’un champ de signature. (Voir [Suppression de signatures](digitally-signing-certifying-documents.md#removing-digital-signatures)numériques.)

>[!NOTE]
>
> For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)..

## Ajout de champs de signature {#adding-signature-fields}

Les signatures numériques apparaissent dans les champs de signature qui sont des champs de formulaire contenant une représentation graphique de la signature. Les champs de signature peuvent être visibles ou invisibles. Les signataires peuvent utiliser un champ de signature préexistant ou un champ de signature peut être ajouté par programmation. Dans les deux cas, le champ de signature doit exister avant la signature du document PDF.

Vous pouvez programmer l’ajout d’un champ de signature à l’aide de l’API Java du service Signature ou de l’API du service Web de signature. Vous pouvez ajouter plusieurs champs de signature à un  PDF ; toutefois, chaque nom de champ de signature doit être unique.

>[!NOTE]
>
>Certains types de  PDF ne vous permettent pas d’ajouter par programmation un champ de signature. Pour plus d’informations sur le service Signature et l’ajout de champs de signature, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour ajouter un champ de signature à un  PDF, effectuez l’ suivante :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez un PDF auquel un champ de signature est ajouté.
1. Ajouter un champ de signature.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un client Signature**

Avant de pouvoir exécuter une opération du service Signature par programmation, vous devez créer un client du service Signature.

**Obtenir un PDF auquel un champ de signature est ajouté**

Vous devez obtenir un PDF auquel un champ de signature est ajouté.

**Ajouter d’un champ de signature**

Pour ajouter un champ de signature à un  PDF, vous devez spécifier des valeurs de coordonnées qui identifient l’emplacement du champ de signature. (Si vous ajoutez un champ de signature invisible, ces valeurs ne sont pas requises.) Vous pouvez également spécifier les champs du PDF qui sont verrouillés une fois qu’une signature est appliquée au champ de signature.

**Enregistrer le  PDF en tant que fichier PDF**

Une fois que le service Signature a ajouté un champ de signature au  du PDF, vous pouvez enregistrer le sous forme de fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[de signature numérique de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Ajouter de champs de signature à l’aide de l’API Java {#add-signature-fields-using-the-java-api}

Ajouter un champ de signature à l’aide de l’API de signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir un PDF auquel un champ de signature est ajouté

   * Créez un `java.io.FileInputStream` objet représentant le PDF auquel un champ de signature est ajouté à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Ajouter d’un champ de signature

   * Créez un `PositionRectangle` objet qui spécifie l’emplacement du champ de signature à l’aide de son constructeur. Dans le constructeur, spécifiez des valeurs de coordonnées.
   * Si vous le souhaitez, créez un `FieldMDPOptions` objet qui spécifie les champs verrouillés lorsqu’une signature numérique est appliquée au champ de signature.
   * Ajouter un champ de signature dans un PDF  en appelant la `SignatureServiceClient` `addSignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

      * A `com.adobe.idp`. `Document` qui représente le PDF auquel un champ de signature est ajouté.
      * Valeur de chaîne qui spécifie le nom du champ de signature.
      * Valeur `java.lang.Integer` représentant le numéro de page auquel un champ de signature est ajouté.
      * Objet `PositionRectangle` spécifiant l’emplacement du champ de signature.
      * Objet `FieldMDPOptions` spécifiant les champs du PDF verrouillés après l’application d’une signature numérique au champ de signature. Cette valeur de paramètre est facultative et vous pouvez la transmettre `null`.
   * Objet `PDFSeedValueOptions` spécifiant diverses valeurs d’exécution. Cette valeur de paramètre est facultative et vous pouvez la transmettre `null`.

      The `addSignatureField` method returns a `com.adobe.idp`. `Document` qui représente un  PDF contenant un champ de signature.
   >[!NOTE]
   >
   >Vous pouvez appeler la `SignatureServiceClient` `addInvisibleSignatureField` méthode de l’objet pour ajouter un champ de signature invisible.

1. Enregistrer le  PDF en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez le `com.adobe.idp`. `Document` méthode `copyToFile` de l’objet pour copier le contenu de l’ `Document` objet dans le fichier. Veillez à utiliser la `com.adobe.idp`. `Document` qui a été renvoyée par la `addSignatureField` méthode.

**Voir également**

[rapide de l’API du service Signature](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Ajouter de champs de signature à l’aide de l’API du service Web {#add-signature-fields-using-the-web-service-api}

Pour ajouter un champ de signature à l’aide de l’API de signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir un PDF auquel un champ de signature est ajouté

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le PDF qui contiendra un champ de signature.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Ajouter d’un champ de signature

   Ajouter un champ de signature au PDF  en appelant la `SignatureServiceClient` `addSignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `BLOB` object that represents the PDF document to which a signature field is added.
   * Valeur de chaîne qui spécifie le nom du champ de signature.
   * Valeur entière représentant le numéro de page auquel un champ de signature est ajouté.
   * Objet `PositionRect` spécifiant l’emplacement du champ de signature.
   * Objet `FieldMDPOptions` spécifiant les champs du PDF verrouillés après l’application d’une signature numérique au champ de signature. Cette valeur de paramètre est facultative et vous pouvez la transmettre `null`.
   * Objet `PDFSeedValueOptions` spécifiant diverses valeurs d’exécution. Cette valeur de paramètre est facultative et vous pouvez la transmettre `null`.
   La `addSignatureField` méthode renvoie un `BLOB` objet qui représente un PDF contenant un champ de signature.

1. Enregistrer le  PDF en tant que fichier PDF

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du PDF qui contiendra le champ de signature et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `addSignatureField` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `binaryData` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Récupération des noms des champs de signature {#retrieving-signature-field-names}

Vous pouvez récupérer les noms de tous les champs de signature d’un document PDF que vous souhaitez signer ou certifier. Si vous n’êtes pas certain de connaître les noms de champ de signature d’un document PDF ou si vous souhaitez vérifier leurs noms, vous pouvez programmer leur récupération. The Signature service returns the fully qualified name of the signature field, such as `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Résumé des étapes {#summary_of_steps-1}

Pour récupérer les noms des champs de signature, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le  PDF contenant les champs de signature.
1. Récupérez les noms des champs de signature.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant de pouvoir exécuter une opération du service Signature par programmation, vous devez créer un client du service Signature.

**Obtention du PDF contenant les champs de signature**

Récupérez un PDF contenant des champs de signature.

**Récupérer les noms des champs de signature**

Vous pouvez récupérer les noms des champs de signature après avoir récupéré un  PDF contenant un ou plusieurs champs de signature.

**Voir également**

[Récupérer les noms des champs de signature à l’aide de l’API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Récupérer le champ de signature à l’aide de l’API du service Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout de champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Récupérer les noms des champs de signature à l’aide de l’API Java {#retrieve-signature-field-names-using-the-java-api}

Récupérez les noms des champs de signature à l’aide de l’API Signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtention du PDF contenant les champs de signature

   * Créez un `java.io.FileInputStream` objet représentant le PDF qui contient des champs de signature à l’aide de son constructeur et transmettez une valeur de chaîne qui spécifie l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Récupérer les noms des champs de signature

   * Récupérez les noms des champs de signature en appelant la `SignatureServiceClient` méthode de l’ `getSignatureFieldList` objet et en transmettant l’ `com.adobe.idp.Document` objet contenant le PDF qui contient les champs de signature. Cette méthode renvoie un `java.util.List` objet dans lequel chaque élément contient un `PDFSignatureField` objet. Cet objet vous permet d’obtenir des informations supplémentaires sur un champ de signature, par exemple s’il est visible.
   * Parcourez l’ `java.util.List` objet pour déterminer s’il existe des noms de champ de signature. Pour chaque champ de signature du  PDF, vous pouvez obtenir un `PDFSignatureField` objet distinct. Pour obtenir le nom du champ de signature, appelez la `PDFSignatureField` `getName` méthode de l’objet. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du champ de signature.

**Voir également**

[Récupération des noms des champs de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[rapide (mode SOAP) : Récupération des noms de champ de signature à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer le champ de signature à l’aide de l’API du service Web {#retrieve-signature-field-using-the-web-service-api}

Récupérez les noms des champs de signature à l’aide de l’API Signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtention du PDF contenant les champs de signature

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le PDF qui contient des champs de signature.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Récupérer les noms des champs de signature

   * Récupérez les noms des champs de signature en appelant la `SignatureServiceClient` méthode de `getSignatureFieldList` l’objet et en transmettant l’ `BLOB` objet qui contient le PDF contenant les champs de signature. Cette méthode renvoie un objet `MyArrayOfPDFSignatureField` de collection où chaque élément contient un `PDFSignatureField` objet.
   * Parcourez l’ `MyArrayOfPDFSignatureField` objet pour déterminer s’il existe des noms de champ de signature. Pour chaque champ de signature du  PDF, vous pouvez obtenir un `PDFSignatureField` objet. Pour obtenir le nom du champ de signature, appelez la `PDFSignatureField` `getName` méthode de l’objet. Cette méthode renvoie une valeur de chaîne qui spécifie le nom du champ de signature.

**Voir également**

[Récupération des noms des champs de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifying Signature Fields {#modifying-signature-fields}

Vous pouvez modifier les champs de signature situés dans un PDF à l’aide de l’API Java et de l’API de service Web. La modification d’un champ de signature implique de manipuler ses valeurs de dictionnaire de verrouillage des champs de signature ou ses valeurs du dictionnaire de valeur de départ.

A *field lock dictionary* specifies a list of fields that are locked when the signature field is signed. Un champ verrouillé empêche les utilisateurs d’apporter des modifications au champ. A *seed value dictionary* contains constraining information that is used at the time the signature is applied. Par exemple, vous pouvez modifier les autorisations qui contrôlent les actions pouvant se produire sans invalider la signature.

En modifiant un champ de signature existant, vous pouvez apporter des modifications au PDF afin de refléter l’évolution des besoins de l’entreprise. Par exemple, une nouvelle exigence professionnelle peut nécessiter le verrouillage de tous les champs de  du une fois le  du signé.

Cette section explique comment modifier un champ de signature en modifiant les valeurs du dictionnaire de verrou de champ et du dictionnaire de valeurs de départ. Les modifications apportées au dictionnaire de verrouillage de champ de signature entraînent le verrouillage de tous les champs du PDF  lorsqu’un champ de signature est signé. Les modifications apportées au dictionnaire des valeurs de départ interdisent des types spécifiques de modifications au .

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la modification des champs de signature, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour modifier les champs de signature situés dans un  PDF, effectuez l’ de suivante :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le  PDF contenant le champ de signature à modifier.
1. Définissez les valeurs du dictionnaire.
1. Modifiez le champ de signature.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including LiveCycle Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant de pouvoir exécuter une opération du service Signature par programmation, vous devez créer un client du service Signature.

**Obtenir le  PDF contenant le champ de signature à modifier**

Récupérez un  PDF contenant le champ de signature à modifier.

**Définition des valeurs de dictionnaire**

Pour modifier un champ de signature, affectez des valeurs à son dictionnaire de verrouillage de champ ou à son dictionnaire de valeur de départ. La spécification des valeurs du dictionnaire de verrouillage de champ de signature implique la spécification des champs de PDF verrouillés lors de la signature du champ de signature. (Cette section explique comment verrouiller tous les champs.)

Vous pouvez définir les valeurs suivantes du dictionnaire des valeurs de base :

* **Vérification** de révision : Indique si la vérification de révocation est effectuée lorsqu’une signature est appliquée au champ de signature.
* **Options** de certificat : Attribue des valeurs au dictionnaire de valeurs de départ du certificat. Avant de spécifier les options de certificat, il est recommandé de se familiariser avec un dictionnaire de valeurs de départ de certificat. (Voir Référence [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF.)
* **Options** de résumé : Attribue des algorithmes digest utilisés pour la signature. Les valeurs valides sont SHA1, SHA256, SHA384, SHA512 et RIPEMD160.
* **Filtre**: Indique le filtre utilisé avec le champ de signature. Par exemple, vous pouvez utiliser le filtre Adobe.PPKLite. (Voir Référence [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF.)
* **Options** d’indicateur : Indique les valeurs d’indicateur associées à ce champ de signature. La valeur 1 signifie qu’un signataire ne doit utiliser que les valeurs spécifiées pour l’entrée. La valeur 0 signifie que d’autres valeurs sont autorisées. Voici les positions de Bit :

   * **1(Filtre) :** Gestionnaire de signatures à utiliser pour signer le champ de signature
   * **2 (Sous-filtre) :** Tableau de noms indiquant des codages acceptables à utiliser lors de la signature
   * **3 V)**: Numéro de version minimum requis du gestionnaire de signatures à utiliser pour signer le champ de signature
   * **4 (Raisons) :** Tableau de chaînes spécifiant les raisons possibles de la signature d’un 
   * **5 (PDFLegalWarnings) :** Tableau de chaînes spécifiant des attestations légales possibles

* **Attestations** légales : Lorsqu’un est certifié, il est automatiquement analysé à la recherche de types de contenu spécifiques qui peuvent rendre le contenu visible d’un  ambigu ou trompeur. Par exemple, une annotation peut masquer du texte important pour comprendre ce qui est certifié. Le processus d’analyse génère des avertissements indiquant la présence de ce type de contenu. Il fournit également une explication supplémentaire du contenu susceptible d’avoir généré des avertissements.
* **Autorisations**: Indique les autorisations pouvant être utilisées sur un PDF sans invalider la signature.
* **Raisons**: Indique les raisons pour lesquelles cette  doit être signée.
* **Horodatage**: Spécifie les options d’horodatage. Vous pouvez, par exemple, définir l’URL du serveur d’horodatage utilisé.
* **Version**: Indique le numéro de version minimum du gestionnaire de signatures à utiliser pour signer le champ de signature.

**Modification du champ de signature**

Après avoir créé un client de service Signature, récupéré le PDF qui contient le champ de signature à modifier et défini les valeurs du dictionnaire, vous pouvez demander au service Signature de modifier le champ de signature. Le service Signature renvoie ensuite un PDF contenant le champ de signature modifié. Le  PDF d’origine n’est pas affecté.

**Enregistrer le  PDF en tant que fichier PDF**

Enregistrez le  PDF contenant le champ de signature modifié au format PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Signature](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[de signature numérique de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modification des champs de signature à l’aide de l’API Java {#modify-signature-fields-using-the-java-api}

Modifiez un champ de signature à l’aide de l’API de signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le  PDF contenant le champ de signature à modifier

   * Créez un `java.io.FileInputStream` objet représentant le PDF qui contient le champ de signature à modifier à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des valeurs de dictionnaire

   * Créez un objet `PDFSignatureFieldProperties` en utilisant son constructeur. Un `PDFSignatureFieldProperties` objet stocke des informations sur le dictionnaire de verrou du champ de signature et le dictionnaire des valeurs de départ.
   * Créez un objet `PDFSeedValueOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de valeurs de départ.
   * Interdisez les modifications apportées au PDF en appelant la `PDFSeedValueOptionSpec` méthode de l’ `setMdpValue` objet et en transmettant la `MDPPermissions.NoChanges` valeur .
   * Créez un objet `FieldMDPOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de verrouillage des champs de signature.
   * Verrouillez tous les champs du PDF en appelant la `FieldMDPOptionSpec` méthode de l’ `setMdpValue` objet et en transmettant la `FieldMDPAction.ALL` valeur .
   * Définissez les informations du dictionnaire des valeurs de départ en appelant la `PDFSignatureFieldProperties` méthode de l’objet et en transmettant l’ `setSeedValue` `PDFSeedValueOptionSpec` objet.
   * Définissez les informations du dictionnaire de verrouillage de champ de signature en appelant la `PDFSignatureFieldProperties`méthode de l’ `setFieldMDP` objet et en transmettant l’ `FieldMDPOptionSpec` objet.
   >[!NOTE]
   >
   >Pour afficher toutes les valeurs du dictionnaire de valeurs de base que vous pouvez définir, voir la référence de `PDFSeedValueOptionSpec` classe. (voir Référence [sur l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

1. Modification du champ de signature

   Modifiez le champ de signature en appelant la `SignatureServiceClient` `modifySignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` qui stocke le PDF contenant le champ de signature à modifier
   * Valeur de chaîne qui spécifie le nom du champ de signature
   * L’ `PDFSignatureFieldProperties` objet qui stocke les informations du dictionnaire de verrou du champ de signature et du dictionnaire de valeur de départ
   La `modifySignatureField` méthode renvoie un `com.adobe.idp.Document` objet qui stocke un PDF contenant le champ de signature modifié.

1. Enregistrer le  PDF en tant que fichier PDF

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. Veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `modifySignatureField` méthode.

### Modification des champs de signature à l’aide de l’API du service Web {#modify-signature-fields-using-the-web-service-api}

Modifiez un champ de signature à l’aide de l’API Signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le  PDF contenant le champ de signature à modifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le PDF qui contient le champ de signature à modifier.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Définition des valeurs de dictionnaire

   * Créez un objet `PDFSignatureFieldProperties` en utilisant son constructeur. Cet objet stocke des informations sur le dictionnaire de verrou du champ de signature et le dictionnaire des valeurs de départ.
   * Créez un objet `PDFSeedValueOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de valeurs de départ.
   * Interdisez les modifications apportées au PDF en attribuant la valeur de l’ `MDPPermissions.NoChanges` de au membre `PDFSeedValueOptionSpec` `mdpValue` de données de l’objet.
   * Créez un objet `FieldMDPOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de verrouillage des champs de signature.
   * Verrouillez tous les champs du PDF en attribuant la `FieldMDPAction.ALL` valeur  au membre `FieldMDPOptionSpec` `mdpValue` de données de l’objet.
   * Définissez les informations du dictionnaire des valeurs de départ en affectant l’ `PDFSeedValueOptionSpec` objet au membre `PDFSignatureFieldProperties` `seedValue` de données de l’objet.
   * Définissez les informations du dictionnaire de verrouillage de champ de signature en affectant l’ `FieldMDPOptionSpec` objet au membre `PDFSignatureFieldProperties` `fieldMDP` de données de l’objet.
   >[!NOTE]
   >
   >Pour afficher toutes les valeurs du dictionnaire de valeurs de base que vous pouvez définir, voir la référence de `PDFSeedValueOptionSpec` classe. (Voir Référence [sur l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms).

1. Modification du champ de signature

   Modifiez le champ de signature en appelant la `SignatureServiceClient` `modifySignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` qui stocke le PDF contenant le champ de signature à modifier
   * Valeur de chaîne qui spécifie le nom du champ de signature
   * L’ `PDFSignatureFieldProperties` objet qui stocke les informations du dictionnaire de verrou du champ de signature et du dictionnaire de valeur de départ
   La `modifySignatureField` méthode renvoie un `BLOB` objet qui stocke un PDF contenant le champ de signature modifié.

1. Enregistrer le  PDF en tant que fichier PDF

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF qui contiendra le champ de signature et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `addSignatureField` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Digitally Signing PDF Documents {#digitally-signing-pdf-documents}

Les signatures numériques peuvent être appliquées aux documents PDF pour fournir un niveau de sécurité. Les signatures numériques, tout comme les signatures manuscrites, permettent aux signataires de s’identifier et d’effectuer des instructions sur le document. La technologie utilisée pour signer numériquement des documents permet de s’assurer que le signataire et les destinataires se sont accordés sur ce qui a été signé et croient en la non-altération du document signé.

Les documents PDF sont signés au moyen de la technologie de clé publique. Le signataire a deux clés : une clé publique et une clé privée. La clé privée est stockée dans les informations d’identification d’un utilisateur qui doivent être disponibles au moment de la signature. La clé publique est stockée dans le certificat de l’utilisateur, qui doit être accessible aux pour valider la signature. Les informations relatives aux certificats révoqués se trouvent dans les listes de révocation des certificats et les réponses OCSP (Online Certificate Status Protocol) distribuées par les autorités de certification (CA). L’heure de la signature peut être obtenue d’une source approuvée appelée Autorité de d’horodatage.

>[!NOTE]
>
>Avant de pouvoir signer numériquement un  PDF, vous devez vous assurer d’ajouter le certificat à AEM Forms. Un certificat est ajouté à l’aide d’Administration Console ou par programmation à l’aide de l’API Trust Manager. (voir [Importation des informations d’identification à l’aide de l’API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)Trust Manager).

Vous pouvez signer numériquement des  PDF par programmation. Lors de la signature numérique d’un  PDF, vous devez référencer des informations d’identification de sécurité qui existent dans AEM Forms. Les informations d’identification sont la clé privée utilisée pour la signature.

Le service Signature effectue les étapes suivantes lorsqu’un PDF est signé :

1. Le service Signature récupère les informations d’identification auprès de Truststore en transmettant l’alias spécifié dans la requête.
1. TrustStore recherche les informations d’identification spécifiées.
1. Les informations d’identification sont renvoyées au service Signature et sont utilisées pour signer le . Les informations d’identification sont également mises en cache par rapport à l’alias pour les futures demandes.

Pour plus d’informations sur la gestion des informations d’identification de sécurité, voir le guide *Installation et déploiement d’AEM Forms* pour votre serveur d’applications.

>[!NOTE]
>
>Il existe des différences entre la signature et la certification des  de. (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Tous les PDF ne prennent pas en charge la signature. Pour plus d’informations sur le service Signature et la  de signature numérique du, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Le service Signature ne prend pas en charge les fichiers XDP contenant des données PDF incorporées en entrée dans une opération, telle que la certification d’un . Cette action entraîne le déclenchement d’une `PDFOperationException`erreur par le service Signature. Pour résoudre ce problème, convertissez le fichier XDP en fichier PDF à l’aide du service PDF Utilities, puis transmettez le fichier PDF converti en opération de service Signature. (voir [Utilisation des utilitaires](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)PDF).

**Informations d’identification nCipher nShield HSM**

Lors de l’utilisation d’informations d’identification HSM nCipher nShield pour signer ou certifier un PDF, les nouvelles informations d’identification ne peuvent pas être utilisées tant que le serveur d’applications J2EE sur lequel AEM Forms est déployé n’a pas été redémarré. Cependant, vous pouvez définir une valeur de configuration, ce qui entraîne le fonctionnement de l’opération de signature ou de certification sans redémarrer le serveur d’applications J2EE.

Vous pouvez ajouter la valeur de configuration suivante dans le fichier cknfastrc, qui se trouve dans /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc) :

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Après avoir ajouté cette valeur de configuration au fichier cknfastrc, vous pouvez utiliser les nouvelles informations d’identification sans redémarrer le serveur d’applications J2EE.

**Signature non approuvée**

Lors de la certification et de la signature du même PDF, si la signature de certification n’est pas approuvée, un triangle jaune apparaît par rapport à la première signature lors de l’ouverture du PDF  dans Acrobat ou Adobe Reader. La signature de certification doit être approuvée pour éviter cette situation.

**de signature de formulaires XFA**

Si vous tentez de signer un formulaire XFA à l’aide de l’API du service Signature, il se peut que les données soient absentes du formulaire `View``Signed` `Version` situé dans Acrobat. Prenons l’exemple du processus suivant :

* A l’aide d’un fichier XDP créé à l’aide de Designer, vous fusionnez une conception de formulaire contenant un champ de signature et des données XML contenant des données de formulaire. Utilisez le service Forms pour générer un PDF interactif.
* Vous signez le PDF à l’aide de l’API du service Signature.

### Résumé des étapes {#summary_of_steps-3}

Pour signer numériquement un  PDF, effectuez l’ de suivante :

1. Incluez des fichiers de projet.
1. Créez un client de service Signature.
1. Demandez au PDF de signer.
1. Signez le  PDF.
1. Enregistrez le  PDF signé au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un client Signatures**

Avant de pouvoir exécuter une opération du service Signature par programmation, vous devez créer un client du service Signature.

**Obtenir le PDF à signer**

Pour signer un  PDF, vous devez obtenir un PDF  contenant un champ de signature. Si un PDF ne contient pas de champ de signature, il ne peut pas être signé. Un champ de signature peut être ajouté à l’aide de Designer ou par programmation.

**Signature du PDF**

Lors de la signature d’un  PDF, vous pouvez définir les options d’exécution utilisées par le service Signature. Vous pouvez définir les options suivantes :

* Options d’aspect
* Vérification de révocation
* Valeurs d’horodatage

Vous définissez les options d’aspect à l’aide d’un `PDFSignatureAppearanceOptionSpec` objet. Par exemple, vous pouvez afficher la date dans une signature en appelant la `PDFSignatureAppearanceOptionSpec` méthode de l’objet et en transmettant `setShowDate` `true`.

Vous pouvez également indiquer si une vérification de révocation doit être effectuée afin de déterminer si le certificat utilisé pour signer numériquement un PDF a été révoqué. Pour effectuer une vérification de révocation, vous pouvez spécifier l’une des valeurs suivantes :

* **NoCheck**: N’effectuez pas de vérification de révocation.
* **BestEffort**: Essayez toujours de vérifier la révocation de tous les certificats de la chaîne. En cas de problème lors de la vérification, la révocation est considérée comme valide. En cas d’échec, supposons que le certificat n’est pas révoqué.
* **CheckIfAvailable :** Vérifiez la révocation de tous les certificats de la chaîne si des informations de révocation sont disponibles. En cas de problème lors de la vérification, la révocation est considérée comme non valide. En cas d’échec, supposons que le certificat est révoqué et non valide. (Il s’agit de la valeur par défaut.)
* **AlwaysCheck**: Vérifiez la révocation de tous les certificats de la chaîne. Si les informations de révocation ne figurent dans aucun certificat, la révocation est considérée comme non valide.

Pour effectuer une vérification de révocation sur un certificat, vous pouvez spécifier une URL vers un serveur CRL (Certificate Revocation) à l’aide d’un `CRLOptionSpec` objet. Toutefois, si vous souhaitez effectuer une vérification de révocation et que vous ne spécifiez pas d’URL vers un serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP plutôt qu’un serveur CRL, la vérification de révocation est effectuée plus rapidement. (Voir &quot;Protocole d’état du certificat en ligne&quot; à l’adresse [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir l’ordre CRL et OCSP Server que le service Signature utilise à l’aide des applications et services Adobe. Par exemple, si le serveur OCSP est défini en premier dans les applications et services Adobe, le serveur OCSP est coché, suivi du serveur CRL. (voir &quot;Gestion des certificats et des informations d’identification à l’aide de Trust Store&quot; dans l’aide AAC).

Si vous indiquez de ne pas effectuer la vérification de révocation, le service Signature ne vérifie pas si le certificat utilisé pour signer ou certifier un  a été révoqué. En d’autres termes, les informations sur les CRL et les serveurs OCSP sont ignorées.

>[!NOTE]
>
>Bien qu’une liste CRL ou un serveur OCSP puisse être spécifié dans le certificat, vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’un objet `CRLOptionSpec` et d’un `OCSPOptionSpec` objet. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la `CRLOptionSpec` `setLocalURI` méthode de l’objet.

L’horodatage fait référence au processus de suivi de l’heure de modification d’un signé ou certifié. Une fois qu’un  est signé, il ne doit pas être modifié, même par le propriétaire de l’. L’horodatage permet de garantir la validité d’un  signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un `TSPOptionSpec` objet. Par exemple, vous pouvez spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>Dans les sections Java et Web du service, puis dans le  rapide correspondant, la vérification de révocation est utilisée. Aucune information CRL ou OCSP n’étant spécifiée, les informations du serveur sont obtenues à partir du certificat utilisé pour signer numériquement le  PDF.

Pour signer un  PDF, vous pouvez spécifier le nom complet du champ de signature qui contiendra la signature numérique, par exemple `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, le nom partiel du champ de signature peut également être utilisé : `SignatureField3[3]`.

Vous devez également référencer des informations d’identification de sécurité pour signer numériquement un PDF. Pour référencer des informations d’identification de sécurité, vous spécifiez un alias. L’alias est une référence à des informations d’identification réelles qui peuvent se trouver dans un fichier PKCS#12 (avec une extension .pfx) ou un module de sécurité matérielle (HSM). Pour plus d’informations sur les informations d’identification de sécurité, voir le guide *Installation et déploiement d’AEM Forms* pour votre serveur d’applications.

**Enregistrer le PDF signé**

Une fois que le service Signature a signé numériquement le  PDF, vous pouvez l’enregistrer au format PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Signer numériquement le PDF à l’aide de l’API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Signature numérique d’un PDF à l’aide de l’API du service Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout de champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

[Récupération des noms des champs de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Signer numériquement le PDF à l’aide de l’API Java {#digitally-sign-pdf-documents-using-the-java-api}

Signez numériquement un PDF à l’aide de l’API de signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signatures

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le PDF à signer

   * Créez un `java.io.FileInputStream` objet représentant le PDF à signer numériquement à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Signature du PDF 

   Signez le PDF en appelant la `SignatureServiceClient` `sign` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `com.adobe.idp.Document` object that represents the PDF document to sign.
   * Valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature numérique.
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. Créez un `Credential` objet en appelant la `Credential` méthode statique de l’ `getInstance` objet et en transmettant une valeur de chaîne qui spécifie la valeur d’alias correspondant aux informations d’identification de sécurité.
   * Objet `HashAlgorithm` spécifiant un membre de données statique représentant l’algorithme de hachage à utiliser pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été signé numériquement.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Objet `java.lang.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation.
   * Objet `OCSPOptionSpec` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`. For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   La `sign` méthode renvoie un `com.adobe.idp.Document` objet représentant le  PDF signé.

1. Enregistrer le PDF signé 

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `sign`.

**Voir également**

[de signature numérique de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[rapide (mode SOAP) : Signature numérique d’un PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signature numérique d’un PDF à l’aide de l’API du service Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Pour signer numériquement un PDF à l’aide de l’API de signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signatures

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le PDF à signer

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF signé.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à signer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Signature du PDF 

   Signez le PDF en appelant la `SignatureServiceClient` `sign` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `BLOB` object that represents the PDF document to sign.
   * Valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature numérique.
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. Créez un `Credential` objet à l’aide de son constructeur et spécifiez l’alias en affectant une valeur à la `Credential` `alias` propriété de l’objet.
   * Objet `HashAlgorithm` spécifiant un membre de données statique représentant l’algorithme de hachage à utiliser pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur booléenne qui spécifie si l’algorithme de hachage est utilisé.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été signé numériquement.
   * Valeur de chaîne représentant l’emplacement du signataire.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Objet `System.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation. Si cette vérification de révocation est effectuée, elle est incorporée dans la signature. La valeur par défaut est `false`.
   * Objet `OCSPOptionSpec` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.
   La `sign` méthode renvoie un `BLOB` objet représentant le  PDF signé.

1. Enregistrer le PDF signé 

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du  PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `sign` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[de signature numérique de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Signature numérique de formulaires interactifs {#digitally-signing-interactive-forms}

Vous pouvez signer un formulaire interactif que le service Forms crée. Prenons l’exemple du processus suivant :

* Vous fusionnez un formulaire PDF XFA créé à l’aide de Designer et des données de formulaire situées dans un XML à l’aide du service Forms. Le serveur Forms génère un formulaire interactif.
* Vous signez le formulaire interactif à l’aide de l’API du service Signature.

Le résultat est un formulaire PDF interactif signé numériquement. Lors de la signature d’un formulaire PDF basé sur un formulaire XFA, veillez à enregistrer le fichier PDF en tant que formulaire PDF statique Adobe. Si vous tentez de signer un formulaire PDF enregistré en tant que formulaire PDF dynamique Adobe, une exception se produit. Etant donné que vous signez le formulaire renvoyé par le service Forms, assurez-vous que le formulaire contient un champ de signature.

>[!NOTE]
>
>Avant de pouvoir signer numériquement un formulaire interactif, vous devez vous assurer d’ajouter le certificat à AEM Forms. Un certificat est ajouté à l’aide d’Administration Console ou par programmation à l’aide de l’API Trust Manager. (voir [Importation des informations d’identification à l’aide de l’API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)Trust Manager).

Lors de l’utilisation de l’API Forms Service, définissez l’option `GenerateServerAppearance` d’exécution sur `true`. Cette option d’exécution garantit que l’aspect du formulaire généré sur le serveur reste valide lorsqu’il est ouvert dans Acrobat ou Adobe Reader. Il est recommandé de définir cette option d’exécution lors de la génération d’un formulaire interactif à signer à l’aide de l’API Forms.

>[!NOTE]
>
>Avant de lire Signature numérique de formulaires interactifs, nous vous recommandons de vous familiariser avec la signature de  PDF. (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Résumé des étapes {#summary_of_steps-4}

Pour signer numériquement un formulaire interactif renvoyé par le service Forms, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un client Forms et Signatures.
1. Obtenez le formulaire interactif à l’aide du service Forms.
1. Signez le formulaire interactif.
1. Enregistrez le  PDF signé au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Forms et Signatures**

Ce flux de travaux invoque les services Forms et Signature. Vous devez donc créer un client de service Forms et un client de service Signature.

**Obtention du formulaire interactif à l’aide du service Forms**

Vous pouvez utiliser le service Forms pour obtenir le formulaire PDF interactif à signer. Depuis AEM Forms, vous pouvez transmettre un `com.adobe.idp.Document` objet au service Forms qui contient le formulaire à rendre. Le nom de cette méthode est `renderPDFForm2`. Cette méthode renvoie un `com.adobe.idp.Document` objet contenant le formulaire à signer. Vous pouvez transmettre cette `com.adobe.idp.Document` instance au service Signature.

De même, si vous utilisez des services Web, vous pouvez transmettre l’ `BLOB` instance que le service Forms renvoie au service Signature.

>[!NOTE]
>
>Le rapide associé à la section Signature numérique de formulaires interactifs appelle la `renderPDFForm2` méthode.

**Signature du formulaire interactif**

Lors de la signature d’un  PDF, vous pouvez définir les options d’exécution utilisées par le service Signature. Vous pouvez définir les options suivantes :

* Options d’aspect
* Vérification de révocation
* Valeurs d’horodatage

Vous définissez les options d’aspect à l’aide d’un `PDFSignatureAppearanceOptionSpec` objet. Par exemple, vous pouvez afficher la date dans une signature en appelant la `PDFSignatureAppearanceOptionSpec` méthode de l’objet et en transmettant `setShowDate` `true`.

**Enregistrer le PDF signé**

Une fois que le service Signature a signé numériquement le  PDF, vous pouvez l’enregistrer au format PDF. Le fichier PDF peut être ouvert dans Acrobat ou Adobe Reader.

**Voir également**

[Signature numérique d’un formulaire interactif à l’aide de l’API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Signature numérique d’un formulaire interactif à l’aide de l’API du service Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[de signature numérique de PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Rendu de formulaires PDF interactifs](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Signature numérique d’un formulaire interactif à l’aide de l’API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Signez numériquement un formulaire interactif à l’aide de l’API Forms et Signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar et adobe-forms-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Forms et Signatures

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtention du formulaire interactif à l’aide du service Forms

   * Créez un `java.io.FileInputStream` objet représentant le PDF à transmettre au service Forms à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un `java.io.FileInputStream` objet représentant le XML qui contient les données de formulaire à transmettre au service Forms à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un `PDFFormRenderSpec` objet utilisé pour définir les options d’exécution. Appelez la `PDFFormRenderSpec` méthode de l’ `setGenerateServerAppearance` objet et passez `true`.
   * Appelez la méthode `FormsServiceClient` `renderPDFForm2` de l’objet et transmettez les valeurs suivantes :

      * Objet `com.adobe.idp.Document` contenant le formulaire PDF à générer.
      * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire.
      * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
      * Objet `URLSpec` contenant des valeurs URI requises par le service Forms. Vous pouvez spécifier `null` cette valeur de paramètre.
      * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
      La `renderPDFForm2` méthode renvoie un `FormsResult` objet contenant un flux de données de formulaire.

   * Récupérez le formulaire PDF en appelant la `FormsResult` `getOutputContent` méthode de l’objet. Cette méthode renvoie un `com.adobe.idp.Document` objet qui représente le formulaire interactif.


1. Signature du formulaire interactif

   Signez le PDF en appelant la `SignatureServiceClient` `sign` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `com.adobe.idp.Document` object that represents the PDF document to sign. Assurez-vous que cet objet est l’ `com.adobe.idp.Document` objet obtenu du service Forms.
   * Valeur de chaîne qui représente le nom du champ de signature signé.
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. Créez un `Credential` objet en appelant la `Credential` méthode statique de l’ `getInstance` objet. Transmettez une valeur de chaîne qui spécifie la valeur d’alias qui correspond aux informations d’identification de sécurité.
   * Objet `HashAlgorithm` spécifiant un membre de données statique représentant l’algorithme de hachage à utiliser pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été signé numériquement.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Objet `java.lang.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation.
   * Objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.
   La `sign` méthode renvoie un `com.adobe.idp.Document` objet représentant le  PDF signé.

1. Enregistrer le PDF signé 

   * Create a `java.io.File` object and ensure that the filename extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. Veillez à utiliser l’ `com.adobe.idp.Document` objet renvoyé par la `sign` méthode.

**Voir également**

[Signature numérique de formulaires interactifs](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[rapide (mode SOAP) : Signature numérique d’un PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signature numérique d’un formulaire interactif à l’aide de l’API du service Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Signez numériquement un formulaire interactif à l’aide de l’API Forms et Signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Comme cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Signature : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Forms : `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Le type de `BLOB` données étant commun aux deux références de service, qualifiez pleinement le type de `BLOB` données lors de son utilisation. Dans le  rapide du service Web correspondant, toutes les `BLOB` instances sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Forms et Signatures

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Répétez ces étapes pour le client du service Forms.

1. Obtention du formulaire interactif à l’aide du service Forms

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF signé.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à signer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.
   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker les données de formulaire.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier XML contenant les données du formulaire et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.
   * Créez un `PDFFormRenderSpec` objet utilisé pour définir les options d’exécution. Attribuez la valeur `true` au `PDFFormRenderSpec` `generateServerAppearance` champ de l’objet.
   * Appelez la méthode `FormsServiceClient` `renderPDFForm2` de l’objet et transmettez les valeurs suivantes :

      * Objet `BLOB` contenant le formulaire PDF à générer.
      * Objet `BLOB` contenant des données à fusionner avec le formulaire.
      * Objet `PDFFormRenderSpec` qui stocke les options d’exécution.
      * Objet `URLSpec` contenant des valeurs URI requises par le service Forms. Vous pouvez spécifier `null` cette valeur de paramètre.
      * Objet `java.util.HashMap` qui stocke les pièces jointes. Il s’agit d’un paramètre facultatif que vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
      * Paramètre de sortie long utilisé pour stocker le nombre de pages dans le formulaire.
      * Paramètre de sortie de chaîne utilisé pour la valeur du paramètre régional.
      * Valeur `FormResult` du paramètre de sortie utilisé pour stocker le formulaire interactif.
   * Supprimez le formulaire PDF en appelant le `FormsResult` `outputContent` champ de l’objet. Ce champ stocke un `BLOB` objet qui représente le formulaire interactif.


1. Signature du formulaire interactif

   Signez le PDF en appelant la `SignatureServiceClient` `sign` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `BLOB` object that represents the PDF document to sign. Utilisez l’ `BLOB` instance renvoyée par le service Forms.
   * Valeur de chaîne qui représente le nom du champ de signature signé.
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. Créez un `Credential` objet à l’aide de son constructeur et spécifiez l’alias en affectant une valeur à la `Credential` `alias` propriété de l’objet.
   * Objet `HashAlgorithm` spécifiant un membre de données statique représentant l’algorithme de hachage à utiliser pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur booléenne qui spécifie si l’algorithme de hachage est utilisé.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été signé numériquement.
   * Valeur de chaîne représentant l’emplacement du signataire.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Objet `System.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation. Si cette vérification de révocation est effectuée, elle est incorporée dans la signature. La valeur par défaut est `false`.
   * Objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.
   La `sign` méthode renvoie un `BLOB` objet représentant le  PDF signé.

1. Enregistrer le PDF signé 

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du  PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `sign` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Signature numérique de formulaires interactifs](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certification de documents PDF {#certifying-pdf-documents}

Vous pouvez définir un document PDF en le certifiant avec un type de signature particulier appelé signature certifiée. Une signature certifiée se différencie d’une signature numérique de plusieurs manières :

* Elle doit être la première signature appliquée au document PDF ; cela veut dire que lorsque la signature certifiée est appliquée, tous les autres champs de signature du document doivent être non signés. Une seule signature certifiée est autorisée dans un document PDF. Si vous souhaitez signer ou certifier un document PDF, vous devez le certifier avant de le signer. Après avoir certifié un document PDF, vous pouvez signer numériquement les champs de signature supplémentaires.
* L’auteur ou l’expéditeur du document peut indiquer que le document peut être modifié de certaines manières sans invalider la signature certifiée. Par exemple, le document peut autoriser le remplissage de formulaires ou de commentaires. Si l’auteur spécifie qu’une modification spécifique est autorisée, Acrobat limite ainsi les utilisateurs dans la modification du document. Si ces modifications sont effectuées, à l’aide d’une autre application par exemple, la signature certifiée est alors non valide et Acrobat affiche un avertissement à l’ouverture du document. (Avec des signatures non certifiées, les modifications ne sont pas empêchées et les opérations normales de modification n’invalident pas la signature d’origine.)
* Au moment de la signature, les différents types de contenus du document susceptibles de rendre le document ambigu ou trompeur sont analysés. Par exemple, une annotation peut assombrir du texte sur une page qui est essentiel pour comprendre ce qui est certifié. Une explication (attestation légale) peut être fournie pour un type de contenu.

Vous pouvez programmer la certification des PDF à l’aide de l’API Java du service Signature ou de l’API du service Web Signature. Lors de la certification d’un PDF, vous devez référencer des informations d’identification de sécurité qui existent dans le service d’informations d’identification. Pour plus d’informations sur les informations d’identification de sécurité, voir le guide *Installation et déploiement d’AEM Forms* pour votre serveur d’applications.

>[!NOTE]
>
>Lors de la certification et de la signature du même  PDF, si la signature de certification n’est pas approuvée, un triangle jaune apparaît en regard de la signature du premier signe lorsque vous ouvrez le PDF  dans Acrobat ou Adobe Reader. La signature de certification doit être approuvée pour éviter cette situation.

>[!NOTE]
>
>Lors de l’utilisation d’informations d’identification HSM nCipher nShield pour signer ou certifier un PDF, les nouvelles informations d’identification ne peuvent pas être utilisées tant que le serveur d’applications J2EE sur lequel AEM Forms est déployé n’a pas été redémarré. Cependant, vous pouvez définir une valeur de configuration, ce qui entraîne le fonctionnement de l’opération de signature ou de certification sans redémarrer le serveur d’applications J2EE.

Vous pouvez ajouter la valeur de configuration suivante dans le fichier cknfastrc, qui se trouve dans /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc) :

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Après avoir ajouté cette valeur de configuration au fichier cknfastrc, vous pouvez utiliser les nouvelles informations d’identification sans redémarrer le serveur d’applications J2EE.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la certification d’un , voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-5}

Pour certifier un  PDF, effectuez l’ de suivante :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le PDF à certifier.
1. Certifiez le  PDF.
1. Enregistrez le  PDF certifié au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant de pouvoir exécuter une opération Signature par programmation, vous devez créer un client Signature.

**Obtention du PDF à certifier**

Pour certifier un  PDF, vous devez obtenir un PDF  contenant un champ de signature. Si un PDF ne contient pas de champ de signature, il ne peut pas être certifié. Un champ de signature peut être ajouté à l’aide de Designer ou par programmation. Pour plus d’informations sur l’ajout programmatique d’un champ de signature, voir [Ajout de champs](digitally-signing-certifying-documents.md#adding-signature-fields)de signature.

**Certifier le PDF**

Pour réussir la certification d’un  PDF, vous avez besoin des valeurs d’entrée suivantes, utilisées par le service Signature, pour certifier un PDF  :

* **** PDF : PDF contenant un champ de signature, qui est un champ de formulaire contenant une représentation graphique de la signature certifiée. Un PDF doit contenir un champ de signature pour pouvoir être certifié. Un champ de signature peut être ajouté à l’aide de Designer ou par programmation. (Voir [Ajout de champs](digitally-signing-certifying-documents.md#adding-signature-fields)de signature.)
* **Nom** du champ de signature : Nom qualifié complet du champ de signature certifié. La valeur suivante est un exemple : `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, le nom partiel du champ de signature peut également être utilisé : `SignatureField3[3]`. Si une valeur nulle est transmise pour le nom du champ, un champ de signature invisible est créé et certifié de manière dynamique.
* **Informations d’identification** de sécurité : Informations d’identification utilisées pour certifier le  PDF. Ces informations d’identification de sécurité contiennent un mot de passe et un alias, qui doivent correspondre à un alias qui apparaît dans les informations d’identification situées dans le service d’informations d’identification. L’alias est une référence à des informations d’identification réelles qui peuvent se trouver dans un fichier PKCS#12 (avec une extension .pfx) ou un module de sécurité matérielle (HSM).
* **Algorithme** de hachage : Algorithme de hachage à utiliser pour digérer le PDF.
* **Raison de la signature**: Valeur affichée dans Acrobat ou Adobe Reader afin que les autres utilisateurs connaissent la raison pour laquelle le PDF a été certifié.
* **Emplacement du signataire**: Emplacement du signataire spécifié par les informations d’identification.
* **Coordonnées**: Coordonnées, telles que l’adresse et le numéro de téléphone, du signataire.
* **Informations** sur les autorisations : Autorisations qui contrôlent les actions qu’un utilisateur final peut effectuer sur un  sans que la signature certifiée ne soit incorrecte. Par exemple, vous pouvez définir l’autorisation de sorte que toute modification apportée au PDF entraîne la non-validité de la signature certifiée.
* **Explication** juridique : Lorsqu’un est certifié, il est automatiquement analysé à la recherche de types de contenu spécifiques susceptibles de rendre le contenu d’un  ambigu ou trompeur. Par exemple, une annotation peut assombrir du texte sur une page qui est essentiel pour comprendre ce qui est certifié. Le processus d’analyse génère des avertissements concernant ces types de contenu. Cette valeur fournit une explication supplémentaire du contenu susceptible d’avoir généré des avertissements.
* **Options** d’aspect : Options qui contrôlent l’aspect de la signature certifiée. Par exemple, la signature certifiée peut afficher des informations sur la date.
* **Vérification** de révocation : Cette valeur indique si la vérification de révocation est effectuée pour le certificat du signataire. Le paramètre par défaut de `false` signifie que la vérification de révocation n’est pas effectuée.
* **Paramètres** OCSP : Paramètres de prise en charge du protocole OCSP (Online Certificate Status Protocol), qui fournit des informations sur l’état des informations d’identification utilisées pour certifier le PDF. Vous pouvez, par exemple, spécifier l’URL du serveur qui fournit des informations sur les informations d’identification que vous utilisez pour vous connecter au PDF .
* **Paramètres** CRL : Paramètres des préférences de de révocation de certificats (CRL) si la vérification de révocation est effectuée. Par exemple, vous pouvez spécifier de toujours vérifier si les informations d’identification ont été révoquées.
* **Horodatage**: Paramètres qui définissent les informations d’horodatage appliquées à la signature certifiée. Un horodatage indique que des données spécifiques ont été établies avant un certain temps. Ces connaissances permettent de bâtir une relation de confiance entre le signataire et le vérificateur.

**Enregistrer le PDF certifié en tant que fichier PDF**

Une fois que le service Signature a certifié le  PDF, vous pouvez l’enregistrer au format PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Certifier le PDF à l’aide de l’API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certifier le PDF à l’aide de l’API du service Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout de champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certifier le PDF à l’aide de l’API Java {#certify-pdf-documents-using-the-java-api}

Certifier un PDF à l’aide de l’API Signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtention du PDF à certifier

   * Créez un `java.io.FileInputStream` objet représentant le PDF à certifier à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Certifier le PDF 

   Certifiez le PDF en appelant la `SignatureServiceClient` méthode de l’ `certify` objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le PDF à certifier.
   * Valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature.
   * A `Credential` object that represents the credential that is used to certify the PDF document. Créez un `Credential` objet en appelant la `Credential` méthode statique de l’ `getInstance` objet et en transmettant une valeur de chaîne qui spécifie la valeur d’alias correspondant aux informations d’identification de sécurité.
   * Objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage utilisé pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été certifié.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Objet `MDPPermissions` spécifiant les actions qui peuvent être exécutées sur le PDF et qui invalide la signature.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature certifiée. Si vous le souhaitez, modifiez l’aspect de la signature en appelant une méthode, telle que `setShowDate`.
   * Valeur de chaîne qui fournit une explication des actions qui invalident la signature.
   * Objet `java.lang.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation. Si cette vérification de révocation est effectuée, elle est incorporée dans la signature. La valeur par défaut est `false`.
   * Objet `java.lang.Boolean` spécifiant si le champ de signature en cours de certification est verrouillé. Si le champ est verrouillé, le champ de signature est marqué en lecture seule, ses propriétés ne peuvent pas être modifiées et il ne peut pas être effacé par quiconque ne dispose pas des autorisations requises. La valeur par défaut est `false`.
   * Objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir Référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Par exemple, après avoir créé un `TSPPreferences` objet, vous pouvez définir l’URL du serveur TSP en appelant la `TSPPreferences` `setTspServerURL` méthode de l’objet. Ce paramètre est facultatif et peut être `null`. For more information, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).
   La `certify` méthode renvoie un `com.adobe.idp.Document` objet qui représente le  PDF certifié.

1. Enregistrer le PDF certifié en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.

**Voir également**

[Certification de documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[rapide (mode SOAP) : Certification d’un PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certifier le PDF à l’aide de l’API du service Web {#certify-pdf-documents-using-the-web-service-api}

Certifier un PDF à l’aide de l’API Signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtention du PDF à certifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF certifié.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF à certifier et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant à son `MTOM` membre de données le contenu du tableau d’octets.

1. Certifier le PDF 

   Certifiez le PDF en appelant la `SignatureServiceClient` méthode de l’ `certify` objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` représentant le PDF à certifier.
   * Valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature.
   * A `Credential` object that represents the credential that is used to certify the PDF document. Créez un `Credential` objet à l’aide de son constructeur, puis spécifiez l’alias en affectant une valeur à la `Credential` `alias` propriété de l’objet.
   * Objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage utilisé pour digérer le PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` d’utiliser l’algorithme SHA1.
   * Valeur booléenne qui spécifie si l’algorithme de hachage est utilisé.
   * Valeur de chaîne qui représente la raison pour laquelle le PDF a été certifié.
   * Valeur de chaîne représentant l’emplacement du signataire.
   * Valeur de chaîne représentant les coordonnées du signataire.
   * Membre de données statiques d’un `MDPPermissions` objet qui spécifie les actions pouvant être exécutées sur le PDF qui invalident la signature.
   * Valeur booléenne qui spécifie si l’ `MDPPermissions` objet transmis comme valeur de paramètre précédente doit être utilisé.
   * Valeur de chaîne qui explique les actions qui invalident la signature.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature certifiée. Créez un objet `PDFSignatureAppearanceOptions` en utilisant son constructeur. Vous pouvez modifier l’aspect de la signature en définissant l’un de ses membres de données.
   * Objet `System.Boolean` spécifiant si le certificat du signataire doit faire l’objet d’une vérification de révocation. Si cette vérification de révocation est effectuée, elle est incorporée dans la signature. La valeur par défaut est `false`.
   * Objet `System.Boolean` spécifiant si le champ de signature en cours de certification est verrouillé. Si le champ est verrouillé, le champ de signature est marqué en lecture seule, ses propriétés ne peuvent pas être modifiées et il ne peut pas être effacé par quiconque ne dispose pas des autorisations requises. La valeur par défaut est `false`.
   * Objet `System.Boolean` spécifiant si le champ de signature est verrouillé. En d’autres termes, si vous passez `true` au paramètre précédent, passez `true` à ce paramètre.
   * Objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol), qui fournit des informations sur l’état des informations d’identification utilisées pour certifier le PDF. Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` qui stocke les préférences du de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` qui stocke les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Par exemple, après avoir créé un `TSPPreferences` objet, vous pouvez définir l’URL du fournisseur de services de télécommunication en définissant le membre `TSPPreferences` de données de l’ `tspServerURL` objet. Ce paramètre est facultatif et peut être `null`.
   La `certify` méthode renvoie un `BLOB` objet qui représente le  PDF certifié.

1. Enregistrer le PDF certifié en tant que fichier PDF

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du PDF qui contiendra le PDF certifié et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `certify` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `binaryData` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Certification de documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Digital Signatures {#verifying-digital-signatures}

Les signatures numériques peuvent être vérifiées pour vous assurer qu’un document PDF signé n’a pas été modifié et que la signature numérique est valide. Lors de la vérification d’une signature numérique, vous pouvez vérifier l’état de la signature et ses propriétés, telles que l’identité du signataire. Avant d’approuver une signature numérique, il est recommandé de la vérifier. Lors de la vérification d’une signature numérique, référencez un document PDF contenant une signature numérique.

Supposons que l’identité du signataire soit inconnue. Lorsque vous ouvrez le PDF dans Acrobat, un message d’avertissement indique que l’identité du signataire est inconnue, comme illustré ci-dessous.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

De même, lorsque vous vérifiez par programmation une signature numérique, vous pouvez déterminer l’état de l’identité du signataire. Par exemple, si vous vérifiez la signature numérique dans le  du illustré ci-dessus, l’identité du signataire est inconnue.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la vérification des signatures numériques, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-6}

Pour vérifier une signature numérique, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le PDF qui contient la signature à vérifier.
1. Définissez les options d’exécution PKI.
1. Vérifiez la signature numérique.
1. Déterminez l’état de la signature.
1. Déterminez l’identité du signataire.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant d’effectuer une opération de service Signature par programmation, créez un client de service Signature.

**Obtenez le  PDF contenant la signature à vérifier**

Pour vérifier une signature utilisée pour signer numériquement ou certifier un PDF, obtenez un PDF  contenant une signature.

**Définition des options d’exécution PKI**

Définissez les options d’exécution PKI que le service Signature utilise lors de la vérification des signatures dans un PDF :

* Heure de vérification
* Vérification de révocation
* Valeurs d’horodatage

Dans le cadre de la définition de ces options, vous pouvez spécifier l’heure de vérification. Par exemple, vous pouvez sélectionner l’heure actuelle (l’heure sur l’ordinateur du validateur), qui indique d’utiliser l’heure actuelle. Pour plus d’informations sur les différentes valeurs d’heure, voir la `VerificationTime` valeur  dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

Vous pouvez également indiquer si la vérification de révocation doit être effectuée dans le cadre du processus de vérification. Par exemple, vous pouvez effectuer une vérification de révocation pour déterminer si le certificat est révoqué. Pour plus d’informations sur les options de vérification de révocation, voir la valeur de  `RevocationCheckStyle` dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

Pour effectuer une vérification de révocation sur un certificat, spécifiez une URL vers un serveur CRL (Certificate Revocation) à l’aide d’un `CRLOptionSpec` objet. Toutefois, si vous ne spécifiez pas d’URL vers le serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP plutôt qu’un serveur CRL, la vérification de révocation est effectuée plus rapidement. (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir l’ordre CRL et OCSP du serveur utilisé par le service Signature à l’aide des applications et services Adobe. Par exemple, si le serveur OCSP est défini en premier dans les applications et services Adobe, le serveur OCSP est coché, suivi du serveur CRL.

Si vous n’effectuez pas de vérification de révocation, le service Signature ne vérifie pas si le certificat est révoqué. En d’autres termes, les informations sur les CRL et les serveurs OCSP sont ignorées.

>[!NOTE]
>
>Vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’un `CRLOptionSpec` objet et d’un `OCSPOptionSpec` objet. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la `CRLOptionSpec` `setLocalURI` méthode de l’objet.

L’horodatage est le processus de suivi de l’heure de modification d’un signé ou certifié. Une fois qu’un a été signé, personne ne peut le modifier. L’horodatage permet de garantir la validité d’un  signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un `TSPOptionSpec` objet. Par exemple, vous pouvez spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>Dans le  rapide Java et du service Web, l’heure de vérification est définie sur `VerificationTime.CURRENT_TIME` et la vérification de révocation est définie sur `RevocationCheckStyle.BestEffort`. Aucune information CRL ou OCSP n’étant spécifiée, les informations du serveur sont obtenues à partir du certificat.

**Vérification de la signature numérique**

Pour vérifier une signature, spécifiez le nom qualifié complet du champ de signature qui contient la signature, par exemple `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, vous pouvez également utiliser le nom partiel du champ de signature : `SignatureField3`.

Par défaut, le service Signature limite à 65 minutes la durée pendant laquelle un peut être signé après l’heure de validation. Si un utilisateur tente de vérifier une signature à l’heure actuelle et que l’heure de la signature est postérieure à l’heure actuelle et qu’elle est inférieure à 65 minutes, le service Signature ne crée pas d’erreur de vérification.

>[!NOTE]
>
>Pour connaître les autres valeurs requises lors de la vérification d’une signature, voir Référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Déterminer l’état de la signature**

Dans le cadre de la vérification d’une signature numérique, vous pouvez vérifier l’état de la signature.

**Déterminer l’identité du signataire**

Vous pouvez déterminer l’identité du signataire, qui peut être l’une des valeurs suivantes :

* **Inconnu**: Ce signataire est inconnu car la vérification du signataire ne peut pas être effectuée.
* **Approuvée**: Ce signataire est fiable.
* **Non approuvé**: Ce signataire n&#39;est pas approuvé.

**Voir également**

[Vérification des signatures numériques à l’aide de l’API Java](#verify-digital-signatures-using-the-java-api)

[Vérification des signatures numériques à l’aide de l’API du service Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérification des signatures numériques à l’aide de l’API Java {#verify-digital-signatures-using-the-java-api}

Vérifiez une signature numérique à l’aide de l’API Signature Service (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenez le  PDF contenant la signature à vérifier

   * Créez un `java.io.FileInputStream` objet représentant le PDF qui contient la signature à vérifier à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en appelant la `PKIOptions` méthode de l’ `setVerificationTime` objet et en transmettant une valeur de `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en appelant la `PKIOptions` méthode de l’ `setRevocationCheckStyle` objet et en transmettant une valeur de  `RevocationCheckStyle` qui indique s’il convient d’effectuer une vérification de révocation.

1. Vérification de la signature numérique

   Vérifiez la signature en appelant la `SignatureServiceClient` `verify2` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant un  PDF signé numériquement ou certifié.
   * Valeur de chaîne représentant le nom du champ de signature qui contient la signature à vérifier.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Une `VerifySPIOptions` instance contenant des informations SPI. Vous pouvez spécifier `null` ce paramètre.
   La `verify2` méthode renvoie un `PDFSignatureVerificationInfo` objet qui contient des informations pouvant être utilisées pour vérifier la signature numérique.

1. Déterminer l’état de la signature

   * Déterminez l’état de la signature en appelant la `PDFSignatureVerificationInfo` `getStatus` méthode de l’objet. Cette méthode renvoie un `SignatureStatus` objet qui spécifie l’état de la signature. Par exemple, si un PDF signé n’est pas modifié, cette méthode renvoie `SignatureStatus.DocumentSigNoChanges`.

1. Déterminer l’identité du signataire

   * Déterminez l’identité du signataire en appelant la `PDFSignatureVerificationInfo` `getSigner` méthode de l’objet. Cette méthode renvoie un `IdentityInformation` objet.
   * Appelez la méthode `IdentityInformation` `getStatus` de l’objet pour déterminer l’identité du signataire. Cette méthode renvoie une `IdentityStatus` valeur  qui spécifie l’identité. Par exemple, si le signataire est approuvé, cette méthode renvoie `IdentityStatus.TRUSTED`.

**Voir également**

[Vérification des signatures numériques](#verify-digital-signatures-using-the-java-api)

[rapide (mode SOAP) : Vérification d’une signature numérique à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérification des signatures numériques à l’aide de l’API du service Web {#verify-digital-signatures-using-the-web-service-api}

Vérifiez une signature numérique à l’aide de l’API Signature Service (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le  PDF contenant la signature à vérifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF contenant une signature numérique ou certifiée à vérifier.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du  PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Définition des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en affectant au membre `PKIOptions` de données de l’ `verificationTime` objet une valeur de  `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en affectant au membre `PKIOptions` de données de l’ `revocationCheckStyle` objet une valeur de  `RevocationCheckStyle` qui indique s’il convient d’effectuer une vérification de révocation.

1. Vérification de la signature numérique

   Vérifiez la signature en appelant la `SignatureServiceClient` `verify2` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant un PDF signé numériquement ou certifié.
   * Valeur de chaîne représentant le nom du champ de signature qui contient la signature à vérifier.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Une `VerifySPIOptions` instance contenant des informations SPI. Vous pouvez spécifier `null` ce paramètre.
   La `verify2` méthode renvoie un `PDFSignatureVerificationInfo` objet qui contient des informations pouvant être utilisées pour vérifier la signature numérique.

1. Déterminer l’état de la signature

   Déterminez l’état de la signature en obtenant la valeur du membre `PDFSignatureVerificationInfo` `status` de données de l’objet. Ce membre de données stocke un `SignatureStatus` objet qui spécifie l’état de la signature. Par exemple, si un PDF signé est modifié, le membre `status` de données stocke la valeur `SignatureStatus.DocumentSigNoChanges`.

1. Déterminer l’identité du signataire

   * Déterminez l’identité du signataire en récupérant la valeur du membre de `PDFSignatureVerificationInfo` `signer` données de l’objet. Ce membre renvoie un `IdentityInformation` objet.
   * Récupérez le membre `IdentityInformation` `status` de données de l’objet pour déterminer l’identité du signataire. Ce membre de données renvoie une `IdentityStatus` valeur  qui spécifie l’identité. Par exemple, si le signataire est approuvé, ce membre revient `IdentityStatus.TRUSTED`.

**Voir également**

[Vérification des signatures numériques](#verify-digital-signatures-using-the-java-api)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Multiple Digital Signatures {#verifying-multiple-digital-signatures}

AEM Forms permet de vérifier toutes les signatures numériques qui se trouvent dans un  PDF. Supposons qu’un PDF contienne plusieurs signatures numériques suite à un processus d’entreprise qui requiert des signatures de plusieurs signataires. Prenons l’exemple d’une transaction financière qui requiert à la fois la signature d’un agent de prêt et celle d’un gestionnaire. Vous pouvez utiliser l’API Java du service Signature ou l’API du service Web pour vérifier toutes les signatures dans le PDF. Lors de la vérification de plusieurs signatures numériques, vous pouvez vérifier l’état et les propriétés de chaque signature. Avant de faire confiance à une signature numérique, il est recommandé de la vérifier. Il est recommandé de savoir vérifier une signature numérique unique.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la vérification des signatures numériques, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-7}

Pour vérifier plusieurs signatures numériques, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le  PDF contenant les signatures à vérifier.
1. Définissez les options d’exécution PKI.
1. Récupérez toutes les signatures numériques.
1. Effectuez une itération sur toutes les signatures.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant d’effectuer une opération de service Signature par programmation, créez un client de service Signature.

**Obtenez le  PDF contenant les signatures à vérifier**

Pour vérifier une signature utilisée pour signer numériquement ou certifier un PDF, obtenez un PDF  contenant une signature.

**Définition des options d’exécution PKI**

Définissez les options d’exécution PKI que le service Signature utilise lors de la vérification de toutes les signatures dans un PDF :

* Heure de vérification
* Vérification de révocation
* Valeurs d’horodatage

Dans le cadre de la définition de ces options, vous pouvez spécifier l’heure de vérification. Par exemple, vous pouvez sélectionner l’heure actuelle (l’heure sur l’ordinateur du validateur), qui indique d’utiliser l’heure actuelle. Pour plus d’informations sur les différentes valeurs d’heure, voir la `VerificationTime` valeur  dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

Vous pouvez également indiquer si la vérification de révocation doit être effectuée dans le cadre du processus de vérification. Par exemple, vous pouvez effectuer une vérification de révocation pour déterminer si le certificat est révoqué. Pour plus d’informations sur les options de vérification de révocation, voir la valeur de  `RevocationCheckStyle` dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

Pour effectuer une vérification de révocation sur un certificat, spécifiez une URL vers un serveur CRL (Certificate Revocation) à l’aide d’un `CRLOptionSpec` objet. Toutefois, si vous ne spécifiez pas d’URL vers un serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP au lieu d’un serveur CRL, la vérification de révocation est effectuée plus rapidement. (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir l’ordre CRL et OCSP du serveur utilisé par le service Signature à l’aide des applications et services Adobe. Par exemple, si le serveur OCSP est défini en premier dans les applications et services Adobe, le serveur OCSP est coché, suivi du serveur CRL.

Si vous n’effectuez pas de vérification de révocation, le service Signature ne vérifie pas si le certificat est révoqué. En d’autres termes, les informations sur les CRL et les serveurs OCSP sont ignorées.

>[!NOTE]
>
>Vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’un `CRLOptionSpec` objet et d’un `OCSPOptionSpec` objet. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la `CRLOptionSpec` `setLocalURI` méthode de l’objet.

L’horodatage est le processus de suivi de l’heure de modification d’un signé ou certifié. Une fois qu’un a été signé, personne ne peut le modifier. L’horodatage permet de garantir la validité d’un  signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un `TSPOptionSpec` objet. Vous pouvez, par exemple, spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>Dans le  rapide Java et du service Web, l’heure de vérification est définie sur `VerificationTime.CURRENT_TIME` et la vérification de révocation est définie sur `RevocationCheckStyle.BestEffort`. Aucune information CRL ou OCSP n’étant spécifiée, les informations du serveur sont obtenues à partir du certificat.

**Récupérer toutes les signatures numériques**

Pour vérifier toutes les signatures numériques se trouvant dans un  PDF, récupérez les signatures numériques du PDF. Toutes les signatures sont renvoyées dans un  de. Dans le cadre de la vérification d’une signature numérique, vérifiez l’état de la signature.

>[!NOTE]
>
>Contrairement à la vérification d’une signature numérique unique, lorsque vous vérifiez plusieurs signatures, vous n’êtes pas tenu de spécifier le nom du champ de signature.

**Itérer toutes les signatures**

Effectuez une itération sur chaque signature. C’est-à-dire, pour chaque signature, vérifier la signature numérique et l’identité du signataire et l’état de chaque signature. (Voir [Vérification des signatures](#verify-digital-signatures-using-the-java-api)numériques.)

>[!NOTE]
>
>Vous n’avez pas besoin de parcourir toutes les signatures si l’exigence correspond à l’ensemble du  du.

**Voir également**

[Vérification de plusieurs signatures numériques à l’aide de l’API Java](#verify-digital-signatures-using-the-java-api)

[Vérification de plusieurs signatures numériques à l’aide de l’API du service Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérification de plusieurs signatures numériques à l’aide de l’API Java {#verify-multiple-digital-signatures-using-the-java-api}

Vérifiez plusieurs signatures numériques à l’aide de l’API Signature Service (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client Signature

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenez le  PDF contenant les signatures à vérifier

   * Créez un `java.io.FileInputStream` objet représentant le PDF qui contient plusieurs signatures numériques à vérifier à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du  PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en appelant la `PKIOptions` méthode de l’ `setVerificationTime` objet et en transmettant une valeur de `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en appelant la `PKIOptions` méthode de l’ `setRevocationCheckStyle` objet et en transmettant une valeur de  `RevocationCheckStyle` qui indique s’il convient d’effectuer une vérification de révocation.

1. Récupérer toutes les signatures numériques

   Appelez la méthode `SignatureServiceClient` `verifyPDFDocument` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant un PDF contenant plusieurs signatures numériques.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Une `VerifySPIOptions` instance contenant des informations SPI. Vous pouvez spécifier `null` ce paramètre.
   La `verifyPDFDocument` méthode renvoie un `PDFDocumentVerificationInfo` objet contenant des informations sur toutes les signatures numériques figurant dans le  PDF.

1. Itérer toutes les signatures

   * Interrompez toutes les signatures en appelant la `PDFDocumentVerificationInfo` `getVerificationInfos` méthode de l’objet. Cette méthode renvoie un `java.util.List` objet où chaque élément est un `PDFSignatureVerificationInfo` objet. Utilisez un `java.util.Iterator` objet pour effectuer une itération dans le de signatures.
   * L’ `PDFSignatureVerificationInfo` objet permet d’effectuer des , comme de déterminer l’état de la signature en appelant la `PDFSignatureVerificationInfo` méthode de l’ `getStatus` objet. Cette méthode renvoie un `SignatureStatus` objet dont le membre de données statiques vous informe sur l’état de la signature. Par exemple, si la signature est inconnue, cette méthode renvoie `SignatureStatus.DocumentSignatureUnknown`.

**Voir également**

[Vérification de plusieurs signatures numériques](#verifying-multiple-digital-signatures)

[rapide (mode SOAP) : Vérification de plusieurs signatures numériques à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Vérification des signatures numériques](#verify-digital-signatures-using-the-java-api)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérification de plusieurs signatures numériques à l’aide de l’API du service Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Vérifiez plusieurs signatures numériques à l’aide de l’API Signature Service (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenez le  PDF contenant les signatures à vérifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet stocke un PDF contenant plusieurs signatures numériques à vérifier.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier du  PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Définition des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en affectant au membre `PKIOptions` de données de l’ `verificationTime` objet une valeur de  `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en affectant au membre de `PKIOptions` données de l’ `revocationCheckStyle` objet une valeur de  `RevocationCheckStyle` qui indique s’il convient d’effectuer cette vérification.

1. Récupérer toutes les signatures numériques

   Appelez la méthode `SignatureServiceClient` `verifyPDFDocument` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant un PDF contenant plusieurs signatures numériques.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Une `VerifySPIOptions` instance contenant des informations SPI. Vous pouvez spécifier null pour ce paramètre.
   La `verifyPDFDocument` méthode renvoie un `PDFDocumentVerificationInfo` objet contenant des informations sur toutes les signatures numériques figurant dans le  PDF.

1. Itérer toutes les signatures

   * Parcourez toutes les signatures en obtenant le membre `PDFDocumentVerificationInfo` `verificationInfos` de données de l’objet. Ce membre de données renvoie un `Object` tableau où chaque élément est un `PDFSignatureVerificationInfo` objet.
   * L’ `PDFSignatureVerificationInfo` objet permet d’effectuer des  comme de déterminer l’état de la signature en obtenant le membre `PDFSignatureVerificationInfo` de données de l’ `status` objet. Ce membre de données renvoie un `SignatureStatus` objet dont le membre de données statique vous informe sur l’état de la signature. Par exemple, si la signature est inconnue, cette méthode renvoie `SignatureStatus.DocumentSignatureUnknown`.

**Voir également**

[Vérification de plusieurs signatures numériques](#verifying-multiple-digital-signatures)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removing Digital Signatures {#removing-digital-signatures}

Les signatures numériques doivent être supprimées d’un champ de signature pour qu’une signature numérique plus récente puisse être appliquée. Une signature numérique ne peut pas être remplacée. Si vous tentez d’appliquer une signature numérique à un champ de signature contenant une signature, une exception se produit.

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une signature numérique d’un champ de signature, effectuez le  suivant :

1. Incluez des fichiers de projet.
1. Créez un client Signature.
1. Obtenez le PDF contenant une signature à supprimer.
1. Supprimez la signature numérique du champ de signature.
1. Enregistrez le  PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, assurez-vous d’inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Signature**

Avant de pouvoir exécuter une opération du service Signature par programmation, vous devez créer un client du service Signature.

**Obtenir le PDF  contenant une signature à supprimer**

Pour supprimer une signature d’un  PDF, vous devez obtenir un PDF  contenant une signature.

**Supprimer la signature numérique du champ de signature**

Pour supprimer une signature numérique d’un  PDF, vous devez indiquer le nom du champ de signature qui contient la signature numérique. Vous devez également être autorisé à supprimer la signature numérique ; dans le cas contraire, une exception se produit.

**Enregistrer le  PDF en tant que fichier PDF**

Une fois que le service Signature a supprimé une signature numérique d’un champ de signature, vous pouvez enregistrer le PDF au format PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Suppression des signatures numériques à l’aide de l’API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Suppression des signatures numériques à l’aide de l’API du service Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajout de champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Suppression des signatures numériques à l’aide de l’API Java {#remove-digital-signatures-using-the-java-api}

Supprimez une signature numérique à l’aide de l’API Signature (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-signatures-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Signature.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le PDF  contenant une signature à supprimer

   * Créez un `java.io.FileInputStream` objet représentant le PDF qui contient la signature à supprimer à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimer la signature numérique du champ de signature

   Supprimez une signature numérique d’un champ de signature en appelant la `SignatureServiceClient` `clearSignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le PDF qui contient la signature à supprimer.
   * Valeur de chaîne qui spécifie le nom du champ de signature qui contient la signature numérique.
   La `clearSignatureField` méthode renvoie un `com.adobe.idp.Document` objet représentant le PDF à partir duquel la signature numérique a été supprimée.

1. Enregistrer le  PDF en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet. Transmettez l’ `java.io.File` objet pour copier le contenu de l’ `com.adobe.idp.Document` objet dans le fichier. Assurez-vous d’utiliser l’objet `Document` qui a été retourné par la méthode `clearSignatureField`.

**Voir également**

[Suppression des signatures numériques](digitally-signing-certifying-documents.md#removing-digital-signatures)

[rapide (mode SOAP) : Suppression d’une signature numérique à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Suppression des signatures numériques à l’aide de l’API du service Web {#remove-digital-signatures-using-the-web-service-api}

Supprimez une signature numérique à l’aide de l’API Signature (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un client Signature

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `SignatureServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le PDF  contenant une signature à supprimer

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF contenant une signature numérique à supprimer.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Supprimer la signature numérique du champ de signature

   Supprimez la signature numérique en appelant la `SignatureServiceClient` `clearSignatureField` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le  PDF signé.
   * Valeur de chaîne représentant le nom du champ de signature qui contient la signature numérique à supprimer.
   La `clearSignatureField` méthode renvoie un `BLOB` objet représentant le PDF à partir duquel la signature numérique a été supprimée.

1. Enregistrer le  PDF en tant que fichier PDF

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du PDF qui contient un champ de signature vide et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `sign` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Suppression des signatures numériques](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
