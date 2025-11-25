---
title: Signer numériquement et certifier des documents
description: Utilisez le service Signature pour ajouter et supprimer des champs de signature numérique à un document PDF, récupérer les noms des champs de signature d’un document PDF, modifier les champs de signature, signer numériquement des documents PDF, certifier des documents PDF, valider les signatures numériques d’un document PDF, valider toutes les signatures numériques d’un document PDF et supprimer une signature numérique d’un champ de signature.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '16916'
ht-degree: 99%

---

# Signer numériquement et certifier des documents {#digitally-signing-and-certifying-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Signature**

Le service Signature permet à votre entreprise de garantir la sécurité et la confidentialité des documents Adobe PDF qu’elle diffuse et reçoit. Ce service utilise les signatures numériques et la certification pour s’assurer que seuls les destinataires prévus peuvent modifier les documents. Les fonctions de sécurité étant appliquées au document lui-même, celui-ci reste sécurisé et contrôlé pendant tout son cycle de vie. Un document reste sécurisé au-delà du pare-feu lorsqu’il est téléchargé hors ligne et lorsqu’il est renvoyé à votre entreprise.

>[!NOTE]
>
>vous pouvez créer un gestionnaire de signatures personnalisé pour le service Signature qui est appelé lorsque certaines opérations sont réalisées, comme la signature d’un document PDF.

**Noms des champs de signature**

Certaines opérations du service Signature requièrent la spécification du nom du champ de signature sur lequel une opération est effectuée. Par exemple, lors de la signature d’un document PDF, vous spécifiez le nom du champ de signature à signer. Supposons que le nom complet d’un champ de signature soit `form1[0].Form1[0].SignatureField1[0]`. Vous pouvez indiquer `SignatureField1[0]` au lieu de `form1[0].Form1[0].SignatureField1[0]`.

Il arrive qu’en raison d’un conflit, le service Signature signe (ou effectue une autre opération nécessitant le nom du champ de signature) le mauvais champ. Ce conflit est le résultat du nom `SignatureField1[0]` apparaissant à plusieurs endroits dans le même document PDF. Prenons l’exemple d’un document PDF qui contient deux champs de signature nommés `form1[0].Form1[0].SignatureField1[0]` et `form1[0].Form1[0].SubForm1[0].SignatureField1[0]`, et vous spécifiez `SignatureField1[0]`. Dans ce cas, le service Signature signe le premier champ de signature qu’il détecte lors de l’itération sur tous les champs de signature du document.

Si plusieurs champs de signature sont situés dans un document PDF, il est recommandé de spécifier le nom complet des champs de signature. Autrement dit, spécifiez `form1[0].Form1[0].SignatureField1[0]` au lieu de `SignatureField1[0]`.

Vous pouvez accomplir les tâches suivantes à l’aide du service Signature :

