---
title: Assemblage de documents PDF par programmation
seo-title: Assemblage de documents PDF par programmation
description: Utilisez l’API du service Assembler pour assembler plusieurs documents PDF en un seul document PDF à l’aide de l’API Java et de l’API Web Service.
seo-description: Utilisez l’API du service Assembler pour assembler plusieurs documents PDF en un seul document PDF à l’aide de l’API Java et de l’API Web Service.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 2%

---

# Assemblage de documents PDF par programmation {#programmatically-assembling-pdf-documents}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Vous pouvez utiliser l’API du service Assembler pour assembler plusieurs documents PDF en un seul document PDF. L’illustration suivante présente trois documents PDF fusionnés en un seul document PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Pour assembler plusieurs documents PDF en un seul document PDF, vous avez besoin d’un document DDX. Un document DDX décrit le document PDF produit par le service Assembler. En d’autres termes, le document DDX indique au service Assembler les actions à effectuer.

Dans le cadre de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Ce document DDX fusionne deux documents PDF nommés *map.pdf* et *directions.pdf* en un seul document PDF.

>[!NOTE]
>
>Pour voir un document DDX qui déassemble un document PDF, voir [Démontage programmatique de documents PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Remarques concernant l’appel du service Assembler à l’aide de services Web {#considerations-when-invoking-assembler-service-using-web-services}

Lorsque vous ajoutez des en-têtes et des pieds de page lors de l’assemblage de documents volumineux, vous risquez de rencontrer une erreur `OutOfMemory` et les fichiers ne seront pas assemblés. Pour réduire les risques que ce problème se produise, ajoutez un élément `DDXProcessorSetting` à votre document DDX, comme illustré dans l’exemple suivant.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Vous pouvez ajouter cet élément en tant qu’enfant de l’élément `DDX` ou enfant d’un élément `PDF result`. La valeur par défaut de ce paramètre est 0 (zéro), ce qui désactive la coche et le DDX se comporte comme si l’élément `DDXProcessorSetting` n’était pas présent. Si vous avez rencontré une erreur `OutOfMemory`, vous devrez peut-être définir la valeur sur un entier, généralement entre 500 et 5000. Une petite valeur de point de contrôle entraîne un pointage plus fréquent.

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF unique à partir de plusieurs documents PDF, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DX existant.
1. Documents PDF d’entrée de référence.
1. Définissez les options d’exécution.
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

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un client PDF Assembler**

Avant d’effectuer une opération Assembler par programmation, vous devez créer un client Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX introduit dans cette section. Ce document DDX demande au service Assembler de fusionner deux documents PDF en un seul document PDF.

**Documents PDF d’entrée de référence**

Référencez les documents PDF d’entrée que vous souhaitez transmettre au service Assembler. Par exemple, si vous souhaitez transmettre deux documents PDF d’entrée nommés Carte et Instructions, vous devez transmettre les fichiers PDF correspondants.

Le fichier map.pdf et le fichier directions.pdf doivent être placés dans un objet de collection. Le nom de la clé doit correspondre à la valeur de l’attribut de source PDF dans le document DDX. Peu importe le nom du fichier PDF si la clé et l’attribut source du document DDX correspondent.

>[!NOTE]
>
>Un objet `AssemblerResult` contenant un objet de collection est renvoyé si vous appelez l’opération `invokeDDX`. Cette opération est utilisée lorsque vous transmettez plusieurs documents PDF d’entrée au service Assembler. Cependant, si vous ne transmettez qu’un seul PDF d’entrée au service Assembler et ne vous attendez qu’à un seul document de retour, appelez l’opération `invokeOneDocument` . Lors de l’appel de cette opération, un seul document est renvoyé. Pour plus d’informations sur l’utilisation de cette opération, voir [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de classe `AssemblerOptionSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblage des documents PDF d’entrée**

Après avoir créé le client de service, référencé un fichier DDX, créé un objet de collection qui stocke les documents PDF d’entrée et défini les options d’exécution, vous pouvez appeler l’opération DDX. Lors de l’utilisation du document DDX spécifié dans cette section, les fichiers map.pdf et direction.pdf sont fusionnés en un document PDF.

**Extraire les résultats**

Le service Assembler renvoie un objet `java.util.Map` qui peut être obtenu à partir de l’objet `AssemblerResult` et qui contient les résultats de l’opération. L’objet `java.util.Map` renvoyé contient les documents créés et toutes les exceptions.

Le tableau suivant résume certaines des valeurs clés et des types d’objets qui peuvent se trouver dans l’objet `java.util.Map` renvoyé.

<table>
 <thead>
  <tr>
   <th><p>Valeur clé</p></th>
   <th><p>Type d’objet</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contient les documents générés qui sont spécifiés dans un élément cible DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contient toute exception pour le document</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contient le journal des tâches</p></td>
  </tr>
 </tbody>
</table>

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démontage programmatique de documents PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Assemblage de documents PDF à l’aide de l’API Java {#assemble-pdf-documents-using-the-java-api}

Assemblez un document PDF à l’aide de l’API Assembler Service (Java) :

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
   * Pour chaque document PDF d’entrée, créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.
   * Pour chaque document d’entrée, ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur string qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément de source PDF spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` (ou `java.util.List` spécifiant plusieurs documents) contenant le document PDF source.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l’objet `AssemblerOptionSpec` . Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `false` et transmettez `AssemblerOptionSpec`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers PDF d’entrée à assembler
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui se sont produites.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les actions suivantes :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cela renvoie un objet `java.util.Map`.
   * Effectuez une itération sur l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document.)
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

   >[!NOTE]
   >
   >Si `LOG_LEVEL` a été défini pour générer un journal, vous pouvez extraire le journal à l’aide de la méthode `getJobLog` de l’objet `AssemblerResult`.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage d’un document PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de documents PDF à l’aide de l’API de service Web {#assemble-pdf-documents-using-the-web-service-api}

Assemblez des documents PDF à l’aide de l’API Assembler Service (service Web) :

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
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Documents PDF d’entrée de référence.

   * Pour chaque document PDF d’entrée, créez un objet `BLOB` à l’aide de son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType` . Cet objet de collection est utilisé pour stocker des documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux objets `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur string qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément de source PDF spécifié dans le document DDX. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Affectez l’objet `BLOB` qui stocke le document PDF dans le champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType` . (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invoke` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Tableau `mapItem` contenant les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être les objets `BLOB` correspondant à ces fichiers.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invoke` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui peuvent s’être produites.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `Map`, qui est un objet `AssemblerResult` contenant les documents PDF obtenus.
   * Effectuez une itération sur l’objet `Map` jusqu’à ce que vous trouviez la clé correspondant au nom du document généré. Convertissez ensuite la balise `value` de ce membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

   >[!NOTE]
   >
   >Si `LOG_LEVEL` a été défini pour générer un journal, vous pouvez extraire le journal en obtenant la valeur du membre de données `jobLog` de l’objet `AssemblerResult`.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
