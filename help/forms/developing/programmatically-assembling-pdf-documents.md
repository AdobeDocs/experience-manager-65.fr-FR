---
title: Assemblage par programmation de documents PDF
seo-title: Assemblage par programmation de documents PDF
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 868936e0fd20d3867e31f0351d7b388149472fd2

---


# Assemblage par programmation de documents PDF {#programmatically-assembling-pdf-documents}

Vous pouvez utiliser l’API du service Assembler pour assembler plusieurs documents PDF dans un seul document PDF. L’illustration suivante présente trois documents PDF fusionnés en un seul document PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Pour assembler plusieurs documents PDF en un seul document PDF, vous devez disposer d’un document DDX. Un document DDX décrit le document PDF produit par le service Assembler. En d’autres termes, le document DDX indique au service Assembler les actions à effectuer.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```as3
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
>Pour afficher un document DDX qui démonte un document PDF, voir Démontage [programmatique de documents](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)PDF.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Assembler Service et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Remarques concernant l’appel du service Assembler à l’aide de services Web {#considerations-when-invoking-assembler-service-using-web-services}

Lorsque vous ajoutez des en-têtes et des pieds de page lors de l’assemblage de documents volumineux, vous risquez de rencontrer une `OutOfMemory` erreur et les fichiers ne seront pas assemblés. Pour réduire les risques que ce problème se produise, ajoutez un `DDXProcessorSetting` élément à votre document DDX, comme illustré dans l’exemple suivant.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Vous pouvez ajouter cet élément en tant qu’enfant de l’ `DDX` élément ou enfant d’un `PDF result` élément. La valeur par défaut de ce paramètre est 0 (zéro), ce qui désactive le point de contrôle et le DDX se comporte comme si l’ `DDXProcessorSetting` élément n’était pas présent. Si vous avez rencontré une `OutOfMemory` erreur, vous devrez peut-être définir la valeur sur un entier, généralement entre 500 et 5000. Une petite valeur de point de contrôle entraîne un pointage plus fréquent.

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF unique à partir de plusieurs documents PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
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
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX présenté dans cette section. Ce document DDX demande au service Assembler de fusionner deux documents PDF en un seul document PDF.

**Documents PDF d’entrée de référence**

Référencez les documents PDF d’entrée que vous souhaitez transmettre au service Assembler. Par exemple, si vous souhaitez transmettre deux documents PDF d’entrée nommés Carte et Direction, vous devez transmettre les fichiers PDF correspondants.

Le fichier map.pdf et le fichier directions.pdf doivent être placés dans un objet de collection. Le nom de la clé doit correspondre à la valeur de l’attribut source PDF dans le document DDX. Peu importe le nom du fichier PDF si la clé et l’attribut source du document DDX correspondent.

>[!NOTE]
>
>Un `AssemblerResult` objet, qui contient un objet de collection, est renvoyé si vous appelez l’ `invokeDDX` opération. Cette opération est utilisée lorsque vous transmettez au service Assembler plusieurs documents PDF d’entrée. Cependant, si vous transmettez un seul fichier PDF d’entrée au service Assembler et que vous attendez un seul document de retour, appelez l’ `invokeOneDocument` opération. Lors de l’appel de cette opération, un seul document est renvoyé. Pour plus d’informations sur l’utilisation de cette opération, voir [Assemblage de documents](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)PDF chiffrés.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Assemblage des documents PDF d’entrée**

Après avoir créé le client de service, référencez un fichier DDX, créez un objet de collection qui stocke les documents PDF d’entrée et définissez les options d’exécution, vous pouvez appeler l’opération DDX. Lors de l’utilisation du document DDX spécifié dans cette section, les fichiers map.pdf et direction.pdf sont fusionnés dans un seul document PDF.

**Extraire les résultats**

Le service Assembler renvoie un `java.util.Map` objet, qui peut être obtenu à partir de l’ `AssemblerResult` objet et qui contient les résultats de l’opération. L’ `java.util.Map` objet renvoyé contient les documents résultants et les exceptions éventuelles.

Le tableau suivant récapitule certaines des valeurs clés et des types d’objet qui peuvent se trouver dans l’ `java.util.Map` objet renvoyé.

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
   <td><p>Contient les documents cible spécifiés dans un élément cible DDX</p></td>
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

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Désassemblage programmatique de documents PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Assemblage de documents PDF à l’aide de l’API Java {#assemble-pdf-documents-using-the-java-api}

Assemblez un document PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Documents PDF d’entrée de référence.

   * Créez un `java.util.Map` objet utilisé pour stocker des documents PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Pour chaque document PDF d’entrée, créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet qui contient le document PDF.
   * Pour chaque document d’entrée, ajoutez une entrée à l’ `java.util.Map` objet en appelant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
      * Objet (ou `com.adobe.idp.Document` `java.util.List` objet spécifiant plusieurs documents) contenant le document PDF source.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et transmettez-la `false`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `AssemblerServiceClient` `invokeDDX` de l’objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers PDF d’entrée à assembler
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau du journal des tâches
   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `AssemblerResult` `getDocuments` de l’objet. Renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet résultant. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document.)
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document PDF.
   >[!NOTE]
   >
   >Si `LOG_LEVEL` vous avez défini pour produire un journal, vous pouvez l’extraire à l’aide de la `AssemblerResult` `getJobLog` méthode de l’objet.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage d’un document PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de documents PDF à l’aide de l’API du service Web {#assemble-pdf-documents-using-the-web-service-api}

Assembler des documents PDF à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Documents PDF d’entrée de référence.

   * Pour chaque document PDF d’entrée, créez un `BLOB` objet à l’aide de son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker des documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux `MyMapOf_xsd_string_To_xsd_anyType_Item` objets.
   * Attribuez une valeur de chaîne représentant le nom de la clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Affectez l’ `BLOB` objet qui stocke le document PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet. (Effectuez cette tâche pour chaque document PDF d’entrée.)
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet à l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (Effectuez cette tâche pour chaque document PDF d’entrée.)

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez `false` au membre `AssemblerOptionSpec` `failOnError` de données de l’objet.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `AssemblerServiceClient` `invoke` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Tableau `mapItem` contenant les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être les `BLOB` objets qui correspondent à ces fichiers.
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution.
   La `invoke` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions qui peuvent s’être produites.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF obtenus.
   * Parcourez l’ `Map` objet jusqu’à ce que vous trouviez la clé correspondant au nom du document cible. Jetez ensuite le numéro `value` de l’élément de tableau sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la `BLOB` `MTOM` propriété de son objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.
   >[!NOTE]
   >
   >Si `LOG_LEVEL` vous avez défini pour produire un journal, vous pouvez extraire le journal en obtenant la valeur du membre `AssemblerResult` `jobLog` de données de l’objet.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
