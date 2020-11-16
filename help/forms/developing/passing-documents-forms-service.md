---
title: Transmission de Documents à FormsService
seo-title: Transmission de Documents à FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 3%

---


# Transmission de Documents au service Forms {#passing-documents-to-the-formsservice}

Le service AEM Forms effectue le rendu de PDF forms interactifs sur les périphériques clients, généralement les navigateurs Web, afin de recueillir des informations auprès des utilisateurs. Un formulaire PDF interactif est basé sur une conception de formulaire généralement enregistrée sous la forme d’un fichier XDP et créée dans Designer. Depuis AEM Forms, vous pouvez transmettre un `com.adobe.idp.Document` objet contenant la conception de formulaire au service Forms. Le service Forms effectue ensuite le rendu de la conception de formulaire située dans l’ `com.adobe.idp.Document` objet.

L’avantage de transmettre un `com.adobe.idp.Document` objet au service Forms réside dans le fait que d’autres opérations de service renvoient une `com.adobe.idp.Document` instance. En d’autres termes, vous pouvez obtenir une `com.adobe.idp.Document` instance à partir d’une autre opération de service et la générer. Supposons, par exemple, qu’un fichier XDP soit stocké dans un noeud Content Services (obsolète) nommé `/Company Home/Form Designs`, comme illustré ci-dessous.

Vous pouvez récupérer par programmation le fichier Loan.xdp de Content Services (obsolète) (obsolète) et transmettre le fichier XDP au service Forms dans un `com.adobe.idp.Document` objet.

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour transmettre un document obtenu à partir de Content Services (obsolète) (obsolète) au service Forms, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un Forms et un objet API Client Document Management.
1. Récupérez la conception de formulaire auprès de Content Services (obsolète).
1. Générer le formulaire PDF interactif
1. Exécutez une action avec le flux de données du formulaire.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un Forms et d’un objet API Client Document Management**

Avant de pouvoir exécuter par programmation une opération d’API de service Forms, créez un objet API Client Forms. En outre, dans la mesure où ce processus récupère un fichier XDP de Content Services (obsolète), créez un objet API de gestion de Document.

**Récupération de la conception de formulaire à partir de Content Services (obsolète)**

Récupérez le fichier XDP à partir de Content Services (obsolète) à l’aide de l’API Java ou de service Web. Le fichier XDP est renvoyé au sein d’une `com.adobe.idp.Document` instance (ou d’une `BLOB` instance si vous utilisez des services Web). Vous pouvez ensuite transmettre l’ `com.adobe.idp.Document` instance au service Forms.

**Génération d’un formulaire PDF interactif**

Pour générer un formulaire interactif, transmettez l’ `com.adobe.idp.Document` instance qui a été renvoyée de Content Services (obsolète) au service Forms.

>[!NOTE]
>
>Vous pouvez transmettre au service Forms un formulaire `com.adobe.idp.Document` contenant la conception de formulaire. Deux nouvelles méthodes nomment `renderPDFForm2` et `renderHTMLForm2` acceptent un `com.adobe.idp.Document` objet contenant une conception de formulaire.

**Exécution d’une action avec le flux de données de formulaire**

