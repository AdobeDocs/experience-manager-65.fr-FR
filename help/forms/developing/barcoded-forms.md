---
title: Utilisation de formulaires à code-barres
seo-title: Utilisation de formulaires à code-barres
description: Décodez les données d’un formulaire PDF ou d’une image contenant un code à barres à l’aide de l’API Java et de l’API Web Service.
seo-description: Décodez les données d’un formulaire PDF ou d’une image contenant un code à barres à l’aide de l’API Java et de l’API Web Service.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1945'
ht-degree: 2%

---

# Utilisation de formulaires à code-barres {#working-with-barcoded-forms}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

## À propos du service Barcoded Forms {#about-the-barcoded-forms-service}

Le service Barcoded Forms automatise la capture de données à partir de formulaires de remplissage et d’impression et intègre les informations capturées aux systèmes informatiques de base d’une entreprise.

Grâce au service Barcoded Forms, vous pouvez ajouter des codes à barres unidimensionnels et bidimensionnels aux PDF forms interactifs. Vous pouvez ensuite publier les formulaires à code-barres sur un site web ou les distribuer par email ou CD. Lorsqu’un utilisateur remplit un formulaire à code à barres à l’aide d’Adobe Reader, d’Acrobat Professional ou d’Acrobat Standard, le code à barres est automatiquement mis à jour pour coder les données de formulaire fournies par l’utilisateur. L’utilisateur peut envoyer le formulaire par voie électronique ou l’imprimer sur papier et le soumettre par courrier, par fax ou main. Vous pouvez ensuite extraire les données fournies par l’utilisateur dans le cadre d’un workflow automatisé, en acheminant les données entre les processus d’approbation et les systèmes d’entreprise.

