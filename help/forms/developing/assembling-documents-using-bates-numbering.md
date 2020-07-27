---
title: Assemblage de Documents à l’aide de la numérotation Bates
seo-title: Assemblage de Documents à l’aide de la numérotation Bates
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 5%

---


# Assembling Documents Using Bates Numbering {#assembling-documents-using-bates-numbering}

Vous pouvez assembler des documents PDF contenant des identifiants de page uniques à l’aide de la numérotation Bates. *La numérotation* Bates est une méthode permettant d&#39;appliquer des identifiants uniques à un lot de documents associés. Chaque page du document (ou jeu de documents) se voit attribuer un numéro Bates qui identifie de manière unique la page. Par exemple, des documents d’entreprise contenant une nomenclature et liés à la production d’un assemblage peuvent contenir un identifiant. Un numéro Bates contient une valeur numérique incrémentée séquentiellement et optionnellement un préfixe et un suffixe. Le préfixe + suffixe numérique + est appelé modèle ** Bates.

L’illustration suivante présente un document PDF contenant un identifiant unique, situé dans l’en-tête du document.

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

Ce document DDX fusionne deux documents PDF nommés *map.pdf* et *directions.pdf* en un seul document PDF. Le document PDF résultant contient un en-tête constitué d’un identifiant de page unique. Par exemple, le document de l’illustration ci-dessus montre 000016.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts tels que la création d’un objet de collection contenant des documents d’entrée ou l’extraction des résultats de l’objet de collection renvoyé. (voir Assemblage [par programmation de Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF contenant un identifiant de page unique (numérotation Bates), effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. documents PDF d’entrée de référence.
1. Définissez la valeur initiale du nombre Bates.
1. Assemblage des documents PDF d’entrée.
1. Extrayez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

Si le AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel les AEM Forms sont déployés. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX introduit dans cette section. Pour assembler un document PDF contenant des identifiants de page uniques, le document DDX doit contenir l’ `BatesNumber` élément.

**documents PDF d’entrée de référence**

Les documents PDF d’entrée doivent être référencés pour assembler un document PDF. Par exemple, les documents map.pdf et directions.pdf doivent être référencés pour assembler ces documents PDF en un seul document PDF.

**Définir la valeur initiale du nombre Bates**

Vous pouvez définir la valeur du numéro Bates initial pour répondre aux besoins de votre entreprise. Supposons, par exemple, qu’il soit nécessaire de définir la valeur initiale sur 000100. Si vous ne définissez pas la valeur initiale, la valeur de la première page est 000000.

**Assemblage des documents PDF d’entrée**

Après avoir créé le client de service Assembler, fait référence au document DDX qui contient des informations sur les `BatesNumber` éléments, fait référence à un document PDF d’entrée et défini les options d’exécution, vous pouvez appeler l’ `invokeDDX` opération qui entraîne l’assemblage d’un document PDF contenant des identifiants de page uniques.

**Extraire les résultats**

Le service Assembler renvoie un objet de collection contenant les résultats de la tâche. Vous pouvez extraire le document PDF résultant et les exceptions qui sont générées. Dans ce cas, un document PDF chiffré se trouve dans l’objet de collection.

>[!NOTE]
>
>Un objet de collection est renvoyé si vous appelez l’ `invokeDDX` opération. Cette opération est utilisée lors du transfert de plusieurs documents PDF d’entrée au service Assembler. Cependant, si vous ne transmettez qu’un seul document PDF d’entrée au service Assembler, vous devez appeler l’ `invokeOneDocument` opération. Pour plus d’informations sur l’utilisation de cette opération, voir [Assemblage de Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md)PDF chiffrés.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage de documents avec numérotation Bates à l’aide de l’API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblez un document PDF qui utilise des identificateurs de page uniques (numérotation Bates) à l’aide de l’API Service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. documents PDF d’entrée de référence.

   * Créez un `java.util.Map` objet utilisé pour stocker des documents PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Pour chaque document PDF d’entrée, créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée. Dans ce cas, transmettez l’emplacement d’un document PDF non sécurisé.
   * Pour chaque document PDF d’entrée, créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet contenant le document PDF.
   * Ajoutez une entrée à l’ `java.util.Map` objet en invoquant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX. Par exemple, le nom du fichier source PDF spécifié dans le document DDX introduit dans cette section est Loan.pdf.
      * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.

1. Définissez la valeur initiale du nombre Bates.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez le nombre Bates initial en appelant l’objet `AssemblerOptionSpec` `setFirstBatesNumber` et en transmettant une valeur numérique qui spécifie la valeur initiale.

1. Assemblage des documents PDF d’entrée.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX.
   * Objet `java.util.Map` contenant le fichier PDF non sécurisé d’entrée.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau de journal des tâches.

   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant un document PDF chiffré par mot de passe.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Appelle la méthode `AssemblerResult` de l’ `getDocuments` objet. Cette action renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document PDF.

**Voir également**

[Début rapide (mode SOAP) : Assemblage d’un document PDF avec numérotation Bates à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de documents avec numérotation Bates à l’aide de l’API du service Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblez un document PDF qui utilise des identificateurs de page uniques (numérotation Bates) à l’aide de l’API Service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. documents PDF d’entrée de référence.

   * Pour chaque document PDF d’entrée, créez un `BLOB` objet à l’aide de son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` méthode de l’ `Read` objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en attribuant sa `MTOM` propriété au contenu du tableau d’octets.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker les documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux `MyMapOf_xsd_string_To_xsd_anyType_Item` objets.
   * Attribuez une valeur de chaîne qui représente le nom de clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Affectez l’ `BLOB` objet qui stocke le document PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet sur l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez la valeur initiale du nombre Bates.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez le nombre Bates initial en attribuant une valeur numérique au membre `firstBatesNumber` de données qui appartient à l&#39; `AssemblerOptionSpec` objet.

1. Assemblage des documents PDF d’entrée.

   Appelez la méthode `AssemblerServiceClient` de l’ `invoke` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être les `BLOB` objets qui correspondent à ces fichiers.
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution.

   La `invoke` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF de résultat.
   * Effectuez une itération sur l’ `Map` objet jusqu’à ce que vous trouviez la clé correspondant au nom du document résultant. Ensuite, déposez les éléments `value` de ce membre de la baie sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la `BLOB` propriété de l’objet `MTOM` en question. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
