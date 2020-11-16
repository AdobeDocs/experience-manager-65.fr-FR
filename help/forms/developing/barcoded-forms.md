---
title: Utilisation de formulaires à code à barres
seo-title: Utilisation de formulaires à code à barres
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 2%

---


# Utilisation de formulaires à code à barres {#working-with-barcoded-forms}

## A propos du service Barcoded Forms {#about-the-barcoded-forms-service}

Le service Barcoded Forms automatise la capture des données des formulaires à remplir et à imprimer et intègre les informations capturées dans les systèmes informatiques principaux d’une entreprise.

Grâce au service Barcoded Forms, vous pouvez ajouter des codes à barres unidimensionnels et bidimensionnels aux PDF forms interactifs. Vous pouvez ensuite publier les formulaires à code à barres sur un site Web ou les distribuer par courrier électronique ou CD. Lorsqu’un utilisateur remplit un formulaire à code à barres à l’aide d’Adobe Reader, Acrobat Professional ou Acrobat Standard, le code à barres est mis à jour automatiquement afin de coder les données de formulaire fournies par l’utilisateur. L’utilisateur peut envoyer le formulaire par voie électronique ou l’imprimer sur papier et l’envoyer par la poste, par télécopieur ou par la main. Vous pourrez ensuite extraire les données fournies par l’utilisateur dans le cadre d’un processus automatisé, en les routage entre les processus d’approbation et les systèmes d’entreprise.