Selon le type d’application cliente, vous pouvez écrire le formulaire dans un navigateur Web client ou l’enregistrer dans un fichier PDF. En règle générale, une application Web écrit le formulaire dans un navigateur Web. Cependant, une application de bureau enregistre généralement le formulaire au format PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Transmettre des documents au service Forms à l’aide de l’API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmettez un document obtenu à partir de Content Services (obsolète) à l’aide du service Forms et de l’API Content Services (obsolète) (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar et adobe-contentservices-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un Forms et d’un objet API Client Document Management

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération de la conception de formulaire à partir de Content Services (obsolète)

   Appelez la méthode `DocumentManagementServiceClientImpl` de l’ `retrieveContent` objet et transmettez les valeurs suivantes :

   * Valeur de chaîne qui spécifie la banque où le contenu est ajouté. The default store is `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le chemin d’accès complet au contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.

   La `retrieveContent` méthode renvoie un `CRCResult` objet contenant le fichier XDP. Obtenez une `com.adobe.idp.Document` instance en appelant la `CRCResult` méthode de l’ `getDocument` objet.

1. Génération d’un formulaire PDF interactif

   Appelez la méthode `FormsServiceClient` de l’ `renderPDFForm2` objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant la conception de formulaire récupérée auprès de Content Services (obsolète).
   * Objet `com.adobe.idp.Document` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un `com.adobe.idp.Document` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null`.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La `renderPDFForm` méthode renvoie un `FormsResult` objet qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Exécution d’une action avec le flux de données de formulaire

   * Créez un `com.adobe.idp.Document` objet en appelant la `FormsResult` méthode de l’ `getOutputContent` objet.
   * Obtenez le type de contenu de l’ `com.adobe.idp.Document` objet en appelant sa `getContentType` méthode.
   * Définissez le type de contenu de l’ `javax.servlet.http.HttpServletResponse` objet en appelant sa `setContentType` méthode et en transmettant le type de contenu de l’ `com.adobe.idp.Document` objet.
   * Créez un `javax.servlet.ServletOutputStream` objet utilisé pour écrire le flux de données du formulaire dans le navigateur Web client en appelant la `javax.servlet.http.HttpServletResponse` méthode de l’ `getOutputStream` objet.
   * Créez un `java.io.InputStream` objet en appelant la `com.adobe.idp.Document` méthode de l’ `getInputStream` objet.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la `InputStream` méthode de l’ `read` objet. Transmettez le tableau d’octets comme argument.
   * Appelez la méthode `javax.servlet.ServletOutputStream` de l’objet `write` pour envoyer le flux de données du formulaire au navigateur Web client. Transférez le tableau d’octets à la `write` méthode.

**Voir également**

[Début rapide (mode SOAP) : Transmission de documents au service Forms à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmettre des documents au service Forms à l’aide de l’API du service Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmettez un document obtenu à partir de Content Services (obsolète) à l’aide du service Forms et de l’API Content Services (obsolète) (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Dans la mesure où cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Forms : `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Document Management : `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Comme le type de `BLOB` données est commun aux deux références de service, qualifiez pleinement le type de `BLOB` données lors de son utilisation. Dans le début rapide du service Web correspondant, toutes les `BLOB` instances sont qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost`par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un Forms et d’un objet API Client Document Management

   * Create a `FormsServiceClient` object by using its default constructor.
   * Create a `FormsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/FormsService?WSDL`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `FormsServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour le client de `DocumentManagementServiceClient`service.

1. Récupération de la conception de formulaire à partir de Content Services (obsolète)

   Récupérez le contenu en appelant la `DocumentManagementServiceClient` `retrieveContent` méthode de l’objet et en transmettant les valeurs suivantes :

   * Valeur de chaîne qui spécifie la banque où le contenu est ajouté. The default store is `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie le chemin d’accès complet au contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur de chaîne qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   * Paramètre de sortie de chaîne qui stocke la valeur du lien de navigation.
   * Paramètre `BLOB` de sortie qui stocke le contenu. Vous pouvez utiliser ce paramètre de sortie pour récupérer le contenu.
   * Paramètre `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` de sortie qui stocke les attributs de contenu.
   * Paramètre `CRCResult` de sortie. Au lieu d’utiliser cet objet, vous pouvez utiliser le paramètre `BLOB` output pour obtenir le contenu.

1. Génération d’un formulaire PDF interactif

   Appelez la méthode `FormsServiceClient` de l’ `renderPDFForm2` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant la conception de formulaire récupérée auprès de Content Services (obsolète).
   * Objet `BLOB` contenant des données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un `BLOB` objet vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null`.
   * Objet `Map` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Paramètre de sortie long utilisé pour stocker le nombre de pages.
   * Paramètre de sortie de chaîne utilisé pour stocker la valeur du paramètre régional.
   * Paramètre `FormsResult` de sortie utilisé pour stocker le formulaire PDF interactif `.`

   La `renderPDFForm2` méthode renvoie un `FormsResult` objet contenant le formulaire PDF interactif.

1. Exécution d’une action avec le flux de données de formulaire

   * Créez un `BLOB` objet contenant des données de formulaire en obtenant la valeur du `FormsResult` champ de l’ `outputContent` objet.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet récupéré de l’ `FormsResult` objet. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` de données de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
