---
title: Importation et exportation de données
seo-title: Importation et exportation de données
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 6%

---


# Importation et exportation de données {#importing-and-exporting-data}

## À propos du service d’intégration des données de formulaire {#about-the-form-data-integration-service}

Le service d’intégration des données de formulaire peut importer des données dans un formulaire PDF et exporter des données d’un formulaire PDF. Les opérations d’importation et d’exportation prennent en charge deux types de PDF forms :

* Un formulaire Acrobat (créé dans Acrobat) est un document PDF qui contient des champs de formulaire.
* Un formulaire XML Adobe (créé dans Designer) est un document PDF conforme à l’architecture de formulaires XML Adobe (XFA).

Les données de formulaire peuvent exister dans l’un des formats suivants, selon le type de formulaire PDF :

* Un fichier XFDF, qui constitue une version XML du format de données de formulaire Acrobat.
* Un fichier XDP, qui correspond à un fichier XML contenant des définitions de champ de formulaire. Ce fichier peut également inclure des données de champ de formulaire, ainsi qu’un fichier PDF incorporé. Un fichier XDP généré par Designer ne peut être utilisé que s’il contient un document PDF codé en base 64 incorporé.

Vous pouvez accomplir ces tâches à l’aide du service d’intégration des données de formulaire :

* Importez des données en PDF forms. Pour plus d’informations, voir [Importation de données](importing-exporting-data.md#importing-form-data)de formulaire.
* Exportez des données à partir de PDF forms. Pour plus d’informations, voir [Exportation de données](importing-exporting-data.md#exporting-form-data)de formulaire.

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importation de données de formulaire {#importing-form-data}

Vous pouvez importer des données de formulaire dans des PDF forms interactifs à l’aide du service d’intégration des données de formulaire. Un formulaire PDF interactif est un document PDF qui contient un ou plusieurs champs permettant de collecter des informations auprès d’un utilisateur ou d’afficher des informations personnalisées. Le service d’intégration des données de formulaire ne prend pas en charge les calculs de formulaire, la validation ou les scripts.

Pour importer des données dans un formulaire créé dans Designer, vous devez référencer une source de données XML XDP valide. Examinez l&#39;exemple de formulaire de demande de prêt immobilier suivant.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Pour importer des valeurs de données dans ce formulaire, vous devez disposer d’une source de données XML XDP valide qui correspond au formulaire. Vous ne pouvez pas utiliser une source de données XML arbitraire pour importer des données dans un formulaire à l’aide du service d’intégration des données de formulaire. La différence entre une source de données XML arbitraire et une source de données XML XDP est qu’une source de données XDP est conforme à l’architecture de formulaires XML (XFA). Le code XML suivant représente une source de données XML XDP qui correspond à l’exemple de formulaire de demande de prêt immobilier.

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

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour importer des données de formulaire dans un formulaire PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client du service d’intégration des données de formulaire.
1. Référence à un formulaire PDF.
1. Référence à une source de données XML.
1. Importez des données dans le formulaire PDF.
1. Enregistrez le formulaire PDF au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client de service d’intégration de données de formulaire**

Avant de pouvoir importer des données par programmation dans une API Client de formulaire PDF, vous devez créer un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, voir [Définition des propriétés](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de connexion.

**Référence à un formulaire PDF**

Pour importer des données dans un formulaire PDF, vous devez référencer un formulaire XML créé dans Designer ou un formulaire Acrobat créé dans Acrobat.

**Référence à une source de données XML**

Pour importer des données de formulaire, vous devez référencer une source de données valide. Pour importer des données dans un formulaire XML XFA créé dans Designer, vous devez utiliser une source de données XML XDP. Si vous référencez un formulaire Acrobat, vous devez alors utiliser une source de données XFDF. Pour chaque champ dans lequel vous souhaitez importer des données, une valeur doit être spécifiée. Si un élément situé dans la source de données XML ne correspond pas à un champ du formulaire, l’élément est ignoré.

**Importer des données dans le formulaire PDF**

Après avoir référencé un formulaire PDF et une source de données XML valide, vous pouvez importer les données dans le formulaire PDF.

**Enregistrer le formulaire PDF en tant que fichier PDF**

Après avoir importé des données dans un formulaire, vous pouvez enregistrer le formulaire au format PDF. Une fois enregistré en tant que fichier PDF, un utilisateur peut ouvrir le formulaire dans Adobe Reader ou Acrobat et afficher le formulaire contenant les données importées.

**Voir également**

[Importation des données de formulaire à l’aide de l’API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importation de données de formulaire à l’aide de l’API de service Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service d’intégration des données de formulaire](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportation des données de formulaire](importing-exporting-data.md#exporting-form-data)

### Importation des données de formulaire à l’aide de l’API Java {#import-form-data-using-the-java-api}

Importez des données de formulaire à l’aide de l’API d’intégration des données de formulaire (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-formdataintegration-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client du service d’intégration des données de formulaire.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un formulaire PDF.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF.
   * Créez un `com.adobe.idp.Document` objet qui stocke le formulaire PDF à l’aide du `com.adobe.idp.Document` constructeur. Transférez l’objet `java.io.FileInputStream` contenant le formulaire PDF au constructeur.

1. Référence à une source de données XML.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML qui contient les données à importer dans le formulaire.
   * Créez un `com.adobe.idp.Document` objet qui stocke les données de formulaire à l’aide du `com.adobe.idp.Document` constructeur. Transmettez l’objet `java.io.FileInputStream` contenant des données de formulaire au constructeur.

1. Importez des données dans le formulaire PDF.

   Importez des données dans un formulaire PDF en appelant la `FormDataIntegrationClient` `importData` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` qui stocke le formulaire PDF.
   * Objet `com.adobe.idp.Document` qui stocke les données de formulaire.

   La `importData` méthode renvoie un `com.adobe.idp.Document` objet qui stocke un formulaire PDF contenant les données se trouvant dans la source de données XML.

1. Enregistrez le formulaire PDF au format PDF.

   * Create a `java.io.File` object and ensure that the file extension is “.PDF”.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `importData` méthode).

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Début rapide (mode SOAP) : Importation de données de formulaire à l’aide de l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importation de données de formulaire à l’aide de l’API de service Web {#import-form-data-using-the-web-service-api}

Importez des données de formulaire à l’aide de l’API d’intégration des données de formulaire (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client du service d’intégration des données de formulaire.

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `FormDataIntegrationClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référence à un formulaire PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet est utilisé pour stocker le formulaire PDF.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référence à une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet est utilisé pour stocker les données importées dans le formulaire.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier XML qui contient les données à importer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Importez des données dans le formulaire PDF.

   Importez des données dans le formulaire PDF en appelant la `FormDataIntegrationClient` `importData` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` qui stocke le formulaire PDF.
   * Objet `BLOB` qui stocke les données de formulaire.

   La `importData` méthode renvoie un `BLOB` objet qui stocke un formulaire PDF contenant les données se trouvant dans la source de données XML.

1. Enregistrez le formulaire PDF au format PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `importData` méthode. Renseignez le tableau d’octets en obtenant la valeur du `BLOB` champ de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportation des données de formulaire {#exporting-form-data}

Vous pouvez exporter des données de formulaire à partir d’un formulaire PDF interactif à l’aide du service d’intégration des données de formulaire. Le format des données exportées dépend du type de formulaire. Si le type de formulaire est un formulaire Acrobat créé dans Acrobat, les données exportées sont alors au format XFDF. Si le type de formulaire est un formulaire XML créé dans Designer, les données exportées sont au format XDP.

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour exporter les données d’un formulaire PDF, procédez comme suit :

1. Inclure les fichiers de projet
1. Créez un client du service d’intégration des données de formulaire.
1. Référence à un formulaire PDF.
1. Exportez les données du formulaire PDF.
1. Enregistrez les données exportées dans un fichier XML.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

**Création d’un client de service d’intégration de données de formulaire**

Avant de pouvoir importer des données par programmation dans une API FormsClient PDF, vous devez créer un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, [Définition des propriétés](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de connexion.

**Référence à un formulaire PDF**

Pour exporter des données d’un formulaire PDF, vous devez référencer un formulaire PDF créé dans Designer ou Acrobat et contenant des données de formulaire. Si vous tentez d’exporter des données à partir d’un formulaire PDF vide, vous obtiendrez un schéma XML vide.

**Exportation de données à partir du formulaire PDF**

Après avoir référencé un formulaire PDF contenant des données de formulaire, vous pouvez exporter les données du formulaire. Les données sont exportées dans un schéma XML basé sur le formulaire.

**Enregistrer les données du formulaire dans un fichier XML**

Après avoir exporté des données de formulaire, vous pouvez enregistrer les données dans un fichier XML. Une fois enregistré en tant que fichier XML, vous pouvez ouvrir le fichier XML dans un lecteur XML pour vue des données du formulaire.

**Voir également**

[Exportation des données de formulaire à l’aide de l’API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportation des données de formulaire à l’aide de l’API de service Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API du service d’intégration des données de formulaire](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importation de données de formulaire](importing-exporting-data.md#importing-form-data)

### Exportation des données de formulaire à l’aide de l’API Java {#export-form-data-using-the-java-api}

Exportez les données de formulaire à l’aide de l’API d’intégration des données de formulaire (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-formdataintegration-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client du service d’intégration des données de formulaire.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un formulaire PDF.

   * Créez un `java.io.FileInputStream` objet à l’aide de son constructeur et transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF contenant les données à exporter.
   * Créez un `com.adobe.idp.Document` objet qui stocke le formulaire PDF à l’aide du `com.adobe.idp.Document` constructeur. Transférez l’objet `java.io.FileInputStream` contenant le formulaire PDF au constructeur.

1. Exportez les données du formulaire PDF.

   Exportez les données de formulaire en appelant la `FormDataIntegrationClient` méthode de l’ `exportData` objet et en transmettant l’ `com.adobe.idp.Document` objet qui stocke le formulaire PDF. Cette méthode renvoie un `com.adobe.idp.Document` objet qui stocke les données de formulaire sous la forme d’un schéma XML.

1. Enregistrez le formulaire PDF au format PDF.

   * Create a `java.io.File` object and ensure that the file extension is XML.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `exportData` méthode).

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Début rapide (mode SOAP) : Exportation des données de formulaire à l’aide de l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportation des données de formulaire à l’aide de l’API de service Web {#export-form-data-using-the-web-service-api}

Exportez les données de formulaire à l’aide de l’API d’intégration des données de formulaire (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client du service d’intégration des données de formulaire.

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `FormDataIntegrationClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référence à un formulaire PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet est utilisé pour stocker le formulaire PDF à partir duquel les données sont exportées.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Exportez les données du formulaire PDF.

   Importez des données dans un formulaire PDF en appelant la `FormDataIntegrationClient` méthode de l’ `exportData` objet et en transmettant l’ `BLOB` objet qui stocke le formulaire PDF. Cette méthode renvoie un `BLOB` objet qui stocke les données de formulaire sous la forme d’un schéma XML.

1. Enregistrez le formulaire PDF au format PDF.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier XML.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `exportData` méthode. Renseignez le tableau d’octets en obtenant la valeur du `BLOB` champ de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier XML en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
