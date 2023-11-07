---
title: Assembler plusieurs fragments XDP
seo-title: Assembling Multiple XDP Fragments
description: Assemblez plusieurs fragments XDP en un seul document XDP à l’aide de l’API Java et de l’API de service Web.
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 96%

---

# Assembler plusieurs fragments XDP{#assembling-multiple-xdp-fragments}

Vous pouvez assembler plusieurs fragments XDP en un seul document XDP. Prenons l’exemple des fragments XDP où chaque fichier XDP contient un ou plusieurs sous-formulaires utilisés pour créer un formulaire d’intégrité. L’illustration suivante montre le mode Plan (représente le fichier tuc018_template_flowed.xdp utilisé dans le démarrage rapide *Assembler plusieurs fragments XDP*) :

![am_am_forma](assets/am_am_forma.png)

L’illustration suivante montre la section du patient (représente le fichier tuc018_contact.xdp utilisé dans le démarrage rapide *Assembler plusieurs fragments XDP*) :

![am_am_formb](assets/am_am_formb.png)

L’illustration suivante montre la section d’intégrité du patient (représente le fichier tuc018_patient.xdp utilisé dans le démarrage rapide *Assembler plusieurs fragments XDP*) :

![am_am_formc](assets/am_am_formc.png)

Ce fragment contient deux sous-formulaires nommés *subPatientPhysical* et *subPatientHealth*. Ces deux sous-formulaires sont référencés dans le document DDX transmis au service Assembler. À l’aide du service Assembler, vous pouvez combiner tous ces fragments XDP en un seul document XDP, comme illustré ci-dessous.

![am_am_formd](assets/am_am_formd.png)

Le document DDX suivant assemble plusieurs fragments XDP en un document XDP.

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

Le document DDX contient une balise XDP `result` qui spécifie le nom du résultat. Dans ce cas, la valeur est `tuc018result.xdp`. Cette valeur est référencée dans la logique d’application utilisée pour récupérer le document XDP une fois que le service Assembler a renvoyé le résultat. Par exemple, prenez en compte la logique d’application Java suivante utilisée pour récupérer le document XDP assemblé (notez que la valeur est en gras) :

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

La variable `XDP source` tag spécifie le fichier XDP qui représente un document XDP complet qui peut être utilisé comme conteneur pour ajouter des fragments XDP ou comme l’un des documents annexés ensemble dans l’ordre. Dans ce cas, le document XDP est utilisé uniquement comme conteneur (première illustration présentée dans la section *Assembler plusieurs fragments XDP*). En d’autres termes, les autres fichiers XDP sont placés dans le conteneur XDP.

Pour chaque sous-formulaire, vous pouvez ajouter un élément `XDPContent` (cet élément est facultatif). Dans l’exemple ci-dessus, notez qu’il existe trois sous-formulaires : `subPatientContact`, `subPatientPhysical`, et `subPatientHealth`. Les deux `subPatientPhysical` et le sous-formulaire `subPatientHealth` Les sous-formulaires se trouvent dans le même fichier XDP, tuc018_patient.xdp. L’élément de fragment spécifie le nom du sous-formulaire, tel que défini dans Designer.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler plusieurs fragments XDP, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez les documents XDP.
1. Définissez les options d’exécution.
1. Assemblez plusieurs documents XDP.
1. Récupérez le document XDP assemblé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler plusieurs documents XDP. Ce document DDX doit contenir les éléments `XDP result`, `XDP source` et `XDPContent`.

**Référencer les documents XDP**

Pour assembler plusieurs documents XDP, référencez tous les fichiers XDP utilisés pour assembler le document XDP obtenu. Assurez-vous que le nom du sous-formulaire contenu dans le document XDP référencé par l’attribut `source` est spécifié dans l’attribut `fragment`. Un sous-formulaire est défini dans Designer. Par exemple, considérez le XML suivant.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Le sous-formulaire nommé *subPatientContact* doit se trouver dans le fichier XDP nommé *tuc018_contact.xdp*.

**Définir les options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assembler plusieurs documents XDP**

Pour assembler plusieurs fichiers XDP, appelez l’opération `invokeDDX`. Le service Assembler renvoie le document XDP assemblé dans un objet de collection.

**Récupérer le document XDP assemblé**

Un document XDP assemblé est renvoyé dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez le document XDP en tant que fichier XDP. Vous pouvez également transmettre le document XDP à un autre service AEM Forms, tel qu’Output.

**Voir également**

[Assembler plusieurs fragments XDP à l’aide de l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assembler plusieurs fragments XDP à l’aide de l’API de service Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclure des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Créer des documents PDF à l’aide de fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assembler plusieurs fragments XDP à l’aide de l’API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`.

1. Référencez les documents XDP.

   * Créez un objet `java.util.Map` utilisé pour stocker les documents XDP d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le fichier XDP d’entrée (répétez cette tâche pour chaque fichier XDP).
   * Ajoutez une entrée à l’objet `java.util.Map` en invoquant sa méthode `put` et en appelant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément `source` spécifiée dans le document DDX (répétez cette tâche pour chaque fichier XDP).
      * Un objet `com.adobe.idp.Document` qui contient le document XDP correspondant à l’élément `source` (répétez cette tâche pour chaque fichier XDP).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Assemblez plusieurs documents XDP.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document DDX à utiliser.
   * Un objet `java.util.Map` qui contient les fichiers XDP d’entrée.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau du journal de tâche.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le document XDP assemblé.

1. Récupérez le document XDP assemblé.

   Pour obtenir le document XDP assemblé, effectuez les actions suivantes :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération à l’aide de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document XDP assemblé.

**Voir également**

[Assembler plusieurs fragments XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Démarrage rapide (mode SOAP) : Assembler plusieurs fragments XDP à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Régler les propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assembler plusieurs fragments XDP à l’aide de l’API de service Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Assembler Service (service Web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service :

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms, telle que `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur des formulaires AEM au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur du mot de passe correspondant au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Remplissez l’objet `BLOB` en attribuant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Référencez les documents XDP.

   * Pour chaque fichier XDP d’entrée, créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le fichier d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez lʼobjet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker les fichiers d’entrée nécessaires à la création d’un document XDP assemblé.
   * Pour chaque fichier d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Effectuez cette tâche pour chaque fichier XDP d’entrée).
   * Attribuez lʼobjet `BLOB` qui stocke le fichier d’entrée dans le champ `value` de lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Effectuez cette tâche pour chaque fichier XDP d’entrée).
   * Ajoutez lʼobjet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez-la à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. (Effectuez cette tâche pour chaque document XDP d’entrée).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de poursuivre le traitement dʼune tâche en cas d’erreur, attribuez `false` au membre de données `failOnError` de lʼobjet `AssemblerOptionSpec`.

1. Assemblez plusieurs documents XDP.

   Appelez la méthode `invokeDDX` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient les résultats de la tâche et les exceptions éventuelles qui se sont produites.

1. Récupérez le document XDP assemblé.

   Pour obtenir le document XDP nouvellement créé, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF générés.
   * Effectuez une itération sur l’objet `Map` pour obtenir chaque document généré. Convertissez ensuite l’élément `value` du membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de son objet`BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez retranscrire dans un fichier XDP.

**Voir également**

[Assemblage de plusieurs fragments XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