* Ajouter et supprimer des champs de signature numérique à un document PDF. (Voir [Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Récupérer les noms des champs de signature d’un document PDF. (Voir [Récupérer les noms des champs de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modifier des champs de signature. (Voir [Modifier les champs de signature](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Signer numériquement des documents PDF. (Voir [Signer numériquement des documents PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifier des documents PDF. (Voir [Certifier des documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Valider les signatures numériques d’un document PDF. (Voir [Vérifier les signatures numériques](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valider toutes les signatures numériques d’un document PDF. (Voir [Vérifier plusieurs signatures numériques](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Supprimer une signature numérique d’un champ de signature. (Voir [Supprimer des signatures numériques](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>pour plus d’informations sur le service Signature, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Ajouter des champs de signature {#adding-signature-fields}

Les signatures numériques apparaissent dans les champs de signature qui sont des champs de formulaire contenant une représentation graphique de la signature. Les champs de signature peuvent être visibles ou invisibles. Les signataires peuvent utiliser un champ de signature existant ou l’ajout d’un champ de signature peut être programmé. Dans les deux cas, le champ de signature doit exister avant la signature du document PDF.

Vous pouvez programmer l’ajout d’un champ de signature à l’aide de l’API Java du service Signature ou de l’API du service Web de signature. Vous pouvez ajouter plusieurs champs de signature à un document PDF. Cependant, chaque nom de champ de signature doit être unique.

>[!NOTE]
>
>certains types de documents PDF ne vous permettent pas d’ajouter un champ de signature par programme. Pour plus d’informations sur le service Signature et l’ajout de champs de signature, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour ajouter un champ de signature à un document PDF, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Obtenir un document PDF auquel un champ de signature est ajouté.
1. Ajouter un champ de signature.
1. Enregistrez le document PDF au format PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client Signature**

Avant d’effectuer par programmation une opération du service Signature, vous devez créer un client du service Signature.

**Obtenir un document PDF auquel un champ de signature est ajouté**

Obtenir un document PDF auquel un champ de signature est ajouté.

**Ajouter un champ de signature**

Pour ajouter avec succès un champ de signature à un document PDF, spécifiez des valeurs de coordonnées qui identifient l’emplacement du champ de signature. (Si vous ajoutez un champ de signature invisible, ces valeurs ne sont pas requises.) Vous pouvez également spécifier les champs du document PDF qui sont verrouillés après l’apposition d’une signature dans le champ de signature.

**Enregistrer le document PDF en tant que fichier PDF**

Une fois que le service Signature a ajouté un champ de signature au document PDF, vous pouvez enregistrer le document en tant que fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signer des documents PDF numériquement](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Ajouter des champs de signature à l’aide de l’API Java {#add-signature-fields-using-the-java-api}

Ajoutez un champ de signature à l’aide de l’API Signature (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir un document PDF auquel un champ de signature est ajouté

   * Créez un objet `java.io.FileInputStream` représentant le document PDF auquel un champ de signature est ajouté en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Ajouter un champ de signature

   * Créez un objet `PositionRectangle` spécifiant l’emplacement du champ de signature à l’aide de son constructeur. Dans le constructeur, spécifiez des valeurs de coordonnée.
   * Si vous le souhaitez, créez un objet `FieldMDPOptions` spécifiant les champs verrouillés lorsqu’une signature numérique est appliquée au champ de signature.
   * Ajoutez un champ de signature à un document PDF en appelant la méthode `addSignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

      * A `com.adobe.idp`. Objet `Document` représentant le document PDF auquel un champ de signature est ajouté.
      * Valeur de chaîne spécifiant le nom du champ de signature.
      * Valeur `java.lang.Integer` représentant le numéro de page auquel un champ de signature est ajouté.
      * Objet `PositionRectangle` spécifiant l’emplacement du champ de signature.
      * Objet `FieldMDPOptions` spécifiant les champs du document PDF verrouillés après l’application d’une signature numérique au champ de signature. Cette valeur de paramètre est facultative et vous pouvez transmettre `null`.

   * Objet `PDFSeedValueOptions` spécifiant différentes valeurs de temps d’exécution. Cette valeur de paramètre est facultative et vous pouvez transmettre `null`.

     La méthode `addSignatureField` renvoie un objet `com.adobe.idp`. Objet `Document` représentant un document PDF contenant un champ de signature.

   >[!NOTE]
   >
   >Vous pouvez appeler la méthode `addInvisibleSignatureField` de l’objet `SignatureServiceClient` pour ajouter un champ de signature invisible.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez l’objet `com.adobe.idp`. Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier. Veillez à utiliser l’objet `com.adobe.idp`. Objet `Document` qui a été renvoyé par la méthode `addSignatureField`.

**Voir également**

[Tutoriels de démarrage rapide API du service Signature ](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Ajouter des champs de signature à l’aide de l’API de service web {#add-signature-fields-using-the-web-service-api}

Pour ajouter un champ de signature à l’aide de l’API Signature (service web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir un document PDF auquel un champ de signature est ajouté

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF qui contiendra un champ de signature.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement de fichier du document PDF et le mode d’ouverture du fichier
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à ses propriétés `MTOM` le contenu du tableau d’octets.

1. Ajouter un champ de signature

   Ajoutez un champ de signature au document PDF en appelant la méthode `addSignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Objet `BLOB` représentant le document PDF auquel le champ de signature invisible est ajouté.
   * Valeur de chaîne spécifiant le nom du champ de signature.
   * Une valeur entière qui représente le numéro de page auquel un champ de signature est ajouté.
   * Objet `PositionRect` spécifiant l’emplacement du champ de signature.
   * Objet `FieldMDPOptions` spécifiant les champs du document PDF verrouillés après l’application d’une signature numérique au champ de signature. Cette valeur de paramètre est facultative et vous pouvez transmettre `null`.
   * Objet `PDFSeedValueOptions` spécifiant différentes valeurs de temps d’exécution. Cette valeur de paramètre est facultative et vous pouvez transmettre `null`.

   La méthode `addSignatureField` renvoie un objet `BLOB` représentant un document PDF contenant un champ de signature.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF qui contiendra le champ de signature et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode `addSignatureField`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Récupérer des noms de champ de signature {#retrieving-signature-field-names}

Vous pouvez récupérer les noms de tous les champs de signature d’un document PDF que vous souhaitez signer ou certifier. Si vous n’avez pas la certitude de connaître les noms de champ de signature d’un document PDF ou si vous souhaitez vérifier leurs noms, vous pouvez programmer leur récupération. Le service Signature renvoie le nom qualifié complet du champ de signature, tel que `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour récupérer les noms des champs de signature, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Accédez au document PDF contenant les champs de signature.
1. Récupérez les noms des champs de signature.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer par programmation une opération du service Signature, vous devez créer un client du service Signature.

**Accéder au document PDF contenant les champs de signature**

Récupérez un document PDF contenant des champs de signature.

**Récupérer les noms des champs de signature**

Vous pouvez récupérer les noms des champs de signature après avoir récupéré un document PDF qui contient un ou plusieurs champs de signature.

**Voir également**

[Récupérer les noms des champs de signature à l’aide de l’API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Récupérer le champ de signature à l’aide de l’API Web Service](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Récupérer les noms des champs de signature à l’aide de l’API Java {#retrieve-signature-field-names-using-the-java-api}

Récupérez les noms des champs de signature à l’aide de l’API Signature (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels qu’adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Accéder au document PDF contenant les champs de signature

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF contenant les champs de signature en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Récupérer des noms des champs de signature

   * Récupérez les noms des champs de signature en appelant la méthode `getSignatureFieldList` de l’objet `SignatureServiceClient` et en transmettant l’objet `com.adobe.idp.Document` qui contient le document PDF avec les champs de signature. Cette méthode renvoie un objet `java.util.List`, dont chaque élément contient un objet `PDFSignatureField`. Grâce à cet objet, vous pouvez obtenir des informations supplémentaires sur un champ de signature, par exemple s’il est visible.
   * Effectuez une itération dans l’objet `java.util.List` pour déterminer s’il existe des noms de champ de signature. Pour chaque champ de signature du document PDF, vous pouvez obtenir un objet `PDFSignatureField`. Pour obtenir le nom du champ de signature, appelez la méthode `getName` de l’objet `PDFSignatureField`. Cette méthode renvoie une valeur de chaîne indiquant le nom du champ de signature.

**Voir également**

[Récupérer des noms de champ de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Tutoriel de mise en route (mode SOAP) : récupération des noms de champ de signature à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer le champ de signature à l’aide de l’API Web Service {#retrieve-signature-field-using-the-web-service-api}

Récupérez les noms des champs de signature à l’aide de l’API de signature (Web Service) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Accéder au document PDF contenant les champs de signature

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF qui contient les champs de signature.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant le contenu du tableau d’octets à son champ `MTOM`.

1. Récupérer des noms des champs de signature

   * Récupérez les noms des champs de signature en appelant la méthode `getSignatureFieldList` de l’objet `SignatureServiceClient` et en transmettant l’objet `BLOB` qui contient le document PDF avec les champs de signature. Cette méthode renvoie un objet de collection `MyArrayOfPDFSignatureField` dans lequel chaque élément contient un objet `PDFSignatureField`.
   * Effectuez une itération sur l’objet `MyArrayOfPDFSignatureField` pour déterminer s’il existe des noms de champ de signature. Pour chaque champ de signature du document PDF, vous pouvez obtenir un objet `PDFSignatureField`. Pour obtenir le nom du champ de signature, appelez la méthode `getName` de l’objet `PDFSignatureField`. Cette méthode renvoie une valeur de chaîne indiquant le nom du champ de signature.

**Voir également**

[Récupérer des noms de champ de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifier des champs de signature {#modifying-signature-fields}

Vous pouvez modifier les champs de signature d’un document PDF à l’aide de l’API Java et de l’API de service web. La modification d’un champ de signature implique de manipuler ses valeurs de dictionnaire de verrouillage des champs de signature ou ses valeurs du dictionnaire de valeur de départ.

Un *dictionnaire de verrouillage de champ* spécifie la liste des champs qui sont verrouillés lorsque le champ de signature est signé. Un champ verrouillé empêche les utilisateurs d’apporter des modifications au champ. Un *dictionnaire de valeur de départ* contient des informations contraignantes utilisées au moment de l’apposition de la signature. Par exemple, vous pouvez modifier les autorisations qui contrôlent les actions pouvant se produire sans invalider la signature.

Lors de la modification d’un champ de signature existant, vous pouvez modifier le document PDF en fonction des besoins de votre entreprise. Par exemple, un nouveau besoin d’activité pourrait nécessiter de verrouiller tous les champs du document une fois le document signé.

Cette section explique comment modifier un champ de signature en modifiant les valeurs du dictionnaire de verrouillage de champ et du dictionnaire de valeur de départ. Les modifications apportées au dictionnaire de verrouillage des champs de signature entraînent le verrouillage de tous les champs du document PDF lors de la signature d’un champ de signature. Les modifications apportées au dictionnaire des valeurs de départ interdisent certains types de modifications apportées au document.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la modification des champs de signature, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour modifier les champs de signature d’un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Accédez au document PDF contenant le champ de signature à modifier.
1. Définissez les valeurs du dictionnaire.
1. Modifiez le champ de signature.
1. Enregistrez le document PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer par programmation une opération du service Signature, vous devez créer un client du service Signature.

**Accéder au document PDF contenant le champ de signature à modifier**

Récupérez un document PDF contenant le champ de signature à modifier.

**Définir des valeurs de dictionnaire**

Pour modifier un champ de signature, affectez des valeurs à son dictionnaire de verrouillage de champs ou à son dictionnaire de valeur de départ. En spécifiant les valeurs du dictionnaire de verrouillage des champs de signature, vous devez également indiquer les champs du document PDF verrouillés lorsque le champ de signature est signé. (Cette section explique comment verrouiller tous les champs.)

Les valeurs du dictionnaire de valeurs de départ suivantes peuvent être définies :

* **Vérification des révisions** : cette option indique si la vérification de révocation est effectuée lorsqu’une signature est appliquée au champ de signature.
* **Options de certificat** : cette option attribue des valeurs au dictionnaire de valeurs de départ du certificat. Avant de spécifier des options de certificat, il est recommandé de vous familiariser avec un dictionnaire de valeur de départ du certificat. (Voir [Référence PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Options de prétraitement** : Cette option attribue des algorithmes de prétraitement utilisés pour la signature. Les valeurs valides sont SHA1, SHA256, SHA384, SHA512 et RIPEMD160.
* **Filtre** : cette option indique le filtre utilisé pour le champ de signature. Par exemple, vous pouvez utiliser le filtre Adobe.PPKLite. (Voir [Référence PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Options d’indicateur** : cette option indique les valeurs d’indicateur associées à ce champ de signature. Une valeur définie sur 1 signifie qu’un signataire doit utiliser uniquement les valeurs spécifiées pour l’entrée. Une valeur définie sur 0 signifie que d’autres valeurs sont permises. Voici les positions Bit :

   * **1 (Filtre) :** gestionnaire de signatures à utiliser pour signer le champ de signature
   * **2 (Sous-filtre) :** tableau de noms indiquant des encodages acceptables à utiliser lors de la signature
   * **3 (V)** : numéro de version minimum requise du gestionnaire de signatures utilisé pour signer le champ de signature.
   * **4 (Motifs) :** tableau de chaînes spécifiant les motifs possibles de la signature d’un document.
   * **5 (PDFLegalWarnings) :** tableau de chaînes spécifiant les attestations juridiques possibles.

* **Attestations juridiques** : lorsqu’un document est certifié, il est automatiquement analysé à la recherche de types de contenu spécifiques qui peuvent rendre le contenu visible d’un document ambigu ou déroutant. Par exemple, une annotation peut assombrir du texte essentiel pour comprendre ce qui est certifié. Le processus d’analyse génère des avertissements indiquant la présence de ce type de contenu. Il fournit également une explication supplémentaire du contenu susceptible d’avoir généré des avertissements.
* **Autorisations** : cette option spécifie les autorisations pouvant être utilisées sur un document PDF sans invalider la signature.
* **Motifs** : indique les motifs pour lesquels ce document doit être signé.
* **Horodatage** : spécifie les options d’horodatage. Vous pouvez, par exemple, définir l’URL du serveur d’horodatage utilisé.
* **Version** : indique le numéro de version minimum du gestionnaire de signatures à utiliser pour signer le champ de signature.

**Modifier un champ de signature**

Après avoir créé un client du service Signature, récupéré le document PDF contenant le champ de signature à modifier et défini les valeurs du dictionnaire, vous pouvez demander au service Signature de modifier le champ de signature. Le service Signature renvoie ensuite un document PDF contenant le champ de signature modifié. Le document PDF d’origine n’est pas affecté.

**Enregistrer le document PDF en tant que fichier PDF**

Enregistrez le document PDF contenant le champ de signature modifié en tant que fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Tutoriels de démarrage rapide API du service Signature ](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Signer des documents PDF numériquement](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modifier des champs de signature à l’aide de l’API Java {#modify-signature-fields-using-the-java-api}

Modifiez un champ de signature à l’aide de l’API Signature (Java) :

1. Inclure les fichiers du projet

   Incluez des fichiers JAR du client, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Accéder au document PDF contenant le champ de signature à modifier

   * Créez un objet `java.io.FileInputStream` représentant le document PDF contenant le champ de signature à modifier à l’aide de son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir des valeurs du dictionnaire

   * Créez un objet `PDFSignatureFieldProperties` en utilisant son constructeur. Un objet `PDFSignatureFieldProperties` stocke les informations du dictionnaire de verrouillage des champs de signature et du dictionnaire de valeurs de départ.
   * Créez un objet `PDFSeedValueOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de valeurs de départ.
   * Interdisez les modifications apportées au document PDF en appelant la méthode `setMdpValue` de l’objet `PDFSeedValueOptionSpec` et en transmettant la valeur d’énumération `MDPPermissions.NoChanges`.
   * Créez un objet `FieldMDPOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de verrouillage des champs de signature.
   * Verrouillez tous les champs du document PDF en appelant la méthode `setMdpValue` de l’objet `FieldMDPOptionSpec` et en transmettant la valeur d’énumération `FieldMDPAction.ALL`.
   * Définissez les informations du dictionnaire de valeur de départ en appelant la méthode `setSeedValue` de l’objet `PDFSignatureFieldProperties` et en transmettant l’objet `PDFSeedValueOptionSpec`.
   * Définissez les informations du dictionnaire de verrouillage des champs de signature en appelant la méthode `setFieldMDP` de l’objet `PDFSignatureFieldProperties` et en transmettant l’objet `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs du dictionnaire de valeurs de départ que vous pouvez définir, reportez-vous à la référence de classe `PDFSeedValueOptionSpec`. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modifier un champ de signature

   Modifiez le champ de signature en appelant la méthode `modifySignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` stockant le document PDF contenant le champ de signature à modifier.
   * Valeur de chaîne spécifiant le nom du champ de signature.
   * Objet `PDFSignatureFieldProperties` stockant les informations du dictionnaire de verrouillage de champs de signature et du dictionnaire de valeurs de départ.

   La méthode `modifySignatureField` renvoie un objet `com.adobe.idp.Document` qui stocke un document PDF contenant le champ de signature modifié.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du nom du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Veillez à utiliser l’objet `com.adobe.idp.Document` renvoyé par la méthode `modifySignatureField`.

### Modifier des champs de signature à l’aide de l’API Web Service {#modify-signature-fields-using-the-web-service-api}

Modifiez un champ de signature à l’aide de l’API Signature (Web Service) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Accéder au document PDF contenant le champ de signature à modifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF contenant le champ de signature à modifier.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Définir des valeurs du dictionnaire

   * Créez un objet `PDFSignatureFieldProperties` en utilisant son constructeur. Cet objet stocke les informations du dictionnaire de verrouillage de champs de signature et du dictionnaire de valeurs de départ.
   * Créez un objet `PDFSeedValueOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de valeurs de départ.
   * Interdisez les modifications apportées au document PDF en attribuant la valeur de l’énumération `MDPPermissions.NoChanges` au membre de données `mdpValue` de l’objet `PDFSeedValueOptionSpec`.
   * Créez un objet `FieldMDPOptionSpec` en utilisant son constructeur. Cet objet vous permet de définir les valeurs du dictionnaire de verrouillage des champs de signature.
   * Verrouillez tous les champs du document PDF en attribuant la valeur d’énumération `FieldMDPAction.ALL` au membre de données `mdpValue` de l’objet `FieldMDPOptionSpec`.
   * Définissez les informations du dictionnaire de valeur de départ en attribuant l’objet `PDFSeedValueOptionSpec` au membre de données `seedValue` de l’objet `PDFSignatureFieldProperties`.
   * Définissez les informations du dictionnaire de verrouillage des champs de signature en attribuant l’objet `FieldMDPOptionSpec` au membre de données `fieldMDP` de l’objet `PDFSignatureFieldProperties`.

   >[!NOTE]
   >
   >Pour afficher toutes les valeurs du dictionnaire de valeurs de départ que vous pouvez définir, reportez-vous à la référence de classe `PDFSeedValueOptionSpec`. (Voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modifier un champ de signature

   Modifiez le champ de signature en appelant la méthode `modifySignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Objet `BLOB` stockant le document PDF contenant le champ de signature à modifier.
   * Valeur de chaîne spécifiant le nom du champ de signature.
   * Objet `PDFSignatureFieldProperties` stockant les informations du dictionnaire de verrouillage de champs de signature et du dictionnaire de valeurs de départ.

   La méthode `modifySignatureField` renvoie un objet `BLOB` qui stocke un document PDF contenant le champ de signature modifié.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF qui contiendra le champ de signature et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `addSignatureField`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Signer des documents PDF numériquement {#digitally-signing-pdf-documents}

Les signatures numériques peuvent être appliquées aux documents PDF pour fournir un niveau de sécurité. Les signatures numériques, tout comme les signatures manuscrites, permettent aux signataires de s’identifier et d’effectuer des instructions sur le document. La technologie utilisée pour signer numériquement des documents permet de s’assurer que la personne signataire et que les destinataires sont formels sur ce qui a été signé et certains que le document n’a pas été modifié depuis sa signature.

Les documents PDF sont signés à l’aide d’une technologie de clé publique. Une personne signataire possède deux clés : une clé publique et une clé privée. La clé privée est stockée dans les informations d’identification d’un utilisateur ou d’une utilisatrice. Cette clé doit être disponible au moment de la signature. La clé publique est stockée dans le certificat de l’utilisateur ou de l’utilisatrice qui doit être accessible aux destinataires pour valider la signature. Les informations relatives aux certificats révoqués se trouvent dans les listes de révocation des certificats et les réponses OCSP (Online Certificate Status Protocol) distribuées par les autorités de certification (CA). L’heure de signature peut être obtenue auprès d’une source fiable appelée Autorité d’horodatage.

>[!NOTE]
>
>Avant de pouvoir signer numériquement un document PDF, vous devez vérifier que vous ajoutez le certificat dans AEM Forms. Un certificat est ajouté à l’aide de la console d’administration ou par programmation à l’aide de l’API Trust Manager. (Voir [Importer des informations d’identification à l’aide de l’API Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Vous pouvez signer numériquement des documents PDF par programmation. Lors de la signature numérique d’un document PDF, vous devez référencer des informations d’identification de sécurité qui existent dans AEM Forms. Les informations d’identification sont la clé privée utilisée pour la signature.

Le service Signature effectue les étapes suivantes lorsqu’un document PDF est signé :

1. Le service Signature récupère les informations d’identification de TrustStore en transmettant l’alias spécifié dans la demande.
1. TrustStore recherche les informations d’identification spécifiées.
1. Les informations d’identification sont renvoyées au service Signature et sont utilisées pour signer le document. Les informations d’identification sont également mises en cache par rapport à l’alias pour les futures demandes.

Pour plus d’informations sur la gestion des informations d’identification de sécurité, reportez-vous au guide d’*installation et de déploiement d’AEM Forms* correspondant à votre serveur d’applications.

>[!NOTE]
>
>Il existe des différences entre signer et certifier des documents. (Voir [Certifier des documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Tous les documents PDF ne prennent pas en charge la signature. Pour plus d’informations sur le service Signature et la signature numérique de documents, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Le service Signature ne prend pas en charge les fichiers XDP contenant des données PDF incorporées en tant qu’entrée d’une opération, telle que la certification d’un document. Cette action entraîne la génération d’une exception `PDFOperationException` par le service Signature. Pour résoudre ce problème, convertissez le fichier XDP en fichier PDF à l’aide du service PDF Utilities, puis transmettez le fichier PDF converti à une opération de service Signature. (Voir [Utiliser PDF Utilities](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Informations d’identification nCipher nShield HSM**

Lors de l’utilisation d’informations d’identification nCipher nShield HSM pour signer ou certifier un document PDF, les nouvelles informations d’identification ne peuvent pas être utilisées tant que le serveur d’applications J2EE sur lequel AEM Forms est déployé n’a pas été redémarré. Cependant, vous pouvez définir une valeur de configuration, ce qui permet à l’opération de signature ou de certification de fonctionner sans redémarrer le serveur d’applications J2EE.

Vous pouvez ajouter la valeur de configuration suivante dans le fichier cknfastrc, qui se trouve sous /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc) :

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Après avoir ajouté cette valeur de configuration au fichier cknfastrc, les nouvelles informations d’identification peuvent être utilisées sans redémarrer le serveur d’applications J2EE.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

**Signature non approuvée**

Lors de la certification et de la signature d’un même document PDF, si la signature de certification n’est pas approuvée, un triangle jaune apparaît sur la première signature lors de l’ouverture du document PDF dans Acrobat ou Adobe Reader. La signature de certification doit être fiable pour éviter cette situation.

**Signer des documents qui sont des formulaires XFA**

Si vous tentez de signer un formulaire XFA à l’aide de l’API du service Signature, les données peuvent ne pas figurer dans l’élément `View` `Signed` `Version` situé dans Acrobat. Prenons comme exemple le workflow suivant :

* À l’aide d’un fichier XDP créé à l’aide de Designer, vous fusionnez une conception de formulaire contenant un champ de signature et des données XML contenant des données de formulaire. Vous utilisez le service Forms pour générer un document PDF interactif.
* Signez le document PDF à l’aide de l’API du service Signature.

### Résumé des étapes {#summary_of_steps-3}

Pour signer numériquement un document PDF, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client de service Signature.
1. Obtenez le document PDF à signer.
1. Signez le document PDF.
1. Enregistrez le document PDF signé en tant que fichier PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client Signatures**

Avant d’effectuer par programmation une opération du service Signature, vous devez créer un client du service Signature.

**Obtenir le document PDF à signer**

Pour signer un document PDF, vous devez obtenir un document PDF contenant un champ de signature. Si un document PDF ne contient pas de champ de signature, il ne peut pas être signé. Vous pouvez ajouter un champ de signature à l’aide de Designer ou par programmation.

**Signer le document PDF**

Lors de la signature d’un document PDF, vous pouvez définir les options d’exécution utilisées par le service Signature. Vous pouvez configurer les options suivantes :

* Options d’aspect
* Vérification de la révocation
* Valeurs d’horodatage

Pour définir les options d’apparence, utilisez un objet `PDFSignatureAppearanceOptionSpec`. Par exemple, vous pouvez afficher la date dans une signature en appelant la méthode `setShowDate` de l’objet `PDFSignatureAppearanceOptionSpec` et en transmettant `true`.

Vous pouvez également indiquer s’il faut effectuer ou non une vérification de révocation qui détermine si le certificat utilisé pour signer numériquement un document PDF a été révoqué. Pour effectuer une vérification de révocation, vous pouvez spécifier l’une des valeurs suivantes :

* **NoCheck** : ne pas effectuer de vérification de révocation.
* **BestEffort** : toujours essayer de vérifier la révocation de tous les certificats de la chaîne. Si un problème se produit lors de la vérification, la révocation est supposée être valide. En cas d’échec, considérez que le certificat n’est pas révoqué.
* **CheckIfAvailable** : vérifier la révocation de tous les certificats de la chaîne si des informations de révocation sont disponibles. En cas de problème lors de la vérification, la révocation est considérée comme non valide. En cas d’échec, considérez que le certificat est révoqué et non valide. (Il s’agit de la valeur par défaut.)
* **AlwaysCheck** : vérifier la révocation de tous les certificats de la chaîne. Si les informations de révocation ne figurent dans aucun certificat, la révocation est considérée comme non valide.

Pour effectuer une vérification de révocation sur un certificat, vous pouvez spécifier une URL vers un serveur de liste de révocation des certificats (CRL) à l’aide d’un objet `CRLOptionSpec`. Cependant, si vous souhaitez effectuer une vérification de révocation et que vous ne spécifiez pas d’URL vers un serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP plutôt qu’un serveur CRL, la vérification de révocation est effectuée plus rapidement. (Voir « Online Certificate Status Protocol » à l’adresse [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir l’ordre des serveurs CRL et OCSP que le service Signature utilise à l’aide d’Adobe Applications and Services. Par exemple, si le serveur OCSP est défini en premier lieu dans Adobe Applications and Services, le serveur OCSP est vérifié, suivi du serveur CRL. (Voir « Gérer les certificats et les informations d’identification à l’aide de TrustStore » dans l’aide d’AAC.)

Si vous indiquez de ne pas effectuer de vérification de révocation, le service Signature ne vérifie pas si le certificat utilisé pour signer ou certifier un document a été révoqué. En d’autres termes, les informations des serveurs CRL et OCSP sont ignorées.

>[!NOTE]
>
>bien qu’un serveur CRL ou OCSP puisse être spécifié dans le certificat, vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’un élément `CRLOptionSpec` et d’un objet `OCSPOptionSpec`. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la méthode `setLocalURI` de l’objet `CRLOptionSpec`.

L’horodatage désigne le processus de suivi de l’heure de modification d’un document signé ou certifié. Une fois signé, un document ne doit pas être modifié, même par son propriétaire. L’horodatage aide à assurer la validité d’un document signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un objet `TSPOptionSpec`. Par exemple, vous pouvez spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>dans les sections Java et service web ainsi que les démarrages rapides correspondants, la vérification de révocation est utilisée. Comme aucune information de serveur CRL ou OCSP n’est spécifiée, les informations du serveur sont obtenues à partir du certificat utilisé pour signer numériquement le document PDF.

Pour signer un document PDF, vous pouvez spécifier le nom qualifié complet du champ de signature qui contiendra la signature numérique, tel que `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, le nom partiel du champ de signature peut également être utilisé : `SignatureField3[3]`.

Vous devez également référencer des informations d’identification de sécurité pour signer numériquement un document PDF. Pour référencer des informations d’identification de sécurité, vous spécifiez un alias. L’alias est une référence à des informations d’identification réelles qui peuvent se trouver dans un fichier PKCS#12 (avec l’extension .pfx) ou un module de sécurité matérielle (HSM). Pour plus d’informations sur les informations d’identification de sécurité, reportez-vous au guide d’*installation et de déploiement d’AEM Forms* correspondant à votre serveur d’applications.

**Enregistrer le document PDF signé**

Une fois que le service Signature a signé numériquement le document PDF, vous pouvez l’enregistrer en tant que fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Signer numériquement des documents PDF à l’aide de l’API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Signer numériquement des documents PDF à l’aide de l’API du service web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

[Récupérer des noms de champ de signature](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Signer numériquement des documents PDF à l’aide de l’API Java {#digitally-sign-pdf-documents-using-the-java-api}

Signez numériquement un document PDF à l’aide de l’API Signature (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un client Signatures

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le document PDF à signer

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à signer numériquement en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Signer le document PDF

   Signez le document PDF en appelant la méthode `sign` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` représentant le document PDF à signer.
   * Une valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature numérique.
   * Un objet `Credential` représentant les informations d’identification utilisées pour signer numériquement le document PDF. Créez un objet `Credential` en appelant la méthode `getInstance` statique de l’objet `Credential` et en transmettant une valeur de chaîne spécifiant la valeur de l’alias correspondant aux informations d’identification de sécurité.
   * Un objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage à utiliser pour synthétiser le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Une valeur de chaîne qui représente la raison pour laquelle le document PDF a été signé numériquement.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Un objet `java.lang.Boolean` indiquant si la révocation doit être vérifiée sur le certificat du signataire.
   * Un objet `OCSPOptionSpec` stockant les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` stockant les préférences de la liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`. Pour plus d’informations, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   La méthode `sign` renvoie un objet `com.adobe.idp.Document` représentant le document PDF signé.

1. Enregistrer le document PDF signé

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et transmettez `java.io.File` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `sign`.

**Voir également**

[Signer des documents PDF numériquement](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Didacticiel de mise en route (mode SOAP) : signature numérique d’un document PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signer numériquement des documents PDF à l’aide de l’API du service web {#digitally-signing-pdf-documents-using-the-web-service-api}

Pour signer numériquement un document PDF à l’aide de l’API Signature (service web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer un client Signatures

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le document PDF à signer

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF signé.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement de fichier du document PDF à signer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Signer un document PDF

   Signez le document PDF en appelant la méthode `sign` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `BLOB` représentant le document PDF à signer.
   * Une valeur de chaîne qui représente le nom du champ de signature qui contiendra la signature numérique.
   * Un objet `Credential` représentant les informations d’identification utilisées pour signer numériquement le document PDF. Créez un objet `Credential` en utilisant son constructeur et en spécifiant l’alias en attribuant une valeur à la propriété `alias` de l’objet `Credential`.
   * Un objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage à utiliser pour synthétiser le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Une valeur booléenne qui indique si l’algorithme de hachage est utilisé.
   * Une valeur de chaîne qui représente la raison pour laquelle le document PDF a été signé numériquement.
   * Une valeur de chaîne qui représente l’emplacement du ou de la signataire.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Un objet `System.Boolean` qui spécifie s’il faut effectuer une vérification de la révocation sur le certificat du signataire. Si cette vérification de la révocation est effectuée, elle est intégrée à la signature. La valeur par défaut est de `false`.
   * Un objet `OCSPOptionSpec` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de la révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objet `CRLPreferences` qui stocke les préférences de la liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Un objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.

   La méthode `sign` renvoie un objet `BLOB` représentant le document PDF signé.

1. Enregistrer le document PDF signé

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier du document PDF signé et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode `sign`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Signer des documents PDF numériquement](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Signer numériquement les formulaires interactifs {#digitally-signing-interactive-forms}

Vous pouvez signer un formulaire interactif que le service Forms crée. Prenons comme exemple le workflow suivant :

* Vous fusionnez un formulaire PDF basé sur XFA créé à l’aide de Designer avec des données de formulaire situées dans un document XML à l’aide du service Forms. Le serveur Forms effectue le rendu d’un formulaire interactif.
* Vous pouvez signer le formulaire interactif à l’aide de l’API du service Signature.

Le résultat est un formulaire PDF interactif signé numériquement. Lors de la signature d’un formulaire PDF basé sur un formulaire XFA, veillez à enregistrer le fichier PDF en tant que formulaire PDF statique Adobe. Si vous tentez de signer un formulaire PDF enregistré en tant que formulaire PDF dynamique Adobe, une exception se produit. Puisque vous signez le formulaire renvoyé par le service Forms, assurez-vous que le formulaire contient un champ de signature.

>[!NOTE]
>
>Avant de pouvoir signer numériquement un formulaire interactif, vous devez vous assurer d’ajouter le certificat à AEM Forms. Un certificat est ajouté à l’aide de la console d’administration ou par programmation à l’aide de l’API Trust Manager. (Voir [Importer des informations d’identification à l’aide de l’API Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Lors de l’utilisation de l’API du service Forms, définissez l’option d’exécution `GenerateServerAppearance` sur `true`. Cette option d’exécution garantit que l’aspect du formulaire généré sur le serveur reste valide lorsqu’il est ouvert dans Acrobat ou Adobe Reader. Il est recommandé de définir cette option d’exécution lors de la génération d’un formulaire interactif à signer à l’aide de l’API Forms.

>[!NOTE]
>
>Avant de lire la section Signature numérique de formulaires interactifs, il est recommandé de bien connaître la procédure de signature des documents PDF. (Voir [Signature numérique de documents PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Résumé des étapes {#summary_of_steps-4}

Pour signer numériquement un formulaire interactif que le service Forms renvoie, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Forms et Signatures.
1. Accédez au formulaire interactif à l’aide du service Forms.
1. Signez le formulaire interactif.
1. Enregistrez le document PDF signé en tant que fichier PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Forms et Signatures**

Comme ce workflow appelle les services Forms et Signature, créez un client de service Forms et un client de service Signature.

**Obtenir le formulaire interactif à l’aide du service Forms**

Vous pouvez utiliser le service Forms pour obtenir le formulaire PDF interactif à signer. À partir d’AEM Forms, vous pouvez transmettre un objet `com.adobe.idp.Document` au service Forms contenant le formulaire à générer. Le nom de cette méthode est `renderPDFForm2`. Cette méthode renvoie un objet `com.adobe.idp.Document` contenant le formulaire à signer. Vous pouvez transmettre cette instance `com.adobe.idp.Document` au service Signature.

De même, si vous utilisez des services web, vous pouvez transmettre l’instance `BLOB` que le service Forms renvoie au service Signature.

>[!NOTE]
>
>Le démarrage rapide associé à la section de signature numérique d’un formulaire interactif appelle la méthode `renderPDFForm2`.

**Signer le formulaire interactif**

Lors de la signature d’un document PDF, vous pouvez définir les options d’exécution utilisées par le service Signature. Vous pouvez configurer les options suivantes :

* Options d’aspect
* Vérification de la révocation
* Valeurs d’horodatage

Pour définir les options d’apparence, utilisez un objet `PDFSignatureAppearanceOptionSpec`. Par exemple, vous pouvez afficher la date dans une signature en appelant la méthode `setShowDate` de l’objet `PDFSignatureAppearanceOptionSpec` et en transmettant `true`.

**Enregistrer le document PDF signé**

Une fois que le service Signature a signé numériquement le document PDF, vous pouvez l’enregistrer en tant que fichier PDF. Le fichier PDF peut être ouvert dans Acrobat ou Adobe Reader.

**Voir également**

[Signer numériquement un formulaire interactif à l’aide de l’API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Signer numériquement un formulaire interactif à l’aide de l’API du service web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signer des documents PDF numériquement](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Signer numériquement un formulaire interactif à l’aide de l’API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Signez numériquement un formulaire interactif à l’aide de l’API Forms et Signature (Java) :

1. Inclure les fichiers du projet

   Inclure les fichiers JAR du client, tels que adobe-signatures-client.jar et adobe-forms-client.jar, dans le paramètre Classpath de votre projet Java.

1. Créez un client Forms et Signatures

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le formulaire interactif à l’aide du service Forms

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à transmettre au service Forms en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un objet `java.io.FileInputStream` représentant le document XML contenant les données de formulaire à transmettre au service Forms en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 
   * Créez un objet `PDFFormRenderSpec` utilisé pour définir les options d’exécution. Appelez la méthode `setGenerateServerAppearance` de l’objet `PDFFormRenderSpec` et transmettez `true`.
   * Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

      * Un objet `com.adobe.idp.Document` contenant le formulaire PDF à afficher.
      * Un objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire.
      * Un objet `PDFFormRenderSpec` stockant les options d’exécution.
      * Un objet `URLSpec` contenant les valeurs URI requises par le service Forms. Vous pouvez indiquer la valeur `null` pour ce paramètre.
      * Un objet `java.util.HashMap` stockant les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

     La méthode `renderPDFForm2` renvoie un objet `FormsResult` contenant un flux de données de formulaire.

   * Récupérez le formulaire PDF en appelant la méthode `getOutputContent` de l’objet `FormsResult`. Cette méthode renvoie un objet `com.adobe.idp.Document` représentant le formulaire interactif.

1. Signer le formulaire interactif

   Signez le document PDF en appelant la méthode `sign` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` représentant le document PDF à signer. Assurez-vous que cet objet correspond à l’objet `com.adobe.idp.Document` obtenu à partir du service Forms.
   * Une valeur de chaîne représentant le nom du champ de signature signé.
   * Un objet `Credential` représentant les informations d’identification utilisées pour signer le document PDF. Créez un objet `Credential` en appelant la méthode `getInstance` statique de l’objet `Credential`. Transmettez une valeur de chaîne spécifiant la valeur d’alias correspondant aux informations d’identification de sécurité.
   * Un objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage à utiliser pour synthétiser le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Une valeur de chaîne qui représente la raison pour laquelle le document PDF a été signé numériquement.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Un objet `java.lang.Boolean` indiquant si la révocation doit être vérifiée sur le certificat du signataire.
   * Un objet `OCSPPreferences` stockant les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` stockant les préférences de la liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Un objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.

   La méthode `sign` renvoie un objet `com.adobe.idp.Document` représentant le document PDF signé.

1. Enregistrer le document PDF signé

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et transmettez `java.io.File` pour copier le contenu de l’objet `Document` dans le fichier. Veillez à utiliser l’objet `com.adobe.idp.Document` que la méthode `sign` a renvoyé.

**Voir également**

[Signer numériquement les formulaires interactifs](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Didacticiel de mise en route (mode SOAP) : signature numérique d’un document PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Signer numériquement un formulaire interactif à l’aide de l’API du service web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Signez numériquement un formulaire interactif à l’aide de l’API Forms et Signature (service web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Étant donné que cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Signature : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Forms : `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Puisque le type de données `BLOB` est commun aux deux références de service, qualifiez pleinement le type de données `BLOB` lors de son utilisation. Dans le démarrage rapide du service web correspondant, toutes les instances `BLOB` sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Forms et Signatures

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour le client de service Forms.

1. Obtenir le formulaire interactif à l’aide du service Forms

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF signé.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement de fichier du document PDF à signer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Remplissez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.
   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker des données de formulaire.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier XML contenant les données de formulaire, ainsi que le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.
   * Créez un objet `PDFFormRenderSpec` utilisé pour définir les options d’exécution. Attribuez la valeur `true` au champ `generateServerAppearance` de l’objet `PDFFormRenderSpec`.
   * Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

      * Un objet `BLOB` contenant le formulaire PDF à afficher.
      * Un objet `BLOB` contenant les données à fusionner avec le formulaire.
      * Un objet `PDFFormRenderSpec` stockant les options d’exécution.
      * Un objet `URLSpec` contenant les valeurs URI requises par le service Forms. Vous pouvez indiquer la valeur `null` pour ce paramètre.
      * Un objet `java.util.HashMap` stockant les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
      * Paramètre de sortie long utilisé pour stocker le nombre de pages dans le formulaire.
      * Paramètre de sortie de chaîne utilisé pour la valeur des paramètres régionaux.
      * Valeur `FormResult` étant un paramètre de sortie utilisé pour stocker le formulaire interactif.

   * Récupérez le formulaire PDF en appelant le champ `outputContent` de l’objet `FormsResult`. Ce champ stocke un objet `BLOB` représentant le formulaire interactif.

1. Signer le formulaire interactif

   Signez le document PDF en appelant la méthode `sign` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Objet `BLOB` représentant le document PDF à signer. Utilisez l’instance `BLOB` renvoyée par le service Forms.
   * Une valeur de chaîne représentant le nom du champ de signature signé.
   * Un objet `Credential` représentant les informations d’identification utilisées pour signer le document PDF. Créez un objet `Credential` en utilisant son constructeur et en spécifiant l’alias en attribuant une valeur à la propriété `alias` de l’objet `Credential`.
   * Un objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage à utiliser pour synthétiser le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Une valeur booléenne qui indique si l’algorithme de hachage est utilisé.
   * Une valeur de chaîne qui représente la raison pour laquelle le document PDF a été signé numériquement.
   * Une valeur de chaîne qui représente l’emplacement du ou de la signataire.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature numérique. Vous pouvez, par exemple, utiliser cet objet pour ajouter un logo personnalisé à une signature numérique.
   * Un objet `System.Boolean` qui spécifie s’il faut effectuer une vérification de la révocation sur le certificat du signataire. Si cette vérification de la révocation est effectuée, elle est intégrée à la signature. La valeur par défaut est de `false`.
   * Un objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de la révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objet `CRLPreferences` qui stocke les préférences de la liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Un objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Ce paramètre est facultatif et peut être `null`.

   La méthode `sign` renvoie un objet `BLOB` représentant le document PDF signé.

1. Enregistrer le document PDF signé

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier du document PDF signé et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode `sign`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Signer numériquement les formulaires interactifs](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certification de documents PDF {#certifying-pdf-documents}

Vous pouvez sécuriser un document PDF en le certifiant avec un type particulier de signature appelé signature certifiée. Une signature certifiée se distingue d’une signature numérique de plusieurs manières :

* Elle doit être la première signature appliquée au document PDF ; cela veut dire que lorsque la signature certifiée est appliquée, tous les autres champs de signature du document doivent être non signés. Une seule signature certifiée est autorisée dans un document PDF. Si vous souhaitez signer ou certifier un document PDF, vous devez le certifier avant de le signer. Après avoir certifié un document PDF, vous pouvez signer numériquement des champs de signature supplémentaires.
* La personne ayant créé le document ou celle en charge de l’expédier peut indiquer que le document peut être modifié de certaines manières sans invalider la signature certifiée. Par exemple, le document peut autoriser le remplissage de formulaires ou de commentaires. Si l’auteur ou l’autrice spécifie qu’une modification en particulier n’est pas autorisée, Acrobat empêche les utilisateurs et utilisatrices d’effectuer cette modification sur le document. Si de telles modifications sont effectuées, par exemple à l’aide d’une autre application, la signature certifiée est invalide et Acrobat affiche un avertissement lorsqu’un utilisateur ou une utilisatrice ouvre le document. (Avec des signatures non certifiées, les modifications ne sont pas interdites et les opérations de modification normales n’invalident pas la signature d’origine.)
* Au moment de la signature, les différents types de contenus du document susceptibles de rendre le document ambigu ou trompeur sont analysés. Par exemple, une annotation peut assombrir du texte sur une page qui est essentiel pour comprendre ce qui est certifié. Une explication (attestation légale) peut être fournie pour ce type de contenu.

Vous pouvez certifier des documents PDF par programmation en utilisant l’API Java du service Signature ou l’API du service web de Signature. Lorsque vous certifiez un document PDF, vous devez faire référence à des informations d’identification de sécurité qui existent dans le service d’informations d’identification. Pour plus d’informations sur les informations d’identification de sécurité, consultez le guide *Installation et déploiement d’AEM Forms* pour votre serveur d’applications.

>[!NOTE]
>
>Lorsque vous certifiez et signez le même document PDF, si la signature de certification n’est pas fiable, un triangle jaune apparaît en regard de la première signature lorsque vous ouvrez le document PDF dans Acrobat ou dans Adobe Reader. La signature de certification doit être fiable pour éviter cette situation.

>[!NOTE]
>
>Lorsque vous utilisez des informations d’identification nCipher nShield HSM pour signer ou certifier un document PDF, les nouvelles informations d’identification ne peuvent pas être utilisées tant que le serveur d’applications J2EE sur lequel AEM Forms est déployé n’est pas redémarré. Cependant, vous pouvez définir une valeur de configuration, ce qui permet à l’opération de signature ou de certification de fonctionner sans redémarrer le serveur d’applications J2EE.

Vous pouvez ajouter la valeur de configuration suivante dans le fichier cknfastrc, qui se trouve sous /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc) :

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Après avoir ajouté cette valeur de configuration au fichier cknfastrc, les nouvelles informations d’identification peuvent être utilisées sans redémarrer le serveur d’applications J2EE.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la certification d’un document, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-5}

Pour certifier un document PDF, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Obtenez le document PDF à certifier.
1. Certifiez le document PDF.
1. Enregistrez le document PDF certifié en tant que fichier PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer par programmation une opération Signature, vous devez créer un client Signature.

**Obtenir le document PDF à certifier**

Pour certifier un document PDF, vous devez obtenir un document PDF contenant un champ de signature. Si un document PDF ne contient pas de champ de signature, il ne peut pas être certifié. Vous pouvez ajouter un champ de signature à l’aide de Designer ou par programmation. Pour plus d’informations sur l’ajout par programmation d’un champ de signature, voir [Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certifier un document PDF**

Pour certifier correctement un document PDF, vous avez besoin des valeurs d’entrée suivantes utilisées par le service Signature pour certifier un document PDF :

* **Document PDF** : un document PDF qui contient un champ de signature, qui est un champ de formulaire contenant une représentation graphique de la signature certifiée. Un document PDF doit contenir un champ de signature pour pouvoir être certifié. Vous pouvez ajouter un champ de signature à l’aide de Designer ou par programmation. (Voir [Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nom du champ de signature** : nom complet qualifié du champ de signature certifié. La valeur suivante en est un exemple : `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, le nom partiel du champ de signature peut également être utilisé : `SignatureField3[3]`. Si une valeur null est transmise comme nom du champ, un champ de signature invisible est créé et certifié dynamiquement.
* **Informations d’identification de sécurité** : informations d’identification utilisées pour certifier le document PDF. Ces informations d’identification de sécurité contiennent un mot de passe et un alias, qui doivent correspondre à un alias qui apparaît dans les informations d’identification se trouvant dans le service d’informations d’identification. L’alias correspond à des informations d’identification réelles qui peuvent se trouver dans un fichier PKCS#12 (avec une extension .pfx) ou un module de sécurité matérielle (HSM).
* **Algorithme de hachage** : algorithme de hachage à utiliser pour condenser le document PDF.
* **Motif de la signature** : une valeur qui s’affiche dans Acrobat ou Adobe Reader afin que d’autres utilisateurs connaissent le motif pour lequel le document PDF a été certifié.
* **Emplacement du signataire** : emplacement du signataire spécifié par les informations d’identification.
* **Coordonnées** : les informations de contact, telles que l’adresse et le numéro de téléphone du signataire.
* **Informations d’autorisation** : autorisations qui contrôlent les actions qu’un utilisateur final peut effectuer sur un document sans que la signature certifiée ne devienne invalide. Par exemple, vous pouvez définir l’autorisation de sorte que toute modification apportée au document PDF entraîne la non-validité de la signature certifiée.
* **Explication légale** : lorsqu’un document est certifié, il est automatiquement analysé pour rechercher des types de contenu spécifiques susceptibles de rendre le contenu d’un document ambigu ou déroutant. Par exemple, une annotation peut assombrir du texte sur une page qui est essentiel pour comprendre ce qui est certifié. Le processus d’analyse génère des avertissements concernant ces types de contenu. Cette valeur fournit une explication supplémentaire du contenu qui pourrait générer des avertissements.
* **Options d’aspect** : options qui contrôlent l’aspect de la signature certifiée. Par exemple, la signature certifiée peut afficher des informations sur la date.
* **Vérification de révocation** : cette valeur indique si la vérification de révocation est effectuée pour le certificat du signataire. Le paramètre par défaut de `false` signifie que la vérification de révocation n’est pas effectuée.
* **Paramètres OCSP** : paramètres de prise en charge du protocole OCSP (Online Certificate Status Protocol), qui fournit des informations sur l’état des informations d’identification utilisées pour certifier le document PDF. Vous pouvez, par exemple, spécifier l’URL du serveur qui fournit des informations sur les informations d’identification que vous utilisez pour vous connecter au document PDF.
* **Paramètres CRL** : paramètres des préférences de liste de révocation des certificats (CRL) si la vérification de révocation est effectuée. Par exemple, vous pouvez spécifier de toujours vérifier si des informations d’identification ont été révoquées.
* **Horodatage** : paramètres qui définissent les informations d’horodatage appliquées à la signature certifiée. Un horodatage indique que des données spécifiques ont été établies avant une certaine période. Ces connaissances contribuent à établir une relation de confiance entre le signataire et le vérificateur.

**Enregistrer le document PDF certifié en tant que fichier PDF**

Une fois que le service Signature a certifié le document PDF, vous pouvez l’enregistrer en tant que fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Certifier des documents PDF à l’aide de l’API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certifier les documents PDF à l’aide de l’API du service web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certifier des documents PDF à l’aide de l’API Java {#certify-pdf-documents-using-the-java-api}

Certifiez un document PDF à l’aide de l’API Signature (Java) :

1. Inclure les fichiers du projet

   Inclure les fichiers JAR clients, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le document PDF à certifier

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à certifier en utilisant son constructeur et en transmettant une valeur de chaîne spécifiant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Certifier le document PDF

   Certifiez le document PDF en appelant la méthode `certify` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * L’objet `com.adobe.idp.Document` représentant le document PDF à certifier.
   * Une valeur de chaîne représentant le nom du champ de signature qui contient la signature.
   * Objet `Credential` représentant les informations d’authentification utilisées pour certifier le document PDF. Créez un objet `Credential` en appelant la méthode `getInstance` statique de l’objet `Credential` et en transmettant une valeur de chaîne qui spécifie la valeur d’alias correspondant aux informations d’identification de sécurité.
   * Objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage utilisé pour résumer le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Valeur string représentant la raison pour laquelle le document PDF a été certifié.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un objet `MDPPermissions` spécifiant les actions pouvant être effectuées sur le document PDF et qui invalide la signature.
   * Un objet `PDFSignatureAppearanceOptions` qui contrôle l’aspect de la signature certifiée. Si vous le souhaitez, modifiez l’aspect de la signature en appelant une méthode, telle que `setShowDate`.
   * Une valeur de chaîne qui fournit une explication des actions qui invalident la signature.
   * Un objet `java.lang.Boolean` spécifiant si la révocation doit être vérifiée sur le certificat du signataire. Si cette vérification de la révocation est effectuée, elle est intégrée à la signature. La valeur par défaut est de `false`.
   * Objet `java.lang.Boolean` spécifiant si le champ de signature en cours de certification est verrouillé. Si le champ est verrouillé, le champ de signature est marqué comme étant en lecture seule, ses propriétés ne peuvent pas être modifiées et il ne peut pas être effacé par un utilisateur ne disposant pas d’autorisations requises. La valeur par défaut est de `false`.
   * Un objet `OCSPPreferences` qui stocke les préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`. Pour plus d’informations sur cet objet, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objet `CRLPreferences` qui stocke les préférences de liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Par exemple, après avoir créé un objet `TSPPreferences`, vous pouvez définir l’URL du serveur TSP en appelant la méthode `setTspServerURL` de l’objet `TSPPreferences`. Ce paramètre est facultatif et peut être `null`. Pour plus d’informations, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

   La méthode `certify` renvoie un objet `com.adobe.idp.Document` représentant le document PDF certifié.

1. Enregistrer le document PDF certifié en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` afin de copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier.

**Voir également**

[Certification de documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Didacticiel de mise en route (mode SOAP) : certification d’un document PDF à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certifier les documents PDF à l’aide de l’API du service web {#certify-pdf-documents-using-the-web-service-api}

Certifiez un document PDF à l’aide de l’API Signature (service web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le document PDF à certifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF certifié.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement fichier du document PDF à certifier et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à som membre de données `MTOM` le contenu du tableau d’octets.

1. Certifier le document PDF

   Certifiez le document PDF en appelant la méthode `certify` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * L’objet `BLOB` représentant le document PDF à certifier.
   * Une valeur de chaîne représentant le nom du champ de signature qui contient la signature.
   * Objet `Credential` représentant les informations d’authentification utilisées pour certifier le document PDF. Créez un objet `Credential` en utilisant son constructeur, puis spécifiez l’alias en affectant une valeur à la propriété `alias` de l’objet `Credential`.
   * Objet `HashAlgorithm` spécifiant un membre de données statique qui représente l’algorithme de hachage utilisé pour résumer le document PDF. Par exemple, vous pouvez spécifier `HashAlgorithm.SHA1` pour utiliser l’algorithme SHA1.
   * Valeur booléenne spécifiant si l’algorithme de hachage est utilisé.
   * Valeur string représentant la raison pour laquelle le document PDF a été certifié.
   * Une valeur de chaîne qui représente l’emplacement du ou de la signataire.
   * Une valeur de chaîne qui représente les informations de contact du ou de la signataire.
   * Un membre de données statique de l’objet `MDPPermissions` spécifiant les actions pouvant être effectuées sur le document PDF qui invalide la signature.
   * Valeur booléenne spécifiant s’il faut utiliser l’objet `MDPPermissions` qui a été transmis comme valeur du paramètre précédent.
   * Valeur string expliquant les actions qui invalident la signature.
   * Objet `PDFSignatureAppearanceOptions` contrôlant l’aspect de la signature certifiée. Créez un objet `PDFSignatureAppearanceOptions` en utilisant son constructeur. Vous pouvez modifier l’aspect de la signature en définissant l’un de ses membres de données.
   * Objet `System.Boolean` spécifiant si la révocation doit être vérifiée sur le certificat du signataire. Si cette vérification de la révocation est effectuée, elle est intégrée à la signature. La valeur par défaut est de `false`.
   * Objet `System.Boolean` spécifiant si le champ de signature en cours de certification est verrouillé. Si le champ est verrouillé, le champ de signature est marqué comme étant en lecture seule, ses propriétés ne peuvent pas être modifiées et il ne peut pas être effacé par un utilisateur ne disposant pas d’autorisations requises. La valeur par défaut est de `false`.
   * Objet `System.Boolean` spécifiant si le champ de signature est verrouillé. Autrement dit, si vous transmettez `true` au paramètre précédent, transmettez `true` à ce paramètre.
   * Objet `OCSPPreferences` stockant des préférences pour la prise en charge du protocole OCSP (Online Certificate Status Protocol), qui fournit des informations sur le statut des informations d’identification utilisées pour certifier le document PDF. Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `CRLPreferences` stockant les préférences de la liste de révocation des certificats (CRL). Si la vérification de révocation n’est pas effectuée, ce paramètre n’est pas utilisé et vous pouvez spécifier `null`.
   * Objet `TSPPreferences` stockant les préférences pour la prise en charge du fournisseur d’horodatage (TSP). Par exemple, après avoir créé un objet `TSPPreferences`, vous pouvez définir l’URL du TSP en définissant le membre de données `tspServerURL` de l’objet `TSPPreferences`. Ce paramètre est facultatif et peut être `null`.

   La méthode `certify` renvoie un objet `BLOB` représentant le document PDF certifié.

1. Enregistrer le document PDF certifié en tant que fichier PDF

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF qui contiendra le document PDF certifié et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode `certify`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Certification de documents PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Vérifier des signatures numériques {#verifying-digital-signatures}

Les signatures numériques peuvent être vérifiées pour vous assurer qu’un document PDF signé n’a pas été modifié et que la signature numérique est valide. Lors de la vérification d’une signature numérique, vous pouvez vérifier l’état et les propriétés de la signature, comme l’identité de la personne signataire. Avant de faire confiance à une signature numérique, il est recommandé de la vérifier. Lors de la vérification d’une signature numérique, référencez un document PDF contenant une signature numérique.

Supposons que l’identité du signataire soit inconnue. Lorsque vous ouvrez le document PDF dans Acrobat, un message d’avertissement indique que l’identité du signataire est inconnue, comme illustré ci-dessous.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

De même, lorsque vous vérifiez par programmation une signature numérique, vous pouvez déterminer le statut de l’identité duou de la signataire. Par exemple, si vous vérifiez la signature numérique dans le document illustré précédemment, il en ressort que l’identité du ou de la signataire est inconnue.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la vérification des signatures numériques, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-6}

Pour vérifier une signature numérique, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Accédez au document PDF contenant la signature à vérifier.
1. Définissez les options d’exécution PKI.
1. Vérifiez la signature numérique.
1. Déterminez le statut de la signature.
1. Déterminez l’identité du signataire.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer une opération du service Signature par programmation, créez un client de service Signature.

**Accéder au document PDF contenant la signature à vérifier**

Pour vérifier une signature utilisée pour signer ou certifier numériquement un document PDF, accédez à un document PDF contenant une signature.

**Définir des options d’exécution PKI**

Définissez les options d’exécution PKI que le service Signature utilise lors de la vérification des signatures dans un document PDF :

* Heure de vérification
* Vérification de la révocation
* Valeurs d’horodatage

Dans le cadre de la définition de ces options, vous pouvez indiquer l’heure de vérification. Par exemple, vous pouvez sélectionner l’heure actuelle (l’heure sur l’ordinateur du programme de validation), qui indique d’utiliser l’heure actuelle. Pour plus d’informations sur les différentes valeurs temporelles, reportez-vous à la valeur d’énumération `VerificationTime` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Vous pouvez également indiquer si la vérification de révocation doit être effectuée dans le cadre du processus de vérification. Par exemple, vous pouvez effectuer une vérification de révocation pour déterminer si le certificat est révoqué. Pour plus d’informations sur les options de vérification de révocation, reportez-vous à la valeur d’énumération `RevocationCheckStyle` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Pour effectuer une vérification de révocation sur un certificat, spécifiez une URL vers un serveur de la liste de révocation des certificats (CRL) à l’aide d’un objet `CRLOptionSpec`. Cependant, si vous ne spécifiez pas d’URL au serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP plutôt qu’un serveur CRL, la vérification de révocation est plus rapide. (Voir [Protocole OCSP (Online Certificate Status Protocol)](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir la liste de révocation des certificats et l’ordre du serveur OCSP que le service Signature utilise à l’aide des applications et services Adobe. Par exemple, si le serveur OCSP est d’abord défini dans Applications et services Adobe, alors le serveur OCSP est vérifié, suivi du serveur CRL.

Si vous n’effectuez pas de vérification de révocation, le service Signature ne vérifie pas si le certificat est révoqué. En d’autres termes, les informations des serveurs CRL et OCSP sont ignorées.

>[!NOTE]
>
>Vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’une `CRLOptionSpec` et d’un objet `OCSPOptionSpec`. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la méthode `setLocalURI` de l’objet `CRLOptionSpec`.

L’horodatage est le processus de suivi de l’heure de modification d’un document signé ou certifié. Une fois le document signé, personne ne peut le modifier. L’horodatage aide à assurer la validité d’un document signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un objet `TSPOptionSpec`. Par exemple, vous pouvez spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>Dans les démarrages rapides Java et de service web, l’heure de vérification est définie sur `VerificationTime.CURRENT_TIME` et la vérification de révocation est définie sur `RevocationCheckStyle.BestEffort`. Étant donné qu’aucune information du serveur CRL ou OCSP n’est spécifiée, les informations du serveur sont obtenues à partir du certificat.

**Vérifier la signature numérique**

Pour vérifier une signature, indiquez le nom qualifié complet du champ de signature qui contient la signature, tel que `form1[0].#subform[1].SignatureField3[3]`. Lors de l’utilisation d’un champ de formulaire XFA, vous pouvez également utiliser le nom partiel du champ de signature : `SignatureField3`.

Par défaut, le service Signature limite à 65 minutes la durée pendant laquelle un document peut être signé après validation. Si un utilisateur tente de vérifier une signature à l’heure actuelle et que l’heure de signature est postérieure à l’heure actuelle et se situe dans les 65 minutes, le service Signature ne crée pas d’erreur de vérification.

>[!NOTE]
>
>Pour connaître les autres valeurs dont vous avez besoin lors de la vérification d’une signature, voir [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Déterminer l’état de la signature**

Dans le cadre de la vérification d’une signature numérique, vous pouvez vérifier l’état de la signature.

**Déterminer l’identité du signataire**

Vous pouvez déterminer l’identité du signataire, qui peut être l’une des valeurs suivantes :

* **Inconnu** : ce signataire est inconnu, car la vérification du signataire ne peut pas être effectuée.
* **Fiable** : ce signataire est fiable.
* **Non fiable** : ce signataire n’est pas fiable.

**Voir également**

[Vérifier des signatures numériques à l’aide de l’API Java](#verify-digital-signatures-using-the-java-api)

[Vérifier des signatures numériques à l’aide de l’API de service web](#verify-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérifier des signatures numériques à l’aide de l’API Java {#verify-digital-signatures-using-the-java-api}

Vérifiez une signature numérique à l’aide de l’API du service Signature (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Obtenir le document PDF qui contient la signature à vérifier

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF contenant la signature à vérifier à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir les options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en appelant la méthode `setVerificationTime` de l’objet `PKIOptions` et en transmettant une valeur d’énumération `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de la révocation en appelant la méthode `setRevocationCheckStyle` de l’objet `PKIOptions` et en transmettant une valeur d’énumération `RevocationCheckStyle` qui spécifie s’il faut effectuer une vérification de révocation.

1. Vérifier la signature numérique

   Vérifiez la signature en appelant la méthode `verify2` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` qui contient un document PDF signé numériquement ou certifié.
   * Valeur de chaîne représentant le nom du champ de signature qui contient la signature à vérifier.
   * Un objet `PKIOptions` qui contient des options d’exécution PKI.
   * Une instance `VerifySPIOptions` qui contient des informations SPI. Vous pouvez spécifier `null` pour ce paramètre.

   La méthode `verify2` renvoie un objet `PDFSignatureVerificationInfo` qui contient des informations pouvant être utilisées pour vérifier la signature numérique.

1. Déterminer le statut de la signature

   * Déterminez le statut de la signature en appelant la méthode `getStatus` de l’objet `PDFSignatureVerificationInfo`. Cette méthode renvoie un objet `SignatureStatus` qui spécifie le statut de la signature. Par exemple, si un document PDF signé n’est pas modifié, cette méthode renvoie `SignatureStatus.DocumentSigNoChanges`.

1. Déterminer l’identité du signataire

   * Déterminez l’identité du ou de la signataire en appelant la méthode `getSigner` de l’objet `PDFSignatureVerificationInfo`. Cette méthode renvoie un objet `IdentityInformation`.
   * Appelez la méthode `getStatus` de l’objet `IdentityInformation` pour déterminer l’identité du ou de la signataire. Cette méthode renvoie une valeur d’énumération `IdentityStatus` qui spécifie l’identité. Par exemple, si le signataire est approuvé, cette méthode renvoie `IdentityStatus.TRUSTED`.

**Voir également**

[Vérifier des signatures numériques](#verify-digital-signatures-using-the-java-api)

[Didacticiel de mise en route (mode SOAP) : vérification d’une signature numérique à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérifier des signatures numériques à l’aide de l’API de service web {#verify-digital-signatures-using-the-web-service-api}

Vérifiez une signature numérique en utilisant l’API du service Signature (Web Service) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenir le document PDF qui contient la signature à vérifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF qui contient une signature numérique ou certifiée à vérifier.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier du document PDF signé et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Définir les options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en affectant au membre de données `verificationTime` de l’objet `PKIOptions` une valeur d’énumération `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en attribuant au membre de données `revocationCheckStyle` de l’objet `PKIOptions` une valeur d’énumération `RevocationCheckStyle` qui indique s’il faut effectuer une vérification de révocation.

1. Vérifier la signature numérique

   Vérifiez la signature en appelant la méthode `verify2` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant un document PDF signé numériquement ou certifié.
   * Valeur de chaîne représentant le nom du champ de signature qui contient la signature à vérifier.
   * Un objet `PKIOptions` qui contient des options d’exécution PKI.
   * Une instance `VerifySPIOptions` qui contient des informations SPI. Vous pouvez spécifier `null` pour ce paramètre.

   La méthode `verify2` renvoie un objet `PDFSignatureVerificationInfo` qui contient des informations pouvant être utilisées pour vérifier la signature numérique.

1. Déterminer le statut de la signature

   Déterminez le statut de la signature en obtenant la valeur du membre de données `status` de l’objet `PDFSignatureVerificationInfo`. Ce membre de données stocke un objet `SignatureStatus` indiquant le statut de la signature. Par exemple, si un document PDF signé est modifié, le membre de données `status` stocke la valeur `SignatureStatus.DocumentSigNoChanges`.

1. Déterminer l’identité du signataire

   * Déterminez l’identité du ou de la signataire en récupérant la valeur du membre de données `signer` de l’objet `PDFSignatureVerificationInfo`. Ce membre renvoie un objet `IdentityInformation`.
   * Récupérez le membre de données `status` de l’objet `IdentityInformation` pour déterminer l’identité du ou de la signataire. Ce membre de données renvoie une valeur d’énumération `IdentityStatus` indiquant l’identité. Par exemple, si le signataire est fiable, ce membre renvoie `IdentityStatus.TRUSTED`.

**Voir également**

[Vérifier des signatures numériques](#verify-digital-signatures-using-the-java-api)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Vérification de plusieurs signatures numériques {#verifying-multiple-digital-signatures}

AEM Forms permet de vérifier toutes les signatures numériques qui se trouvent dans un document PDF. Supposons qu’un document PDF contienne plusieurs signatures numériques suite à un processus d’entreprise qui requiert des signatures de plusieurs signataires. Prenons l’exemple d’une transaction financière qui requiert à la fois la signature d’un agent ou d’une agente de prêt et celle d’un dirigeant ou d’une dirigeante. Vous pouvez utiliser l’API du service Signature pour vérifier toutes les signatures contenues dans un document PDF. Lors de la vérification de plusieurs signatures numériques, vous pouvez vérifier l’état et les propriétés de chaque signature. Avant d’approuver une signature numérique, il est recommandé de la vérifier. Il est recommandé de vous familiariser avec la vérification d’une signature numérique unique.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature et la vérification des signatures numériques, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-7}

Pour vérifier plusieurs signatures numériques, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Accédez au document PDF qui contient les signatures à vérifier.
1. Définissez les options d’exécution PKI.
1. Récupérez toutes les signatures numériques.
1. Effectuez une itération sur toutes les signatures.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer une opération du service Signature par programmation, créez un client de service Signature.

**Accéder au document PDF contenant les signatures à vérifier**

Pour vérifier une signature utilisée pour signer ou certifier numériquement un document PDF, accédez à un document PDF contenant une signature.

**Définir des options d’exécution PKI**

Définissez les options d’exécution PKI que le service Signature utilise lors de la vérification de toutes les signatures dans un document PDF :

* Heure de vérification
* Vérification de la révocation
* Valeurs d’horodatage

Dans le cadre de la définition de ces options, vous pouvez indiquer l’heure de vérification. Par exemple, vous pouvez sélectionner l’heure actuelle (l’heure sur l’ordinateur du programme de validation), qui indique d’utiliser l’heure actuelle. Pour plus d’informations sur les différentes valeurs temporelles, reportez-vous à la valeur d’énumération `VerificationTime` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Vous pouvez également indiquer si la vérification de révocation doit être effectuée dans le cadre du processus de vérification. Par exemple, vous pouvez effectuer une vérification de révocation pour déterminer si le certificat est révoqué. Pour plus d’informations sur les options de vérification de révocation, reportez-vous à la valeur d’énumération `RevocationCheckStyle` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Pour effectuer une vérification de révocation sur un certificat, spécifiez une URL à un serveur de liste de révocation des certificats (CRL) à l’aide d’un objet `CRLOptionSpec`. Cependant, si vous ne spécifiez pas d’URL à un serveur CRL, le service Signature obtient l’URL à partir du certificat.

Au lieu d’utiliser un serveur CRL, vous pouvez utiliser un serveur OCSP (Online Certificate Status Protocol) lors de la vérification de révocation. En règle générale, lorsque vous utilisez un serveur OCSP plutôt qu’un serveur CRL, la vérification de révocation est plus rapide. (Voir [Protocole OCSP (Online Certificate Status Protocol)](https://tools.ietf.org/html/rfc2560).)

Vous pouvez définir la liste de révocation des certificats et l’ordre du serveur OCSP que le service Signature utilise à l’aide des applications et services Adobe. Par exemple, si le serveur OCSP est défini en premier dans Applications et services Adobe, le serveur OCSP est d’abord vérifié, suivi du serveur CRL.

Si vous n’effectuez pas de vérification de révocation, le service Signature ne vérifie pas si le certificat est révoqué. En d’autres termes, les informations des serveurs CRL et OCSP sont ignorées.

>[!NOTE]
>
>Vous pouvez remplacer l’URL spécifiée dans le certificat à l’aide d’une `CRLOptionSpec` et d’un objet `OCSPOptionSpec`. Par exemple, pour remplacer le serveur CRL, vous pouvez appeler la méthode `setLocalURI` de l’objet `CRLOptionSpec`.

L’horodatage est le processus de suivi de l’heure de modification d’un document signé ou certifié. Une fois le document signé, personne ne peut le modifier. L’horodatage aide à assurer la validité d’un document signé ou certifié. Vous pouvez définir des options d’horodatage à l’aide d’un objet `TSPOptionSpec`. Par exemple, vous pouvez spécifier l’URL d’un serveur de fournisseur d’horodatage (TSP).

>[!NOTE]
>
>Dans les démarrages rapides Java et de service web, l’heure de vérification est définie sur `VerificationTime.CURRENT_TIME` et la vérification de révocation est définie sur `RevocationCheckStyle.BestEffort`. Étant donné qu’aucune information du serveur CRL ou OCSP n’est spécifiée, les informations du serveur sont obtenues à partir du certificat.

**Récupérer toutes les signatures numériques**

Pour vérifier toutes les signatures numériques figurant dans un document PDF, récupérez les signatures numériques du document PDF. Toutes les signatures sont renvoyées dans une liste. Dans le cadre de la vérification d’une signature numérique, vérifiez l’état de la signature.

>[!NOTE]
>
>Contrairement à ce qui se passe lorsque vous vérifiez une signature numérique unique, lorsque vous vérifiez plusieurs signatures, vous n’avez pas à spécifier le nom du champ de signature.

**Effectuer une itération sur toutes les signatures**

Effectuez une itération sur chaque signature. Autrement dit, pour chaque signature, vérifiez la signature numérique, l’identité du ou de la signataire ainsi que le satut de chaque signature. (Voir [Vérifier des signatures numériques](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Vous n’avez pas besoin d’effectuer une itération sur toutes les signatures si l’exigence correspond à l’intégralité du document.

**Voir également**

[Vérifier plusieurs signatures numériques à l’aide de l’API Java](#verify-digital-signatures-using-the-java-api)

[Vérifier plusieurs signatures numériques à l’aide de l’API Web Service](#verify-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérifier plusieurs signatures numériques à l’aide de l’API Java {#verify-multiple-digital-signatures-using-the-java-api}

Vérifiez plusieurs signatures numériques à l’aide de l’API du service Signature (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer une Signature client

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Accéder au document PDF contenant les signatures à vérifier

   * Créez un objet `java.io.FileInputStream` représentant le document PDF contenant plusieurs signatures numériques à vérifier à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définir des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en appelant la méthode `setVerificationTime` de l’objet `PKIOptions` et en transmettant une valeur d’énumération `VerificationTime` qui spécifie l’heure de vérification.
   * Définissez l’option de vérification de révocation en appelant la méthode `setRevocationCheckStyle` de l’objet `PKIOptions` et en transmettant une valeur d’énumération `RevocationCheckStyle` qui spécifie s’il faut effectuer une vérification de révocation.

1. Récupérer toutes les signatures numériques

   Appelez la méthode `verifyPDFDocument` de l’objet `SignatureServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant un document PDF contenant plusieurs signatures numériques.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Une instance `VerifySPIOptions` qui contient des informations SPI. Vous pouvez spécifier `null` pour ce paramètre.

   La méthode `verifyPDFDocument` renvoie un objet `PDFDocumentVerificationInfo` qui contient des informations sur toutes les signatures numériques figurant dans le document PDF.

1. Faire une itération sur toutes les signatures

   * Itérez toutes les signatures en appelant la méthode `getVerificationInfos` de l’objet `PDFDocumentVerificationInfo`. Cette méthode renvoie un objet `java.util.List` dont chaque élément est un objet `PDFSignatureVerificationInfo`. Utilisez un objet `java.util.Iterator` pour effectuer une itération sur la liste des signatures.
   * Avec l’objet `PDFSignatureVerificationInfo`, vous pouvez effectuer des tâches telles que déterminer le statut de la signature en appelant la méthode `getStatus` de l’objet `PDFSignatureVerificationInfo`. Cette méthode renvoie un objet `SignatureStatus` dont le membre de données statique vous informe sur le statut de la signature. Par exemple, si la signature est inconnue, cette méthode renvoie la valeur `SignatureStatus.DocumentSignatureUnknown`.

**Voir également**

[Vérification de plusieurs signatures numériques](#verifying-multiple-digital-signatures)

[Didacticiel de mise en route (mode SOAP) : vérification de plusieurs signatures numériques à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Vérifier des signatures numériques](#verify-digital-signatures-using-the-java-api)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Vérifier plusieurs signatures numériques à l’aide de l’API du service web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Vérifiez plusieurs signatures numériques à l’aide de l’API du service de signature (service Web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Accéder au document PDF contenant les signatures à vérifier

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` stocke un document PDF qui contient plusieurs signatures numériques à vérifier.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Définir des options d’exécution PKI

   * Créez un objet `PKIOptions` en utilisant son constructeur.
   * Définissez l’heure de vérification en attribuant au membre de données `verificationTime` de l’objet `PKIOptions` une valeur d’énumération `VerificationTime` spécifiant l’heure de vérification.
   * Définissez l’option de vérification de révocation en attribuant au membre de données `revocationCheckStyle` de l’objet `PKIOptions` une valeur d’énumération `RevocationCheckStyle` qui spécifie s’il faut effectuer une vérification de révocation.

1. Récupérer toutes les signatures numériques

   Appelez la méthode `verifyPDFDocument` de l’objet `SignatureServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant un document PDF contenant plusieurs signatures numériques.
   * Objet `PKIOptions` contenant des options d’exécution PKI.
   * Un objet `VerifySPIOptions` contenant des informations SPI. Vous pouvez spécifier la valeur null pour ce paramètre.

   La méthode `verifyPDFDocument` renvoie un objet `PDFDocumentVerificationInfo` qui contient des informations sur toutes les signatures numériques figurant dans le document PDF.

1. Faire une itération sur toutes les signatures

   * Faites une itération sur toutes les signatures en obtenant le membre de données `verificationInfos` de l’objet `PDFDocumentVerificationInfo`. Ce membre de données renvoie un tableau `Object` où chaque élément représente un objet `PDFSignatureVerificationInfo`.
   * En utilisant l’objet `PDFSignatureVerificationInfo`, vous pouvez effectuer des tâches comme déterminer le statut de la signature en obtenant le membre de données `status` de l’objet `PDFSignatureVerificationInfo`. Ce membre de données renvoie un objet `SignatureStatus` dont le membre de données statique vous informe de l’état de la signature. Par exemple, si la signature est inconnue, cette méthode renvoie `SignatureStatus.DocumentSignatureUnknown`.

**Voir également**

[Vérification de plusieurs signatures numériques](#verifying-multiple-digital-signatures)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Supprimer des signatures numériques {#removing-digital-signatures}

Les signatures numériques doivent être supprimées d’un champ de signature pour qu’une signature numérique plus récente puisse être appliquée. Une signature numérique ne peut pas être remplacée. Si vous tentez d’apposer une signature numérique à un champ de signature contenant déjà une signature, une exception sera générée.

>[!NOTE]
>
>Pour plus d’informations sur le service Signature, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-8}

Pour supprimer une signature numérique d’un champ de signature, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Signature.
1. Accédez au document PDF contenant une signature à supprimer.
1. Supprimez la signature numérique du champ de signature.
1. Enregistrez le document PDF au format PDF.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Vous devez ajouter les fichiers JAR suivants au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Signature**

Avant d’effectuer par programmation une opération du service Signature, vous devez créer un client du service Signature.

**Accéder au document PDF contenant une signature à supprimer**

Pour supprimer une signature dans un document PDF, vous devez accéder à un document PDF contenant une signature.

**Supprimer la signature numérique du champ de signature**

Pour supprimer une signature numérique d’un document PDF, vous devez indiquer le nom du champ de signature qui contient la signature numérique. Vous devez également disposer des autorisations nécessaires pour supprimer la signature numérique ; dans le cas contraire, une exception se produit.

**Enregistrer le document PDF en tant que fichier PDF**

Une fois que le service Signature a supprimé une signature numérique d’un champ de signature, vous pouvez enregistrer le document PDF en tant que fichier PDF afin que les utilisateurs puissent l’ouvrir dans Acrobat ou Adobe Reader.

**Voir également**

[Supprimer des signatures numériques à l’aide de l’API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Supprimer des signatures numériques à l’aide de l’API de service web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Ajouter des champs de signature](digitally-signing-certifying-documents.md#adding-signature-fields)

### Supprimer des signatures numériques à l’aide de l’API Java {#remove-digital-signatures-using-the-java-api}

Supprimez une signature numérique à l’aide de l’API de signature (Java) :

1. Inclure les fichiers du projet

   Inclure les fichiers JAR clients, tels que adobe-signatures-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Signature.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `SignatureServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Accéder au document PDF contenant une signature à supprimer

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF contenant la signature à supprimer en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Supprimer la signature numérique du champ de signature

   Supprimez la signature numérique d’un champ de signature en appelant la méthode `clearSignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document PDF contenant la signature à supprimer.
   * Une valeur de chaîne qui spécifie le nom du champ de signature qui contient la signature numérique.

   La méthode `clearSignatureField` renvoie un objet `com.adobe.idp.Document` qui représente le document PDF dont la signature numérique a été supprimée.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
   * Appelez la méthode `copyToFile` de lʼobjet `com.adobe.idp.Document`. Transmettez l’objet `java.io.File` pour copier le contenu de l’objet `com.adobe.idp.Document` dans le fichier. Assurez-vous d’utiliser l’objet `Document` qui a été retourné par la méthode `clearSignatureField`.

**Voir également**

[Supprimer des signatures numériques](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Didacticiel de mise en route (mode SOAP) : suppression d’une signature numérique à l’aide de l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Supprimer des signatures numériques à l’aide de l’API de service web {#remove-digital-signatures-using-the-web-service-api}

Supprimez une signature numérique en utilisant l’API de signature (service Web) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer une Signature client

   * Créez un objet `SignatureServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `SignatureServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/SignatureService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `SignatureServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Accéder au document PDF contenant une signature à supprimer

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF qui contient une signature numérique à supprimer.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à sa propriété `MTOM`.

1. Supprimer la signature numérique du champ de signature

   Supprimez la signature numérique en appelant la méthode `clearSignatureField` de l’objet `SignatureServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `BLOB` qui contient le document PDF signé.
   * Une valeur de chaîne représentant le nom du champ de signature qui contient la signature numérique à supprimer.

   La méthode `clearSignatureField` renvoie un objet `BLOB` qui représente le document PDF dont la signature numérique a été supprimée.

1. Enregistrer le document PDF en tant que fichier PDF

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF contenant un champ de signature vide et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode de `sign`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Supprimer des signatures numériques](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
