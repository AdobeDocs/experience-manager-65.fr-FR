---
title: Assemblage de plusieurs fragments XDP
seo-title: Assemblage de plusieurs fragments XDP
description: Assemblez plusieurs fragments XDP dans un seul document XDP à l’aide de l’API Java et de l’API de service Web.
seo-description: Assemblez plusieurs fragments XDP dans un seul document XDP à l’aide de l’API Java et de l’API de service Web.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 2%

---


# Assemblage de plusieurs fragments XDP{#assembling-multiple-xdp-fragments}

Vous pouvez assembler plusieurs fragments XDP en un seul document XDP. Prenons l’exemple des fragments XDP dans lesquels chaque fichier XDP contient un ou plusieurs sous-formulaires utilisés pour créer un formulaire d’intégrité. L’illustration suivante présente la vue hiérarchique (représente le fichier tuc018_template_fleed.xdp utilisé dans le *Assemblage de fragments XDP multiples* début rapide) :

![am_am_forma](assets/am_am_forma.png)

L’illustration suivante présente la section du patient (représente le fichier tuc018_contact.xdp utilisé dans le *Assemblage de fragments XDP multiples* début rapide) :

![am_am_formb](assets/am_am_formb.png)

L’illustration suivante présente la section de santé du patient (représente le fichier tuc018_patient.xdp utilisé dans le *Assemblage de fragments XDP multiples* début rapide) :

![am_am_formc](assets/am_am_formc.png)

Ce fragment contient deux sous-formulaires nommés *subPatientPhysical* et *subPatientHealth*. Ces deux sous-formulaires sont référencés dans le document DDX transmis au service Assembler. Le service Assembler vous permet de combiner tous ces fragments XDP en un seul document XDP, comme le montre l’illustration suivante.

![am_am_formd](assets/am_am_formd.png)

Le document DDX suivant assemble plusieurs fragments XDP dans un document XDP.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

Le document DDX contient une balise XDP `result` qui spécifie le nom du résultat. Dans ce cas, la valeur est `tuc018result.xdp`. Cette valeur est référencée dans la logique d’application utilisée pour récupérer le document XDP une fois que le service Assembler a renvoyé le résultat. Par exemple, prenez en compte la logique d’application Java suivante utilisée pour récupérer le document XDP assemblé (notez que la valeur est en gras) :

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

La balise `XDP source` spécifie le fichier XDP qui représente un document XDP complet qui peut être utilisé comme conteneur pour l’ajout de fragments XDP ou comme l’un des documents qui sont ajoutés ensemble dans l’ordre. Dans ce cas, le document XDP est utilisé uniquement comme conteneur (la première illustration illustrée dans *Assemblage de plusieurs fragments XDP*). Autrement dit, les autres fichiers XDP sont placés dans le conteneur XDP.

Pour chaque sous-formulaire, vous pouvez ajouter un élément `XDPContent` (cet élément est facultatif). Dans l’exemple ci-dessus, notez qu’il existe trois sous-formulaires : `subPatientContact`, `subPatientPhysical` et `subPatientHealth`. Le sous-formulaire `subPatientPhysical` et le sous-formulaire `subPatientHealth` se trouvent tous deux dans le même fichier XDP, tuc018_patient.xdp. L’élément de fragment spécifie le nom du sous-formulaire, tel que défini dans Designer.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler plusieurs fragments XDP, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez les documents XDP.
1. Définissez les options d’exécution.
1. Assemblage de plusieurs documents XDP.
1. Récupérez le document XDP assemblé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler plusieurs documents XDP. Ce document DDX doit contenir des éléments `XDP result`, `XDP source` et `XDPContent`.

**Référence aux documents XDP**

Pour assembler plusieurs documents XDP, référencez tous les fichiers XDP utilisés pour assembler le document XDP de résultat. Assurez-vous que le nom du sous-formulaire contenu dans le document XDP référencé par l’attribut `source` est spécifié dans l’attribut `fragment`. Un sous-formulaire est défini dans Designer. Prenons l’exemple du XML suivant.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Le sous-formulaire *subPatientContact* doit se trouver dans le fichier XDP *tuc018_contact.xdp*.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assemblage de plusieurs documents XDP**

