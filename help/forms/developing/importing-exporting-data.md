---
title: Importer et exporter des données
seo-title: Importing and Exporting Data
description: Utilisez le service d’intégration des données de formulaire pour importer des données dans un formulaire PDF et exporter des données d’un formulaire PDF à l’aide de l’API Java et de l’API Web Service.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2771'
ht-degree: 95%

---

# Importer et exporter des données {#importing-and-exporting-data}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## À propos du service d’intégration des données de formulaire {#about-the-form-data-integration-service}

Le service d’intégration des données de formulaire peut importer des données dans un formulaire PDF et exporter des données d’un formulaire PDF. Les opérations d’import et d’export prennent en charge deux types de formulaires PDF :

* Un formulaire PDF (créé dans Acrobat) est un document PDF qui contient des champs de formulaire.
* Un formulaire XML d’Adobe (créé dans Designer) est un document PDF conforme à l’Adobe XML Forms Architecture (XFA).

Les données de formulaire peuvent exister dans l’un des formats suivants en fonction du type de formulaire de PDF :

* Un fichier XFDF, qui est une version XML du format de données de formulaire Acrobat.
* Un fichier XDP, qui correspond à un fichier XML contenant des définitions de champ de formulaire. Il peut également contenir des données de champ de formulaire et un fichier de PDF incorporé. Un fichier XDP généré par Designer n’est utilisable que s’il incorpore un document PDF codé en base 64.

Vous pouvez accomplir ces tâches à l’aide du service d’intégration des données de formulaire :

