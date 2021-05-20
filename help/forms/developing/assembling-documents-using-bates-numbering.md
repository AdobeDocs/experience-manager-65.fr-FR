---
title: Assemblage de documents à l’aide de la numérotation Bates
seo-title: Assemblage de documents à l’aide de la numérotation Bates
description: 'Utilisez la numérotation Bates pour assembler des documents PDF à l’aide de l’API Java et Web Service. '
seo-description: 'Utilisez la numérotation Bates pour assembler des documents PDF à l’aide de l’API Java et Web Service. '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 5%

---

# Assemblage de documents à l’aide de la numérotation Bates {#assembling-documents-using-bates-numbering}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Vous pouvez assembler des documents PDF contenant des identifiants de page uniques à l’aide de la numérotation Bates. *La* numérotation Bates est une méthode d’application d’identifiants uniques à un lot de documents associés. Chaque page du document (ou ensemble de documents) se voit attribuer un numéro Bates qui identifie la page de manière unique. Par exemple, des documents d’entreprise contenant une nomenclature et liés à la production d’un assemblage peuvent contenir un identifiant. Un numéro Bates contient une valeur numérique incrémentée séquentiellement et optionnellement un préfixe et un suffixe. Le préfixe + suffixe numérique + est appelé modèle *bates*.

L’illustration suivante présente un document PDF contenant un identifiant unique, situé dans l’en-tête du document.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Dans le cadre de cette discussion, l’identifiant de page unique est placé dans l’en-tête d’un document. Supposons que le document DX suivant soit utilisé.

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

Ce document DDX fusionne deux documents PDF nommés *map.pdf* et *directions.pdf* en un seul document PDF. Le document PDF généré contient un en-tête constitué d’un identifiant de page unique. Par exemple, le document de l’illustration ci-dessus affiche 000016.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de vous familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts tels que la création d’un objet de collection contenant des documents d’entrée ou l’extraction des résultats de l’objet de collection renvoyé. (Voir [Assemblage par programmation de documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF contenant un identifiant de page unique (numérotation Bates), effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DX existant.
1. Documents PDF d’entrée de référence.
1. Définissez la valeur initiale du nombre Bates.
1. Assemblez les documents PDF d’entrée.
1. Extrayez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant d’effectuer une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX introduit dans cette section. Pour assembler un document PDF contenant des identifiants de page uniques, le document DDX doit contenir l’élément `BatesNumber` .

**Documents PDF d’entrée de référence**

Les documents PDF d’entrée doivent être référencés pour assembler un document PDF. Par exemple, les documents map.pdf et directions.pdf doivent être référencés pour assembler ces documents PDF en un seul document PDF.

**Définition de la valeur initiale du nombre Bates**

Vous pouvez définir la valeur de numéro Bates initiale pour répondre aux besoins de votre entreprise. Supposons, par exemple, qu’il soit nécessaire de définir la valeur initiale sur 000100. Si vous ne définissez pas la valeur initiale, la valeur de la première page est 000000.

**Assemblage des documents PDF d’entrée**

Après avoir créé le client de service Assembler, référencez le document DDX contenant les informations sur les éléments `BatesNumber`, référencez un document PDF d’entrée et définissez les options d’exécution. Vous pouvez appeler l’opération `invokeDDX` qui entraîne l’assemblage d’un document PDF contenant des identifiants de page uniques par le service Assembler.

**Extraire les résultats**

Le service Assembler renvoie un objet de collection contenant les résultats de la tâche. Vous pouvez extraire le document PDF généré et les exceptions qui sont générées. Dans ce cas, un document PDF chiffré se trouve dans l’objet de collection.

>[!NOTE]
>
>Un objet de collection est renvoyé si vous appelez l’opération `invokeDDX`. Cette opération est utilisée lors de la transmission de plusieurs documents PDF d’entrée au service Assembler. Cependant, si vous ne transmettez qu’un seul document PDF d’entrée au service Assembler, vous devez appeler l’opération `invokeOneDocument`. Pour plus d’informations sur l’utilisation de cette opération, voir [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage de documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblez des documents avec numérotation Bates à l’aide de l’API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblez un document PDF qui utilise des identifiants de page uniques (numérotation Bates) à l’aide de l’API Assembler Service (Java) :

1. Inclure les fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Documents PDF d’entrée de référence.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Pour chaque document PDF d’entrée, créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée. Dans ce cas, transmettez l’emplacement d’un document PDF non sécurisé.
   * Pour chaque document PDF d’entrée, créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur string qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément de source PDF spécifié dans le document DDX. Par exemple, le nom du fichier source PDF spécifié dans le document DDX introduit dans cette section est Loan.pdf.
      * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.

1. Définissez la valeur initiale du nombre Bates.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez le numéro Bates initial en appelant la `setFirstBatesNumber` de l’objet `AssemblerOptionSpec` et en transmettant une valeur numérique qui spécifie la valeur initiale.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX.
   * Objet `java.util.Map` contenant le fichier PDF non sécurisé d’entrée.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant un document PDF chiffré par mot de passe.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les actions suivantes :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette action renvoie un objet `java.util.Map` .
   * Effectuez une itération sur l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` .
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage d’un document PDF avec numérotation bates à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblez des documents avec numérotation Bates à l’aide de l’API de service Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblez un document PDF qui utilise des identifiants de page uniques (numérotation Bates) à l’aide de l’API Assembler Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.

1. Documents PDF d’entrée de référence.

   * Pour chaque document PDF d’entrée, créez un objet `BLOB` à l’aide de son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType` . Cet objet de collection est utilisé pour stocker les documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux objets `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur string qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément de source PDF spécifié dans le document DDX. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Affectez l’objet `BLOB` qui stocke le document PDF dans le champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType` . (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez la valeur initiale du nombre Bates.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez le nombre Bates initial en attribuant une valeur numérique au membre de données `firstBatesNumber` qui appartient à l’objet `AssemblerOptionSpec`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invoke` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être les objets `BLOB` correspondant à ces fichiers.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invoke` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui se sont produites.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `Map`, qui est un objet `AssemblerResult` contenant les documents PDF obtenus.
   * Effectuez une itération sur l’objet `Map` jusqu’à ce que vous trouviez la clé correspondant au nom du document généré. Convertissez ensuite la balise `value` de ce membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