Pour assembler plusieurs fichiers XDP, appelez l’opération `invokeDDX`. Le service Assembler renvoie le document XDP assemblé dans un objet de collection.

**Récupérer le document XDP assemblé**

Un document XDP assemblé est renvoyé dans un objet de collection. Effectuez une itération dans l’objet de collection et enregistrez le document XDP sous la forme d’un fichier XDP. Vous pouvez également transmettre le document XDP à un autre service AEM Forms, tel qu’Output.

**Voir également**

[Assemblage de plusieurs fragments XDP à l’aide de l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblage de plusieurs fragments XDP à l’aide de l’API du service Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Création de Documents PDF à l’aide de fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblage de plusieurs fragments XDP à l’aide de l’API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référencez un document DDX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents XDP.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents XDP d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `com.adobe.idp.Document` et transmettez l&#39;objet `java.io.FileInputStream` qui contient le fichier XDP d&#39;entrée (répétez cette tâche pour chaque fichier XDP).
   * Ajoutez une entrée à l&#39;objet `java.util.Map` en invoquant sa méthode `put` et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur d’élément `source` spécifiée dans le document DDX (répétez cette tâche pour chaque fichier XDP).
      * Objet `com.adobe.idp.Document` contenant le document XDP correspondant à l’élément `source` (répétez cette tâche pour chaque fichier XDP).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `AssemblerOptionSpec` de l’objet `setFailOnError` et transmettez `false`.

1. Assemblage de plusieurs documents XDP.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers XDP d’entrée
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau du journal des tâches

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le document XDP assemblé.

1. Récupérez le document XDP assemblé.

   Pour obtenir le document XDP assemblé, effectuez les actions suivantes :

   * Appelez la méthode `AssemblerResult` de l’objet `getDocuments`. Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération dans l&#39;objet `java.util.Map` jusqu&#39;à ce que vous trouviez l&#39;objet `com.adobe.idp.Document` obtenu.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document XDP assemblé.

**Voir également**

[Assemblage de plusieurs ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragments XDPDébut rapide (mode SOAP) : Assemblage de plusieurs fragments XDP à l’aide de l’](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[API JavaInclusion de ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[fichiers de bibliothèque Java AEM FormsDéfinition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de plusieurs fragments XDP à l’aide de l’API de service Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service :

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms, par exemple `https://localhost:8080/soap/services/AssemblerService?blob=mtom`. Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur de constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur de constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Référencez les documents XDP.

   * Pour chaque fichier XDP d’entrée, créez un objet `BLOB` à l’aide de son constructeur. L&#39;objet `BLOB` est utilisé pour stocker le fichier d&#39;entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier d&#39;entrée et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection permet de stocker les fichiers d’entrée nécessaires à la création d’un document XDP assemblé.
   * Pour chaque fichier d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de clé au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l&#39;objet `key`. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Effectuez cette tâche pour chaque fichier XDP d’entrée.)
   * Affectez l&#39;objet `BLOB` qui stocke le fichier d&#39;entrée au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l&#39;objet `value`. (Effectuez cette tâche pour chaque fichier XDP d’entrée.)
   * Ajoutez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `MyMapOf_xsd_string_To_xsd_anyType` de l&#39;objet `Add` et transmettez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`. (Effectuez cette tâche pour chaque document XDP d’entrée.)

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblage de plusieurs documents XDP.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions survenues.

1. Récupérez le document XDP assemblé.

   Pour obtenir le nouveau document XDP, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF résultants.
   * Effectuez une itération dans l&#39;objet `Map` pour obtenir chaque document cible. Ensuite, définissez `value` sur `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `BLOB` `MTOM` de l’objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier XDP.

**Voir également**

[Assemblage de plusieurs ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragments XDPAppel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)