Pour plus d’informations sur le service Barcoded Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Décodage des données de formulaire à code-barres {#decoding-barcoded-form-data}

Vous pouvez utiliser l’API du service Barcoded Forms pour décoder les données d’un formulaire PDF ou d’une image contenant un code à barres. Le décodage des données de formulaire consiste à extraire les données qui se trouvent dans le code à barres. Avant que les données ne puissent être décodées à partir d’un formulaire PDF (ou d’une image), l’utilisateur doit remplir le formulaire avec des données.

>[!NOTE]
>
>Pour plus d’informations sur le service Barcoded Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour décoder les données d’un formulaire PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un objet API Barcoded FormsClient .
1. Obtenez un formulaire PDF contenant des données à code à barres.
1. Décodez les données du formulaire PDF.
1. Convertissez les données en une source de données XML.
1. Traitez les données décodées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utility.jar (Obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)
* xercesImpl.jar (situé dans &lt;répertoire d’installation>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBOSS, vous devez remplacer adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un objet API client de formulaires à code à barres**

Avant de pouvoir effectuer par programmation une opération de service Barcoded Forms, vous devez créer un client de service Barcoded Forms. Si vous utilisez l’API Java, créez un objet `BarcodedFormsServiceClient` . Si vous utilisez l’API du service Web de formulaires à code à barres, créez un objet `BarcodedFormsServiceService` .

**Obtention d’un formulaire PDF contenant des données à code à barres**

Vous devez obtenir un formulaire PDF contenant un code à barres contenant des données utilisateur.

**Décoder les données du formulaire PDF**

Après avoir obtenu un formulaire PDF (ou une image) contenant un code à barres, vous pouvez décoder les données. Le service Barcoded Forms prend en charge les types de codes à barres suivants :

* Codes à barres PDF417.
* Codes à barres de la matrice de données.
* Codes à barres de code QR.
* Codes à barres Codabar.
* Codes à barres Code 128.
* Codes à barres Code 39.
* Codes à barres EAN-13.
* Codes à barres EAN-8.

L’entrée de jeu de caractères au format hexadécimal dans l’API de décodage implique que le contenu du code à barres soit codé en tant que chaîne hexadécimale. Par exemple, si UTF-8 est spécifié en tant que codage de caractères dans le formulaire et que Hex est spécifié dans l’opération de décodage, le contenu du code à barres est codé en tant que chaîne hexadécimale dans l’élément &lt; &lt;a0/&quot; dans la sortie décodée. `xb:content` Vous pouvez convertir cette valeur Hex pour obtenir le contenu d’origine en créant la logique d’application dans votre application cliente.

**Convertir les données en source de données XML**

Après avoir décodé les données de formulaire, vous pouvez les convertir en données XDP ou XFDF. Supposons, par exemple, que vous souhaitiez importer les données dans un autre formulaire. Pour importer les données dans un formulaire XFA, vous devez convertir les données en données XDP. Pour plus d’informations, voir [Importation de données de formulaire](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Traitement des données décodées**

Vous pouvez traiter les données converties pour répondre aux besoins de votre entreprise. Par exemple, après avoir décodé et converti les données, vous pouvez les enregistrer dans un fichier, les stocker dans une base de données d’entreprise, remplir un autre formulaire, etc. Cette section explique comment enregistrer les données converties sous la forme d’un fichier XML.

>[!NOTE]
>
>Le service Barcoded Forms ne parvient pas à décoder les données de code à barres lorsque le délimiteur de ligne et les paramètres de délimiteur de champ ont la même valeur.

**Voir également**

[Décodez les données de formulaire à code à barres à l’aide de l’API Java.](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Décodez les données de formulaire à code à barres à l’aide de l’API du service Web.](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décodez les données de formulaire à code-barres à l’aide de l’API Java {#decode-barcoded-form-data-using-the-java-api}

Décodez les données de formulaire à l’aide de l’API Barcoded Forms (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Création d’un objet API client de formulaires à code à barres

   Créez un objet `BarcodedFormsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Obtention d’un formulaire PDF contenant des données à code à barres

   * Créez un objet `java.io.FileInputStream` qui représente le formulaire PDF contenant des données à code à barres à l’aide de son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la méthode `decode` de l’objet `BarcodedFormsServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le formulaire PDF.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres PDF417.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres de la matrice de données.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres de code QR.
   * Objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres codabar.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres 128.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres 39.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres EAN-13.
   * Objet `java.lang.Boolean` qui spécifie s’il faut décoder un code à barres EAN-8.
   * Valeur d’énumération `com.adobe.livecycle.barcodedforms.CharSet` qui spécifie la valeur d’encodage du jeu de caractères utilisée dans le code à barres.

   La méthode `decode` renvoie un objet `org.w3c.dom.Document` contenant des données de formulaire décodées.

1. Convertir les données en source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la méthode `extractToXML` de l’objet `BarcodedFormsServiceClient` et en transmettant les valeurs suivantes :

   * Objet `org.w3c.dom.Document` contenant des données décodées (veillez à utiliser la valeur renvoyée par la méthode `decode`).
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.Delimiter` qui spécifie le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.Delimiter` qui spécifie le délimiteur de champ. Par exemple, spécifiez `Delimiter.Tab`.
   * Valeur d’énumération `com.adobe.livecycle.barcodedforms.XMLFormat` qui spécifie s’il faut convertir les données du code à barres en données XDP ou XFDF XML. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La méthode `extractToXML` renvoie un objet `java.util.List` où chaque élément est un objet `org.w3c.dom.Document`. Il existe un élément distinct pour chaque code à barres situé sur le formulaire. En d’autres termes, s’il existe quatre codes à barres sur le formulaire, il y a quatre éléments dans l’objet `java.util.List` renvoyé.

1. Traitement des données décodées

   * Parcourez l’objet `java.util.List` pour obtenir chaque objet `org.w3c.dom.Document` situé dans la liste.
   * Pour chaque élément de la liste, convertissez l’objet `org.w3c.dom.Document` en objet `com.adobe.idp.Document`. (La logique d’application qui convertit un objet `org.w3c.dom.Document` en objet `com.adobe.idp.Document` s’affiche dans les données de formulaire à code à barres de décodage à l’aide de l’exemple d’API Java).
   * Enregistrez les données XML sous forme de fichier XML en appelant la balise `copyToFile` de l’objet `com.adobe.idp.Document` et en transmettant un objet File représentant le fichier XML.

**Voir également**

[Démarrage rapide (mode SOAP) : Décodage des données de formulaire à code à barres à l’aide de l’API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décodez les données de formulaire à code-barres à l’aide de l’API de service Web {#decode-barcoded-form-data-using-the-web-service-api}

Décodez les données de formulaire à l’aide de l’API Barcoded Forms (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le WSDL du service Barcoded Forms. Pour plus d’informations, voir [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Référencez l’assemblage client Microsoft .NET. Pour plus d’informations, voir &quot;Référencer l’assemblage client .NET&quot; dans [Appel d’AEM Forms à l’aide de l’encodage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Création d’un objet API client de formulaires à code à barres

   À l’aide de l’assemblage client Microsoft .NET qui utilise le WSDL du service Barcoded Forms, créez un objet `BarcodedFormsServiceService` en appelant son constructeur par défaut.

1. Obtention d’un formulaire PDF contenant des données à code à barres

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF contenant un code à barres.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `binaryData` avec le contenu du tableau d’octets.

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la méthode `decode` de l’objet `BarcodedFormsServiceService` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le formulaire PDF.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres PDF417.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres de la matrice de données.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres de code QR.
   * Objet `Boolean` spécifiant s’il faut décoder un code à barres codabar.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres 128.
   * Objet `Bolean` qui spécifie s’il faut décoder un code à barres 39.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres EAN-13.
   * Objet `Boolean` qui spécifie s’il faut décoder un code à barres EAN-8.
   * Valeur d’énumération `CharSet` qui spécifie la valeur d’encodage du jeu de caractères utilisée dans le code à barres.

   La méthode `decode` renvoie une valeur string qui contient les données de formulaire décodées.

1. Convertir les données en source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la méthode `extractToXML` de l’objet `BarcodedFormsServiceService` et en transmettant les valeurs suivantes :

   * Une valeur string qui contient des données décodées (veillez à utiliser la valeur renvoyée par la méthode `decode`).
   * Une valeur d’énumération `Delimiter` qui spécifie le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Une valeur d’énumération `Delimiter` qui spécifie le délimiteur de champ. Par exemple, spécifiez `Delimiter.Tab`.
   * Valeur d’énumération `XMLFormat` qui spécifie s’il faut convertir les données du code à barres en données XDP ou XFDF XML. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La méthode `extractToXML` renvoie un tableau `Object` où chaque élément est une instance `BLOB`. Il existe un élément distinct pour chaque code à barres situé sur le formulaire. En d’autres termes, s’il existe quatre codes à barres sur le formulaire, il y a quatre éléments dans le tableau `Object` renvoyé.

1. Traitement des données décodées

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