* Importez des données dans les formulaires PDF. Pour plus d’informations, voir [Importer des données de formulaire](importing-exporting-data.md#importing-form-data).
* Exporter des données des formulaires PDF Pour plus d’informations, voir [Exporter des données de formulaire](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Pour plus d’informations sur le service d’intégration des données de formulaire, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Importer des données de formulaire {#importing-form-data}

Vous pouvez importer des données de formulaire dans des formulaires PDF interactifs à l’aide du service d’intégration des données de formulaire. Un formulaire PDF interactif est un document PDF contenant un ou plusieurs champs pour la collecte d’informations auprès d’un utilisateur ou l’affichage d’informations personnalisées. Le service d’intégration des données de formulaire ne prend pas en charge les calculs de formulaire, la validation ou les scripts.

Pour importer des données dans un formulaire créé dans Designer, vous devez référencer une source de données XML XDP valide. Examinez l’exemple de formulaire de demande de prêt suivant :

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Pour importer des valeurs de données dans ce formulaire, vous devez disposer d’une source de données XDP XML valide correspondant au formulaire. Vous ne pouvez pas utiliser une source de données XML arbitraire pour importer des données dans un formulaire à l’aide du service d’intégration des données de formulaire. La différence entre une source de données XML arbitraire et une source de données XML XDP est qu’une source de données XDP est conforme à l’architecture Forms XML (XFA). Le code XML suivant représente une source de données XML XDP correspondant à l’exemple de formulaire de demande de prêt immobilier.

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
>Pour plus d’informations sur le service d’intégration des données de formulaire, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour importer des données de formulaire dans un formulaire PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service d’intégration des données de formulaire.
1. Référencez un formulaire PDF.
1. Référencez une source de données XML.
1. Importez des données dans un formulaire PDF.
1. Enregistrez le formulaire au format PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client de service d’intégration des données de formulaire**

Avant de pouvoir importer des données par programmation dans une API client de formulaire PDF, vous devez créer un client de service Data Integration (Intégration de données). Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, voir [Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Référencer un formulaire PDF**

Pour importer des données dans un formulaire PDF, vous devez référencer un formulaire XML créé dans Designer ou un formulaire Acrobat créé dans Acrobat.

**Référencer une source de données XML**

Pour importer des données de formulaire, vous devez référencer une source de données valide. Pour importer des données dans un formulaire XML XFA créé dans Designer, vous devez utiliser une source de données XML XDP. Si vous référencez un formulaire Acrobat, vous devez utiliser une source de données XFDF. Pour chaque champ dans lequel vous souhaitez importer des données, une valeur doit être spécifiée. Si un élément de la source de données XML ne correspond pas à un champ du formulaire, l’élément est ignoré.

**Importer les données dans un formulaire PDF**

Après avoir référencé un formulaire PDF et une source de données XML valide, vous pouvez importer les données dans le formulaire PDF.

**Enregistrer le formulaire au format PDF**

Après avoir importé des données dans un formulaire, vous pouvez enregistrer le formulaire en tant que fichier PDF. Une fois enregistré en tant que fichier PDF, l’utilisateur peut ouvrir le formulaire dans Adobe Reader ou Acrobat et l’afficher avec les données importées.

**Voir également**

[Importer des données de formulaire à l’aide de l’API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importer des données de formulaire à l’aide de l’API Web Service](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Form Data du service d’intégration](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exporter des données de formulaire](importing-exporting-data.md#exporting-form-data)

### Importer des données de formulaire à l’aide de l’API Java {#import-form-data-using-the-java-api}

Pour importer des données de formulaire à l’aide de l’API Form Data Integration (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-formdataintegration-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service d’intégration des données de formulaire.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencez un formulaire PDF.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur. Transmettez une valeur de chaîne spécifiant l’emplacement du formulaire PDF.
   * Créez un objet `com.adobe.idp.Document` qui stocke le formulaire PDF à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` qui contient le formulaire PDF au constructeur.

1. Référencez une source de données XML.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier XML contenant les données à importer dans le formulaire.
   * Créez un objet `com.adobe.idp.Document` qui stocke les données de formulaire à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` contenant des données de formulaire au constructeur.

1. Importez des données dans un formulaire PDF.

   Importez des données dans un formulaire PDF en appelant la méthode `importData` de l’objet `FormDataIntegrationClient` et en transmettant les valeurs suivantes :

   * L’objet `com.adobe.idp.Document` qui stocke le formulaire PDF.
   * L’objet `com.adobe.idp.Document` qui stocke les données de formulaire.

   La variable `importData` renvoie une `com.adobe.idp.Document` qui stocke un formulaire de PDF contenant les données de la source de données XML.

1. Enregistrez le formulaire au format PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est « .PDF ».
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier (assurez-vous d’utiliser l’objet `Document` qui a été renvoyé par la méthode `importData`).

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Didacticiel de mise en route (mode SOAP) : importer des données de formulaire à l’aide de l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importer des données de formulaire à l’aide de l’API Web Service {#import-form-data-using-the-web-service-api}

Pour importer des données de formulaire à l’aide de l’API Form Data Integration (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service d’intégration des données de formulaire.

   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur par défaut.
   * Créez un objet `FormDataIntegrationClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `FormDataIntegrationClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un formulaire PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` sert à stocker le formulaire PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Référencez une source de données XML.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` sert à stocker les données importées dans le formulaire.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne indiquant l’emplacement du fichier XML qui contient les données à importer et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Importez des données dans un formulaire PDF.

   Importez des données dans le formulaire PDF en appelant la méthode `importData` de l’objet `FormDataIntegrationClient` et en transmettant les valeurs suivantes :

   * L’objet `BLOB` qui stocke le formulaire PDF.
   * L’objet `BLOB` qui stocke les données de formulaire.

   La variable `importData` renvoie une `BLOB` qui stocke un formulaire de PDF contenant les données de la source de données XML.

1. Enregistrez le formulaire au format PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `importData`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exporter des données de formulaire {#exporting-form-data}

Vous pouvez exporter des données de formulaire à partir d’un formulaire PDF interactif à l’aide du service d’intégration de données de formulaire. Le format des données exportées dépend du type de formulaire. Si le type de formulaire est un formulaire Acrobat créé dans Acrobat, alors les données exportées sont au format XFDF. Si le type de formulaire est un formulaire XML qui a été créé dans Designer, alors les données exportées sont au format XDP.

>[!NOTE]
>
>Pour plus d’informations sur le service d’intégration des données de formulaire, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour exporter les données d’un formulaire PDF, procédez comme suit :

1. Inclure les fichiers du projet
1. Créez un client de service d’intégration des données de formulaire.
1. Référencez un formulaire PDF.
1. Exportez les données du formulaire PDF.
1. Enregistrez les données exportées sous forme de fichier XML.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)

**Créer un client de service d’intégration de données de formulaire**

Avant de pouvoir importer des données par programmation dans une API formClient PDF, vous devez créer un client de service d’intégration de données. Lors de la création d’un client de service, vous définissez les paramètres de connexion requis pour appeler un service. Pour plus d’informations, consultez la section [Définir les propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Référencer un formulaire PDF**

Pour exporter les données d’un formulaire PDF, vous devez référencer le formulaire PDF créé dans Designer ou Acrobat et contenant des données de formulaire. Si vous tentez d’exporter des données à partir d’un formulaire PDF vide, vous obtiendrez un schéma XML vide.

**Exporter les données du formulaire PDF**

Une fois que vous avez référencé un formulaire PDF contenant des données de formulaire, vous pouvez exporter les données du formulaire. Les données sont exportées dans un schéma XML basé sur le formulaire.

**Enregistrer les données du formulaire sous forme de fichier XML**

Une fois les données de formulaire exportées, vous pouvez les enregistrer au format XML. Une fois enregistré en tant que fichier XML, vous pouvez lʼouvrir dans une visionneuse XML pour afficher les données de formulaire.

**Voir également**

[Exporter des données de formulaire à l’aide de l’API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exporter des données de formulaire à l’aide de l’API de service web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Form Data du service d’intégration](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importer des données de formulaire](importing-exporting-data.md#importing-form-data)

### Exporter des données de formulaire à l’aide de l’API Java {#export-form-data-using-the-java-api}

Pour exporter les données de formulaire à l’aide de l’API Form Data Integration (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-formdataintegration-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service d’intégration des données de formulaire.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencez un formulaire PDF.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du formulaire PDF contenant les données à exporter.
   * Créez un objet `com.adobe.idp.Document` qui stocke le formulaire PDF à l’aide du constructeur `com.adobe.idp.Document`. Transmettez au constructeur l’objet `java.io.FileInputStream` qui contient le formulaire PDF.

1. Exportez les données du formulaire PDF.

   Exportez les données du formulaire en appelant la méthode `exportData` de l’objet `FormDataIntegrationClient` et en transmettant l’objet `com.adobe.idp.Document` qui stocke le formulaire PDF. Cette méthode renvoie un objet `com.adobe.idp.Document` qui stocke les données du formulaire sous forme de schéma XML.

1. Enregistrez le formulaire au format PDF.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est XML.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier (veillez à utiliser l’objet `Document` renvoyé par la méthode `exportData`).

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Didacticiel de mise en route (mode SOAP) : exporter des données de formulaire à l’aide de l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exporter des données de formulaire à l’aide de l’API de service web {#export-form-data-using-the-web-service-api}

Pour exporter les données de formulaire à l’aide de l’API Form Data Integration (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service d’intégration des données de formulaire.

   * Créez un objet `FormDataIntegrationClient` en utilisant son constructeur par défaut.
   * Créez un objet `FormDataIntegrationClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `FormDataIntegrationClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un formulaire PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` est utilisé pour stocker le formulaire PDF à partir duquel les données sont exportées.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à son champ `MTOM`.

1. Exportez les données du formulaire PDF.

   Importez les données dans un formulaire PDF en appelant la méthode `exportData` de l’objet `FormDataIntegrationClient` et en transmettant l’objet `BLOB` qui stocke le formulaire PDF. Cette méthode renvoie un objet `BLOB` qui stocke les données du formulaire sous forme de schéma XML.

1. Enregistrez le formulaire au format PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier XML.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `exportData`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier XML en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](importing-exporting-data.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
