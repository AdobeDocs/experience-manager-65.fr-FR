---
title: Assembler des documents à l’aide de la numérotation Bates
seo-title: Assembling Documents Using Bates Numbering
description: Utilisez la numérotation Bates pour assembler des documents PDF à l’aide de l’API Java et Web Service.
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 88%

---

# Assembler des documents à l’aide de la numérotation Bates {#assembling-documents-using-bates-numbering}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez assembler des documents PDF qui contiennent des identifiants de page uniques à l’aide de la numérotation Bates. La *numérotation Bates* est une méthode d’application d’identifiants uniques à un lot de documents associés. Chaque page du document (ou ensemble de documents) se voit attribuer un numéro Bates qui identifie la page de manière unique. Par exemple, des documents d’entreprise contenant une nomenclature et liés à la production d’un assemblage peuvent contenir un identifiant. Un numéro Bates contient une valeur numérique incrémentée séquentiellement et optionnellement un préfixe et un suffixe. La chaîne préfixe+numérique+suffixe est appelée *modèle bates*.

L’illustration suivante présente un document de PDF qui contient un identifiant unique dans l’en-tête du document.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Dans le cadre de cette discussion, l’identifiant de page unique est placé dans l’en-tête d’un document. Supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Ce document DDX fusionne deux documents PDF nommés *map.pdf* et *directions.pdf* en un document PDF unique. Le document PDF généré contient un en-tête constitué d’un identifiant de page unique. Par exemple, le document de l’illustration ci-dessus affiche 000016.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de vous familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts tels que la création d’un objet de collection contenant des documents d’entrée ou l’extraction des résultats de l’objet de collection renvoyé. (Voir [Assembler par programmation des documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF contenant un identifiant de page unique (numérotation Bates), effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez les documents PDF d’entrée.
1. Définissez la valeur initiale du nombre Bates.
1. Assemblez les documents PDF d’entrée.
1. Extrayez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations à propos de l’emplacement de ces fichiers, voir [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Assembler PDF**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons par exemple le document DDX qui a été présenté dans cette section. Pour assembler un document PDF contenant des identifiants de page uniques, le document DDX doit contenir l’élément `BatesNumber`.

**Référencer des documents PDF d’entrée**

Les documents PDF d’entrée doivent être référencés pour assembler un document PDF. Par exemple, les documents map.pdf et directions.pdf doivent être référencés pour assembler ces documents PDF en un seul document PDF.

**Définir la valeur initiale du numéro Bates**

Vous pouvez définir la valeur de numéro Bates initiale pour répondre aux besoins de votre entreprise. Supposons, par exemple, qu’il soit nécessaire de définir la valeur initiale sur 000100. Si vous ne définissez pas la valeur initiale, la valeur de la première page est 000000.

**Assembler des documents PDF d’entrée**

Après avoir créé le client de service Assembler, référencé le document DDX qui contient des informations sur l’élément `BatesNumber`, référencé un document PDF d’entrée et défini les options d’exécution, vous pouvez appeler la fonction `invokeDDX` qui entraîne l’assemblage par le service Assembler d’un document PDF contenant des identifiants de page uniques.

**Extraire les résultats**

Le service Assembler renvoie un objet de collection contenant les résultats de la tâche. Vous pouvez extraire le document PDF généré et les exceptions qui sont générées. Dans ce cas, un document de PDF chiffré se trouve dans l’objet de collection.

>[!NOTE]
>
>Un objet de collection est renvoyé si vous appelez l’opération `invokeDDX`. Cette opération est utilisée lors de la transmission de plusieurs documents PDF d’entrée au service Assembler. Cependant, si vous ne transmettez qu’un seul document PDF d’entrée au service Assembler, vous devez appeler l’opération `invokeOneDocument`. Pour plus d’informations sur l’utilisation de cette opération, voir [Assembler des documents PDF chiffrés](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assembler des documents avec numérotation Bates à l’aide de l’API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblez un document PDF qui utilise des identifiants de page uniques (numérotation Bates) à l’aide de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez des documents PDF d’entrée.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Pour chaque document PDF d’entrée, créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée. Dans ce cas, transmettez l’emplacement d’un document PDF non sécurisé.
   * Pour chaque document PDF d’entrée, créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant la méthode `put` correspondante et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX. Par exemple, le nom du fichier source du PDF spécifié dans le document DDX présenté dans cette section est Loan.pdf.
      * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.

1. Définissez la valeur initiale du nombre Bates.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez le numéro Bates initial en appelant la variable `AssemblerOptionSpec` de `setFirstBatesNumber` et transmission d’une valeur numérique qui spécifie la valeur initiale.

1. Assemblez les documents PDF d’entrée.

   Appeler la variable `AssemblerServiceClient` de `invokeDDX` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX.
   * Objet `java.util.Map` contenant le fichier PDF non sécurisé entré.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau de journalisation des tâches.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant un document PDF chiffré par mot de passe.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appeler la variable `AssemblerResult` de `getDocuments` . Cette action renvoie un objet `java.util.Map`.
   * Effectuez une itération à l’aide de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document`.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour extraire le document du PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : assembler un document PDF avec numérotation Bates à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assembler des documents avec numérotation Bates à l’aide de l’API Web Service {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblez un document PDF qui utilise des identifiants de page uniques (numérotation Bates) à l’aide de l’API Assembler Service (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à son champ `MTOM` le contenu du tableau d’octets.

1. Référencez les documents PDF d’entrée.

   * Pour chaque document PDF d’entrée, créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker les documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux objets `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX. (Répétez cette tâche pour chaque document PDF d’entrée).
   * Attribuez lʼobjet `BLOB` qui stocke le document PDF au champ `value` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Répétez cette tâche pour chaque document PDF d’entrée).
   * Ajoutez lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item` à lʼobjet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`. (Répétez cette tâche pour chaque document PDF d’entrée).

1. Définissez la valeur initiale du nombre Bates.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez le nombre Bates initial en attribuant une valeur numérique au membre de données `firstBatesNumber` appartenant à l’objet `AssemblerOptionSpec`.

1. Assemblez les documents PDF d’entrée.

   Appeler la variable `AssemblerServiceClient` de `invoke` et transmettez les valeurs suivantes :

   * Un objet `BLOB` représentant le document DDX.
   * L’objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être les objets `BLOB` correspondant à ces fichiers.
   * Un objet `AssemblerOptionSpec` indiquant les options d’exécution.

   La méthode `invoke` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions survenues.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Accédez au `AssemblerResult` de `documents` , qui est un `Map` contenant les documents du PDF de résultats.
   * Effectuez une itération au sein de l’objet `Map` jusqu’à ce que vous trouviez la clé correspondant au nom du document généré. Collez ensuite le de ce membre du tableau `value` à `BLOB`.
   * Extrayez les données binaires qui représentent le document du PDF en accédant à ses `BLOB` de `MTOM` . Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