For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Décodage des données de formulaire à code à barres {#decoding-barcoded-form-data}

Vous pouvez utiliser l’API du service Barcoded Forms pour décoder les données d’un formulaire PDF ou d’une image contenant un code à barres. Le décodage des données de formulaire consiste à extraire les données qui se trouvent dans le code à barres. Avant de pouvoir décoder des données à partir d’un formulaire PDF (ou d’une image), un utilisateur doit renseigner le formulaire avec des données.

>[!NOTE]
>
>For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour décoder les données d’un formulaire PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un objet API Barcoded FormsClient.
1. Obtenez un formulaire PDF contenant des données à code à barres.
1. Décodez les données du formulaire PDF.
1. Convertissez les données en une source de données XML.
1. Traitez les données décodées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)
* xercesImpl.jar (situé dans &lt;répertoire d’installation>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBOSS, vous devrez remplacer adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API client de formulaires à code à barres**

Avant de pouvoir exécuter par programmation une opération de service Barcoded Forms, vous devez créer un client de service Forms Barcoded. Si vous utilisez l’API Java, créez un `BarcodedFormsServiceClient` objet. Si vous utilisez l’API du service Web de formulaires à code à barres, créez un `BarcodedFormsServiceService` objet.

**Obtenir un formulaire PDF contenant des données à code à barres**

Vous devez obtenir un formulaire PDF contenant un code à barres rempli de données utilisateur.

**Décoder les données du formulaire PDF**

Après avoir obtenu un formulaire PDF (ou une image) contenant un code à barres, vous pouvez décoder les données. Le service Barcoded Forms prend en charge les types de codes à barres suivants :

* Codes à barres PDF417.
* Codes à barres de matrice de données.
* Codes à barres de code QR.
* Codes à barres de codes à barres de code.
* Codes à barres Code 128.
* Codes à barres Code 39.
* Codes à barres EAN-13.
* Codes à barres EAN-8.

L’entrée de jeu de caractères au format hexadécimal dans l’API de décodage implique que le contenu du code à barres soit codé en tant que chaîne hexadécimale. Par exemple, si le codage UTF-8 est spécifié en tant que codage de caractères dans le formulaire et que Hex est spécifié dans l’opération de décodage, le contenu du code à barres est codé en tant que chaîne hexadécimale dans l’élément &lt; `xb:content`> de la sortie décodée. Vous pouvez convertir cette valeur hexadécimale pour obtenir le contenu d’origine en créant une logique d’application dans votre application cliente.

**Convertir les données en une source de données XML**

Après avoir décodé les données de formulaire, vous pouvez les convertir en données XDP ou XFDF. Supposons, par exemple, que vous souhaitiez importer les données dans un autre formulaire. Pour importer les données dans un formulaire XFA, vous devez convertir les données en données XDP. Pour plus d’informations, voir [Importation de données](/help/forms/developing/importing-exporting-data.md#importing-form-data)de formulaire.

**Traiter les données décodées**

Vous pouvez traiter les données converties pour répondre aux besoins de votre entreprise. Par exemple, après avoir décodé et converti les données, vous pouvez les enregistrer dans un fichier, les stocker dans une base de données d’entreprise, remplir un autre formulaire, etc. Cette section explique comment enregistrer les données converties sous la forme d’un fichier XML.

>[!NOTE]
>
>Le service Barcoded Forms ne parvient pas à décoder les données de code à barres lorsque les paramètres de délimiteur de ligne et de champ ont la même valeur.

**Voir également**

[Décoder les données de formulaire à code à barres à l’aide de l’API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Décoder les données de formulaire à code à barres à l’aide de l’API du service Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décoder les données de formulaire à code à barres à l’aide de l’API Java {#decode-barcoded-form-data-using-the-java-api}

Décodez les données de formulaire à l’aide de l’API de formulaires à code à barres (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création d’un objet API client de formulaires à code à barres

   Créez un `BarcodedFormsServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Obtenir un formulaire PDF contenant des données à code à barres

   * Créez un `java.io.FileInputStream` objet qui représente le formulaire PDF contenant des données à code à barres à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la `BarcodedFormsServiceClient` méthode de l’ `decode` objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le formulaire PDF.
   * Objet `java.lang.Boolean` spécifiant si un code à barres PDF417 doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres de matrice de données doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres de code QR doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres de codes à barres doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres 128 doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres code 39 doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres EAN-13 doit être décodé.
   * Objet `java.lang.Boolean` spécifiant si un code à barres EAN-8 doit être décodé.
   * Valeur de `com.adobe.livecycle.barcodedforms.CharSet` énumération spécifiant la valeur de codage du jeu de caractères utilisée dans le code à barres.

   La `decode` méthode renvoie un `org.w3c.dom.Document` objet contenant des données de formulaire décodées.

1. Convertir les données en une source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la `BarcodedFormsServiceClient` `extractToXML` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `org.w3c.dom.Document` contenant des données décodées (veillez à utiliser la valeur de retour de la `decode` méthode).
   * Valeur de `com.adobe.livecycle.barcodedforms.Delimiter` énumération spécifiant le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Valeur de `com.adobe.livecycle.barcodedforms.Delimiter` énumération spécifiant le délimiteur de champ. For example, specify `Delimiter.Tab`.
   * Valeur de `com.adobe.livecycle.barcodedforms.XMLFormat` énumération qui spécifie si les données du code à barres doivent être converties en données XML XDP ou XFDF. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La `extractToXML` méthode renvoie un `java.util.List` objet où chaque élément est un `org.w3c.dom.Document` objet. Il existe un élément distinct pour chaque code à barres situé dans le formulaire. En d’autres termes, s’il y a quatre codes à barres sur le formulaire, il y a quatre éléments dans l’ `java.util.List` objet renvoyé.

1. Traiter les données décodées

   * Effectuez une itération sur l’ `java.util.List` objet pour obtenir chaque `org.w3c.dom.Document` objet situé dans la liste.
   * Pour chaque élément de la liste, convertissez l’ `org.w3c.dom.Document` objet en `com.adobe.idp.Document` objet. (La logique d’application qui convertit un `org.w3c.dom.Document` objet en `com.adobe.idp.Document` objet est présentée dans les données de formulaire à code à barres de décodage à l’aide de l’exemple d’API Java).
   * Enregistrez les données XML sous la forme d’un fichier XML en appelant l’objet `com.adobe.idp.Document` `copyToFile`et en transmettant un objet File représentant le fichier XML.

**Voir également**

[Début rapide (mode SOAP) : Décodage des données de formulaire à code à barres à l’aide de l’API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décoder les données de formulaire à code à barres à l’aide de l’API du service Web {#decode-barcoded-form-data-using-the-web-service-api}

Décodez les données de formulaire à l’aide de l’API de formulaires à code à barres (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le WSDL du service de formulaires à code à barres. Pour plus d’informations, voir [Appel d’AEM Forms à l’aide du codage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.
   * Référencez l&#39;assembly client Microsoft .NET. Pour plus d&#39;informations, voir &quot;Référence à l&#39;assembly client .NET&quot; dans [Appel d&#39;AEM Forms à l&#39;aide du codage](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.

1. Création d’un objet API client de formulaires à code à barres

   A l’aide de l’assembly client Microsoft .NET qui consomme le fichier WSDL du service Barcoded Forms, créez un `BarcodedFormsServiceService` objet en appelant son constructeur par défaut.

1. Obtenir un formulaire PDF contenant des données à code à barres

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF contenant un code à barres.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en attribuant sa `binaryData` propriété au contenu du tableau d’octets.

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la `BarcodedFormsServiceService` méthode de l’ `decode` objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le formulaire PDF.
   * Objet `Boolean` spécifiant si un code à barres PDF417 doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres de matrice de données doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres de code QR doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres de codes à barres doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres 128 doit être décodé.
   * Objet `Bolean` spécifiant si un code à barres code 39 doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres EAN-13 doit être décodé.
   * Objet `Boolean` spécifiant si un code à barres EAN-8 doit être décodé.
   * Valeur de `CharSet` énumération spécifiant la valeur de codage du jeu de caractères utilisée dans le code à barres.

   La `decode` méthode renvoie une valeur de chaîne contenant des données de formulaire décodées.

1. Convertir les données en une source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la `BarcodedFormsServiceService` `extractToXML` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur de chaîne contenant des données décodées (veillez à utiliser la valeur renvoyée par la `decode` méthode).
   * Valeur de `Delimiter` énumération spécifiant le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Valeur de `Delimiter` énumération spécifiant le délimiteur de champ. For example, specify `Delimiter.Tab`.
   * Valeur de `XMLFormat` énumération qui spécifie si les données du code à barres doivent être converties en données XML XDP ou XFDF. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La `extractToXML` méthode renvoie un `Object` tableau où chaque élément est une `BLOB` instance. Il existe un élément distinct pour chaque code à barres situé dans le formulaire. En d’autres termes, s’il y a quatre codes à barres sur le formulaire, il y a quatre éléments dans le `Object` tableau renvoyé.

1. Traiter les données décodées

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `encryptPDFUsingPassword` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` de données de l’ `binaryData` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
