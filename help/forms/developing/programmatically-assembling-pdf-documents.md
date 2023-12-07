---
title: Assembler les documents PDF par programmation
description: Utilisez l’API du service Assembler pour assembler plusieurs documents PDF en un seul document PDF à l’aide de l’API Java et de l’API du service Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 99%

---

# Assembler les documents PDF par programmation {#programmatically-assembling-pdf-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

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

Ce document DDX fusionne deux documents PDF appelés *map.pdf* et *directions.pdf* en un seul document PDF.

>[!NOTE]
>
>Pour voir un document DDX qui désassemble un document PDF, voir [Désassembler des documents PDF par programmation](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [service Assembler et référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Remarques concernant l’appel du service Assembler à l’aide des services Web {#considerations-when-invoking-assembler-service-using-web-services}

Lorsque vous ajoutez des en-têtes et des pieds de page pendant l’assemblage de documents volumineux, vous pouvez rencontrer une erreur `OutOfMemory` et les fichiers ne seront pas assemblés. Pour réduire les risques que ce problème se produise, ajoutez un élément `DDXProcessorSetting` à votre document DDX, comme illustré dans l’exemple suivant.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Vous pouvez ajouter cet élément en tant qu’enfant de l’élément `DDX` ou en tant qu’enfant d’un élément de `PDF result`. La valeur par défaut de ce paramètre est 0 (zéro), ce qui désactive le point de contrôle et le DDX se comporte comme si l’élément `DDXProcessorSetting` n’est pas présent. Si vous avez rencontré une erreur `OutOfMemory`, vous devrez peut-être définir la valeur sur un nombre entier, généralement entre 500 et 5000. Une petite valeur de point de contrôle entraîne des points de contrôle plus fréquents.

## Résumé des étapes {#summary-of-steps}

Pour assembler un seul document PDF à partir de plusieurs documents PDF, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez les documents PDF d’entrée.
1. Définissez les options d’exécution.
1. Assemblez les documents PDF d’entrée.
1. Extrayez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge et différent JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un client Assembler PDF**

Avant de pouvoir effectuer une opération Assembler par programmation, vous devez créer un client Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons par exemple le document DDX qui a été présenté dans cette section. Ce document DDX demande au service Assembler de fusionner deux documents PDF en un seul document PDF.

**Documents PDF d’entrée de référence**

Référencez les documents PDF d’entrée que vous souhaitez transmettre au service Assembler. Par exemple, si vous souhaitez transmettre deux documents PDF d’entrée intitulés Map et Directions, vous devez transmettre les fichiers PDF correspondants.

Le fichier map.pdf et le fichier directions.pdf doivent être placés dans un objet de collection. Le nom de la clé doit correspondre à la valeur de l’attribut source PDF dans le document DDX. Le nom du fichier PDF importe peu si la clé et l’attribut source du document DDX correspondent.

>[!NOTE]
>
>Un objet `AssemblerResult`, qui contient un objet de collection, est renvoyé si vous appelez l’opération `invokeDDX`. Cette opération est utilisée lorsque vous transmettez au service Assembler au moins deux documents PDF d’entrée. Cependant, si vous ne transmettez qu’un seul PDF d’entrée au service Assembler et ne vous attendez qu’à un seul document de retour, appelez l’opération `invokeOneDocument`. Lorsque vous appelez cette opération, un seul document est renvoyé. Pour plus d’informations sur l’utilisation de cette opération, voir [Assembler des documents PDF chiffrés](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Définir des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche même en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, consultez référence de la classe `AssemblerOptionSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assembler les documents PDF d’entrée**

Après avoir créé le client de service, référencé un fichier DDX, créé un objet de collection qui stocke les documents PDF d’entrée et défini les options d’exécution, vous pouvez appeler l’opération DDX. Lors de l’utilisation du document DDX spécifié dans cette section, les fichiers map.pdf et direction.pdf sont fusionnés en un document PDF.

**Extraire les résultats**

Le service Assembler renvoie un objet `java.util.Map`, qui peut être obtenu à partir de l’objet `AssemblerResult`, et qui contient les résultats de l’opération. L’objet `java.util.Map` renvoyé contient les documents générés et les éventuelles exceptions.

Le tableau suivant récapitule certaines des valeurs clés et des types d’objets qui peuvent se trouver dans la variable renvoyée. `java.util.Map` .

<table>
 <thead>
  <tr>
   <th><p>Valeur de clé</p></th>
   <th><p>Type d’objet</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contient les documents générés qui sont spécifiés dans un élément généré DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contient toute exception pour le document</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contient le log de traitement</p></td>
  </tr>
 </tbody>
</table>

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Désassembler des documents PDF par programme](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Assembler des documents PDF à l’aide de l’API Java {#assemble-pdf-documents-using-the-java-api}

Assemblez un document PDF en utilisant l’API du service Assembler (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents PDF d’entrée.

   * Créez un objet `java.util.Map` qui est utilisé pour stocker les documents PDF d’entrée en utilisant un constructeur `HashMap`.
   * Pour chaque document PDF d’entrée, créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` qui contient le document PDF.
   * Pour chaque document d’entrée, ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
      * Un objet `com.adobe.idp.Document` (ou un objet `java.util.List` qui spécifie plusieurs documents) contenant le document PDF source.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement dʼune tâche lorsquʼune erreur se produit, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invokeDDX` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document DDX à utiliser.
   * Un objet `java.util.Map` qui contient les fichiers PDF d’entrée à assembler.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, notamment la police par défaut et le niveau de log de traitement.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` qui contient les résultats de la tâche et les éventuelles exceptions.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération au sein de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document).
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

   >[!NOTE]
   >
   >Si `LOG_LEVEL` a été défini pour générer un journal, vous pouvez extraire le journal en utilisant la méthode `getJobLog` de l’objet `AssemblerResult`.

**Voir également**

[Démarrage rapide (mode SOAP) : assembler un document PDF à l’aide de l’API Java.](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assembler des documents PDF en utilisant l’API du service web {#assemble-pdf-documents-using-the-web-service-api}

Assemblez des documents PDF en utilisant l’API du service Assembler (service Web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à sa propriété `MTOM`.

1. Référencez les documents PDF d’entrée.

   * Pour chaque document PDF d’entrée, créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec le flux de données en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez lʼobjet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau dʼoctets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker des documents PDF d’entrée.
   * Pour chaque document PDF d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Par exemple, si deux documents PDF d’entrée sont utilisés, créez deux objets `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX. (Répétez cette tâche pour chaque document PDF d’entrée).
   * Attribuez lʼobjet `BLOB` qui stocke le document PDF au champ `value` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Répétez cette tâche pour chaque document PDF d’entrée).
   * Ajoutez lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item` à lʼobjet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`. (Répétez cette tâche pour chaque document PDF d’entrée).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement dʼune tâche en cas d’erreur, attribuez `false` au membre de données `failOnError` de lʼobjet `AssemblerOptionSpec`.

1. Assemblez les documents PDF d’entrée.

   Appelez la méthode `invoke` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX.
   * Le tableau `mapItem` qui contient les documents PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers sources PDF et ses valeurs doivent être les objets `BLOB` qui correspondent à ces fichiers.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invoke` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions éventuelles.

1. Extrayez les résultats.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF résultants.
   * Effectuez une itération au sein de l’objet `Map` jusqu’à ce que vous trouviez la clé correspondant au nom du document généré. Convertissez ensuite la `value` de ce membre du tableau en un objet `BLOB`.
   * Effectuez lʼextraction des données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

   >[!NOTE]
   >
   >Si `LOG_LEVEL` a été défini pour générer un journal, vous pouvez extraire le journal en obtenant la valeur du membre de données `jobLog` de lʼobjet `AssemblerResult`.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
