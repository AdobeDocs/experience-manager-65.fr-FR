---
title: Assemblage de plusieurs fragments XDP
seo-title: Assemblage de plusieurs fragments XDP
description: Assemblez plusieurs fragments XDP dans un seul document XDP à l’aide de l’API Java et de l’API Web Service.
seo-description: Assemblez plusieurs fragments XDP dans un seul document XDP à l’aide de l’API Java et de l’API Web Service.
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 2%

---

# Assemblage de plusieurs fragments XDP{#assembling-multiple-xdp-fragments}

Vous pouvez assembler plusieurs fragments XDP en un seul document XDP. Prenons l’exemple des fragments XDP où chaque fichier XDP contient un ou plusieurs sous-formulaires utilisés pour créer un formulaire d’intégrité. L’illustration suivante présente la vue de composition (représente le fichier tuc018_template_flowed.xdp utilisé dans le *démarrage rapide de plusieurs fragments XDP*) :

![am_am_forma](assets/am_am_forma.png)

L’illustration suivante présente la section du patient (représente le fichier tuc018_contact.xdp utilisé dans le *Assemblage de plusieurs fragments XDP* démarrage rapide) :

![am_am_formb](assets/am_am_formb.png)

L’illustration suivante présente la section sur l’intégrité du patient (représente le fichier tuc018_patient.xdp utilisé dans le *Assemblage de plusieurs fragments XDP* démarrage rapide) :

![am_am_formc](assets/am_am_formc.png)

Ce fragment contient deux sous-formulaires nommés *subPatientPhysique* et *subPatientHealth*. Ces deux sous-formulaires sont référencés dans le document DDX transmis au service Assembler. À l’aide du service Assembler, vous pouvez combiner tous ces fragments XDP en un seul document XDP, comme illustré ci-dessous.

![am_am_formd](assets/am_am_formd.png)

Le document DDX suivant assemble plusieurs fragments XDP en un document XDP.

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

Le document DDX contient une balise XDP `result` qui spécifie le nom du résultat. Dans ce cas, la valeur est `tuc018result.xdp`. Cette valeur est référencée dans la logique de l’application utilisée pour récupérer le document XDP une fois que le service Assembler a renvoyé le résultat. Par exemple, prenez en compte la logique d’application Java suivante utilisée pour récupérer le document XDP assemblé (notez que la valeur est en gras) :

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

La balise `XDP source` spécifie le fichier XDP qui représente un document XDP complet pouvant être utilisé comme conteneur pour ajouter des fragments XDP ou comme l’un des nombreux documents annexés ensemble dans l’ordre. Dans ce cas, le document XDP est utilisé uniquement comme conteneur (la première illustration illustrée dans *Assembling Multiple XDP Fragments*). En d’autres termes, les autres fichiers XDP sont placés dans le conteneur XDP.

Pour chaque sous-formulaire, vous pouvez ajouter un élément `XDPContent` (cet élément est optionnel). Dans l’exemple ci-dessus, notez qu’il existe trois sous-formulaires : `subPatientContact`, `subPatientPhysical` et `subPatientHealth`. Le sous-formulaire `subPatientPhysical` et le sous-formulaire `subPatientHealth` se trouvent tous deux dans le même fichier XDP, tuc018_patient.xdp. L’élément de fragment spécifie le nom du sous-formulaire, tel que défini dans Designer.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler plusieurs fragments XDP, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DX existant.
1. Référencez les documents XDP.
1. Définissez les options d’exécution.
1. Assemblez les documents XDP multiples.
1. Récupérez le document XDP assemblé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler plusieurs documents XDP. Ce document DDX doit contenir les éléments `XDP result`, `XDP source` et `XDPContent` .

**Référence aux documents XDP**

Pour assembler plusieurs documents XDP, référencez tous les fichiers XDP utilisés pour assembler le document XDP obtenu. Assurez-vous que le nom du sous-formulaire contenu dans le document XDP référencé par l’attribut `source` est spécifié dans l’attribut `fragment` . Un sous-formulaire est défini dans Designer. Prenons l’exemple du XML suivant.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Le sous-formulaire *subPatientContact* doit se trouver dans le fichier XDP *tuc018_contact.xdp*.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assemblage de plusieurs documents XDP**

Pour assembler plusieurs fichiers XDP, appelez l’opération `invokeDDX`. Le service Assembler renvoie le document XDP assemblé dans un objet de collection.

**Récupération du document XDP assemblé**

Un document XDP assemblé est renvoyé dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez le document XDP en tant que fichier XDP. Vous pouvez également transmettre le document XDP à un autre service AEM Forms, tel qu’Output.

**Voir également**

[Assemblage de plusieurs fragments XDP à l’aide de l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblage de plusieurs fragments XDP à l’aide de l’API du service Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage de documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Création de documents PDF à l’aide de fragments](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblez plusieurs fragments XDP à l’aide de l’API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Assembler Service (Java) :

1. Inclure les fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez les documents XDP.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents XDP d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le fichier XDP d’entrée (répétez cette tâche pour chaque fichier XDP).
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur string qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément `source` spécifiée dans le document DDX (répétez cette tâche pour chaque fichier XDP).
      * Objet `com.adobe.idp.Document` contenant le document XDP correspondant à l’élément `source` (répétez cette tâche pour chaque fichier XDP).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l’objet `AssemblerOptionSpec` . Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `false` et transmettez `AssemblerOptionSpec`.

1. Assemblez les documents XDP multiples.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant les fichiers XDP d’entrée
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant le document XDP assemblé.

1. Récupérez le document XDP assemblé.

   Pour obtenir le document XDP assemblé, effectuez les actions suivantes :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map` .
   * Effectuez une itération sur l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document XDP assemblé.

**Voir également**

[Assemblage de plusieurs ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragments XDPQuick Start (mode SOAP) : Assemblage de plusieurs fragments XDP à l’aide de l’](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[API Java, y compris des ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[fichiers de bibliothèque Java AEM Forms. Définition des propriétés de connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblez plusieurs fragments XDP à l’aide de l’API de service Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblez plusieurs fragments XDP à l’aide de l’API Assembler Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service :

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms, par exemple `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
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
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` avec le contenu du tableau d’octets.

1. Référencez les documents XDP.

   * Pour chaque fichier XDP d’entrée, créez un objet `BLOB` à l’aide de son constructeur. L’objet `BLOB` est utilisé pour stocker le fichier d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType` . Cet objet de collection est utilisé pour stocker les fichiers d’entrée nécessaires à la création d’un document XDP assemblé.
   * Pour chaque fichier d’entrée, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Attribuez une valeur string qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à la valeur de l’élément spécifié dans le document DDX. (Effectuez cette tâche pour chaque fichier XDP d’entrée.)
   * Affectez l’objet `BLOB` qui stocke le fichier d’entrée dans le champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Effectuez cette tâche pour chaque fichier XDP d’entrée.)
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType` . (Effectuez cette tâche pour chaque document XDP d’entrée.)

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblez les documents XDP multiples.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant les fichiers requis
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui se sont produites.

1. Récupérez le document XDP assemblé.

   Pour obtenir le document XDP nouvellement créé, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF obtenus.
   * Effectuez une itération sur l’objet `Map` pour obtenir chaque document généré. Ensuite, convertissez le `value` de ce membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier XDP.

**Voir également**

[Assemblage de plusieurs ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[fragments XDPAppel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
